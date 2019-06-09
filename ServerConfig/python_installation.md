# Python Manual Installation

## Prerequisites

![Ah again](https://i.kym-cdn.com/entries/icons/original/000/029/223/cover2.jpg)

* *DEVELOPMENT TOOLS & BUILD-ESSENTIAL INTENSIFIES*
* *WGET*

Debian
```cmd
$ sudo apt install build-essential
```
Fedora/CentOS
```cmd
$ sudo dnf/yum groupinstall "Development Tools"
```

## Download and Unzip

Click the Gzipped source tarball to download,

![Python Source Releases](../assets/server/PythonSrc.png)

then locate to `/usr/src`, run

```cmd
$ sudo wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tgz
$ sudo tar xzf Python-3.7.3.tgz
```

## Compile

Go to the directory you get from last step

```cmd
$ cd Python-3.7.3
$ sudo ./configure --enable-optimization
$ sudo make altinstall
$ sudo rm ../Python-3.7.3.tgz
```

## Check

```cmd
$ python3.7 --version
```

If the output is

```cmd
Python 3.7.3
```

![Happiness Noise](https://i.kym-cdn.com/entries/icons/mobile/000/028/663/cover2.jpg)


## Python Virtual Environment

```cmd
$ python3.7 -m pip --user install virtualenv
```

>Slow downloading speed? Try to find some other PyPi mirror!

Locate to the project directory, run

```cmd
$ python3.7 -m virtualenv some_fancy_env_name
```

If there are error messages, especially in vagrant virtual machine, try

```cmd
$ python3.7 -m virtualenv env_name --always-copy
```

After executing these commands, I suggest a system restarting. Once
the system is ready, re-locate to the directory before, run

```cmd
$ source env_name/bin/activate
```

to activate the virtual environment. Now in front of the `$` is a pair of
parentheses contains your env name you set before.

If you want to leave, simply run `deactivate`.