<div dir="rtl" align="right">

# محمدسجاد دباغ · Backend Engineer

**رزومه و بلاگ فنی** — [mdabagh.github.io](https://mdabagh.github.io)

توسعه‌دهنده بک‌اند با بیش از ۵ سال تجربه در طراحی API، مهاجرت از سیستم‌های Legacy و بهینه‌سازی عملکرد.  
تمرکز اصلی: `PHP` · `Laravel` · `RESTful API` · `System Architecture`

[![Live Site](https://img.shields.io/badge/site-mdabagh.github.io-F2A541?style=for-the-badge)](https://mdabagh.github.io)
[![Blog](https://img.shields.io/badge/blog-یادداشت‌های_فنی-0E2A47?style=for-the-badge)](https://mdabagh.github.io/blog/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-msdabbagh-0A66C2?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/msdabbagh)
[![GitHub](https://img.shields.io/badge/GitHub-mdabagh-181717?style=for-the-badge&logo=github)](https://github.com/mdabagh)

---

## SHEET 00 / WRITING — بلاگ

در بلاگ، تجربه‌ها، آموخته‌ها و برداشت‌های شخصی‌ام از مسیر توسعه نرم‌افزار را می‌نویسم — از مطالعه‌ی کتاب‌های System Design تا چالش‌های روزمره‌ی یک بک‌اند دولوپر.

**[مشاهده بلاگ →](https://mdabagh.github.io/blog/)**

---

### دسته‌بندی‌ها

| # | دسته | توضیح | لینک |
|---|------|-------|------|
| ۰۱ | یادداشت‌های کتاب Design System | خلاصه و برداشت شخصی از مطالعه‌ی کتاب‌های حوزه‌ی Design System و کاربردشان در پروژه‌های واقعی | [مشاهده دسته](https://mdabagh.github.io/blog/category.html?cat=design-system) |

---

### همه‌ی یادداشت‌ها

| # | عنوان | دسته | تاریخ | خلاصه | لینک |
|---|--------|------|-------|-------|------|
| ۰۱ | FORWARD | Design System | ۱۴۰۵/۰۴/۲۱ | مصاحبه طراحی سیستم درباره پیدا کردن یک پاسخ آماده نیست؛ بلکه ارزیابی توانایی تحلیل مسئله، شفاف‌سازی نیازمندی‌ها و طراحی معماری مناسب برای ساخت سیستم‌های مقیاس‌پذیر است. | [مطالعه](https://mdabagh.github.io/blog/post.html?cat=design-system&slug=FORWARD) |
| ۰۲ | فصل ۱ | Design System | ۱۴۰۵/۰۴/۲۱ | در این فصل، ابتدا سیستمی را طراحی می‌کنیم که تنها از یک کاربر پشتیبانی می‌کند و سپس قدم‌به‌قدم آن را گسترش می‌دهیم تا بتواند به میلیون‌ها کاربر سرویس ارائه دهد. | [مطالعه](https://mdabagh.github.io/blog/post.html?cat=design-system&slug=CHAPTER1) |

> یادداشت‌ها به‌صورت زنده از فایل‌های Markdown و JSON بارگذاری می‌شوند. برای افزودن پست جدید، راهنمای ساختار پایین را ببینید.

---

## SHEET 01 / PROFILE — درباره

توسعه‌دهنده بک‌اند با تجربه در طراحی، توسعه و نگهداری سیستم‌های سازمانی و سرویس‌های پرداخت. تمرکز اصلی روی ساخت API، مهاجرت از سامانه‌های قدیمی و بهینه‌سازی پایگاه‌داده است.

| | |
|---|---|
| **تخصص اصلی** | PHP / Laravel |
| **سابقه کار** | +۵ سال |
| **محل سکونت** | تهران |
| **وضعیت** | Open to Work |
| **تحصیلات** | کارشناسی مهندسی IT |

**[دانلود رزومه (PDF)](https://mdabagh.github.io/resume-mohammad-sajad-dabagh.pdf)**

---

## SHEET 02 / STACK — مهارت‌ها

**تخصص اصلی**  
`PHP` · `Laravel` · `HTML` · `CSS` · `JavaScript`

**آشنایی**  
`Node.js` · `Python` · `Go` · `React` · `Next.js`

**زیرساخت**  
`Docker` · `Nginx` · `PHP-FPM` · `Linux` · `MySQL` · `MariaDB` · `Git`

**معماری و فرآیند**  
`Software Architecture` · `System Analysis` · `RESTful API Design` · `Agile` · `Technical Documentation`

---

## SHEET 03 / STRUCTURE — ساختار سایت

```
mdabagh.github.io/
├── index.html              ← رزومه و پروفایل
├── blog/
│   ├── index.html          ← صفحه اصلی بلاگ
│   ├── category.html       ← همه دسته‌ها: ?cat=slug
│   ├── post.html           ← همه پست‌ها: ?cat=slug&slug=post-id
│   └── design-system/
│       ├── detals.json     ← نام و خلاصه دسته
│       └── markdouns/
│           ├── index.json  ← لیست فایل‌های پست
│           ├── FORWARD.json / FORWARD.md
│           └── CHAPTER1.json / CHAPTER1.md
├── robots.txt
└── sitemap.xml
```

### افزودن یادداشت جدید

۱. در پوشه‌ی `blog/{category}/markdouns/` دو فایل بسازید:

```json
// my-post.json
{
  "title": "عنوان یادداشت",
  "summary": "خلاصه‌ی کوتاه برای کارت و سئو",
  "date": "2026-07-13"
}
```

```markdown
<!-- my-post.md -->
متن کامل یادداشت به Markdown
```

۲. نام فایل را به آرایه‌ی `files` در `index.json` اضافه کنید:

```json
{
  "files": ["FORWARD.json", "CHAPTER1.json", "my-post.json"]
}
```

۳. اگر دسته‌بندی جدید است:
   - پوشه‌ی `blog/{category}/` با `detals.json` بسازید
   - slug دسته را به آرایه‌ی `possibleCategories` در `blog/index.html` اضافه کنید
   - URL جدید را به `sitemap.xml` و این README اضافه کنید

**آدرس پست:**  
`https://mdabagh.github.io/blog/post.html?cat={category}&slug={post-id}`

---

## SHEET 04 / CONTACT — تماس

| | |
|---|---|
| **ایمیل** | m3dabagh@gmail.com |
| **تلفن** | ۰۹۱۰ ۴۱۲ ۳۸۰۸ |
| **LinkedIn** | [linkedin.com/in/msdabbagh](https://linkedin.com/in/msdabbagh) |
| **GitHub** | [github.com/mdabagh](https://github.com/mdabagh) |

برای استخدام تمام‌وقت یا همکاری فریلنس در دسترس هستم.

---

<p align="center">
  <sub>© ۲۰۲۶ محمدسجاد دباغ — ساخته شده با عشق · تهران</sub>
</p>

</div>
