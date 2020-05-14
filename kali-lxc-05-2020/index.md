# Setting Up Kali Linux as an LXC Container

<!--more-->
![Banner](/images/categories/guide.png)

___
## Intro

__Kali Linux__ is the go-to linux distribution for penetration testing and CTF challenges. Whenever there was an assignment that I needed to do or a network attack that I needed to simulate I would open vmware and start my kali VM. After switching from running Windows 10 to Pop_OS! 20.04 I decided it would be a great time to explore some of the alternative methods of getting kali linux on your system such as using docker or using an LXC container.
___
## Why LXC and not Docker?

Short answer: LXC containers are better for virtualizing systems. Docker containers in general are designed to virtualize single applications, the containers are small containing only the necessary components to serve up a specific application. By comparison we want our Kali LXC container to contain Kali linux, any packages we install or update, and anything we are working on. While it is possible to do the same thing on docker this task seems better suited for an LXC container.
___
## What do I need to get started?

I will cover how I set it up, this is just a reference for you.
* A linux system with LXC (use LXD if you are on an ubuntu-based distro like Pop_OS!)
    * [Installing LXC on RHEL/Centos](https://www.tecmint.com/install-create-run-lxc-linux-containers-on-centos/)
    * [Installing LXD on Ubuntu](https://ubuntu.com/blog/lxd-in-4-easy-steps)
* The Kali Linux image from the [linux containers image server](https://us.images.linuxcontainers.org/)

___
## Setting Everything up

1. First step is to install LXC (or in my case LXD)
```bash
sudo install lxd
```
2. Initialize lxd (If you get permission denied issues add yourself to the lxd group.)
```
snap init

Would you like to use LXD clustering? (yes/no) [default=no]: 
Do you want to configure a new storage pool? (yes/no) [default=yes]: 
Name of the new storage pool [default=default]: lxcfs
Name of the storage backend to use (btrfs, dir, lvm, zfs, ceph) [default=zfs]: 
Create a new ZFS pool? (yes/no) [default=yes]: 
Would you like to use an existing block device? (yes/no) [default=no]: 
Size in GB of the new loop device (1GB minimum) [default=43GB]: 
Would you like to connect to a MAAS server? (yes/no) [default=no]: 
Would you like to create a new local network bridge? (yes/no) [default=yes]: 
What should the new bridge be called? [default=lxdbr0]: 
What IPv4 address should be used? (CIDR subnet notation, “auto” or “none”) [default=auto]: 
What IPv6 address should be used? (CIDR subnet notation, “auto” or “none”) [default=auto]: 
Would you like LXD to be available over the network? (yes/no) [default=no]: 
Would you like stale cached images to be updated automatically? (yes/no) [default=yes] 
Would you like a YAML "lxd init" preseed to be printed? (yes/no) [default=no]: 
```
3. Create the kali linux container
```
lxc launch images:kali/current/amd64 ck-kali
```
4. Drop into an interactive shell on the container.
```
lxc exec ck-kali /bin/bash
```
5. I prepared a [script](https://raw.githubusercontent.com/ckavidas/scripts/master/kali-lxc-setup.bash) that will help you with:
* Updating, upgrading and installing kali packages
* Add a kali user and configuring ssh
* Installing x2go and the kali xfce4 desktop environment
* Unfortunately wget and curl are missing so you will have to install wget before you can start. I will look into the possibility of using cloud init to do that for you. 
```
apt update && apt install wget -y
wget https://raw.githubusercontent.com/ckavidas/scripts/master/kali-lxc-setup.bash
chmod 744 kali-lxc-setup.bash
./kali-lxc-setup.bash
```
While there are instructions on the page to get a gui on the local system I wanted to have the ability to use x2go so I can access the Kali from my laptop.

6. Point your x2go or pyhocagui client to the kali container.

![Example 1: Using x2go to access the desktop environment.](/images/kali-lxc-5-2020/forwarded-x-session.png "Example 1: Using x2go to access the desktop environment.")
![Example 2: Using x2go to forward specific applications to the host.](/images/kali-lxc-5-2020/app-forwarding.png "Example 2: Using x2go to forward specific applications to the host.")


___
## References:

* [Kali Linux LXC/LXD Images Documentation](https://www.kali.org/docs/containers/kalilinux-lxc-images/)
* [Kali Linux XFCE FAQ](https://www.kali.org/docs/general-use/xfce-faq/)
