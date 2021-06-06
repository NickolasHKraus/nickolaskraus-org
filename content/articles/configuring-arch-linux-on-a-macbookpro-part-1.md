---
title: "Configuring Arch Linux on a MacBookPro - Part 1"
date: 2021-03-05T12:00:00-06:00
draft: false
description: This is part one of a five part series on how to configure Arch Linux on a MacBookPro11,3.
---

## Overview
This is part one of a five part series on how to configure Arch Linux on a MacBookPro11,3:

* [Configuring Arch Linux on a MacBookPro - Part 1](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-1/)
* [Configuring Arch Linux on a MacBookPro - Part 2](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-2/)
* [Configuring Arch Linux on a MacBookPro - Part 3](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-3/)
* [Configuring Arch Linux on a MacBookPro - Part 4](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-4/)
* [Configuring Arch Linux on a MacBookPro - Part 5](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-5/)

## Graphics

**Note**: This section gives a brief overview of the video display and graphics. If on boot, the display is working, it can be assumed that the required kernel modules have been loaded. Hardware video acceleration will be discussed later.

The technical specifications for the MacBookPro11,3 (Retina, 15-inch, Mid 2014) can be found [here](https://support.apple.com/kb/SP704) or by going to  > **About This Mac** > **System Report...**. The graphics should be listed under **Graphics/Displays**. This model has both integrated Intel graphics and an NVIDIA discrete GPU:
* Intel Iris Pro Graphics
* NVIDIA GeForce GT 750M

To determine which graphics card is being used by the video display controller, execute the following:

```bash
lspci | grep VGA
```

```
TODO
```

**Note**: `lspci` is a utility for displaying information about PCI buses in the system and devices connected to them.

Next, we can determine the kernel drivers handling the device. The `-k` option also shows the kernel modules capable of handling the device:

```bash
lspci -k | grep -A 3 -E "VGA"
```

```
TODO
```

We find that the kernel driver in use is `nouveau` and the kernel module is `nouveau`.

A quick note on kernel drivers and kernel modules:
* A **kernel driver** allows the kernel to access hardware connected to the system.
* A **kernel module** is a piece of code that can be loaded and unloaded into the kernel on demand.

Not all kernel modules are kernel drivers. Likewise, a kernel driver may be a kernel module or built directly into the Linux kernel.

[Nouveau](https://nouveau.freedesktop.org/) is both a kernel driver and kernel module. It is responsible for handling the video display.

You can test the primacy of the `nouveau` kernel module by unloading and reloading it:

```bash
rmmod --force nouveau
modprobe nouveau
```

The screen should go blank, however you will still be able to issue the `modprobe` command to reload the module.

It should be noted that the video output ports (HDMI and DisplayPort) are hardwired to the NVIDIA discrete GPU. They will not work if you use the integrated Intel GPU, thereby powering off the NVIDIA GPU. Switching between the Intel and NVIDIA GPU requires a reboot, so if you keep your laptop primarily docked at a desk, configuring your system to switch between graphics cards may not be worth the hassle. That being said, the NVIDIA GPU uses significantly more power than the Intel GPU, so you will take a significant hit on battery life.

## Graphical User Interface

This section provides a foundation for understanding the Linux console (virtual console) and display server (Xorg).

### Linux Console (Virtual Console)

A virtual console is an abstraction of a physical display and input device. Historically, operation of a computer was done using a text terminal and keyboard via the system console. As a continuation of this paradigm, virtual consoles provide an interface for operating a computer with a combination of keyboard and display. Today communication via virtual consoles is generally done abstractly, using the standard streams (stdin, stdout, and stderr), not using the physical transmission of bytes as was done in the past.

When booting Linux, you are first presented with a virtual console. With the Linux console, usually the first six virtual consoles provide a text terminal with a login prompt to a Unix shell. The graphical X Window System starts in the seventh virtual console.

You can switch between virtual consoles using the following key combinations:
* Select a virtual console (1-6): `CTRL` + `ALT` + `F{1, 2, 3...6}`
* Select next virtual console: `ALT` + `->`
* Select previous virtual console: `ALT` + `<-`
* Select the X Window System: `CTRL` + `ALT` + `F7`

Virtual consoles are represented by device special files `/dev/tty1`, `/dev/tty2`, etc. The TTY subsystem is a central component of Unix and Linux systems. TTY derives its name from teletypewriter (**T**ele**T****Y**pewriter), a device used in the early days of computing as input and output devices. Currently, it serves as an interface for the virtual console.

Programs can access the virtual consoles by the device special files. In text mode, writing to the file displays text on the virtual console and reading from the file returns text the user writes to the virtual console.

```bash
echo "Hello, World!" >> /dev/tty1
```

https://en.wikipedia.org/wiki/Linux_console
https://wiki.archlinux.org/index.php/Linux_console

### Display Server

https://wiki.archlinux.org/index.php/Xorg
https://en.wikipedia.org/wiki/X_Window_System
Xorg is the public, open-source implementation of the X Window System (commonly X11, or X). It is required for running applications with graphical user interfaces (GUIs), and the majority of users will want to install it.

https://en.wikipedia.org/wiki/Xinit

The xinit program allows a user to manually start an X display server. The startx script is a front-end for xinit.

https://en.wikipedia.org/wiki/X_display_manager

In the X Window System, X display manager is a graphical login manager which starts a login session on an X server from the same or another computer.

https://wiki.archlinux.org/index.php/Xorg

https://en.wikipedia.org/wiki/X.Org_Server

https://en.wikipedia.org/wiki/Windowing_system

https://wiki.archlinux.org/index.php/HiDPI

Discuss the virtual console:
* https://www.linusakesson.net/programming/tty/index.php
* tty
* vconsole.conf

https://wiki.archlinux.org/index.php/General_recommendations#Graphical_user_interface

Graphical user interface
* Display server
* Display drivers
* Desktop environments
* Window managers
* Display manager
* User directories

Why does my vconsole.conf configuration no work with xorg?
