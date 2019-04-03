# Setting Up Raspberry Pi And Installing LAMP 

## Before You Start

* Hardwares

1. 树莓派及其电源线
2. SD 卡，容量大于等于 16 G
3. 读卡器
4. PC
5. WiFi，且可以登录路由器的管理页面

* Softwares

1. [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)
2. [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
3. [FileZilla](https://filezilla-project.org/download.php?type=client)

## 1. [Raspbian](https://www.raspberrypi.org/documentation/raspbian/) 系统安装

Raspbian 是为树莓派设计基于 Debian 的操作系统，被列为官方支持的系统之一。

### 1.1 下载

在官方提供的[网站](https://www.raspberrypi.org/downloads/raspbian/)下载
可以看到官网提供了 RASPBIAN STRETCH WITH DESKTOP 以及 RASPBIAN STRETCH LITE 两种版本
如果有显示器以及 HDMI 线缆且需要 GUI 的话，选择含有桌面环境的第一个进行下载
_以下内容假定以不含桌面环境_

### 1.2 安装系统

#### 1.2.1 将系统写入 SD 卡

这一步需要 [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)
找到下载的文件进行解压，获得了一个 .img 文件，将含有 SD 卡的读卡器插入 PC，打开 Win32 Disk Imager，在 Image File 处选择镜像存储目录，在 Device 处选择正确的盘符，点击 Write 开始写入

#### 1.2.2 开启 SSH 的准备工作

出于安全的考量，树莓派的系统默认关闭了 SSH 选项，为了开启 SSH，需要新建一个文本文件，命名为 ssh 后去掉扩展名变成空白文件

#### 1.2.3 连接 WiFi 的准备工作

再新建一个文本文件重命名为 wpa_suppliant.conf，用 Notepad 打开，输入以下内容

```conf
country=CN

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev

update_config=1

network={
  ssid="xxxxxx"    # 这里把 xxx 替换为 WiFi 的名字
  psk="xxxxxxx"    # 这里是 WiFi 的密码
  priority=x       # 当环境中存在多个无线网络时，在这里用阿拉伯数字来表明 WiFi 的优先级，数字越大，优先级越高
  id_str="xxxxxx"  # 当前网络的备注，passwd_home 之类的
}
```

完成之后打开文件管理器。把这两个文件拖到名为 boot 的分区里

### 3. 插卡上电

## 2. 系统配置

### 2.1 SSH 连接

访问路由器的管理界面，查看已连接设备，记下 raspberrypi 的 IP 地址。
打开 PuTTY，在 IP address 栏内输入以上地址后点击 Open，在弹出的界面选择 Yes 后会出现以下内容：

```bash
Using username "pi".
pi@xxx.xxx.xxx.xxx's password:
```

输入默认密码 raspberry 登录。

### 2.2 基础设置

在终端中输入以下内容：

```bash
sudo raspi-config
```

在接下来出现的界面使用方向键与回车操作：

* 选择 Change User Password 后输入新设定的密码
* (可选) 选择 Network Options 后选择 Hostname，给树莓派起一个中意的名字，注意不能包含空格及大写字母
* 选择 Localisation Options，
  * 选择 Change Timezone，依次选择 Asia Shanghai
  * 选择 Change WiFi Country，向下找到 CN China 选定
* 选择 Advanced Options 后选择 Expand Filesystem

完成以上工作后重启树莓派等候片刻，重新连接。