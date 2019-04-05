# Install CentOS to Raspberry Pi

## Before you start

* This file is based on
  * Windows 10
  * Your own WiFi
  * An Ethenet cable
* Why CentOS? Because on April 3rd 2019 Jack encountered a bizarre bug on Raspbian. After installing php 7.2, he rebooted it and he could never connect it via ssh by neither WiFI nor Ethenet cable...
* Damn it!
* **And the Official wiki is [here](https://wiki.centos.org/SpecialInterestGroup/AltArch/armhfp)**

## 1. Download the image

1. Find the edition you want [here](http://isoredirect.centos.org/altarch/7/isos/armhfp)
2. Download it and use 7z to deal with it. Just rename the .raw to .img, it works! Now write it into SD card via [Image Writer](https://sourceforge.net/projects/win32diskimager/).
3. Before inserting it into Pi, create an empty file named **ssh** and paste it into boot partition to enable ssh connection. Just ssh, no file extension affix.

## 2. Boot it, connect it, and expand it

1. Find an Ethenet cable and connect the pi to PC
2. Enable network sharing in Settings
3. Open some cmd software and type ```arp -a```
4. Find the IP address corresponding to Pi's MAC
5. Start a ssh session, use ```root@xxx.xxx.xxx.xxx``` and the password is ```centos```
6. ```less README```, follow its advice, so just type ```rootfs-expand```. Very user-friendly, isn't it?

## 3. Welcome to 1969, WiFi

1. It seems that the newest version of ARM CentOS has resolved WiFi firmware distribution dilemma, so just type ```systemctl start network.service``` and, hola, WiFi is now enabled.
2. Type ```nmcli d``` and wlan0 is here.
3. Now type ```nmtui``` and choose ```Activate a connection```, it's very easy to join the WiFi.
4. Type ```date```, damn it.

## 4. Add a Real Time Clock

## 5. A little server

If you browse the package [list](http://mirror.centos.org/altarch/7/os/armhfp/Packages/) of CentOS-altarch-armhfp, and there is no php 7 available. But I found a solution [here](https://seven.centos.org/2018/01/php-7-2-for-centos-7-armhfp/)

```cmd
cat > /etc/yum.repos.d/epel.repo << EOF
[epel]
name=Epel rebuild for armhfp
baseurl=https://armv7.dev.centos.org/repodir/epel-pass-1/
enabled=1
gpgcheck=0
EOF
```

then

```cmd
cat > /etc/yum.repos.d/php72-testing.repo << EOF
[php72-testing]
name=Remi php72 rebuild for armhfp
baseurl=https://armv7.dev.centos.org/repodir/community-php72-testing/
enabled=1
gpgcheck=0
EOF
```

finally

```cmd
cat > /etc/yum.repos.d/remi.repo << EOF
[remi]
name=Remi's RPM repository for Enterprise Linux 7 - $basearch
mirrorlist=http://cdn.remirepo.net/enterprise/7/remi/mirror
enabled=1
gpgcheck=1
gpgkey=https://rpms.remirepo.net/RPM-GPG-KEY-remi
EOF
```

Hola! The rest is easy.