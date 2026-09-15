# PostgreSQL: کوئری‌های پیشرفته

> **راهنمای مطالعه**
>
> در این آموزش، مفاهیم پیشرفته PostgreSQL شامل توابع تجمعی، توابع پنجره‌ای، توابع آماری، رتبه‌بندی، مدیریت مقادیر NULL و تبدیل داده‌ها به صورت گام‌به‌گام و عملی آموزش داده می‌شود. مثال‌ها بر پایه دیتابیس نمونه Two Trees (فروشگاه روغن زیتون) هستند.

---

## فصل ۰: ساخت دیتابیس نمونه

برای تمرین کوئری‌های پیشرفته، ابتدا نیاز به یک دیتابیس نمونه داریم. دیتابیس Two Trees شامل دو schema اصلی است:

- **`inventory`**: شامل جداول `categories` و `products`
- **`sales`**: شامل جداول `customers`، `orders` و `order_lines`

```sql
CREATE SCHEMA inventory;
CREATE SCHEMA sales;

CREATE TABLE inventory.categories (
    category_id          INT NOT NULL PRIMARY KEY,
    category_description VARCHAR(50),
    product_line         VARCHAR(25)
);

CREATE TABLE inventory.products (
    sku             VARCHAR(7) NOT NULL PRIMARY KEY,
    product_name    VARCHAR(50) NOT NULL,
    category_id     INT,
    size            INT,
    price           DECIMAL(5,2) NOT NULL
);

ALTER TABLE inventory.products
ADD CONSTRAINT fk_products_category_id FOREIGN KEY (category_id)
    REFERENCES inventory.categories (category_id);

CREATE TABLE sales.customers (
    customer_id CHAR(5) NOT NULL PRIMARY KEY,
    company     VARCHAR(100),
    address     VARCHAR(100),
    city        VARCHAR(50),
    state       CHAR(2),
    zip         CHAR(5),
    newsletter  BOOLEAN
);

CREATE TABLE sales.orders (
    order_id     INT GENERATED ALWAYS AS IDENTITY (START WITH 100 INCREMENT BY 1) NOT NULL PRIMARY KEY,
    order_date   DATE,
    customer_id  CHAR(5)
);

ALTER TABLE sales.orders
ADD CONSTRAINT fk_customers_customer_id FOREIGN KEY (customer_id)
    REFERENCES sales.customers (customer_id);

CREATE TABLE sales.order_lines (
    order_id    INT,
    line_id     INT GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1) NOT NULL PRIMARY KEY,
    sku         VARCHAR(7),
    quantity    INT
);

ALTER TABLE sales.order_lines
ADD CONSTRAINT fk_orders_order_id FOREIGN KEY (order_id)
    REFERENCES sales.orders (order_id);
```

داده‌های نمونه شامل دسته‌بندی محصولات (روغن زیتون، روغن‌های طعم‌دار، محصولات زیبایی و بهداشت)، مشتریان، سفارشات و اقلام سفارش است.

---

## فصل ۱: توابع تجمعی (Aggregate Functions)

### توابع تجمعی پایه

تابع‌های تجمعی مانند `COUNT`، `MAX`، `MIN`، `AVG` و `SUM` پایه‌ای‌ترین ابزار تحلیل داده در SQL هستند. با استفاده از `GROUP BY` می‌توان این توابع را روی گروه‌های مختلفی از داده اعمال کرد.

```sql
SELECT product_name,
    COUNT(*) AS "number of products",
    MAX(price) AS "highest price",
    MAX(size) AS "largest size",
    MIN(price) AS "lowest price",
    AVG(price) AS "average price"
FROM inventory.products
GROUP BY product_name;
```

این کوئری برای هر نام محصول (مثلاً Extra Virgin، Bold و ...) تعداد محصولات، بالاترین و پایین‌ترین قیمت و میانگین قیمت را نشان می‌دهد.

### فیلتر کردن با WHERE و HAVING

`WHERE` برای فیلتر کردن ردیف‌ها **قبل از** گروه‌بندی و `HAVING` برای فیلتر کردن گروه‌ها **بعد از** گروه‌بندی استفاده می‌شود:

```sql
SELECT product_name, category_id, size, price
FROM inventory.products
WHERE price > 20.00;

SELECT size AS "product size", COUNT(*) AS "number of products"
FROM inventory.products
GROUP BY size
HAVING COUNT(*) > 10
ORDER BY size DESC;
```

کوئری اول تمام محصولات با قیمت بیش از ۲۰ دلار را برمی‌گرداند. کوئری دوم سایزهایی که بیش از ۱۰ محصول دارند را نشان می‌دهد.

### توابع تجمعی بولینی (Boolean Aggregates)

PostgreSQL توابع تجمعی ویژه‌ای برای مقادیر بولین ارائه می‌دهد:

```sql
SELECT newsletter, COUNT(*), MAX(newsletter)
FROM sales.customers
GROUP BY newsletter;

SELECT state, COUNT(*), BOOL_AND(newsletter), BOOL_OR(newsletter)
FROM sales.customers
GROUP BY state;
```

- **`BOOL_AND`**: اگر **همه** مقادیر در گروه `TRUE` باشند، نتیجه `TRUE` است
- **`BOOL_OR`**: اگر **حداقل یکی** از مقادیر در گروه `TRUE` باشد، نتیجه `TRUE` است

### فیلتر شرطی با FILTER

عبارت `FILTER` به شما امکان می‌دهد تابع تجمعی را فقط روی ردیف‌هایی اعمال کنید که شرط خاصی برقرار باشد — بدون نیاز به زیرکوئری:

```sql
SELECT category_id,
    COUNT(*) AS "count all",
    AVG(price) AS "average price",
    COUNT(*) FILTER (WHERE size <= 16) AS "count small",
    AVG(price) FILTER (WHERE size <= 16) AS "average price small",
    COUNT(*) FILTER (WHERE size > 16) AS "count large",
    AVG(price) FILTER (WHERE size > 16) AS "average price large"
FROM inventory.products
GROUP BY ROLLUP (category_id)
ORDER BY category_id;
```

این کوئری همزمان تعداد و میانگین قیمت محصولات کوچک (سایز ≤ ۱۶) و بزرگ (سایز > ۱۶) را در هر دسته‌بندی نشان می‌دهد.

### تعداد سفارشات ماهانه هر مشتری

با ترکیب `FILTER` و `GROUP BY` می‌توان گزارش‌های ماهانه جالبی ساخت:

```sql
SELECT customer_id,
    COUNT(*) FILTER (WHERE order_date >= '2021-03-01' AND order_date <= '2021-03-31') AS "March",
    COUNT(*) FILTER (WHERE order_date BETWEEN '2021-04-01' AND '2021-04-30') AS "April"
FROM sales.orders
GROUP BY customer_id;
```

### ROLLUP: خلاصه‌سازی سلسله‌مراتبی

`ROLLUP` زیرمجموعه‌های تجمعی را به صورت سلسله‌مراتبی تولید می‌کند. به ازای هر ترکیب از ستون‌ها، یک ردیف خلاصه اضافه می‌کند:

```sql
SELECT category_id,
    product_name,
    COUNT(*),
    MIN(price) AS "lowest price",
    MAX(price) AS "highest price",
    AVG(price) AS "average price"
FROM inventory.products
GROUP BY ROLLUP (category_id, product_name)
ORDER BY category_id, product_name;
```

`ROLLUP (category_id, product_name)` سه سطح خلاصه تولید می‌کند:
1. هر ترکیب `(category_id, product_name)`
2. خلاصه بر اساس `category_id` به تنهایی
3. خلاصه کل (ردیف grand total با مقادیر `NULL`)

### CUBE: تمام ترکیبات ممکن

برخلاف `ROLLUP` که فقط زیرمجموعه‌های سلسله‌مراتبی را تولید می‌کند، `CUBE` تمام ترکیبات ممکن ستون‌ها را می‌سازد:

```sql
SELECT category_id,
    size,
    COUNT(*),
    MIN(price) AS "lowest price",
    MAX(price) AS "highest price",
    AVG(price) AS "average price"
FROM inventory.products
GROUP BY CUBE (category_id, size)
ORDER BY category_id, size;
```

`CUBE (category_id, size)` چهار سطح خلاصه تولید می‌کند:
1. هر ترکیب `(category_id, size)`
2. خلاصه بر اساس `category_id`
3. خلاصه بر اساس `size`
4. خلاصه کل

### انحراف معیار و واریانس

PostgreSQL توابع آماری داخلی برای محاسبه انحراف معیار و واریانس دارد:

```sql
SELECT gender, COUNT(*), AVG(height_inches), MIN(height_inches), MAX(height_inches),
    STDDEV_SAMP(height_inches),
    STDDEV_POP(height_inches),
    VAR_SAMP(height_inches),
    VAR_POP(height_inches)
FROM public.people_heights
GROUP BY gender;
```

- **`STDDEV_SAMP`** / **`VAR_SAMP`**: انحراف معیار/واریانس **نمونه** (تقسیم بر `n-1`)
- **`STDDEV_POP`** / **`VAR_POP`**: انحراف معیار/واریانس **جمعیت** (تقسیم بر `n`)

---

## فصل ۲: توابع پنجره‌ای (Window Functions)

توابع پنجره‌ای یکی از قدرتمندترین امکانات PostgreSQL هستند. این توابع محاسباتی را روی مجموعه‌ای از ردیف‌ها انجام می‌دهند **بدون اینکه ردیف‌ها را مانند `GROUP BY` تجمیع کنند** — یعنی ردیف اصلی حفظ می‌شود و نتیجه محاسبه در کنار آن نمایش داده می‌شود.

### عبارت OVER پایه

```sql
SELECT sku, product_name, size, price,
    AVG(price) OVER()
FROM inventory.products;
```

عبارت `OVER()` بدون هیچ پارامتری، میانگین قیمت **تمام** محصولات را به هر ردیف اضافه می‌کند. این با `GROUP BY` تفاوت دارد چون ردیف‌ها حفظ می‌شوند.

### PARTITION BY: گروه‌بندی درون پنجره

`PARTITION BY` مشابه `GROUP BY` عمل می‌کند اما برخلاف آج، ردیف‌ها را تجمیع نمی‌کند:

```sql
SELECT size, AVG(price) AS "average price"
FROM inventory.products
GROUP BY size
ORDER BY size;

SELECT sku, product_name, size, category_id, price,
    AVG(price) OVER(PARTITION BY size) AS "average price for size",
    price - AVG(price) OVER(PARTITION BY size) AS "difference"
FROM inventory.products
ORDER BY sku, size;
```

کوئری دوم برای هر محصول، میانگین قیمت **همان سایز** و اختلاف قیمت آن محصول با میانگین را نشان می‌دهد. این اطلاعات برای تحلیل قیمت‌گذاری بسیار مفید است.

### تعریف پنجره با WINDOW clause

اگر می‌خواهید چند تابع پنجره‌ای را روی **یک پنجره مشترک** اعمال کنید، می‌توانید پنجره را یکبار تعریف کرده و نام‌گذاری کنید:

```sql
SELECT sku, product_name, category_id, size, price,
    AVG(price) OVER (xyz),
    MIN(price) OVER (xyz),
    MAX(price) OVER (xyz)
FROM inventory.products
WINDOW xyz AS (PARTITION BY category_id)
ORDER BY sku, size;
```

این روش هم خوانایی کد را بالا می‌برد و هم از تکرار جلوگیری می‌کند.

### توابع مکانی (Positional Functions)

توابع `FIRST_VALUE`، `LAST_VALUE` و `NTH_VALUE` مقادیر خاصی را از پنجره برمی‌گردانند:

```sql
SELECT company,
    FIRST_VALUE(company) OVER(ORDER BY company
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING),
    LAST_VALUE(company) OVER(ORDER BY company
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING),
    NTH_VALUE(company, 3) OVER(ORDER BY company
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
FROM sales.customers
ORDER BY company;
```

> **نکته مهم:** بدون تعریف فریم (`ROWS BETWEEN ...`)، `LAST_VALUE` فقط آخرین ردیف پنجره فعلی را برمی‌گرداند، نه آخرین ردیف کل مجموعه. به همین دلیل باید `UNBOUNDED FOLLOWING` را مشخص کنید.

### اولین و آخرین تاریخ سفارش هر مشتری

```sql
SELECT DISTINCT customer_id,
    FIRST_VALUE(order_date)
        OVER (PARTITION BY customer_id ORDER BY order_date
              ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING),
    LAST_VALUE(order_date)
        OVER (PARTITION BY customer_id ORDER BY order_date
              ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
FROM sales.orders
ORDER BY customer_id;
```

### فریم‌بندی و میانگین متحرک (Moving Average)

فریم پنجره مشخص می‌کند کدام ردیف‌ها در هر محاسبه لحاظ شوند. با استفاده از `ROWS BETWEEN` می‌توان میانگین متحرک، مجموع پیشرو و مجموع پسرو ساخت:

```sql
SELECT order_id,
    SUM(order_id) OVER (ORDER BY order_id ROWS BETWEEN 0 PRECEDING AND 2 FOLLOWING)
        AS "3 period leading sum",
    SUM(order_id) OVER (ORDER BY order_id ROWS BETWEEN 2 PRECEDING AND 0 FOLLOWING)
        AS "3 period trailing sum",
    AVG(order_id) OVER (ORDER BY order_id ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)
        AS "3 period moving average"
FROM sales.orders;
```

- **Leading (پیشرو)**: `0 PRECEDING AND 2 FOLLOWING` — ردیف فعلی + ۲ ردیف بعد
- **Trailing (پسرو)**: `2 PRECEDING AND 0 FOLLOWING` — ۲ ردیف قبل + ردیف فعلی
- **Moving Average (میانگین متحرک)**: `1 PRECEDING AND 1 FOLLOWING` — یک قبل + فعلی + یک بعد

### محاسبه جمعی سفارشات

ترکیب `PARTITION BY` و `ORDER BY` درون فریم، امکان محاسبات جمعی (running total) را فراهم می‌کند:

```sql
SELECT order_lines.order_id,
    order_lines.line_id,
    order_lines.sku,
    order_lines.quantity,
    products.price AS "price each",
    order_lines.quantity * products.price AS "line total",
    SUM(order_lines.quantity * products.price)
        OVER (PARTITION BY order_id) AS "order total",
    SUM(order_lines.quantity * products.price)
        OVER (PARTITION BY order_id ORDER BY line_id) AS "running total"
FROM sales.order_lines INNER JOIN inventory.products
    ON order_lines.sku = products.sku;
```

- **`ORDER total`**: جمع کل مبلغ هر سفارش (بدون `ORDER BY` در فریم = کل پنجره)
- **`Running total`**: جمع تجمعی اقلام سفارش به ترتیب `line_id`

---

## فصل ۳: توابع آماری

### درصدکل (Percentile) و میانه (Median)

PostgreSQL دو تابع اصلی برای محاسبه درصدکل دارد:

```sql
-- میانه با percentile_disc (مقدار واقعی از داده)
SELECT gender,
    PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY height_inches) AS "discrete median",
    PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY height_inches) AS "continuous median"
FROM public.people_heights
GROUP BY ROLLUP (gender);
```

- **`PERCENTILE_DISC` (گسسته)**: مقدار واقعی نزدیک‌ترین ردیف را برمی‌گرداند
- **`PERCENTILE_CONT` (پیوسته)**: مقدار با اعمال درون‌یابی (interpolation) برمی‌گرداند — برای محاسبات آماری دقیق‌تر مناسب‌تر است

### چارک‌ها (Quartiles)

```sql
SELECT
    PERCENTILE_CONT(.25) WITHIN GROUP (ORDER BY height_inches) AS "1st quartile",
    PERCENTILE_CONT(.50) WITHIN GROUP (ORDER BY height_inches) AS "2nd quartile",
    PERCENTILE_CONT(.75) WITHIN GROUP (ORDER BY height_inches) AS "3rd quartile"
FROM public.people_heights;
```

> **هشدار:** تابع `NTILE()` فقط گروه‌های مساوی ایجاد می‌کند و **چارک‌های آماری واقعی نیست**. برای چارک‌های دقیق از `PERCENTILE_CONT` استفاده کنید.

### حالت (Mode)

Mode یا نما، مقداری است که بیشترین تکرار را دارد:

```sql
SELECT
    MODE() WITHIN GROUP (ORDER BY height_inches)
FROM public.people_heights;

-- بررسی دستی
SELECT height_inches, COUNT(*)
FROM public.people_heights
GROUP BY height_inches
ORDER BY COUNT(*) DESC;
```

### دامنه (Range) و اطلاعات قیمتی

```sql
SELECT 
    gender,
    MAX(height_inches) - MIN(height_inches) AS "height range"
FROM public.people_heights
GROUP BY ROLLUP (gender);
```

### چالش: اطلاعات آماری قیمت محصولات

```sql
SELECT category_id,
    MIN(price) AS "min price",
    PERCENTILE_CONT(.25) WITHIN GROUP (ORDER BY price) AS "1st quartile",
    PERCENTILE_CONT(.50) WITHIN GROUP (ORDER BY price) AS "2nd quartile",
    PERCENTILE_CONT(.75) WITHIN GROUP (ORDER BY price) AS "3rd quartile",
    MAX(price) AS "max price",
    MAX(price) - MIN(price) AS "price range"
FROM inventory.products
GROUP BY ROLLUP (category_id);
```

این کوئری توزیع قیمت را در هر دسته‌بندی و همچنین در کل محصولات نشان می‌دهد.

---

## فصل ۴: رتبه‌بندی و توزیع

### توابع رتبه‌بندی پایه

```sql
SELECT name, height_inches, gender,
    RANK() OVER (PARTITION BY gender ORDER BY height_inches DESC),
    DENSE_RANK() OVER (PARTITION BY gender ORDER BY height_inches DESC)
FROM public.people_heights
ORDER BY gender, height_inches DESC;
```

تفاوت `RANK` و `DENSE_RANK`:
- **`RANK`**: در صورت تساوی، رتبه بعدی ردیف می‌شود (مثلاً ۱، ۱، ۳)
- **`DENSE_RANK`**: بدون ردیف کردن، رتبه بعدی می‌آید (مثلاً ۱، ۱، ۲)

### رتبه‌بندی محصولات

```sql
SELECT product_name, category_id, size, price,
    DENSE_RANK() OVER (ORDER BY price DESC) AS "rank overall",
    DENSE_RANK() OVER (PARTITION BY category_id ORDER BY price DESC) AS "rank category",
    DENSE_RANK() OVER (PARTITION BY size ORDER BY price DESC) AS "rank price"
FROM inventory.products
ORDER BY category_id, price DESC;
```

این کوئری هر محصول را در سه سطح رتبه‌بندی می‌کند: کلی، درون دسته‌بندی و درون سایز.

### درصد رتبه و توزیع تجمعی

```sql
SELECT name, gender, height_inches,
    PERCENT_RANK() OVER (ORDER BY height_inches DESC),
    CUME_DIST() OVER (ORDER BY height_inches DESC)
FROM public.people_heights
ORDER BY height_inches DESC;
```

- **`PERCENT_RANK`**: موقعیت درصدی ردیف نسبت به کل (بین ۰ تا ۱)
- **`CUME_DIST`**: توزیع تجمعی — درصد ردیف‌هایی که مقدار کوچکتر یا مساوی دارند

### تبدیل درصد رتبه به چارک

```sql
SELECT name, gender, height_inches,
    PERCENT_RANK() OVER (ORDER BY height_inches DESC),
    CASE
        WHEN PERCENT_RANK() OVER (ORDER BY height_inches DESC) < .25 THEN '1st'
        WHEN PERCENT_RANK() OVER (ORDER BY height_inches DESC) < .50 THEN '2nd'
        WHEN PERCENT_RANK() OVER (ORDER BY height_inches DESC) < .75 THEN '3rd'
        ELSE '4th'
    END AS "quartile rank"
FROM public.people_heights
ORDER BY height_inches DESC;
```

### رتبه‌بندی فرضی (Hypothetical Ranking)

با `RANK()` به صورت aggregate می‌توان بررسی کرد که یک مقدار فرضی در کجا قرار می‌گرفت:

```sql
SELECT gender,
    RANK(70) WITHIN GROUP (ORDER BY height_inches DESC)
FROM public.people_heights
GROUP BY ROLLUP (gender);
```

این کوئری می‌گوید: «اگر شخصی با قد ۷۰ اینچ وجود داشت، در رتبه چندم قرار می‌گرفت؟»

---

## فصل ۵: مدیریت مقادیر NULL

### CASE: شرط‌گذاری پیشرفته

`CASE` معادل `if-else` در SQL است و برای تبدیل مقادیر بر اساس شرایط مختلف استفاده می‌شود:

```sql
SELECT sku, product_name, category_id,
    CASE
        WHEN category_id = 1 THEN 'Olive Oils'
        WHEN category_id = 2 THEN 'Flavor Infused Oils'
        WHEN category_id = 3 THEN 'Bath and Beauty'
        ELSE 'category unknown'
    END AS "category description",
    size, price
FROM inventory.products;
```

### COALESCE: اولین مقدار غیر NULL

`COALESCE` اولین مقدار غیر `NULL` را از لیست ورودی‌ها برمی‌گرداند:

```sql
-- اضافه کردن یک دسته‌بندی بدون توضیح
INSERT INTO inventory.categories VALUES (4, NULL, 'Gift Baskets');

SELECT category_id,
    COALESCE(category_description, product_line) AS "description",
    product_line
FROM inventory.categories;
```

وقتی `category_description` برابر `NULL` باشد، مقدار `product_line` به عنوان توضیح نمایش داده می‌شود.

### NULLIF: تبدیل مقدار به NULL

`NULLIF` دو مقدار را مقایسه می‌کند و اگر برابر باشند، `NULL` برمی‌گرداند:

```sql
SELECT NULLIF('A', 'A');  -- نتیجه: NULL

SELECT sku, product_name, category_id,
    NULLIF(size, 32) AS "size",
    price
FROM inventory.products;
```

این کوئری تمام محصولات با سایز ۳۲ را به صورت `NULL` نمایش می‌دهد. این تابع معمولاً در ترکیب با `COALESCE` برای مدیریت مقادیر پیش‌فرض استفاده می‌شود.

---

## فصل ۶: توابع کاربردی پیشرفته

### تبدیل نوع داده (CAST)

PostgreSQL روش‌های متعددی برای تبدیل نوع داده دارد. ساده‌ترین آن استفاده از `::` است:

```sql
SELECT order_id,
    order_date::TEXT,
    customer_id
FROM sales.orders;
```

### تابع IN با لیست و زیرکوئری

تابع `IN` برای بررسی عضویت در یک مجموعه استفاده می‌شود و هم با لیست مستقیم و هم با زیرکوئری کار می‌کند:

```sql
-- استفاده با لیست مستقیم
SELECT *
FROM inventory.products
WHERE product_name IN ('Delicate', 'Bold', 'Light');

-- استفاده با زیرکوئری
SELECT *
FROM inventory.products
WHERE product_name IN (
    SELECT product_name
    FROM inventory.products
    GROUP BY product_name
    HAVING COUNT(*) >= 5
);
```

کوئری دوم محصولاتی را برمی‌گرداند که حداقل ۵ اندازه مختلف دارند.

### LAG و LEAD: دسترسی به ردیف‌های مجاور

`LAG` به ردیف قبلی و `LEAD` به ردیف بعدی دسترسی می‌دهند:

```sql
SELECT order_id,
    customer_id,
    order_date,
    LAG(order_date, 1) OVER(PARTITION BY customer_id ORDER BY order_id)
        AS "previous order date",
    LEAD(order_date, 1) OVER(PARTITION BY customer_id ORDER BY order_id)
        AS "next order",
    LEAD(order_date, 1) OVER(PARTITION BY customer_id ORDER BY order_id) -
        order_date AS "time between orders"
FROM sales.orders
ORDER BY customer_id, order_date;
```

این کوئری برای هر سفارش، تاریخ سفارش قبلی و بعدی مشتری و فاصله زمانی بین سفارشات را نشان می‌دهد.

### ROW_NUMBER: شماره ردیف

`ROW_NUMBER` یک شماره یکتا و پیوسته به هر ردیف اختصاص می‌دهد:

```sql
SELECT sku, product_name, size,
    ROW_NUMBER() OVER (PARTITION BY product_name ORDER BY sku)
FROM inventory.products;
```

برای هر نام محصول، ردیف‌ها را از ۱ شماره‌گذاری می‌کند (بر اساس ترتیب `sku`).

### تفاوت ROW_NUMBER, RANK و DENSE_RANK

| تابع | رفتار در تساوی | شماره‌گذاری |
|---|---|---|
| `ROW_NUMBER` | حتی در تساوی، شماره یکتا | ۱، ۲، ۳، ۴ |
| `RANK` | شماره تکراری، رتبه ردیف می‌شود | ۱، ۱، ۳، ۴ |
| `DENSE_RANK` | شماره تکراری، بدون ردیف | ۱، ۱، ۲، ۳ |

### جستجو با generate_series

تابع `generate_series` یک آرایه پیوسته از مقادیر تولید می‌کند. با ترکیب آن با `IN` می‌توانید سفارشات در بازه زمانی خاصی را پیدا کنید:

```sql
SELECT * 
FROM sales.orders
WHERE order_date IN (
    SELECT GENERATE_SERIES('2021-03-15'::TIMESTAMP, '2021-03-31'::TIMESTAMP, '5 days')
)
ORDER BY order_id;
```

این کوئری سفارشاتی را برمی‌گرداند که در تاریخ‌های ۱۵، ۲۰، ۲۵ و ۳۰ مارس ثبت شده‌اند.

### چالش نهایی: مقایسه ردیف‌ها با LAG

```sql
SELECT person_id,
    name,
    height_inches,
    LAG(name, 1) OVER (ORDER BY height_inches) AS "is taller than",
    height_inches - LAG(height_inches, 1) OVER (ORDER BY height_inches)
        AS "by this many inches"
FROM public.people_heights
ORDER BY height_inches DESC;
```

این کوئری هر شخص را با فردی که دقیقاً کوتاه‌تر از اوست مقایسه می‌کند و اختلاف قد را نشان می‌دهد.

---

## خلاصه

| فصل | موضوعات اصلی |
|---|---|
| فصل ۱ | توابع تجمعی، GROUP BY، HAVING، FILTER، ROLLUP، CUBE، انحراف معیار |
| فصل ۲ | Window Functions، OVER، PARTITION BY، WINDOW clause، فریم‌بندی، میانگین متحرک |
| فصل ۳ | PERCENTILE_CONT/DISC، MODE، چارک‌ها، دامنه |
| فصل ۴ | RANK، DENSE_RANK، PERCENT_RANK، CUME_DIST، NTILE |
| فصل ۵ | CASE، COALESCE، NULLIF |
| فصل ۶ | CAST، LAG/LEAD، IN، ROW_NUMBER، generate_series |

> **منبع:** LinkedIn Learning - PostgreSQL Advanced Queries (2022)
