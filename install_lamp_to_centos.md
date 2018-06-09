# 安装 LAMP 环境到 CentOS 7

## 1.系统初始更新
#### 1.1 执行更新
```
# yum update -y
```
#### 1.2 安装 EPEL 源
```
# yum install epel-release -y
```
#### 1.3 安装 REMI 源
```
# yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
#### 1.4 验证 EPEL 源
```
# yum repolist
```
#### 再执行一步更新服务器
```
# yum update -y
```
## 2. 安装 MariaDB 
#### 2.1 创建 MariaDB 的 repo
```
# vi /etc/yum.repos.d/MariaDB.repo
```
#### 2.2 添加 MariaDB 的 yum 源，在文件中添加以下代码
```
[mariadb]
name = MariaDB
baseurl = https://mirrors.tuna.tsinghua.edu.cn/mariadb/yum/10.1/centos7-amd64
gpgkey = https://mirrors.tuna.tsinghua.edu.cn/mariadb/yum//RPM-GPG-KEY-MariaDB
gpgcheck = 1
```
#### 2.3 安装 MariaDB，并设置为开机自启
```
# yum --enablerepo=remi install mariadb mariadb-server -y
# systemctl start mariadb.service
# systemctl enable mariadb.service
```
#### 2.4 设置 MariaDB 的 root 密码，按照提示操作即可
```
# mysql_secure_installation
```
## 3. 配置 Apache
#### 3.1 安装 Apache，并设置为开机自启
```
# yum install httpd -y
# systemctl start httpd.service
# systemctl enable httpd.service
```
#### 3.2 测试 Apache 的安装
在浏览器内输入 http://ip_address/ ,将 ip_address 替换为自己的主机地址<br>
若出现 Apache 的测试页面，即为安装成功
## 4. 安装 PHP 7
#### 4.1 配置源
```
# yum install yum-utils
# yum-config-manager --enable remi-php72
```
#### 4.2 安装 PHP 及相关软件包
```
# yum install php php-curl php-ldap php-zip php-fileinfo php-opcache php-pecl-apcu php-cli php-pear php-pdo php-mysqlnd php-pgsql php-pecl-mongodb php-pecl-redis php-pecl-memcache php-pecl-memcached php-gd php-mbstring php-mcrypt php-xml -y
```
#### 4.3 重启 Apache 服务器
```
# systemctl restart httpd.service
```
#### 4.4 测试 PHP 安装
新建一个 php 文件
```
# vi /var/www/html/info.php
```
将以下代码添加到新建的文件里
```php
<?php
phpinfo();
?>
```
在浏览器地址栏输入 http://ip_address/info.php<br>
若出现含有 php 版本等信息的页面，表示安装成功
## 5. 安装 phpMyAdmin
#### 5.1 安装
```
# yum --enablerepo=remi install phpMyAdmin -y
```
#### 5.2 配置 phpMyAdmin，允许远程连接
打开配置文件进行编辑
```
# vi /etc/httpd/conf.d/phpMyAdmin.conf
```
添加如下代码
```
<Directory /usr/share/phpMyAdmin/>
        Options none
        AllowOverride Limit
        Require all granted
</Directory>
```
将验证方式由 cookie 改为 http，打开以下文件进行编辑
```
# vi /etc/phpMyAdmin/config.inc.php
```
更改为如下所示
```$xslt
[...]
/* Authentication type */
$cfg['Servers'][$i]['auth_type'] = 'http';
/* Server parameters */
[...]
```
#### 5.3 重启 Apache
```$xslt
# systemctl restart httpd.service
```
#### 5.4 验证安装
在浏览器地址栏输入 http://ip_address/phpmyadmin/ <br>
使用 root 及之前设置的 MySQL root 密码登录

# ...done!
