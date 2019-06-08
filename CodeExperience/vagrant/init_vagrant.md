# Vagrant Initialization (with Virtual Box in Windows)

## Installation

The official sites of Vagrant is [here](https://www.vagrantup.com/downloads.html) and VirtualBox's is [here](https://www.virtualbox.org/wiki/Downloads).
Following their default option to install is rather practical. After
the installation is complete, make sure the Environment variables 
contains vagrant.exe's path. To assure this, You may be prompted to 
restart your PC.

## Get Box Preparation Ready

Choose a folder to place your vagrant box, that is, the virtual machine.
By the way, Vagrant provides commands to init and install box simultaneously 
like

```cmd
$ vagrant init hashicorp/precise64
```

But I suggest to download a box file manually from this [site](https://app.vagrantup.com/boxes/search), find
the distro you want and go to host to download directly via tools like
Free Download Manager, etc. Place it in a nearby directory beside your
vagrant box directory chosen before.

For example, I choose CentOS 7 and go to the description page and it goes
like this

![CentOS Release](../../assets/vagrant/CentOSRelease.png)

then go to virtualbox Externally hosted site, as demonstrated below

![CentOS Files](../../assets/vagrant/CentOSFiles.png)

and click and click, find the latest version, use those downloading
tools to get them. Guess what, the hosted images are sometimes further
newer than those listed on the Vagrant Cloud page.

Here, I placed the box downloaded before in `VM` directory and chose the
`Amadeus` directory to store those virtual machine configuration files.

![Vagrant Directories](../../assets/vagrant/VagrantDir.png)

## Initialization Commands

Open a terminal in `Amadeus` directory, and type command

```cmd
vagrant box add BOXNAME BOXPATH
```

for instance, the output shall be like messages below

```cmd
C:\Codes\Vagrant\Amadeus>vagrant box add Amadeus ..\VM\CentOS-7-x86_64-Vagrant-1905_01.VirtualBox.box
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'Amadeus' (v0) for provider:
    box: Unpacking necessary files from: file://C:/Codes/Vagrant/VM/CentOS-7-x86_64-Vagrant-1905_01.VirtualBox.box
    box: Progress: 100% (Rate: 244M/s, Estimated time remaining: --:--:--)
==> box: Successfully added box 'Amadeus' (v0) for 'virtualbox'!
```

Then, type `vagrant init`, the output is

```cmd
C:\Codes\Vagrant\Amadeus>vagrant init
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```

## How to Edit Vagrantfile

The `Vagrantfile` generated defines the behavior of the virtual machine,
from host name to network settings, and it is written in Ruby, so please
make sure the `end`s are closed properly after your editing.