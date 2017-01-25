## Mah Linux

I built a home computer using GA-Z77-HD3 motherboard, i3 CPU and five WD disks. It's supposed to be a file server but I also use it as normal desktop. Here are some notes primarily for myself about the configuration in case I have to redo it.

### BIOS

Motherboard comes with F1 version, GA website says F2b is available but it's beta. I was able to find F3. Here are these versions for the reference. F3 seems to be working just fine so I'm sticking with it. The update is simple: format USB stick with FAT, copy files there, start PC and hit End key or select QFlash from BIOS settings. There you can select BIOS images from USB stick and update the PC.

* [F1 from the GA website](/files/Z77HD3.F1), origin: [GA](http://www.gigabyte.us/products/product-page.aspx?pid=4408#bios)
* [F3 from TweakTown](/files/Z77HD3.F3), origin: [TweakTown](https://forums.tweaktown.com/gigabyte/28441-gigabyte-beta-bios.html)

### Distro

I decided to use Debian because it's stable and well supported.

* Get live image here: [Live CD](https://www.debian.org/CD/live/).
* Copy to USB stick using

```bash
sudo dd if=debian-live-8.7.1-amd64-kde-desktop.iso of=/dev/sdX bs=4M; sync
```

* Boot into Linux from USB stick.
* Use *parted* to create GPT with free space on the new bootable disk.
