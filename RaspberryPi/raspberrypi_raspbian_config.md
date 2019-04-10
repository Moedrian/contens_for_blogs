# Setting up Raspberry Pi with Raspbian Strech Lite

## Before You Start

* Hardwares

1. Raspberry Pi with its power cable
2. SD card 16G or 32G
3. SD card reader
4. PC
5. WiFi or an Ethenet cable

* Softwares

1. [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/) - to write the system into the SD card
2. [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) - to establish ssh connection
3. [FileZilla](https://filezilla-project.org/download.php?type=client) - to transfer files via ftp

* And you need to know

1. Basic usage of vim
2. Basic usage of Linux

## 1. Raspbian

[Raspbian](https://www.raspberrypi.org/documentation/raspbian/) is an official operating system for all models of the Raspberry Pi. They also lists some other systems you can try with. Click [here](./raspberrypi_centos_config.md) for a CentOS installation guide.

### 1.1 Download

Here is the [website](https://www.raspberrypi.org/downloads/raspbian/) for downloading.
If you have a monitor and an HDMI cable, just download the one with desktop, which is quite user-friendly. They get a Minecraft!

### 1.2 Installation

#### 1.2.1 Write SD card

You need [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/) to do this. First, unzip the file you downloaded then open Image Writer, plug the SD card reader into PC, choose the file, finally click the write button.

#### 1.2.2 Enable ssh

For security reasons, Raspbian disables ssh by default. Just create a empty file named ```ssh``` and throw it into boot partition's root directory.

#### 1.2.3 WiFi

Create another file and rename it ```wpa_suppliant.conf``` and add these contents below

```conf
country=CN         # your country abbr

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev

update_config=1

network={
  ssid="xxxxxx"    # your WiFi SSID
  psk="xxxxxxx"    # password for WiFi
  priority=x       # when you have more than one wireless network
                   # use this option to mark its priority
                   # or just ignore it
  id_str="xxxxxx"  # a nickname for this network connection
}
```

Throw this file into boot as well.

## 2. Power on

## 3. Configuration

### 3.1 Secure shell connection

Open router's management page or connect it with an Ethernet cable via shared network then execute ```arp -a``` in cmd, find the IP address corresponding to Pi's MAC, then open a cmd and enter:

```cmd
ssh pi@192.168.xxx.xxx
```

Hit the ```<Enter>```, you'll be prompted to enter the password, which, by default, is ```raspberry```.

### 3.2 Raspi-config

Enter ```sudo raspi-config``` in the command window, and then use arrow keys and Enter to navigate and select.

* Change User Password
* (Optional) Choose Network Options then choose Hostname, set a new name for pi that doesn't contains spaces and capital letters.
* Localisation Options
  * Change Timezone, select according to your location.
  * Change WiFi Country
* Finally select Advanced Options then Expand Filesystem

After you finished all above, reboot it. Reconnect it, do whatever you want.