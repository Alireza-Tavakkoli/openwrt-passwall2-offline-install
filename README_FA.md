# آموزش نصب Passwall2 به صورت دستی روی OpenWrt
<br>

## مقدمه
در این آموزش یاد می‌گیرید چگونه Passwall2 را به صورت دستی (Manual) روی OpenWrt نصب کنید.

این روش برای زمانی است که:
- اینترنت آزاد بر روی روتر ندارید 
- یا می‌خواهید فایل‌ها را خودتان نصب کنید
- یا ابزار opkg / apk به درستی کار نمی‌کند
<br>

## 🔌 مرحله 1 : اتصال به روتر

قبل از هر کاری باید به روتر OpenWrt وصل شوید.

برنامه PuTTY را دانلود کرده .

📥 دانلود:

👉 [https://soft98.ir/internet/network/3197-putty.html]


### 📌 مراحل اتصال

1. برنامه PuTTY را باز کنید
2. در قسمت **Host Name** این را وارد کنید:

```
192.168.1.1
```

3. روی **Open** کلیک کنید



### 🔑 ورود به روتر

وقتی صفحه سیاه باز شد:

* Username :

```
root
```

* Password :

```
رمز روتر (اگر تنظیم نکردی خالی بگذار)
```

## ⚠️ نکات مهم

اگر وصل نشد:

- مطمئن شوید کامپیوتر به روتر وصل است
- آی‌پی ممکن است غیر از 192.168.1.1 باشد
- اولین اتصال ممکن است هشدار امنیتی بدهد (yes بزنید)

<br>

## 🎯 نتیجه این مرحله

اگر درست انجام شود باید وارد محیطی شوید که شبیه این است:

```
root@OpenWrt:~#
```
<br>

## 📊 مرحله 2 : پیدا کردن نسخه OpenWrt و معماری CPU

قبل از دانلود Passwall2 باید دقیقاً بدانید:

* نسخه OpenWrt
* معماری CPU دستگاه



## 🧠 1. بررسی نسخه OpenWrt

وارد SSH شوید و این دستور را بزنید:

```bash id="v1"
cat /etc/openwrt_release
```


### 📌 خروجی نمونه:

```id="v2"
DISTRIB_RELEASE='23.05.2'
DISTRIB_ARCH='aarch64_cortex-a53'
```



## 📌 معنی موارد مهم:

* `DISTRIB_RELEASE` →  OpenWrt نسخه
* `DISTRIB_ARCH` →  CPU معماری 


اگر در یاداشت معماری پردازنده و نسخه OpenWrt اشتباه کنید:

* ❌ پکیج نصب نمی‌شود
* ❌ یا ارور architecture می‌دهد
* ❌ یا Passwall اجرا نمی‌شود
<br>

## 📥 مرحله 3: دانلود فایل‌های Passwall2

برای دانلود فایل‌ها به فیلترشکن نیاز دارید.


## 🌐 سایت دانلود

به [صفحه](https://sourceforge.net/projects/openwrt-passwall-build/files/) زیر بروید:

```text
https://sourceforge.net/projects/openwrt-passwall-build/files/
```

<br>

## 🔑 دانلود کلید نصب

ابتدا کلید مربوط به نسخه OpenWrt خود را دانلود کنید:

### نسخه OpenWrt 24.x و قدیمی‌تر

فایل زیر را [دانلود](https://sourceforge.net/projects/openwrt-passwall-build/files/ipk.pub/download)  کنید:

```text
ipk.pub
```

### نسخه OpenWrt 25.x و جدیدتر

فایل زیر را [دانلود](https://sourceforge.net/projects/openwrt-passwall-build/files/apk.pub/download) کنید:

```text
apk.pub
```

<br>

## 📂 انتخاب فایل‌های مناسب

وارد پوشه:

```text
releases
```

شوید.

سپس پوشه‌ای را انتخاب کنید که با نسخه OpenWrt شما مطابقت دارد.

برای مثال اگر نسخه سیستم شما:

```text
24.10
```

است، وارد پوشه:

```text
packages-24.10
```

شوید.

<br>

### انتخاب معماری CPU دستگاه

حالا باید معماری CPU دستگاه خود را انتخاب کنید.

برای مثال اگر معماری دستگاه شما:

```text
arm_cortex-a15_neon-vfpv4
```

است، وارد پوشه‌ای با همین نام شوید.

<br>

## 📦 دانلود بسته‌های موردنیاز

در این مرحله با دو پوشه کار داریم:

```text
passwall_packages
passwall_luci
```

### 1️⃣ دانلود وابستگی‌ها

وارد پوشه:

```text
passwall_packages
```

شوید.

اگر محدودیت حجم یا فضای ذخیره‌سازی ندارید، پیشنهاد می‌شود تمام فایل‌های موجود را دانلود کنید تا بعداً با خطای وابستگی مواجه نشوید.

### 2️⃣ دانلود رابط کاربری Passwall

سپس وارد پوشه:

```text
passwall_luci
```

شوید و فایل زیر را دانلود کنید:

```text
luci-app-passwall*
```

<br>

## ⚠️ نکات مهم

قبل از دانلود، حتماً موارد زیر را بررسی کنید:

✅ نسخه فایل‌ها با نسخه OpenWrt شما یکسان باشد.

✅ معماری فایل‌ها با معماری دستگاه شما مطابقت داشته باشد.

<br>

## 📤 مرحله 4 : انتقال فایل‌ها به روتر

بعد از دانلود فایل‌های Passwall2 باید آن‌ها را به روتر OpenWrt منتقل کنید.


باید WinSCP را دانلود کنید .

### 📥 دانلود:

👉 [https://soft98.ir/internet/ftp-tools/748-winscp.html]


### 📌 مراحل اتصال:

1. برنامه WinSCP را باز کنید
2. اطلاعات زیر را وارد کنید:

* File protocol: `SCP`
* Host name: `192.168.1.1`
* Username: `root`
* Password: رمز روتر

3. روی Login کلیک کنید

<br>

### 📂 انتقال فایل‌ها:

فایل‌های دانلود شده را به این مسیر منتقل کنید:

```bash id="tmp3"
/tmp/
```
و تمام دیگه کارمون با WinSCP تموم میشه و دوباره وارد برنامه PuTTY میشم.
<br>


## ⚙️ مرحله 4: آماده‌سازی سیستم قبل از نصب Passwall2 و اضافه کردن کلید

قبل از نصب فایل‌های Passwall2، بهتر است سیستم را آماده کنید تا وابستگی‌های مورد نیاز از مخازن رسمی OpenWrt نصب شوند.

<br>

## 🟡 نسخه OpenWrt 24 و پایین‌تر

### نصب پکیج‌های مورد نیاز

```bash
echo "nameserver 8.8.8.8" > /tmp/resolv.conf
echo "nameserver 8.8.4.4" >> /tmp/resolv.conf
opkg update
opkg remove dnsmasq
opkg install dnsmasq-full
opkg install kmod-ipt-nat
opkg install kmod-nft-socket
opkg install kmod-nft-tproxy
```
<br>

## 🔵 نسخه OpenWrt 25 و بالاتر

```bash
echo "nameserver 8.8.8.8" > /tmp/resolv.conf
echo "nameserver 8.8.4.4" >> /tmp/resolv.conf
apk update
apk del dnsmasq
apk add dnsmasq-full
apk add kmod-ipt-nat
apk add kmod-nft-socket
apk add kmod-nft-tproxy
```

<br>


## 🔑 اضافه کردن کلید مناسب

قبل از نصب Passwall2 باید کلید مناسب نسخه OpenWrt خود را اضافه کنید.

### انتخاب کلید

  
نسحه OpenWrt 24 و پایین‌تر  `ipk.pub`      

نسخه OpenWrt 25 و بالاتر    `apk.pub`      

<br>

### نسخه OpenWrt 24 و پایین‌تر

فایل `ipk.pub` را به روتر منتقل کرده و اجرا کنید:

```bash
cp /tmp/ipk.pub /etc/opkg/keys/
```


<br>

### نسخه OpenWrt 25 و بالاتر

فایل `apk.pub` را به روتر منتقل کرده و اجرا کنید:

```bash
cp /tmp/apk.pub /etc/apk/keys/
```

<br>

### نکته مهم

* از کلید متناسب با نسخه OpenWrt خود استفاده کنید.
* استفاده از کلید اشتباه ممکن است باعث خطا در اعتبارسنجی پکیج‌ها شود.
* این کلید برای اعتماد به پکیج‌ها و مخزن استفاده می‌شود.
* در بسیاری از نصب‌های دستی IPK / APK ممکن است بدون این مرحله نیز نصب انجام شود.
* اضافه کردن کلید باعث می‌شود فرآیند نصب تمیزتر و مطمئن‌تر باشد.


<br>

## 📦 مرحله 5: نصب فایل‌های Passwall2

پس از دانلود فایل‌ها، انتقال آن‌ها به روتر و نصب وابستگی‌های لازم، حالا می‌توانید Passwall2 را نصب کنید.



## 🟡 نسخه OpenWrt 24 و پایین‌تر (IPK)

ابتدا وارد مسیر فایل‌ها شوید:

```bash
cd /tmp
```

برای مشاهده فایل‌های منتقل شده:

```bash
ls
```

اگر فایل‌های `.ipk` را مشاهده می‌کنید، نصب را آغاز کنید:

```bash
opkg install *.ipk
```

## 🔵 نسخه OpenWrt 25 و بالاتر (APK)

ابتدا وارد مسیر فایل‌ها شوید:

```bash
cd /tmp
```

برای مشاهده فایل‌ها:

```bash
ls
```

اگر فایل‌های `.apk` را مشاهده می‌کنید:

```bash
apk add --allow-untrusted ./*.apk
```


## 🔍 بررسی نصب

برای اطمینان از نصب Passwall2:

### نسخه OpenWrt 24

```bash
opkg list-installed | grep passwall
```

### نسخه OpenWrt 25

```bash
apk info | grep passwall
```
<br>


## 🚀 مرحله 6: فعال‌سازی و راه‌اندازی Passwall2

پس از نصب موفق Passwall2، بهتر است سرویس را یک بار فعال و راه‌اندازی مجدد کنید.



### 🟡 نسخه OpenWrt 24 و پایین‌تر

فعال‌سازی سرویس:

```bash id="gk3ztn"
/etc/init.d/passwall2 enable
```

راه‌اندازی مجدد:

```bash id="zj7t88"
/etc/init.d/passwall2 restart
```



### 🔵 نسخه OpenWrt 25 و بالاتر

در بیشتر بیلدها همچنان از init.d استفاده می‌شود:

```bash id="d4zsc5"
/etc/init.d/passwall2 enable
/etc/init.d/passwall2 restart
```


