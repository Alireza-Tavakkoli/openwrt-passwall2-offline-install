# Passwall2 Manual Installation Guide for OpenWrt

## Persian Guide
Full Persian documentation: README_FA.md

## Introduction

In this guide, you will learn how to install Passwall2 manually on OpenWrt.

This method is useful when:

* You do not have unrestricted internet access on your router.
* You prefer to install the required files manually.
* The `opkg` or `apk` package manager is not working properly.

## 🔌 Step 1: Connect to Your Router

Before starting, you need to connect to your OpenWrt router.

Download and install PuTTY.

### 📥 Download

👉 [https://www.putty.org/]

### 📌 Connection Steps

1. Open PuTTY.
2. In the **Host Name** field, enter:

```
192.168.1.1
```

3. Click **Open**.

### 🔑 Log In to the Router

When the terminal window appears, enter:

**Username**

```
root
```

**Password**

```
Your router password
(Leave it blank if no password has been configured.)
```

### ❗ Troubleshooting

If you cannot connect:

* Make sure your computer is connected to the router.
* Your router's IP address may be different from `192.168.1.1`.
* On the first connection, PuTTY may display a security warning. Simply click **Yes** to continue.

## 🎯 Expected Result

If everything is successful, you should see a prompt similar to:

```
root@OpenWrt:~#
```

## 📊 Step 2: Identify Your OpenWrt Version and CPU Architecture

Before downloading Passwall2, you must determine:

* Your OpenWrt version
* Your device's CPU architecture

## 🧠 1. Check Your OpenWrt Version

Log in via SSH and run the following command:

```
cat /etc/openwrt_release
```

### 📌 Example Output

```
DISTRIB_RELEASE='23.05.2'
DISTRIB_ARCH='aarch64_cortex-a53'
```

## 📌 Important Fields

* `DISTRIB_RELEASE` → OpenWrt version
* `DISTRIB_ARCH` → CPU architecture

### ⚠️ Why This Matters

If you download packages for the wrong OpenWrt version or CPU architecture:

* ❌ The package may fail to install.
* ❌ You may receive an architecture mismatch error.
* ❌ Passwall2 may not run correctly after installation.

## 📥 Step 3: Download the Passwall2 Files

You will need a VPN or unrestricted internet access to download the required files.

## 🌐 Download Page

Visit the following page:

```
https://sourceforge.net/projects/openwrt-passwall-build/files/
```

## 🔑 Download the Repository Key

First, download the repository key that matches your OpenWrt version.

### OpenWrt 24.x and Earlier

Download the following file:

```
ipk.pub
```

### OpenWrt 25.x and Later

Download the following file:

```
apk.pub
```

## 📂 Select the Correct Package Directory

Open the following directory:

```
releases
```

Then select the folder that matches your OpenWrt version.

For example, if your system is running:

```
24.10
```

open:

```
packages-24.10
```

### 🖥️ Select Your CPU Architecture

Next, choose the directory that matches your device's CPU architecture.

For example, if your architecture is:

```
arm_cortex-a15_neon-vfpv4
```

open the folder with the same name.

## 📦 Download the Required Packages

In this step, you will work with two directories:

```
passwall_packages
passwall_luci
```

### 1️⃣ Download Dependencies

Open the following directory:

```
passwall_packages
```

If you do not have storage or bandwidth limitations, it is recommended to download all available files in this directory. This helps prevent dependency-related errors during installation.

### 2️⃣ Download the Passwall Web Interface

Next, open:

```
passwall_luci
```

and download the following package:

```
luci-app-passwall*
```

This package provides the Passwall web interface for OpenWrt's LuCI administration panel.

## 📤 Step 4: Transfer the Files to Your Router

After downloading the Passwall2 packages, you need to transfer them to your OpenWrt router.

Download and install WinSCP.

### 📥 Download

👉 [https://winscp.net/]

### 📌 Connection Steps

1. Open WinSCP.
2. Enter the following information:

* **File protocol:** `SCP`
* **Host name:** `192.168.1.1`
* **Username:** `root`
* **Password:** Your router password

3. Click **Login**.

### 📂 Transfer the Files

Upload all downloaded files to the following directory on your router:

```
/tmp/
```

### ✅ Done with WinSCP

Once all files have been successfully uploaded, you no longer need WinSCP for the remaining steps.

Return to your SSH session in PuTTY and continue with the installation process.

## ⚙️ Step 4: System Preparation Before Installing Passwall2 & Adding Repository Key

Before installing Passwall2 packages, it is recommended to prepare your system so that all required dependencies can be installed from official OpenWrt repositories.

## 🟡 OpenWrt Version 24 and Earlier

```
echo "nameserver 8.8.8.8" > /tmp/resolv.conf
echo "nameserver 8.8.4.4" >> /tmp/resolv.conf

opkg update
opkg remove dnsmasq
opkg install dnsmasq-full
opkg install kmod-ipt-nat
opkg install kmod-nft-socket
opkg install kmod-nft-tproxy
```

## 🔵 OpenWrt Version 25 and Later

```
echo "nameserver 8.8.8.8" > /tmp/resolv.conf
echo "nameserver 8.8.4.4" >> /tmp/resolv.conf

apk update
apk del dnsmasq
apk add dnsmasq-full
apk add kmod-ipt-nat
apk add kmod-nft-socket
apk add kmod-nft-tproxy
```

## 🔑 Add the Appropriate Repository Key

Before installing Passwall2, you must add the correct key based on your OpenWrt version.

### Key Selection

* OpenWrt 24 and earlier → `ipk.pub`
* OpenWrt 25 and later → `apk.pub`

### 🟡 OpenWrt 24 and Earlier

After transferring `ipk.pub` to your router, run:

```
cp /tmp/ipk.pub /etc/opkg/keys/
```

### 🔵 OpenWrt 25 and Later

After transferring `apk.pub` to your router, run:

```
cp /tmp/apk.pub /etc/apk/keys/
```
## 📦 Step 5: Install Passwall2 Packages

After downloading the files, transferring them to your router, and installing the required dependencies, you can now proceed with installing Passwall2.

## 🟡 OpenWrt 24 and Earlier (IPK)

First, navigate to the uploaded files directory:

```
cd /tmp
```

To list the transferred files:

```
ls
```

If you see `.ipk` files, start the installation:

```
opkg install *.ipk
```

## 🔵 OpenWrt 25 and Later (APK)

First, navigate to the files directory:

```
cd /tmp
```

To verify the files:

```sh id="v3n9sd"
ls
```

If you see `.apk` files, install them using:

```
apk add --allow-untrusted ./*.apk
```

## 🔍 Verify Installation

To confirm that Passwall2 has been installed successfully:

### OpenWrt 24

```
opkg list-installed | grep passwall
```

### OpenWrt 25

```
apk info | grep passwall
```

## 🔄 Final Step

Finally, reboot the router:

```
reboot
```
