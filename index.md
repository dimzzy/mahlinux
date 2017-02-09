## Mah Linux

I built a home computer using GA-Z77-HD3 motherboard, i3 CPU and five WD disks. It's supposed to be a file server but I also use it as normal desktop. Here are some notes primarily for myself about the configuration in case I have to redo it.

### Updating BIOS

Motherboard comes with F1 version, GA website says F2b is available but it's beta. I was able to find F3. Here are these versions for the reference. F3 seems to be working just fine so I'm sticking with it. The update is simple: format USB stick with FAT, copy files there, start PC and hit `End` key or select QFlash from BIOS settings. There you can select BIOS images from USB stick and update the PC.

* [F1 from the GA website](/files/Z77HD3.F1), origin: [GA](http://www.gigabyte.us/products/product-page.aspx?pid=4408#bios)
* [F3 from TweakTown](/files/Z77HD3.F3), origin: [TweakTown](https://forums.tweaktown.com/gigabyte/28441-gigabyte-beta-bios.html)

### Installing Linux

I decided to use Debian because it's stable and well supported.

* Get live image here: [Live CD](https://www.debian.org/CD/live/).
* Copy to USB stick (on Linux):

```shell
sudo dd if=image.iso of=/dev/sdX bs=4M; sync
```

* Boot into Linux from USB stick.
* Use `parted` to create GPT with free space on the new bootable disk:

```shell
sudo parted /dev/sdX
mklabel GPT
```

* Reboot and start install process.
* Use guided partitioning and tell it to use whole disk. I'm planning to leave some free space in case I would want to install other OS so at this point return back, delete primary `etx4` partition and recreate it using some smaller size. It's important though to ask installer to use the whole disk first because it will create partitions for `grub` and `swap`.
* Continue with installation and we should be done.

### User Settings

* Add myself to `sudoers`:

```shell
su
adduser dimzzy sudo
exit
```
### Various Fixes

* Rename `zed.service` to `zfs-zed.service` in `/etc/systemd/system`
* Edit `zfs-zed.service` to point to the right `zed` binary; specifically `/usr/sbin/zed`

### Installing Cisco VPN

Follow this article: [Cisco VPN](http://www.socsci.uci.edu/~jstern/uci_vpn_ubuntu/).
Specifically do:
```shell
sudo apt-get install lib32z1 lib32ncurses5 libpangox-1.0 network-manager-openconnect remmina
```
Remmina is my remote desktop client of choice.
