# راهنمای نصب Passwall2 روی OpenWrt

این پروژه برای نصب Passwall2 و حل مشکل وابستگی‌ها روی OpenWrt ساخته شده.

---

## مشکل

خیلی از کاربران موقع نصب Passwall2 با خطای وابستگی یا نصب آفلاین مشکل دارند.

---

## راه‌حل

### مرحله 1: آپدیت پکیج‌ها
opkg update

### مرحله 2: نصب پیش‌نیازها
opkg install luci-compat luci-base

### مرحله 3: نصب Passwall2
opkg install passwall2.ipk

### مرحله 4: فعال کردن سرویس
/etc/init.d/passwall2 enable
/etc/init.d/passwall2 start

---

## نکته

اگر LuCI نمایش داده نشد، کش مرورگر را پاک کنید
