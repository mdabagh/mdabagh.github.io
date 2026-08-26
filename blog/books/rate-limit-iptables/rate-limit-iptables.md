> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: Rate Limit کردن درخواست‌ها با Iptables

> **مقاله اصلی:** Rate Limit Requests with Iptables
> **نویسنده:** Stuart Page (Programster's Blog)
> **تاریخ انتشار:** August 16, 2018 (آخرین به‌روزرسانی: August 4, 2021)
> **منبع:** https://blog.programster.org/rate-limit-requests-with-iptables

---

## چکیده

> You can rate limit connections to your server by IP so that no single IP can create more than X connections per Y period before being blocked.

می‌توانید اتصالات به سرور خود را بر اساس IP محدود کنید به طوری که هیچ IP واحدی نتواند بیش از X اتصال در هر Y بازه زمانی ایجاد کند قبل از اینکه مسدود شود.

---

## اسکریپت Rate Limiting

```bash
#!/bin/bash
IPT=/sbin/iptables
# حداکثر زمان اتصال (ثانیه)
TIME_PERIOD=100
# حداکثر اتصالات در هر IP
BLOCKCOUNT=100

# عمل پیش‌فرض: DROP یا REJECT
DACTION="DROP"

$IPT -A INPUT -p tcp --dport 80 -i eth0 -m state --state NEW -m recent --set
$IPT -A INPUT -p tcp --dport 80 -i eth0 -m state --state NEW -m recent --update --seconds $TIME_PERIOD --hitcount $BLOCKCOUNT -j $DACTION

$IPT -A INPUT -p tcp --dport 443 -i eth0 -m state --state NEW -m recent --set
$IPT -A INPUT -p tcp --dport 443 -i eth0 -m state --state NEW -m recent --update --seconds $TIME_PERIOD --hitcount $BLOCKCOUNT -j $DACTION
```

> Make sure to run the script with sudo/root privileges on startup.

مطمئن شوید اسکریپت را با دسترسی sudo/root در هنگام راه‌اندازی اجرا کنید.

---

## تست کردن

```bash
#!/bin/bash
ip="آدرس IP سرور خود را اینجا قرار دهید"
port="80"
for i in {1..100}
do
  echo "exit" | nc ${ip} ${port};
done
```

> If you are using a proxy, then all requests will be coming from that one IP. You should add this to your proxy instead of your webserver.

اگر از پروکسی استفاده می‌کنید، تمام درخواست‌ها از آن یک IP می‌آیند. باید این را به جای وب‌سرور خود به پروکسی خود اضافه کنید.

---

## یادداشت شخصی

> **اهمیت این مقاله:** این مقاله نشان می‌دهد چگونه می‌توان Rate Limiting را در **لایه ۳ شبکه (IP)** با استفاده از **iptables** در لینوکس اعمال کرد. این روش برای جلوگیری از حملات DDoS و Brute Force در سطح شبکه مفید است.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۸/۲۶
**منبع اصلی:** [Programster's Blog](https://blog.programster.org/rate-limit-requests-with-iptables)
