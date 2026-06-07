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

---

### انتخاب معماری CPU دستگاه

حالا باید معماری CPU دستگاه خود را انتخاب کنید.

برای مثال اگر معماری دستگاه شما:

```text
arm_cortex-a15_neon-vfpv4
```

است، وارد پوشه‌ای با همین نام شوید.

---

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
* نام کلیدها به نوع بسته‌ها اشاره دارد:

*فایل `ipk.pub` برای بسته‌های IPK
*فایل `apk.pub` برای بسته‌های APK
این کلید برای اعتماد به پکیج‌ها و مخزن استفاده می‌شود.
در بسیاری از نصب‌های دستی IPK / APK ممکن است بدون این مرحله نیز نصب انجام شود.
اضافه کردن کلید باعث می‌شود فرآیند نصب تمیزتر و مطمئن‌تر باشد.
### نتیجه

پس از اضافه شدن کلید، می‌توانید نصب Passwall2 را ادامه دهید.
## ⚙️ مرحله 4: آماده‌سازی سیستم قبل از نصب Passwall2

قبل از نصب فایل‌های Passwall2، بهتر است سیستم را آماده کنید تا وابستگی‌های مورد نیاز از مخازن رسمی OpenWrt نصب شوند.

---

## 🌐 تنظیم DNS

اگر مخازن OpenWrt باز نمی‌شوند، یک DNS عمومی تنظیم کنید.

پیشنهاد:

```text
1.1.1.1
8.8.8.8
```

---

## ⚠️ غیرفعال کردن DNS Masq (در صورت نیاز)

در برخی موارد برای جلوگیری از تداخل DNS بهتر است DNS Masq را متوقف کنید:

### OpenWrt 24 و پایین‌تر

```bash
/etc/init.d/dnsmasq stop
/etc/init.d/dnsmasq disable
```

### OpenWrt 25 و بالاتر

```bash
service dnsmasq stop
```

> در صورت نیاز می‌توانید پس از پایان نصب مجدداً آن را فعال کنید.

---

## 🟡 OpenWrt 24 و پایین‌تر

### بروزرسانی مخازن

```bash
opkg update
```

### نصب پکیج‌های مورد نیاز

```bash
opkg install kmod-ipt-nat
sleep 2

opkg install kmod-nft-socket
sleep 2

opkg install kmod-nft-tproxy
```

---

## 🔵 OpenWrt 25 و بالاتر

### بروزرسانی مخازن

```bash
apk update
```

### نصب پکیج‌های مورد نیاز

```bash
apk add kmod-ipt-nat
sleep 2

apk add kmod-nft-socket
sleep 2

apk add kmod-nft-tproxy
```

---

## 📌 بررسی نصب موفق

برای اطمینان از نصب ماژول‌ها:

```bash
lsmod | grep nft
```

---

## 🎯 نتیجه این مرحله

پس از انجام مراحل بالا:

* DNS تنظیم شده است.
* مخازن بروزرسانی شده‌اند.
* ماژول‌های NAT و TProxy نصب شده‌اند.
* سیستم آماده نصب فایل‌های Passwall2 دانلود شده از SourceForge است.
## 📦 مرحله 5: نصب فایل‌های Passwall2

پس از دانلود فایل‌ها، انتقال آن‌ها به روتر و نصب وابستگی‌های لازم، حالا می‌توانید Passwall2 را نصب کنید.

---

## 🟡 OpenWrt 24 و پایین‌تر (IPK)

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

---

### در صورت مشاهده خطای وابستگی

ابتدا مخازن را بروزرسانی کنید:

```bash
opkg update
```

سپس دوباره نصب را انجام دهید.

---

## 🔵 OpenWrt 25 و بالاتر (APK)

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

---

### در صورت مشاهده خطا

ابتدا مخازن را بروزرسانی کنید:

```bash
apk update
```

سپس دوباره نصب را انجام دهید.

---

## 🔍 بررسی نصب

برای اطمینان از نصب Passwall2:

### OpenWrt 24

```bash
opkg list-installed | grep passwall
```

### OpenWrt 25

```bash
apk info | grep passwall
```

---

## 🎯 نتیجه

اگر مراحل بدون خطا انجام شده باشند:

* Passwall2 نصب شده است.
* رابط LuCI مربوط به Passwall2 نیز نصب شده است.
* آماده راه‌اندازی و تنظیم کانفیگ هستید.
## 📦 مرحله 5: نصب فایل‌های Passwall2

پس از دانلود فایل‌ها، انتقال آن‌ها به روتر و نصب پیش‌نیازها، حالا نوبت نصب Passwall2 است.

---

## 🟡 OpenWrt 24 و پایین‌تر (IPK)

ابتدا وارد مسیر فایل‌ها شوید:

```bash
cd /tmp
```

بررسی فایل‌های موجود:

```bash
ls *.ipk
```

### ترتیب پیشنهادی نصب

#### 1. وابستگی‌ها (Dependencies)

ابتدا تمام فایل‌های وابستگی را نصب کنید:

```bash
opkg install ./dependencies/*.ipk
```

> اگر وابستگی‌ها در پوشه جداگانه نیستند، ابتدا فایل‌هایی را نصب کنید که نام آن‌ها با `luci-i18n` یا `passwall2` شروع نمی‌شود.

---

#### 2. هسته‌های مورد نیاز

در صورت وجود:

```bash
opkg install xray-core*.ipk
```

یا:

```bash
opkg install sing-box*.ipk
```

یا هر دو (بسته به نیاز شما)

---

#### 3. نصب Passwall2

```bash
opkg install passwall2*.ipk
```

---

#### 4. نصب رابط گرافیکی LuCI

```bash
opkg install luci-app-passwall2*.ipk
```

---

#### 5. نصب ترجمه فارسی (اختیاری)

```bash
opkg install luci-i18n-passwall2-*.ipk
```

---

## 🔵 OpenWrt 25 و بالاتر (APK)

وارد مسیر فایل‌ها شوید:

```bash
cd /tmp
```

بررسی فایل‌ها:

```bash
ls *.apk
```

### ترتیب پیشنهادی نصب

#### 1. وابستگی‌ها

```bash
apk add --allow-untrusted ./dependencies/*.apk
```

---

#### 2. هسته‌های مورد نیاز

```bash
apk add --allow-untrusted xray-core*.apk
```

یا:

```bash
apk add --allow-untrusted sing-box*.apk
```

---

#### 3. نصب Passwall2

```bash
apk add --allow-untrusted passwall2*.apk
```

---

#### 4. نصب رابط LuCI

```bash
apk add --allow-untrusted luci-app-passwall2*.apk
```

---

#### 5. نصب ترجمه فارسی (اختیاری)

```bash
apk add --allow-untrusted luci-i18n-passwall2-*.apk
```

---

## 🎯 نتیجه

پس از اتمام مراحل بالا:

* Passwall2 نصب شده است.
* رابط گرافیکی LuCI نصب شده است.
* هسته‌های مورد نیاز (Xray / Sing-box) آماده استفاده هستند.
* سیستم آماده راه‌اندازی Passwall2 است.
## 🚀 مرحله 6: فعال‌سازی و راه‌اندازی Passwall2

پس از نصب موفق Passwall2، بهتر است سرویس را یک بار فعال و راه‌اندازی مجدد کنید.

---

### 🟡 OpenWrt 24 و پایین‌تر

فعال‌سازی سرویس:

```bash id="gk3ztn"
/etc/init.d/passwall2 enable
```

راه‌اندازی مجدد:

```bash id="zj7t88"
/etc/init.d/passwall2 restart
```

---

### 🔵 OpenWrt 25 و بالاتر

در بیشتر بیلدها همچنان از init.d استفاده می‌شود:

```bash id="d4zsc5"
/etc/init.d/passwall2 enable
/etc/init.d/passwall2 restart
```

---

### بررسی وضعیت سرویس

```bash id="40k0fa"
/etc/init.d/passwall2 status
```

یا:

```bash id="vl5u7q"
ps | grep passwall
```

---

### اگر رابط Passwall2 در LuCI نمایش داده نشد

یک بار رابط وب را رفرش کنید یا سرویس وب را ریستارت کنید:

```bash id="i6upn8"
/etc/init.d/uhttpd restart
```

---

## 🎯 پایان نصب

اگر همه مراحل را درست انجام داده باشید:

✅ Passwall2 نصب شده است.

✅ سرویس Passwall2 در حال اجرا است.

✅ بخش Passwall2 در پنل LuCI قابل مشاهده است.

اکنون می‌توانید کانفیگ‌های خود را وارد کرده و از Passwall2 استفاده کنید.
یه نکته کوچیک هم برای README: اگر خودت بعد از نصب معمولاً کل روتر رو ریبوت می‌کنی و نتیجه بهتری می‌گیری، می‌تونی آخرش اینم اضافه کنی:

reboot

چون بعضی ماژول‌های kmod-nft-* بعد از ریبوت مطمئن‌تر بارگذاری می‌شن.
