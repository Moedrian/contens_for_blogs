# How to Install Redis as a Cache (Single Instance)

## Prerequisites

To install redis from compilation, you need to install 

* `wget`, to download the source code
* `compiler`, etc
    On Fedora or CentOS, `dnf/yum groupinstall "Development Tools"`, 
    On Debian, `apt install build essential`

## Download and Compilation

Go to [Redis Homepage](https://redis.io/), copy the link they offered for stable version.

Located to `/usr/src` or just `/home/current_user`, suppose you were at
`/usr/src`. For example,

```cmd
$ sudo wget http://download.redis.io/releases/redis-5.0.5.tar.gz
$ sudo tar xzf redis-5.0.5.tar.gz
$ cd redis-5.0.5/
```

And then now you were at `/usr/src/redis-5.0.5/`. Next, run `make`, which
would take a bit longer. After the compilation is complete, run `make test`
to check the integrity of `make` as suggested in the output messages. If
all of tests passed, run `make install` to place those executable files under
correspond directories.

```cmd
$ sudo make
$ sudo make test
$ sudo make install
```

## Configuration

Create essential directories to store the conf log files.

```cmd
$ sudo mkdir /etc/redis
$ sudo mkdir -p /var/redis/
$ sudo touch /var/log/redis.log
$ sudo chmod 755 /var/log/redis.log
```

Next, edit the configuration file

```cmd
$ sudo vim /etc/redis/redis.conf
```

Find these define statements and change them to the below
expressions, or according to your need.

```config
port             6379
daemonize        yes
supervised       systemd
pidfile          /var/run/redis.pid
loglevel         notice
logfile          /var/log/redis.log
dir              /var/redis/

maxmemory        256mb
maxmemory-policy allkeys-lfu
```

About the `maxmemory-policy` option, check this [page](https://redis.io/topics/lru-cache) for further info.

## Systemd Service

> <pre>
> Ah, systemd is a powerful tool!
>                           -- me 
> </pre>

Create a new systemd service to control Redis's behaviors

```cmd
$ sudo vim /etc/systemd/system/redis.service
```

Then add lines shown below

```systemd service
[Unit]
Description=Redis As LFU Cache
After=network.target

[Service]
User=root
Group=root
ExecStart=/usr/local/bin/redis-server /etc/redis/redis.conf
ExecStop=/usr/local/bin/redis-cli shutdown
Restart=always
Type=notify

[Install]
WantedBy=multi-user.target
```

Save and quit, 

```cmd
$ sudo systemctl start redis
$ sudo systemctl enable redis
$ sudo systemctl status redis
```

The output goes like

```output
   Loaded: loaded (/etc/systemd/system/redis.service; enabled; vendor preset: disabled)
   Active: active (running) since Sun 2019-06-09 15:39:56 CST; 8s ago
  Process: 20668 ExecStop=/usr/local/bin/redis-cli shutdown (code=exited, status=0/SUCCESS)
 Main PID: 20670 (redis-server)
   CGroup: /system.slice/redis.service
           └─20670 /usr/local/bin/redis-server 127.0.0.1:6379
```

## Try...

Type `redis-cli ping`, if you get a response `PONG`, then the installation
is successful completed.