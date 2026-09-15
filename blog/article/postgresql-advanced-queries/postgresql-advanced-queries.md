# PostgreSQL: کوئری‌های پیشرفته

> **راهنمای مطالعه**
>
> در این آموزش، مفاهیم پیشرفته PostgreSQL شامل توابع تجمعی، توابع پنجره‌ای، توابع آماری، رتبه‌بندی، مدیریت مقادیر NULL و تبدیل داده‌ها به صورت گام‌به‌گام و عملی آموزش داده می‌شود. مثال‌ها بر پایه دیتابیس نمونه Two Trees (فروشگاه روغن زیتون) هستند.

---

## فصل ۰: ساخت دیتابیس نمونه

برای تمرین کوئری‌های پیشرفته، ابتدا نیاز به یک دیتابیس نمونه داریم. دیتابیس Two Trees شامل دو schema اصلی `inventory` و `sales` است.

### ساختار جداول

```sql
-- Create the Two Trees Database 

----------------------------------------------------------
-- EMPTY THE TWO TREES DATABASE IN CASE IT CONTAINS CONTENT
----------------------------------------------------------

DROP TABLE IF EXISTS inventory.products;
DROP TABLE IF EXISTS inventory.categories;
DROP SCHEMA IF EXISTS inventory;
DROP TABLE IF EXISTS sales.order_lines;
DROP TABLE IF EXISTS sales.orders;
DROP TABLE IF EXISTS sales.customers;
DROP SCHEMA IF EXISTS sales;

-----------------------------------
-- CREATE THE TABLE STRUCTURE
-----------------------------------

-- Create the database schemas
CREATE SCHEMA inventory;
CREATE SCHEMA sales;


-- Create a table for the Two Trees category data
CREATE TABLE inventory.categories (
    category_id          INT NOT NULL PRIMARY KEY,
    category_description VARCHAR(50),
    product_line         VARCHAR(25)
);

-- Create a table for the Two Trees product data
CREATE TABLE inventory.products (
    sku             VARCHAR(7) NOT NULL PRIMARY KEY,
    product_name    VARCHAR(50) NOT NULL,
    category_id     INT,
    size            INT,
    price           DECIMAL(5,2) NOT NULL
);

ALTER TABLE inventory.products
ADD CONSTRAINT fk_products_category_id FOREIGN KEY (category_id)
    REFERENCES inventory.categories (category_id)
;

-- Create a table for the Two Trees customer data
CREATE TABLE sales.customers (
    customer_id CHAR(5) NOT NULL PRIMARY KEY,
    company     VARCHAR(100),
    address     VARCHAR(100),
    city        VARCHAR(50),
    state       CHAR(2),
    zip         CHAR(5),
    newsletter  BOOLEAN
);

-- Create a table for the Two Trees order data
CREATE TABLE sales.orders (
    order_id     INT GENERATED ALWAYS AS IDENTITY (START WITH 100 INCREMENT BY 1) NOT NULL PRIMARY KEY,
    order_date   DATE,
    customer_id  CHAR(5)
);

ALTER TABLE sales.orders
ADD CONSTRAINT fk_customers_customer_id FOREIGN KEY (customer_id)
    REFERENCES sales.customers (customer_id)
;

-- Create a table for the order's line-item data
CREATE TABLE sales.order_lines (
    order_id    INT,
    line_id     INT GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1) NOT NULL PRIMARY KEY,
    sku         VARCHAR(7),
    quantity    INT
);

ALTER TABLE sales.order_lines
ADD CONSTRAINT fk_orders_order_id FOREIGN KEY (order_id)
    REFERENCES sales.orders (order_id)
;
```

### درج داده‌ها در جداول

```sql
-----------------------------------
-- INSERT DATA INTO TABLES 
-----------------------------------

-- Add data to the categories table
INSERT INTO inventory.categories
    (category_id, category_description, product_line)
VALUES
    (1, 'Olive Oils', 'Gourmet Chef'),
    (2, 'Flavor Infused Oils', 'Gourmet Chef'),
    (3, 'Bath and Beauty', 'Cosmetics')
;

-- Add data to the customers table
INSERT INTO sales.customers VALUES
    ('FV418', 'Flavorville', '798 Ravinia Road', 'Des Moines', 'IA', '50320', TRUE),
    ('WR421', 'Wild Rose', '222 Dakota Lane', 'Kalamazoo', 'MI', '49001', TRUE),
    ('BX305', 'Bread Express', '3362 Ute Loop', 'Tiffin', 'OH', '44883', FALSE),
    ('BV446', 'Blue Vine', '40675 Raymond Curve', 'Columbus', 'GA', '31901', TRUE),
    ('GR208', 'Green Gardens', '394 Mesa Palms Avenue', 'Atlanta', 'GA', '15742', FALSE),
    ('DF600', 'Delish Food', '809 Weathersfield Ctr Park', 'Madisonville', 'OH', '45227', FALSE)
;

-- Add data to the products table
INSERT INTO inventory.products
    (sku, product_name, category_id, size, price)
VALUES
    ('ALB008', 'Delicate', 1, 8, 10.99),
    ('ALB032', 'Delicate', 1, 32, 18.99),
    ('ALB064', 'Delicate', 1, 64, 22.99),
    ('ALB128', 'Delicate', 1, 128, 26.99),
    ('EV008', 'Extra Virgin', 1, 8, 8.99),
    ('EV016', 'Extra Virgin', 1, 16, 12.99),
    ('EV032', 'Extra Virgin', 1, 32, 16.99),
    ('EV064', 'Extra Virgin', 1, 64, 20.99),
    ('EV128', 'Extra Virgin', 1, 128, 24.99),
    ('FCP008', 'First Cold Press', 1, 8, 8.99),
    ('FCP016', 'First Cold Press', 1, 16, 12.99),
    ('FCP032', 'First Cold Press', 1, 32, 16.99),
    ('FCP064', 'First Cold Press', 1, 64, 20.99),
    ('FCP128', 'First Cold Press', 1, 128, 24.99),
    ('FR008', 'Frantoio', 1, 8, 10.99),
    ('FR016', 'Frantoio', 1, 16, 14.99),
    ('FR032', 'Frantoio', 1, 32, 18.99),
    ('FR064', 'Frantoio', 1, 64, 22.99),
    ('FR128', 'Frantoio', 1, 128, 26.99),
    ('HOJ008', 'Bold', 1, 8, 11.99),
    ('HOJ016', 'Bold', 1, 16, 15.99),
    ('HOJ032', 'Bold', 1, 32, 19.99),
    ('HOJ064', 'Bold', 1, 64, 23.99),
    ('HOJ128', 'Bold', 1, 128, 27.99),
    ('KRN008', 'Koroneiki', 1, 8, 10.99),
    ('KRN016', 'Koroneiki', 1, 16, 14.99),
    ('KRN032', 'Koroneiki', 1, 32, 18.99),
    ('KRN064', 'Koroneiki', 1, 64, 22.99),
    ('KRN128', 'Koroneiki', 1, 128, 26.99),
    ('LEC008', 'Leccino', 1, 8, 10.99),
    ('LEC016', 'Leccino', 1, 16, 14.99),
    ('LEC032', 'Leccino', 1, 32, 18.99),
    ('LEC064', 'Leccino', 1, 64, 22.99),
    ('LEC128', 'Leccino', 1, 128, 26.99),
    ('LGT008', 'Light', 1, 8, 8.99),
    ('LGT016', 'Light', 1, 16, 12.99),
    ('LGT032', 'Light', 1, 32, 16.99),
    ('LGT064', 'Light', 1, 64, 20.99),
    ('LGT128', 'Light', 1, 128, 24.99),
    ('MAN008', 'Manzanilla', 1, 8, 10.99),
    ('MAN016', 'Manzanilla', 1, 16, 14.99),
    ('MAN032', 'Manzanilla', 1, 32, 18.99),
    ('MAN064', 'Manzanilla', 1, 64, 22.99),
    ('MAN128', 'Manzanilla', 1, 128, 26.99),
    ('MIS008', 'Mission', 1, 8, 10.99),
    ('MIS016', 'Mission', 1, 16, 14.99),
    ('MIS032', 'Mission', 1, 32, 18.99),
    ('MIS064', 'Mission', 1, 64, 22.99),
    ('MIS128', 'Mission', 1, 128, 26.99),
    ('MOR008', 'Moraiolo', 1, 8, 10.99),
    ('MOR016', 'Moraiolo', 1, 16, 14.99),
    ('MOR032', 'Moraiolo', 1, 32, 18.99),
    ('MOR064', 'Moraiolo', 1, 64, 22.99),
    ('MOR128', 'Moraiolo', 1, 128, 26.99),
    ('OBL008', 'Oblica', 1, 8, 11.99),
    ('OBL016', 'Oblica', 1, 16, 15.99),
    ('OBL032', 'Oblica', 1, 32, 19.99),
    ('OBL064', 'Oblica', 1, 64, 22.99),
    ('OBL128', 'Oblica', 1, 128, 27.99),
    ('PEN008', 'Pendolino', 1, 8, 10.99),
    ('PEN016', 'Pendolino', 1, 16, 14.99),
    ('PEN032', 'Pendolino', 1, 32, 18.99),
    ('PEN064', 'Pendolino', 1, 64, 22.99),
    ('PEN128', 'Pendolino', 1, 128, 26.99),
    ('PCH008', 'Picholine', 1, 8, 11.99),
    ('PCH016', 'Picholine', 1, 16, 15.99),
    ('PCH032', 'Picholine', 1, 32, 19.99),
    ('PCH064', 'Picholine', 1, 64, 23.99),
    ('PCH128', 'Picholine', 1, 128, 27.99),
    ('PIC008', 'Picual', 1, 8, 10.99),
    ('PIC016', 'Picual', 1, 16, 14.99),
    ('PIC032', 'Picual', 1, 32, 18.99),
    ('PIC064', 'Picual', 1, 64, 22.99),
    ('PIC128', 'Picual', 1, 128, 26.99),
    ('PUR008', 'Pure', 1, 8, 8.99),
    ('PUR016', 'Pure', 1, 16, 12.99),
    ('PUR032', 'Pure', 1, 32, 16.99),
    ('PUR064', 'Pure', 1, 64, 20.99),
    ('PUR128', 'Pure', 1, 128, 24.99),
    ('REF008', 'Refined', 1, 8, 8.99),
    ('REF016', 'Refined', 1, 16, 12.99),
    ('REF032', 'Refined', 1, 32, 16.99),
    ('REF064', 'Refined', 1, 64, 20.99),
    ('REF128', 'Refined', 1, 128, 24.99),
    ('V008', 'Virgin', 1, 8, 8.99),
    ('V016', 'Virgin', 1, 16, 12.99),
    ('V032', 'Virgin', 1, 32, 16.99),
    ('V064', 'Virgin', 1, 64, 20.99),
    ('V128', 'Virgin', 1, 128, 24.99),
    ('MI008', 'Mandarin-Infused EVO', 2, 8, 8.99),
    ('MI016', 'Mandarin-Infused EVO', 2, 16, 12.99),
    ('MI032', 'Mandarin-Infused EVO', 2, 32, 16.99),
    ('LI008', 'Lemon-Infused EVO', 2, 8, 8.99),
    ('LI016', 'Lemon-Infused EVO', 2, 16, 12.99),
    ('LI032', 'Lemon-Infused EVO', 2, 32, 16.99),
    ('BI008', 'Basil-Infused EVO', 2, 8, 10.99),
    ('BI016', 'Basil-Infused EVO', 2, 16, 14.99),
    ('BI032', 'Basil-Infused EVO', 2, 32, 18.99),
    ('RI008', 'Rosemary-Infused EVO', 2, 8, 10.99),
    ('RI016', 'Rosemary-Infused EVO', 2, 16, 14.99),
    ('RI032', 'Rosemary-Infused EVO', 2, 32, 18.99),
    ('GI008', 'Garlic-Infused EVO', 2, 8, 11.99),
    ('GI016', 'Garlic-Infused EVO', 2, 16, 15.99),
    ('GI032', 'Garlic-Infused EVO', 2, 32, 19.99),
    ('JI008', 'Chili-Infused EVO', 2, 8, 11.99),
    ('JI016', 'Chili-Infused EVO', 2, 16, 15.99),
    ('JI032', 'Chili-Infused EVO', 2, 32, 19.99),
    ('OGEC004', 'Olive Glow eye cream', 3, 4, 18.99),
    ('OGFL006', 'Olive Glow face lotion', 3, 6, 14.99),
    ('OGBL012', 'Olive Glow body lotion', 3, 12, 12.99),
    ('OGFT006', 'Olive Glow foot treatment', 3, 6, 7.99),
    ('OGNR004', 'Olive Glow night repair', 3, 4, 21.99),
    ('OGBG016', 'Olive Glow bath gel', 3, 16, 9.99),
    ('OGHS006', 'Olive Glow hand soap', 3, 6, 6.99)
;

-- Add data to the orders table
INSERT INTO sales.orders (order_date, customer_id) VALUES
    ('2021-03-15', 'BX305'),
    ('2021-03-17', 'GR208'),
    ('2021-03-19', 'BV446'),
    ('2021-03-19', 'BV446'),
    ('2021-03-20', 'FV418'),
    ('2021-03-21', 'DF600'),
    ('2021-03-22', 'FV418'),
    ('2021-03-23', 'WR421'),
    ('2021-03-24', 'WR421'),
    ('2021-03-25', 'GR208'),
    ('2021-03-25', 'BX305'),
    ('2021-03-26', 'GR208'),
    ('2021-03-26', 'BV446'),
    ('2021-03-27', 'FV418'),
    ('2021-03-28', 'WR421'),
    ('2021-03-28', 'BV446'),
    ('2021-03-28', 'DF600'),
    ('2021-03-29', 'DF600'),
    ('2021-03-29', 'BX305'),
    ('2021-03-30', 'GR208'),
    ('2021-03-31', 'BX305'),
    ('2021-04-01', 'BX305'),
    ('2021-04-03', 'GR208'),
    ('2021-04-05', 'BV446'),
    ('2021-04-05', 'BV446'),
    ('2021-04-06', 'FV418'),
    ('2021-04-07', 'DF600'),
    ('2021-04-08', 'FV418'),
    ('2021-04-09', 'WR421'),
    ('2021-04-10', 'WR421'),
    ('2021-04-11', 'GR208'),
    ('2021-04-11', 'BX305'),
    ('2021-04-12', 'GR208'),
    ('2021-04-12', 'BV446'),
    ('2021-04-13', 'FV418'),
    ('2021-04-14', 'WR421'),
    ('2021-04-14', 'BV446'),
    ('2021-04-14', 'DF600'),
    ('2021-04-15', 'DF600'),
    ('2021-04-15', 'BX305'),
    ('2021-04-16', 'GR208'),
    ('2021-04-16', 'BX305'),
    ('2021-04-17', 'GR208'),
    ('2021-04-19', 'BV446'),
    ('2021-04-19', 'BV446'),
    ('2021-04-20', 'FV418'),
    ('2021-04-21', 'DF600'),
    ('2021-04-22', 'FV418'),
    ('2021-04-23', 'WR421'),
    ('2021-04-24', 'WR421'),
    ('2021-04-25', 'GR208'),
    ('2021-04-25', 'BX305'),
    ('2021-04-26', 'GR208'),
    ('2021-04-26', 'BV446'),
    ('2021-04-27', 'FV418'),
    ('2021-04-28', 'WR421'),
    ('2021-04-28', 'BV446'),
    ('2021-04-28', 'DF600'),
    ('2021-04-29', 'DF600'),
    ('2021-04-29', 'BX305'),
    ('2021-04-30', 'GR208')
;

-- Add data to the order_lines table
INSERT INTO sales.order_lines (order_id, sku, quantity) VALUES
    (100,  'HOJ016',  2),
    (101,  'MAN128',  2),
    (101,  'MIS032',  1),
    (101,  'PEN008',  1),
    (101,  'RI016',  1),
    (102,  'FCP128',  2),
    (102,  'FCP128',  3),
    (102,  'LGT016',  3),
    (102,  'MIS064',  1),
    (102,  'OBL008',  3),
    (103,  'FCP016',  4),
    (104,  'MIS016',  1),
    (105,  'HOJ128',  2),
    (105,  'KRN128',  4),
    (105,  'LEC008',  4),
    (106,  'JI032',  1),
    (106,  'MOR032',  2),
    (106,  'PIC016',  1),
    (106,  'RI032',  4),
    (107,  'LI016',  3),
    (107,  'PIC008',  4),
    (107,  'PIC064',  3),
    (107,  'V032',  4),
    (108,  'FCP008',  4),
    (108,  'RI008',  1),
    (109,  'EV008',  3),
    (109,  'OBL128',  2),
    (110,  'FCP008',  5),
    (110,  'LGT008',  3),
    (110,  'PUR016',  4),
    (110,  'V064',  1),
    (111,  'KRN128',  3),
    (112,  'JI032',  3),
    (112,  'OBL128',  1),
    (112,  'PCH032',  4),
    (113,  'HOJ008',  2),
    (113,  'PUR064',  2),
    (113,  'PUR128',  3),
    (113,  'REF008',  3),
    (114,  'EV128',  5),
    (115,  'FR128',  5),
    (115,  'PCH064',  4),
    (115,  'PUR064',  4),
    (116,  'FCP128',  2),
    (116,  'PEN064',  4),
    (117,  'ALB064',  3),
    (117,  'ALB128',  2),
    (117,  'GI032',  4),
    (117,  'HOJ064',  2),
    (117,  'JI016',  1),
    (117,  'PIC016',  4),
    (118,  'FR008',  2),
    (118,  'PIC016',  2),
    (118,  'REF008',  2),
    (119,  'JI016',  3),
    (119,  'MI008',  3),
    (120,  'BI008',  4),
    (120,  'EV032',  4),
    (120,  'FR064',  1),
    (120,  'PEN032',  2),
    (121,  'HOJ016',  3),
    (122,  'MAN128',  5),
    (122,  'MIS032',  4),
    (122,  'PEN008',  4),
    (122,  'RI016',  3),
    (123,  'FCP128',  1),
    (123,  'FCP128',  4),
    (123,  'LGT016',  2),
    (123,  'MIS064',  2),
    (123,  'OBL008',  3),
    (124,  'FCP016',  1),
    (125,  'MIS016',  1),
    (126,  'HOJ128',  4),
    (126,  'KRN128',  1),
    (126,  'LEC008',  4),
    (127,  'JI032',  2),
    (127,  'MOR032',  4),
    (127,  'PIC016',  2),
    (127,  'RI032',  1),
    (128,  'LI016',  2),
    (128,  'PIC008',  4),
    (128,  'PIC064',  2),
    (128,  'V032',  2),
    (129,  'FCP008',  1),
    (129,  'RI008',  2),
    (130,  'EV008',  3),
    (130,  'OBL128',  2),
    (131,  'FCP008',  3),
    (131,  'LGT008',  4),
    (131,  'PUR016',  1),
    (131,  'V064',  3),
    (132,  'KRN128',  2),
    (133,  'JI032',  3),
    (133,  'OBL128',  4),
    (133,  'PCH032',  4),
    (134,  'HOJ008',  1),
    (134,  'PUR064',  2),
    (134,  'PUR128',  1),
    (134,  'REF008',  3),
    (135,  'EV128',  2),
    (136,  'FR128',  1),
    (136,  'PCH064',  2),
    (136,  'PUR064',  2),
    (137,  'FCP128',  3),
    (137,  'PEN064',  5),
    (138,  'ALB064',  4),
    (138,  'ALB128',  4),
    (138,  'GI032',  4),
    (138,  'HOJ064',  1),
    (138,  'JI016',  2),
    (138,  'PIC016',  5),
    (139,  'FR008',  3),
    (139,  'PIC016',  4),
    (139,  'REF008',  4),
    (140,  'JI016',  3),
    (140,  'MI008',  1),
    (141,  'BI008',  1),
    (141,  'EV032',  4),
    (141,  'FR064',  1),
    (141,  'PEN032',  2),
    (141,  'HOJ016',  1),
    (142,  'MAN128',  3),
    (142,  'MIS032',  4),
    (142,  'PEN008',  3),
    (142,  'RI016',  2),
    (143,  'FCP128',  4),
    (143,  'FCP128',  4),
    (143,  'LGT016',  1),
    (143,  'MIS064',  3),
    (143,  'OBL008',  4),
    (144,  'FCP016',  4),
    (145,  'MIS016',  2),
    (146,  'HOJ128',  5),
    (146,  'KRN128',  3),
    (146,  'LEC008',  3),
    (147,  'JI032',  3),
    (147,  'MOR032',  3),
    (147,  'PIC016',  1),
    (147,  'RI032',  2),
    (148,  'LI016',  1),
    (148,  'PIC008',  2),
    (148,  'PIC064',  2),
    (148,  'V032',  1),
    (149,  'FCP008',  2),
    (149,  'RI008',  3),
    (150,  'EV008',  3),
    (150,  'OBL128',  2),
    (151,  'FCP008',  4),
    (151,  'LGT008',  2),
    (151,  'PUR016',  4),
    (151,  'V064',  5),
    (152,  'KRN128',  2),
    (153,  'JI032',  2),
    (153,  'OBL128',  5),
    (153,  'PCH032',  4),
    (154,  'HOJ008',  4),
    (154,  'PUR064',  4),
    (154,  'PUR128',  3),
    (154,  'REF008',  2),
    (155,  'EV128',  1),
    (156,  'FR128',  1),
    (156,  'PCH064',  4),
    (156,  'PUR064',  3),
    (157,  'FCP128',  3),
    (157,  'PEN064',  3),
    (158,  'ALB064',  3),
    (158,  'ALB128',  3),
    (158,  'GI032',  4),
    (158,  'HOJ064',  1),
    (158,  'JI016',  4),
    (158,  'PIC016',  1),
    (159,  'FR008',  3),
    (159,  'PIC016',  2),
    (159,  'REF008',  3),
    (160,  'JI016',  2),
    (160,  'MI008',  4)
;
```

### بررسی داده‌های درج شده

```sql
--------------------------
-- REVIEW THE ENTERED DATA
--------------------------

SELECT * FROM inventory.categories;
SELECT * FROM inventory.products;
SELECT * FROM sales.customers;
SELECT * FROM sales.orders;
SELECT * FROM sales.order_lines;
```

> **توضیح:** دیتابیس Two Trees شامل یک فروشگاه روغن زیتون است. جدول `categories` سه دسته‌بندی دارد (روغن زیتون، روغن‌های طعم‌دار، و محصولات زیبایی و بهداشت). جدول `products` شامل ۱۰۴ محصول با سایزها و قیمت‌های مختلف است. جدول `customers` شامل ۶ مشتری، جدول `orders` شامل ۶۱ سفارش (از مارس تا آوریل ۲۰۲۱)، و جدول `order_lines` شامل ۱۶۰ قلم سفارش است.

---

## فصل ۱: توابع تجمعی (Aggregate Functions)

### توابع تجمعی پایه

ابتدا تمام محصولات را مشاهده می‌کنیم:

```sql
select sku, product_name, size, price
from inventory.products;
```

سپس از توابع تجمعی برای خلاصه‌سازی اطلاعات هر نام محصول استفاده می‌کنیم:

```sql
select product_name,
	count(*) as "number of products",
	max(price) as "highest price",
	max(size) as "largest size",
	min(price) as "lowest price",
	avg(price) as "average price"
from inventory.products
group by product_name;
```

> **توضیح:** این کوئری برای هر نام محصول (مثلاً Extra Virgin، Bold و ...) تعداد محصولات مرتبط، بالاترین و پایین‌ترین قیمت، بزرگ‌ترین سایز و میانگین قیمت را نشان می‌دهد.

### توابع تجمعی بولینی (Boolean Aggregates)

```sql
select * from sales.customers

select newsletter, count(*), max(newsletter)
from sales.customers
group by newsletter

select state, count(*), bool_and(newsletter), bool_or(newsletter)
from sales.customers
group by state
```

> **توضیح:**
> - کوئری اول تمام مشتریان را نشان می‌دهد.
> - کوئری دوم تعداد مشتریان را بر اساس وضعیت عضویت در خبرنامه گروه‌بندی می‌کند.
> - کوئری سوم از توابع بولینی استفاده می‌کند:
>   - **`BOOL_AND(newsletter)`**: اگر **همه** مشتریان یک ایالت عضو خبرنامه باشند، `TRUE` برمی‌گرداند
>   - **`BOOL_OR(newsletter)`**: اگر **حداقل یکی** از مشتریان یک ایالت عضو خبرنامه باشد، `TRUE` برمی‌گرداند

### فیلتر کردن با WHERE و HAVING

```sql
select product_name, category_id, size, price
from inventory.products
where price > 20.00;

select size as "product size", count(*) as "number of products"
from inventory.products
group by size
having count(*) > 10
order by size DESC;
```

> **توضیح:**
> - `WHERE` برای فیلتر کردن ردیف‌ها **قبل از** گروه‌بندی استفاده می‌شود (محصولاتی با قیمت بیش از ۲۰ دلار).
> - `HAVING` برای فیلتر کردن گروه‌ها **بعد از** گروه‌بندی استفاده می‌شود (سایزهایی که بیش از ۱۰ محصول دارند).

### فیلتر شرطی با FILTER

عبارت `FILTER` به شما امکان می‌دهد تابع تجمعی را فقط روی ردیف‌هایی اعمال کنید که شرط خاصی برقرار باشد — بدون نیاز به زیرکوئری:

```sql
select category_id,
	count(*) as "count all",
	avg(price) as "average price",
	-- small products
	count(*) filter (where size <=16) as "count small",
	avg(price) filter (where size <= 16) as "average price small",
	-- large products
	count(*) filter (where size >16) as "count large",
	avg(price) filter (where size >16) as "average price large"
from inventory.products
group by rollup (category_id)
order by category_id
```

> **توضیح:** این کوئری همزمان تعداد و میانگین قیمت محصولات کوچک (سایز ≤ ۱۶) و بزرگ (سایز > ۱۶) را در هر دسته‌بندی نشان می‌دهد. از `ROLLUP` هم استفاده شده تا در انتهای نتیجه، یک **ردیف خلاصه کلی** (Grand Total) هم تولید شود — یعنی ردیفی که خلاصه تمام دسته‌بندی‌ها را در کنار هم نشان دهد. به عبارت دیگر، وقتی می‌گوییم «ردیف خلاصه کلی»، منظور یک ردیف اضافه در انتهای جدول خروجی است که مقدار `category_id` در آن `NULL` است و اعداد آن مجموع/میانگین **تمام** ردیف‌ها را نشان می‌دهد — بدون اینکه دسته‌بندی خاصی مد نظر باشد.

### چالش ۱: تعداد سفارشات ماهانه و تعداد فروش هر محصول

```sql
-- Number of orders per month for each customer
select * from sales.orders;

select customer_id,
	count(*) filter (where order_date >= '2021-03-01' and order_date <= '2021-03-31') as "March",
	count(*) filter (where order_date between '2021-04-01' and '2021-04-30') as "April"
from sales.orders
group by customer_id;


-- Quantity of each product sold
select * from sales.order_lines;

select sku, sum(quantity) as "Total Sold"
from sales.order_lines
group by rollup (sku)
order by sum(quantity) DESC;
```

> **توضیح:**
> - کوئری اول تعداد سفارشات هر مشتری را در ماه‌های مارس و آوریل با استفاده از `FILTER` نشان می‌دهد.
> - کوئری دوم مجموع تعداد فروش هر محصول (بر اساس SKU) را محاسبه می‌کند. عبارت `GROUP BY ROLLUP (sku)` باعث می‌شود علاوه بر خلاصه هر SKU، یک **ردیف خلاصه کلی** هم در انتهای نتیجه تولید شود — یعنی ردیفی که مقدار SKU در آن `NULL` است و مجموع کل تمام فروش‌ها را نشان می‌دهد. این دقیقاً مثل وقتی است که در یک جدول اکسل، بعد از ردیف‌های داده، یک ردیف SUM کل قرار می‌دهید.

### ROLLUP: خلاصه‌سازی سلسله‌مراتبی

`ROLLUP` زیرمجموعه‌های تجمعی را به صورت سلسله‌مراتبی تولید می‌کند. یعنی به ازای هر سطح از داده‌ها، یک ردیف خلاصه اضافه می‌کند و در نهایت یک ردیف کلی (Grand Total) هم می‌سازد:

```sql
select category_id,
	product_name,
	count(*),
	min(price) as "lowest price",
	max(price) as "highest price",
	avg(price) as "average price"
from inventory.products
group by rollup (category_id, product_name)
order by category_id, product_name;
```

> **توضیح:** `ROLLUP (category_id, product_name)` سه سطح خلاصه تولید می‌کند:
> 1. هر ترکیب `(category_id, product_name)` — مثلاً «دسته ۱ + Delicate»
> 2. خلاصه بر اساس `category_id` به تنهایی — مثلاً «تمام محصولات دسته ۱»
> 3. خلاصه کل (Grand Total) — ردیفی که هر دو ستون `NULL` هستند و میانگین **تمام** محصولات را نشان می‌دهد
>
> **به زبان ساده:** فرض کنید در یک فروشگاه می‌خواهید بدانید «میانگین قیمت هر محصول چقدر است» (سطح ۱)، «میانگین قیمت کل هر دسته‌بندی چقدر است» (سطح ۲) و «میانگین قیمت کل تمام محصولات چقدر است» (سطح ۳ — ردیف Grand Total). `ROLLUP` این سه سطح را همزمان برای شما می‌سازد.

### CUBE: تمام ترکیبات ممکن

برخلاف `ROLLUP` که فقط زیرمجموعه‌های سلسله‌مراتبی را تولید می‌کند، `CUBE` تمام ترکیبات ممکن ستون‌ها را می‌سازد:

```sql
select category_id,
	size,
	count(*),
	min(price) as "lowest price",
	max(price) as "highest price",
	avg(price) as "average price"
from inventory.products
group by cube (category_id, size)
order by category_id, size;
```

> **توضیح:** `CUBE (category_id, size)` چهار سطح خلاصه تولید می‌کند:
> 1. هر ترکیب `(category_id, size)` — مثلاً «دسته ۱ + سایز ۸»
> 2. خلاصه بر اساس `category_id` — «تمام محصولات یک دسته، بدون توجه به سایز»
> 3. خلاصه بر اساس `size` — «تمام محصولات یک سایز، بدون توجه به دسته»
> 4. خلاصه کل (Grand Total) — کل تمام محصولات
>
> **به زبان ساده:** تفاوت `ROLLUP` و `CUBE` مثل تفاوت بین «نگاه عادی» و «نگاه همه‌جانبه» است. `ROLLUP` فقط در یک جهت سلسله‌مراتبی خلاصه می‌سازد (مثلاً از محصول → دسته → کل). اما `CUBE` مثل یک مکعب، از **هر زاویه‌ای** هم خلاصه می‌سازد — هم بر اساس دسته، هم بر اساس سایز، و همه ترکیبات آن‌ها.

### انحراف معیار و واریانس

PostgreSQL توابع آماری داخلی برای محاسبه انحراف معیار و واریانس دارد:

```sql
select gender, count(*), avg(height_inches), min(height_inches), max(height_inches),
stddev_samp(height_inches),
stddev_pop(height_inches),
var_samp(height_inches),
var_pop(height_inches)
from public.people_heights
group by gender
```

> **توضیح:** جدول `people_heights` شامل ۴۰۰ رکورد با اطلاعات قد ۴۰۰ نفر است.
> - **`STDDEV_SAMP`** / **`VAR_SAMP`**: انحراف معیار/واریانس **نمونه** (تقسیم بر `n-1`)
> - **`STDDEV_POP`** / **`VAR_POP`**: انحراف معیار/واریانس **جمعیت** (تقسیم بر `n`)

---

## فصل ۲: توابع پنجره‌ای (Window Functions)

توابع پنجره‌ای یکی از قدرتمندترین امکانات PostgreSQL هستند. این توابع محاسباتی را روی مجموعه‌ای از ردیف‌ها انجام می‌دهند **بدون اینکه ردیف‌ها را مانند `GROUP BY` تجمیع کنند** — یعنی ردیف اصلی حفظ می‌شود و نتیجه محاسبه در کنار آن نمایش داده می‌شود.

### عبارت OVER پایه

```sql
select sku,
	product_name,
	size,
	price,
	avg(price) over()
from inventory.products
```

> **توضیح:** عبارت `OVER()` بدون هیچ پارامتری، میانگین قیمت **تمام** محصولات را به هر ردیف اضافه می‌کند. این با `GROUP BY` تفاوت دارد چون ردیف‌ها حفظ می‌شوند.
>
> **به زبان ساده:** `OVER()` یعنی «این محاسبه را روی اینجا انجام بده و نتیجه را کنار هر ردیف بنویس». برای همین خروجی همچنان ۱۰۴ ردیف (همان تعداد محصولات) دارد، نه کمتر.

### PARTITION BY: گروه‌بندی درون پنجره

```sql
select size, avg(price) as "average price"
from inventory.products
group by size
order by size;

select sku,
	product_name,
	size,
	category_id,
	price,
	avg(price) over(partition by size) as "average price for size",
	price - avg(price) over(partition by size) as "difference"
from inventory.products
order by sku, size;
```

> **توضیح:** کوئری اول میانگین قیمت هر سایز را با `GROUP BY` ساده نشان می‌دهد. کوئری دوم از `PARTITION BY size` استفاده می‌کند تا برای هر محصول، میانگین قیمت **همان سایز** و اختلاف قیمت آن محصول با میانگین را نشان دهد. این اطلاعات برای تحلیل قیمت‌گذاری بسیار مفید است.

### تعریف پنجره با WINDOW clause

اگر می‌خواهید چند تابع پنجره‌ای را روی **یک پنجره مشترک** اعمال کنید، می‌توانید پنجره را یکبار تعریف کرده و نام‌گذاری کنید:

```sql
select sku,
	product_name,
	category_id,
	size,
	price,
	avg(price) over (xyz),
	min(price) over (xyz),
	max(price) over (xyz)
from inventory.products
window xyz as (partition by category_id)
order by sku, size;
```

> **توضیح:** این روش هم خوانایی کد را بالا می‌برد و هم از تکرار جلوگیری می‌کند. پنجره `xyz` بر اساس `category_id` تعریف شده و سه تابع تجمعی روی آن اعمال می‌شود.

### توابع مکانی (Positional Functions)

توابع `FIRST_VALUE`، `LAST_VALUE` و `NTH_VALUE` مقادیر خاصی را از پنجره برمی‌گردانند:

```sql
select company,
	first_value(company) over(order by company
		rows between unbounded preceding and unbounded following),
	last_value(company) over(order by company
		rows between unbounded preceding and unbounded following),
	nth_value(company, 3) over(order by company
		rows between unbounded preceding and unbounded following)
from sales.customers
order by company;
```

> **نکته مهم:** بدون تعریف فریم (`ROWS BETWEEN ...`)، `LAST_VALUE` فقط آخرین ردیف پنجره فعلی را برمی‌گرداند، نه آخرین ردیف کل مجموعه. به همین دلیل باید `UNBOUNDED FOLLOWING` را مشخص کنید.

### اولین و آخرین تاریخ سفارش هر مشتری

```sql
select * from sales.orders;

select distinct customer_id,
	first_value(order_date)
		over (partition by customer_id
			 order by order_date
			 rows between unbounded preceding and unbounded following),
	last_value(order_date)
		over (partition by customer_id
			 order by order_date
			 rows between unbounded preceding and unbounded following)
from sales.orders
order by customer_id;
```

> **توضیح:** این کوئری برای هر مشتری، اولین و آخرین تاریخ سفارش را نشان می‌دهد. از `DISTINCT` استفاده شده تا هر مشتری فقط یکبار نمایش داده شود.

### فریم‌بندی و میانگین متحرک (Moving Average)

تا اینجا پنجره را دیدیم؛ حالا نوبت **فریم (Frame)** است. فریم یعنی «کدام ردیف‌ها دقیقاً در این محاسبه لحاظ شوند؟». اگر پنجره را یک دایره دور گروهی از ردیف‌ها در نظر بگیریم، فریم مشخص می‌کند به کدام بخش از این دایره نگاه کنیم — مثلاً فقط ردیف قبلی و بعدی، یا همه ردیف‌های قبل، یا سه ردیف بعد:

```sql
select order_id,
sum(order_id) over (order by order_id rows between 0 preceding and 2 following)
	as "3 period leading sum",
sum(order_id) over (order by order_id rows between 2 preceding and 0 following)
	as "3 period trailing sum",
avg(order_id) over (order by order_id rows between 1 preceding and 1 following)
	as "3 period moving average"
from sales.orders;
```

> **توضیح:**
> - **Leading (پیشرو)**: `0 PRECEDING AND 2 FOLLOWING` — ردیف فعلی + ۲ ردیف بعد. یعنی برای هر ردیف، مجموع خودش و دو ردیف بعدش.
> - **Trailing (پسرو)**: `2 PRECEDING AND 0 FOLLOWING` — ۲ ردیف قبل + ردیف فعلی. یعنی برای هر ردیف، مجموع خودش و دو ردیف قبلی‌اش.
> - **Moving Average (میانگین متحرک)**: `1 PRECEDING AND 1 FOLLOWING` — یک قبل + فعلی + یک بعد. یعنی میانگین هر ۳ ردیفِ پشت سر هم.
>
> **به زبان ساده:** میانگین متحرک همان میانگین روی یک «پنجره لغزان» است. فرض کنید ۱۰۰ عدد روزانه دارید و می‌خواهید نوسان را صاف کنید؛ به جای میانگین کل، سه‌تا‌سه‌تا جلو می‌روید و از هر سه عددِ پشت‌سرهم یک میانگین می‌گیرید تا نوسانات کوتاه حذف شوند.

### محاسبه جمعی سفارشات (Running Total)

ترکیب `PARTITION BY` و `ORDER BY` درون فریم، امکان محاسبات جمعی (running total) را فراهم می‌کند:

```sql
select order_lines.order_id,
	order_lines.line_id,
	order_lines.sku,
	order_lines.quantity,
	products.price as "price each",
	order_lines.quantity * products.price as "line total",
	sum (order_lines.quantity * products.price)
		over (partition by order_id) as "order total",
	sum (order_lines.quantity * products.price)
		over (partition by order_id order by line_id) as "running total"
from sales.order_lines inner join inventory.products
	on order_lines.sku = products.sku;
```

> **توضیح:**
> - **`ORDER total`**: جمع کل مبلغ هر سفارش (بدون `ORDER BY` در فریم = کل پنجره)
> - **`Running total`**: جمع تجمعی اقلام سفارش به ترتیب `line_id`

### چالش ۲: حداکثر، حداقل و میانگین قیمت در هر دسته و سایز

```sql
select category_id, product_name, size, price,
	max(price) over(w),
	min(price) over(w),
	avg(price) over(w),
	count(*) over(w)
from inventory.products
window w as (partition by category_id, size)
order by category_id, product_name, size;
```

> **توضیح:** این کوئری با استفاده از پنجره `w` که بر اساس هر ترکیب `(category_id, size)` تعریف شده، حداکثر، حداقل، میانگین قیمت و تعداد محصولات هر گروه را نشان می‌دهد.

---

## فصل ۳: توابع آماری

### میانه (Median) با PERCENTILE_DISC و PERCENTILE_CONT

```sql
select gender,
percentile_disc(0.5) within group (order by height_inches) as "discrete median",
percentile_cont(0.5) within group (order by height_inches) as "continuous median"
from public.people_heights
group by rollup (gender);
```

> **توضیح:**
> - **`PERCENTILE_DISC(0.5)` (گسسته)**: مقدار واقعی نزدیک‌ترین ردیف را برمی‌گرداند — یعنی دقیقاً یکی از مقادیر موجود در داده‌ها
> - **`PERCENTILE_CONT(0.5)` (پیوسته)**: مقدار با اعمال درون‌یابی (interpolation) برمی‌گرداند — برای محاسبات آماری دقیق‌تر مناسب‌تر است
> - `ROLLUP (gender)` هم میانه کلی همه افراد و هم میانه هر جنسیت را نشان می‌دهد
>
> **به زبان ساده:** «میانه» همان عددی است که داده‌ها را به دو نیمه‌ی مساوی تقسیم می‌کند. اگر همه قدها را از کوچک به بزرگ بچینید، میانه یعنی «فرد وسط». تابع `PERCENTILE_DISC` از بین قدهای واقعیِ موجود «یک نفر وسط» را برمی‌گرداند، ولی `PERCENTILE_CONT` حتی اگر وسط دقیقاً بین دو عدد باشد، میانگین آن دو را می‌گیرد و یک عدد دقیق‌تر برمی‌گرداند. معنای عدد ۰.۵ هم همین است: «نقطه‌ای که ۵۰٪ داده‌ها قبل از آن هستند» — یعنی میانه. به همین شکل ۰.۲۵ یعنی ۲۵٪ داده جلوتر از آن‌اند و ۰.۷۵ یعنی ۷۵٪.

### حالت (Mode)

```sql
select
mode() within group (order by height_inches)
from public.people_heights;

select height_inches, count(*)
from public.people_heights
group by height_inches
order by count(*) desc;
```

> **توضیح:** `MODE()` مقداری را برمی‌گرداند که بیشترین تکرار را دارد. کوئری دوم برای بررسی دستی تمام مقادیر و تعداد تکرارشان را نشان می‌دهد.

### چارک‌ها (Quartiles)

```sql
select
percentile_cont(.25) within group (order by height_inches) as "1st quartile",
percentile_cont(.50) within group (order by height_inches) as "2nd quartile",
percentile_cont(.75) within group (order by height_inches) as "3rd quartile"
from public.people_heights;

-- WARNING: the ntile() function only creates even groups,
--          not statistical quartiles
select name, height_inches,
	ntile(4) over (order by height_inches)
from public.people_heights
order by height_inches;
```

> **هشدار مهم:** تابع `NTILE()` فقط گروه‌های مساوی ایجاد می‌کند و **چارک‌های آماری واقعی نیست**. برای چارک‌های دقیق از `PERCENTILE_CONT` استفاده کنید.
>
> **به زبان ساده:** چارک‌ها داده‌ها را بر اساس **مقدار** تقسیم می‌کنند (۲۵٪ کوچک‌ترین‌ها، ۲۵٪ بعدی، و...). ولی `NTILE(4)` داده‌ها را بر اساس **شمارش** تقسیم می‌کند — یعنی فقط تعداد ردیف‌ها را ۴ گروه مساوی می‌کند. این دو وقتی داده‌ها یکنواخت نباشند، نتیجه‌های کاملاً متفاوتی می‌دهند. به همین دلیل همیشه کوئری‌های آماری را با `PERCENTILE_CONT` بنویسید.

### دامنه (Range)

```sql
select 
gender,
max(height_inches) - min(height_inches) as "height range"
from public.people_heights
group by rollup (gender);
```

> **توضیح:** این کوئری دامنه قد (اختلاف بلندترین و کوتاه‌ترین فرد) را برای هر جنسیت و همچنین در کل محاسبه می‌کند.

### چالش ۳: اطلاعات آماری قیمت محصولات

```sql
-- Obtain statistical information about product pricing

select category_id,
	min(price) as "min price",
	percentile_cont(.25) within group (order by price) as "1st quartile",
	percentile_cont(.50) within group (order by price) as "2nd quartile",
	percentile_cont(.75) within group (order by price) as "3rd quartile",
	max(price) as "max price",
	max(price) - min(price) as "price range"
from inventory.products
group by rollup (category_id);
```

> **توضیح:** این کوئری توزیع قیمت را در هر دسته‌بندی و همچنین در کل محصولات نشان می‌دهد — شامل حداقل، چارک‌ها، حداکثر و دامنه قیمت.

---

## فصل ۴: رتبه‌بندی و توزیع

### رتبه‌بندی با Window Functions

```sql
-- ranking with window functions
select name, height_inches, gender,
	rank() over (partition by gender order by height_inches desc),
	dense_rank() over (partition by gender order by height_inches desc)
from public.people_heights
order by gender, height_inches desc;
```

> **توضیح تفاوت `RANK` و `DENSE_RANK`:**
> - **`RANK`**: در صورت تساوی، رتبه بعدی ردیف می‌شود (مثلاً ۱، ۱، ۳، ۴)
> - **`DENSE_RANK`**: بدون ردیف کردن، رتبه بعدی می‌آید (مثلاً ۱، ۱، ۲، ۳)
>
> **به زبان ساده:** فرض کنید دو نفر اول هم‌قد هستند. `RANK` به نفر سوم «رتبه ۳» می‌دهد چون جایگاهش در ردیف‌بندی همین است (۱، ۱، ۳) — مثل مسابقه‌ای که نفرات دوم و سوم واقعاً دو نفر جداگانه‌اند. اما `DENSE_RANK` به او «رتبه ۲» می‌دهد چون به ترتیبِ مکان‌ها فکر می‌کند (۱، ۱، ۲) — به این معنا که «مقام بعدی بعد از مقام اول، مقام دوم است». اگر فقط می‌خواهید بدانید چند «مقام» متمایز وجود دارد، `DENSE_RANK`؛ اگر رتبه به معنای «چند نفر از من جلوترند» می‌خواهید، `RANK`.

### چارک با PERCENT_RANK و CUME_DIST

```sql
select name, gender, height_inches,
	percent_rank() over (order by height_inches desc),
	case
		when percent_rank() over (order by height_inches desc) < .25 then '1st'
		when percent_rank() over (order by height_inches desc) < .50 then '2nd'
		when percent_rank() over (order by height_inches desc) < .75 then '3rd'
		else '4th'
	end as "quartile rank"
from public.people_heights
order by height_inches desc;
```

> **توضیح:** این کوئری با ترکیب `PERCENT_RANK` و `CASE`، هر فرد را در یکی از چهار چارک (۱ تا ۴) قرار می‌دهد.

### توزیع درصدی و توزیع تجمعی

```sql
select name, gender, height_inches,
	percent_rank() over (order by height_inches desc),
	cume_dist() over (order by height_inches desc)
from public.people_heights
order by height_inches desc;
```

> **توضیح:**
> - **`PERCENT_RANK`**: موقعیت درصدی ردیف نسبت به کل (بین ۰ تا ۱)
> - **`CUME_DIST`**: توزیع تجمعی — درصد ردیف‌هایی که مقدار کوچکتر یا مساوی دارند

### رتبه‌بندی محصولات در سه سطح

```sql
-- rank product pricing overall, by category, and by size

select product_name, category_id, size, price,
	dense_rank() over (order by price desc) as "rank overall",
	dense_rank() over (partition by category_id order by price desc) as "rank category",
	dense_rank() over (partition by size order by price desc) as "rank price"
from inventory.products
order by category_id, price desc;
```

> **توضیح:** این کوئری هر محصول را در سه سطح رتبه‌بندی می‌کند: کلی، درون دسته‌بندی و درون سایز.

### رتبه‌بندی فرضی (Hypothetical Ranking)

```sql
-- using rank as a hypothetical grouping set aggregate
select name, height_inches
from public.people_heights
order by height_inches desc;

select gender,
rank(70) within group (order by height_inches desc)
from public.people_heights
group by rollup (gender);
```

> **توضیح:** کوئری اول افراد را به ترتیب قد نزولی نشان می‌دهد. کوئری دوم بررسی می‌کند: «اگر شخصی با قد ۷۰ اینچ وجود داشت، در رتبه چندم قرار می‌گرفت؟» — هم برای هر جنسیت و هم در کل.
>
> **به زبان ساده:** گاهی لازم نیست داده‌ای را واقعاً وارد جدول کنید تا ببینید کجا می‌ایستد؛ فقط می‌خواهید بدانید «اگر بود، جایگاهش کجا بود؟». `RANK(70) WITHIN GROUP (ORDER BY ...)` دقیقاً همین را می‌گوید: عدد ۷۰ را به عنوان یک ردیف فرضی در نظر بگیر، رتبه‌اش را در بین ردیف‌های موجود محاسبه کن و برگردان. به این می‌گویند «رتبه‌بندی فرضی» — چون ردیف جدید واقعاً به جدول اضافه نمی‌شود و فقط جایش را به ما می‌گوید.

---

## فصل ۵: مدیریت مقادیر NULL

### CASE: شرط‌گذاری پیشرفته

`CASE` معادل `if-else` در SQL است و برای تبدیل مقادیر بر اساس شرایط مختلف استفاده می‌شود:

```sql
select sku, product_name, category_id,
	case
		when category_id = 1 then 'Olive Oils'
		when category_id = 2 then 'Flavor Infused Oils'
		when category_id = 3 then 'Bath and Beauty'
		else 'category unknown'
	end as "category description",
	size, price
from inventory.products;
```

> **توضیح:** این کوئری شماره دسته‌بندی (عددی) را به نام توصیفی (متنی) تبدیل می‌کند. اگر شماره دسته‌بندی با هیچ‌کدام از شرایط مطابقت نداشت، مقدار `'category unknown'` نمایش داده می‌شود.

### COALESCE: اولین مقدار غیر NULL

```sql
select * from inventory.categories;

insert into inventory.categories values
(4, null, 'Gift Baskets');

select category_id,
	coalesce(category_description, product_line) as "description",
	product_line
from inventory.categories;
```

> **توضیح:** ابتدا تمام دسته‌بندی‌ها را می‌بینیم. سپس یک دسته‌بندی جدید با `category_description` خالی (NULL) اضافه می‌کنیم. تابع `COALESCE` اولین مقدار غیر `NULL` را از لیست ورودی‌ها برمی‌گرداند — وقتی `category_description` برابر `NULL` باشد، مقدار `product_line` به عنوان توضیح نمایش داده می‌شود.

### NULLIF: تبدیل مقدار به NULL

```sql
select nullif('A', 'A');

select * from inventory.products;

select sku, product_name, category_id,
	nullif(size, 32) as "size",
	price
from inventory.products;
```

> **توضیح:** `NULLIF('A', 'A')` نتیجه `NULL` برمی‌گرداند چون دو مقدار برابر هستند. کوئری سوم تمام محصولات با سایز ۳۲ را به صورت `NULL` نمایش می‌دهد. این تابع معمولاً در ترکیب با `COALESCE` برای مدیریت مقادیر پیش‌فرض استفاده می‌شود.

---

## فصل ۶: توابع کاربردی پیشرفته

### تبدیل نوع داده (CAST)

```sql
select order_id,
	order_date::text,
	customer_id
from sales.orders;
```

> **توضیح:** اپراتور `::` روش ساده PostgreSQL برای تبدیل نوع داده است. در اینجا `order_date` از نوع `DATE` به `TEXT` تبدیل می‌شود.

### تابع IN با لیست و زیرکوئری

```sql
-- us an in() function with a list
select *
from inventory.products
where product_name in('Delicate', 'Bold', 'Light');

-- use an in function with a sub select query
select *
from inventory.products
where product_name in(
		select product_name
		from inventory.products
		group by product_name
		having count(*) >= 5
);

-- determine the query used as a sub select above
select product_name, count(*)
from inventory.products
group by product_name
having count(*) >= 5;
```

> **توضیح:**
> - کوئری اول محصولاتی را برمی‌گرداند که نامشان در لیست `'Delicate'`، `'Bold'` یا `'Light'` باشد.
> - کوئری دوم از یک زیرکوئری استفاده می‌کند تا محصولاتی را پیدا کند که حداقل ۵ اندازه مختلف دارند.
> - کوئری سوم همان زیرکوئری را به تنهایی اجرا می‌کند تا ببینیم دقیقاً کدام محصولات واجد شرط هستند.

### LAG و LEAD: دسترسی به ردیف‌های مجاور

```sql
select order_id,
	customer_id,
	order_date,
	lag(order_date, 1) over(partition by customer_id order by order_id)
		as "previous order date",
	lead (order_date, 1) over(partition by customer_id order by order_id)
		as "next order",
	lead (order_date, 1) over(partition by customer_id order by order_id) -
		order_date as "time between orders"
from sales.orders
order by customer_id, order_date;
```

> **توضیح:**
> - **`LAG(order_date, 1)`**: تاریخ سفارش **قبلی** هر مشتری (۱ ردیف قبل)
> - **`LEAD(order_date, 1)`**: تاریخ سفارش **بعدی** هر مشتری (۱ ردیف بعد)
> - ستون سوم فاصله زمانی بین سفارش فعلی و سفارش بعدی را نشان می‌دهد

### ROW_NUMBER: شماره ردیف

```sql
select * from inventory.products;

select sku, product_name, size,
	row_number() over (partition by product_name order by sku)
from inventory.products;
```

> **توضیح:** `ROW_NUMBER` یک شماره یکتا و پیوسته از ۱ به هر ردیف اختصاص می‌دهد. برای هر نام محصول، ردیف‌ها بر اساس ترتیب `sku` شماره‌گذاری می‌شوند.

### جستجو با generate_series

```sql
select * 
from sales.orders
where order_date in(
	select generate_series('2021-03-15'::timestamp, '2021-03-31'::timestamp, '5 days')	
)
order by order_id;
```

> **توضیح:** تابع `generate_series` یک آرایه پیوسته از مقادیر تولید می‌کند. در اینجا مقادیر `'2021-03-15'`، `'2021-03-20'`، `'2021-03-25'` و `'2021-03-30'` تولید می‌شوند. سپس سفارشاتی که تاریخشان در این مجموعه باشد، برگردانده می‌شوند.

### چالش ۵ (نهایی): مقایسه ردیف‌ها با LAG

```sql
select person_id,
	name,
	height_inches,
	lag(name, 1) over (order by height_inches) as "is taller than",
	height_inches - lag(height_inches, 1) over (order by height_inches)
		as "by this many inches"
from public.people_heights
order by height_inches desc;
```

> **توضیح:** این کوئری هر شخص را با فردی که دقیقاً کوتاه‌تر از اوست مقایسه می‌کند و اختلاف قد را نشان می‌دهد. با `ORDER BY height_inches DESC` از بلندترین شروع می‌شود.

---

## خلاصه

| فصل | موضوعات اصلی |
|---|---|
| فصل ۱ | توابع تجمعی، GROUP BY، HAVING، FILTER، ROLLUP، CUBE، BOOL_AND/OR، انحراف معیار و واریانس |
| فصل ۲ | Window Functions، OVER، PARTITION BY، WINDOW clause، فریم‌بندی، میانگین متحرک، FIRST_VALUE/LAST_VALUE/NTH_VALUE، Running Total |
| فصل ۳ | PERCENTILE_CONT/DISC، MODE، چارک‌ها، NTILE (هشدار)، دامنه |
| فصل ۴ | RANK، DENSE_RANK، PERCENT_RANK، CUME_DIST، رتبه‌بندی فرضی |
| فصل ۵ | CASE، COALESCE، NULLIF |
| فصل ۶ | CAST (`::`)، LAG/LEAD، IN با لیست و زیرکوئری، ROW_NUMBER، generate_series |

> **منبع:** LinkedIn Learning - PostgreSQL Advanced Queries (2022)
