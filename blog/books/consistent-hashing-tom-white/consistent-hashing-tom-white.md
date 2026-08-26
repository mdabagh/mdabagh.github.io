> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: Consistent Hashing

> **مقاله اصلی:** Consistent Hashing
> **نویسنده:** Tom White
> **تاریخ انتشار:** November 27, 2007
> **منبع:** https://tom-e-white.com/2007/11/consistent-hashing.html

---

## چکیده

> I've bumped into consistent hashing a couple of times lately. The paper that introduced the idea (Consistent Hashing and Random Trees: Distributed Caching Protocols for Relieving Hot Spots on the World Wide Web by David Karger et al) appeared ten years ago...

اخیراً چندین بار با هشینگ سازگار برخورد کرده‌ام. مقاله‌ای که این ایده را معرفی کرد (Consistent Hashing and Random Trees by David Karger et al) ده سال پیش منتشر شد، اما اخیراً به نظر می‌رسد این ایده به آرامی راه خود را به خدمات بیشتر و بیشتری باز کرده است، از Dynamo آمازون گرفته تا memcached.

---

## مشکل

> The need for consistent hashing arose from limitations experienced while running collections of caching machines. If you have a collection of n cache machines then a common way of load balancing across them is to put object o in cache machine number hash(o) mod n. This works well until you add or remove cache machines...

نیاز به هشینگ سازگار از محدودیت‌های تجربه‌شده هنگام اجرای مجموعه‌ای از ماشین‌های کش ناشی شد. اگر مجموعه‌ای از n ماشین کش دارید، رایج‌ترین راه ایجاد تعادل در بار بین آنها قرار دادن شیء o در ماشین کش شماره hash(o) mod n است. این روش خوب کار می‌کند تا زمانی که ماشین‌های کش را اضافه یا حذف کنید...

---

## راه‌حل

> It would be nice if, when a cache machine was added, it took its fair share of objects from all the other cache machines. Equally, when a cache machine was removed, it would be nice if its objects were shared between the remaining machines. This is exactly what consistent hashing does.

خوب می‌شد اگر وقتی یک ماشین کش اضافه می‌شد، سهم عادلانه خود را از تمام ماشین‌های کش دیگر می‌گرفت. به همین ترتیب، وقتی یک ماشین کش حذف می‌شد، خوب بود اگر اشیاء آن بین ماشین‌های باقی‌مانده تقسیم می‌شد. این دقیقاً کاری است که هشینگ سازگار انجام می‌دهد.

---

## الگوریتم

> The basic idea behind the consistent hashing algorithm is to hash both objects and caches using the same hash function. The reason to do this is to map the cache to an interval, which will contain a number of object hashes.

ایده اصلی پشت الگوریتم هشینگ سازگار این است که هم اشیاء و هم کش‌ها را با همان تابع هش هش کنید. دلیل این کار نگاشت کش به یک بازه است که تعدادی هش شیء را در خود جای می‌دهد.

> The hash function actually maps objects and caches to a number range. Imagine mapping this range into a circle so the values wrap around. To find which cache an object goes in, we move clockwise round the circle until we find a cache point.

تابع هش در واقع اشیاء و کش‌ها را به یک محدوده عددی نگاشت می‌کند. تصور کنید این محدوده را به یک دایره نگاشت کنید تا مقادیر دور بزنند. برای پیدا کردن اینکه شیء کجا می‌رود، ساعتگرد در دایره حرکت می‌کنیم تا به نقطه کش برسیم.

---

## نودهای مجازی

> The size of the intervals assigned to each cache is pretty hit and miss. Since it is essentially random it is possible to have a very non-uniform distribution of objects between caches. The solution to this problem is to introduce the idea of "virtual nodes", which are replicas of cache points in the circle.

اندازه بازه‌های اختصاص‌یافته به هر کش کاملاً تصادفی است. از آنجا که اساساً تصادفی است، ممکن است توزیع بسیار ناهمگنی از اشیاء بین کش‌ها وجود داشته باشد. راه حل این مشکل معرفی مفهوم "نودهای مجازی" است که نسخه‌های کپی نقاط کش در دایره هستند.

---

## پیاده‌سازی Java

```java
public class ConsistentHash<T> {
    private final HashFunction hashFunction;
    private final int numberOfReplicas;
    private final SortedMap<Integer, T> circle = new TreeMap<Integer, T>();

    public ConsistentHash(HashFunction hashFunction, int numberOfReplicas, Collection<T> nodes) {
        this.hashFunction = hashFunction;
        this.numberOfReplicas = numberOfReplicas;
        for (T node : nodes) {
            add(node);
        }
    }

    public void add(T node) {
        for (int i = 0; i < numberOfReplicas; i++) {
            circle.put(hashFunction.hash(node.toString() + i), node);
        }
    }

    public void remove(T node) {
        for (int i = 0; i < numberOfReplicas; i++) {
            circle.remove(hashFunction.hash(node.toString() + i));
        }
    }

    public T get(Object key) {
        if (circle.isEmpty()) {
            return null;
        }
        int hash = hashFunction.hash(key);
        if (!circle.containsKey(hash)) {
            SortedMap<Integer, T> tailMap = circle.tailMap(hash);
            hash = tailMap.isEmpty() ? circle.firstKey() : tailMap.firstKey();
        }
        return circle.get(hash);
    }
}
```

---

## یادداشت شخصی

> **اهمیت این مقاله:** این مقاله Tom White بهترین توضیح ساده و عملی از هشینگ سازگار است. مفهوم نودهای مجازی و پیاده‌سازی Java آن بسیار مفید است. این مقاله مستقیماً توسط کتاب System Design Interview به عنوان مرجع اصلی فصل Consistent Hashing معرفی شده است.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۸/۲۶
**منبع اصلی:** [Tom White - Consistent Hashing](https://tom-e-white.com/2007/11/consistent-hashing.html)
