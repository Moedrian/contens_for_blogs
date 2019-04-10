# Linux Directories

**Most of the following content is extracted from [TLCL](http://linuxcommand.org/tlcl.php)**

![random weird cat image](https://cdn.shopify.com/s/files/1/0344/6469/files/tumblr_oa1tspt5yH1uuyy36o1_500_large.gif?18126303191109649813)

## /

This is the root directory.  This is where the whole tree starts.

### /bin

This directory contains executable programs which are needed in single user mode and to bring the system up or repair it.

### /boot

Contains the Linux kernel, initial RAM disk image (for drivers needed at boot time), and the boot loader.

### /dev

This is a special directory that contains _device nodes_. "Everything is a file" alson applies for devices. Here is where the kernel maintains a list of all the devices it understands.

### /etc

The **`/etc`** directory contains all of the system-wide configuration files. It also contains a collection of shell scripts that start each of the system services at boot time. Everything in this directory should be readable text.

### /home

In normal configurations, each user is given a directory in **`/home`**. Ordinary users can only write files in their home directories. This limitation protects the system from errant user activity.

### /lib

Contains shared library files used by the core system programs. These are similar to dynamic link libraries (DLLs) in Windows.

### /lost+found

Each formatted partition or device using a Linux file system, such as ext4, will have this directory. It is used in the case of a partial recovery from a file system corruption event. Unless something really bad has happened to our system, this directory will remain empty.

### /media

On modern Linux systems the **`/media`** directory will contain the mount points for removable media such as USB drives, CD-ROMs, etc. that are mounted automatically at insertation.

### /mnt

On older Linux systems, the **`/mnt`** directory contains mount points for removable devices that have been mounted manually.

### /opt

The **`/opt`** directory is used to install "optional" software. This is mainly used to hold commercial software products that might be installed on the system.

### /proc

The **`/proc`** directory is special. It's not a real file system in the sense of files stored on the hard drive. Rather, it is a virtual file system maintained by the Linux kernel. The "files" it contains are peepholes into the kernel itself. The files are readable and will give us a picture of how the kernels see the computer.

### /root

This is the home directory for the root account.

### [/run]

According to this [page](https://lists.archlinux.org/pipermail/arch-projects/2011-March/000517.html):

> The **`/run`** mountpoint is supposed to be a tmpfs mounted during early boot, available and writable to for all tools at any time during bootup, it replaces **`/var/run/`**, which should become a symlink some day.

### /sbin

This directory contains "system binaries". These are programs that perform vital system tasks that are generally reserved for the superuser.

### /srv

According to [Wikipedia](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard):
>Site-specific data served by this system, such as data and scripts for web servers, data offered by FTP servers, and repositories for version control systems (appeared in FHS-2.3 in 2004).

### /sys

Contains information about devices, drivers, and some kernel features.

### /tmp

The **`/tmp`** directory is intended for the storage of temporary, transient files created by various programs. Some configurations cause this directory to be emptied each time the system is booted.

### /usr

The **`/usr`** directory tree is likely the largest one on a Linux system. It contains all the programs and support files used by regular users.

#### /usr/bin

**`/usr/bin`** contains the executable programs installed by the Linux distribution. It is not uncommon for this directory to hold thousands of programs.

#### /usr/sbin

Contains more system administration programs.

#### /usr/lib

The shared libraries for the programs in **`/usr/bin`**.

#### /usr/local

The **`/usr/local`** tree is where programs that are not included with the distribution but are intended for system-wide use are installed. Programs compiled from source code are normally installed in **`/usr/local/bin`**. On a newly installed Linux system, this tree exists, but it will be empty until the system administrator puts something in it.

#### /usr/share

**`/usr/share`** contains all the shared data used by programs in **`/usr/bin`**. This includes things such as default configuration files, icons, screen backgrounds, sound files, etc.

#### /usr/share/doc

Most packages installed on the system will include some kind of documentation. In **`/usr/share/doc`**, we will find documentation files organized by package.

### /var

With the exception of **`/tmp`** and **`/home`**, the directories we have looked at so far remain relatively static, that is, their contents don't change. The **`/var`** directory tree is where data that is likely to change is stored. Various databases, spool files, user mail, etc. are located here.

#### /var/log

**`/var/log`** contains log files, records of various system activity. These are important and should be monitored from time to time. The most useful ones are **`/var/log/messages`** and **`/var/log/syslog`**. Note that for security reasons on some systems only the superuser may view log files.