# LAMP Stack Installation on CentOS 7 64 Bit

## Before you start...

* Basic usage of vim, if none, use nano instead

## 1. Install essential repositories and editor

### 1.1 Update

```cmd
$ sudo yum update
```

### 1.2 Install EPEL repository

> Extra Packages for Enterprise Linux (or EPEL) is a Fedora Special
> Interest Group that creates, maintains, and manages a high quality 
>set of additional packages for Enterprise Linux, including, but not 
>limited to, Red Hat Enterprise Linux (RHEL), CentOS and Scientific 
>Linux (SL), Oracle Linux (OL).

```cmd
$ sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

### 1.2.Install Remi's RPM repository

> Remi is a repository providing the latest versions of the PHP stack, 
>full featured, and some other software, to the Fedora and Enterprise 
>Linux (RHEL, CentOS, Oracle, Scientific Linux, ...) users.

```cmd
$ sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```

### 1.4 Check repo list

```cmd
$ sudo yum repolist
```

### 1.5 Install yum-utils package (for the yum-config-manager command)

```cmd
$ sudo yum install yum-utils -y
```

### 1.5 Update it again

```cmd
$ sudo yum update
```

### 1.6 Install Vim

```cmd
$ sudo yum install vim -y
```

## 2. Apache

### 2.1 Install Apache and enable httpd service

```cmd
$ sudo yum install httpd -y
$ sudo systemctl start httpd.service
$ sudo systemctl enable httpd.service
```

### 2.2 Test Apache Installation

Enter http://your_ip_address/ in your browser's address bar, if you can 
see a page reading 'It works' then we could proceed to next step. If not, 
then the 80 port, which is for http, may be closed by default

* If your enabled firewalld then enter

```cmd
$ sudo firewall-cmd --list-all
```

The output may be like this

```output
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: wlan0
  sources:
  services: ssh dhcpv6-client http
  ports: 22/tcp 2888/tcp
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

Enter this command and reload it

```cmd
$ sudo firewall-cmd --add-service=http --permanent
$ sudo firewall-cmd --reload
```

* Or you may refer to port management page via your server vendor

## 3. MariaDB

### 3.1 Create MariaDB repo file

Enter command:

```cmd
$ sudo vim /etc/yum.repos.d/MariaDB.repo
```

Then type or copy & paste these text into it:

```text
# MariaDB 10.3 CentOS repository list
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.3/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

You can always find newest contents [here](https://downloads.mariadb.org/mariadb/repositories)

### 3.2 Install MariaDB and enable its service

```cmd
$ sudo yum install MariaDB-server MariaDB-client -y
$ sudo systemctl start mariadb.service
$ sudo systemctl enable mariadb.service
```

### 3.3 Config MariaDB

```cmd
$ sudo mysql_secure_installation
```

Follow the instructions appearing on the screen, set a root password 
and forbid root remote login for security

### 3.4 Open port for mysql

```cmd
$ sudo firewall-cmd --get-active-zones
```

> Which could print a single public zone or a few, like *public* and 
>*dmz*. Run the command below for any zone shown on the screen, replacing 
>`<zone>` and `<mysql_port>` with your system’s current setup:

```cmd
$ sudo firewall-cmd --zone=public --add-port=3306/tcp --permanent
$ sudo firewall-cmd --reload
```

## 4. PHP 7.3

### 4.1 Config repo

```cmd
$ sudo yum-config-manager --enable remi-php73
```

### 4.2 Install php and php extensions

```bash
$ sudo yum install php73-php
```

Choose the modules you need for your projects:

```bash
$ sudo yum install php-curl php-ldap php-zip php-fileinfo php-opcache \
php-pecl-apcu php-cli php-pear php-pdo php-mysqlnd php-pgsql php-pecl-mongodb \
php-pecl-redis php-pecl-memcache php-pecl-memcached php-gd php-mbstring \
php-mcrypt php-xml -y
```

And don't forget the composer, the dependency manager

```bash
$ sudo yum install composer -y
```

### 4.3 Restart Apache

```cmd
$ sudo systemctl restart httpd.service
```

### 4.4 Test php installation

```cmd
$ sudo echo "<?php phpinfo(); ?>" > /var/www/html/index.php
```

Enter http://your_ip_address/index.php in browser's address bar, if 
successful, you can see a long page listing php's information

## 5. phpMyAdmin

### 5.1 Install

```cmd
$ sudo yum install phpMyAdmin -y
```

### 5.2 Config phpMyAdmin

Open config file

```cmd
$ sudo vim /etc/httpd/conf.d/phpMyAdmin.conf
```
Under those `<RequireAny>` tags, add `Require all granted` right above the
`</RequireAny>` tags.

Better to install SSL support!

```conf
<Directory /usr/share/phpMyAdmin/>
        Options none
        AllowOverride Limit
        Require all granted
</Directory>
```
### 5.3 Restart Apache to apply changes

```cmd
$ sudo systemctl restart httpd.service
```

### 5.4 Test phpMyAdmin installation

Enter http://your_ip_address/phpmyadmin/ in address bar, log in by 
entering mariadb's auth you set before
