# ترجمه فارسی: Rate Limiting Lyft

> **منبع اصلی:** Lyft Rate Limiting (GitHub Repository)
> **لینک:** https://github.com/lyft/ratelimit
> **نوع:** کد متن‌باز (GitHub Repository)

---

## خلاصه

> شرکت Lyft مؤلفه Rate Limiting خود را به صورت متن‌باز منتشر کرده است. این کتابخانه بر اساس **Envoy Proxy** ساخته شده و از الگوریتم **Fixed Window** برای Rate Limiting استفاده می‌کند.

 Lyft این کتابخانه را برای استفاده در سیستم‌های توزیع شده خود طراحی کرده است. ویژگی‌های اصلی آن:

- **پیکربندی از طریق فایل YAML:** قوانین Rate Limiting از طریق فایل‌های YAML پیکربندی می‌شوند
- **پشتیبانی از چندین منبع:** پشتیبانی از Redis, Memcached و سایر بک‌اندها
- **مقیاس‌پذیری:** طراحی شده برای کار در محیط‌های توزیع شده

---

## ساختار پروژه

```
ratelimit/
├── src/                    # کد اصلی
├── configuration/          # نمونه فایل‌های پیکربندی
├── api/                    # تعریف‌های protobuf
├── test/                   # تست‌ها
└── docker/                 # فایل‌های Docker
```

---

## نمونه پیکربندی

```yaml
domain: envoy ratelimit
descriptors:
  - key: path
    value: /api/v1/endpoint
    rate_limit:
      unit: second
      requests_per_unit: 10
```

---

## یادداشت شخصی

> **اهمیت این منبع:** این مخزن GitHub یک پیاده‌سازی واقعی Rate Limiting در مقیاس تولیدی است. Lyft نشان می‌دهد چگونه می‌توان Rate Limiting را با استفاده از Envoy Proxy و سیستم‌های توزیع شده پیاده‌سازی کرد.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۸/۲۶
**منبع اصلی:** [Lyft Rate Limiting - GitHub](https://github.com/lyft/ratelimit)
