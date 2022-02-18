---
title: Linux on older CPUs with PAE
author:
  name: Aphive
  link: https://github.com/aphive
date: 2022-02-11 14:10:00
categories: [Linux, 32bit]
tags: [linux, 32bit, pae]
---

On machines with older Pentium M ™ and Celeron M ™ processors, there is an extra requirement to get Linux installed, I’ve encountered this mainly with Linux Lite as that is the OS of choice I use for older systems. **You can only install 32bit OSs on these CPUs.**

I recently had someone ask if they could install an OS on one of these machines and I had to look this up again. I am still in the process to get this machine up and running but will wupdate the post once I get to end of job whatever the case, be it installed or not.

> This only works if your installation is failing with this error:
> `kernel requires features not present on the CPU: PAE`
{: .prompt-warning }

Once you get to the boot menu screen, make sure **Start Linux Lite** is highlighted then press <kbd>Tab ↹</kbd>, this will bring up a command line with `--` at the end.

Add `forcepae` to the string before and after the two dashes like so: `forcepae -- forcepae`.

Press return, and the installation begins. You may get a warning about forcepae being experimental, just proceeed with your install.

> The “forcepae” option must be entered twice, before and after the delimiter “`–`“, so that it is applied to both the kernel on the ISO and the kernel on the system after installation.
{: .prompt-note }

After booting, run this check from terminal:

```
dmesg | grep -i pae
```

The return should show `PAE forced!`

## So what is PAE anyway?

Physical Address Extension (PAE) is a memory management extension that enables a 32-bit Intel (IA-32) compatible processor to address more than 4 GB of physical memory that was first released in 1995 with the introduction of the Intel Pentium Pro and today is supported in all recent processors and operating systems.

A number of older Pentium M ™ processors produced around 2003-4 (the Banias family) do not display the PAE flag, and hence a normal installation fails. However, these processors are in fact able to run the latest (and PAE-demanding) kernels if only the installation process is modified a little. The problem is not missing PAE, it’s about the processor not displaying its full capabilities.

In spite of their age many of the affected computers (IBM Thinkpads and Dell Latitudes, for example) are suitable for today’s use if given a light distro like Linux Lite, Xubuntu or Lubuntu; among other advantages they have a low power consumption. This guide describes a workaround for installing Linux Lite and bringing your aging machine back to life – actually the guide can be modified to work for any member of the Ubuntu family, but because we are dealing with old hardware we focus on Linux Lite.

If you are handy with hardware and you can get your hands on a Dothan-class Intel Pentium M ™ CPU with a 400MHz front-side bus, replace the non-PAE Banias CPU with a Dothan. Dothans with 400MHz FSB are marked Pentium 7×5, i.e. 715, 725, 735, 745, 755 and 765.

## Which OS still supports 32bit

* [Debian](https://cdimage.debian.org/debian-cd/current/i386/iso-cd/)
* MX Linux
    * [MX-21_386](https://sourceforge.net/projects/mx-linux/files/Final/Xfce/MX-21_386.iso/download)
    * [MX-21_386 Fluxbox](https://sourceforge.net/projects/mx-linux/files/Final/Fluxbox/MX-21_fluxbox_386.iso/download)
* Linux Mint
    * [All Options up to 19.3 Tricia](https://www.linuxmint.com/download_all.php)
* [NixOS](https://nixos.org/download.html#nix-more) - Scroll down to the **NixOS: the Linux distribution** section and click ISO then look for the **Download (32 bit)** button.
* [Zorin OS Lite](https://zorin.com/os/download/)
* [Peppermint](https://peppermintos.com/guide/downloading/)
