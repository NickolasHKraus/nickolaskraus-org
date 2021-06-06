---
title: "Configuring Arch Linux on a MacBookPro - Part 2"
date: 2021-03-12T12:00:00-06:00
draft: false
description: This is part two of a five part series on how to configure Arch Linux on a MacBookPro11,3.
---

## Overview
This is part two of a five part series on how to configure Arch Linux on a MacBookPro11,3:

* [Configuring Arch Linux on a MacBookPro - Part 1](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-1/)
* [Configuring Arch Linux on a MacBookPro - Part 2](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-2/)
* [Configuring Arch Linux on a MacBookPro - Part 3](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-3/)
* [Configuring Arch Linux on a MacBookPro - Part 4](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-4/)
* [Configuring Arch Linux on a MacBookPro - Part 5](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-5/)

## Terminal Emulator
https://man.archlinux.org/man/pty.7.en
https://en.wikipedia.org/wiki/Pseudoterminal
https://en.wikipedia.org/wiki/Terminal_emulator
https://en.wikipedia.org/wiki/Xterm
https://wiki.archlinux.org/index.php/Rxvt-unicode

## Window Manager
https://wiki.archlinux.org/index.php/Window_manager
Window managers
A full-fledged desktop environment provides a complete and consistent graphical user interface, but tends to consume a considerable amount of system resources. Users seeking to maximize performance or otherwise simplify their environment may opt to install a window manager alone and hand-pick desired extras. Most desktop environments allow use of an alternative window manager as well. Dynamic, stacking, and tiling window managers differ in their handling of window placement.

i3


## Display Manager

https://wiki.archlinux.org/index.php/Display_manager
https://wiki.archlinux.org/index.php/Start_X_at_login
Most desktop environments include a display manager for automatically starting the graphical environment and managing user logins. Users without a desktop environment can install one separately. Alternatively you may start X at login as a simple alternative to a display manager.

## Fonts

https://wiki.archlinux.org/index.php/Fonts

Disucss the default virtual console font.

The Linux console changes the font to TER16x32 (based on ter-i32b from terminus-font[11]) accordingly based on the resolution of the display. If your monitor is not recognised as HiDPI, the default font can be changed. In that case, specify fbcon=font:TER16x32 in the kernel command line.

The kbd package provides tools to change virtual console font and font mapping. Available fonts are saved in the /usr/share/kbd/consolefonts/ directory, those ending with .psfu or .psfu.gz have a Unicode translation map built-in.

```bash
showconsolefont
```

With no parameter, setfont returns the console to the default font.

The FONT variable in /etc/vconsole.conf is used to set the font at boot, persistently for all consoles.

/etc/vconsole.conf is usually created and updated using systemd-localed.service(8). localectl(1) may be used to instruct systemd-localed.service to query or update configuration.

Fonts and font collections in the enabled repositories can be installed using pacman.

Available fonts may be found by querying packages (e.g. for font or ttf).

https://en.wikipedia.org/wiki/Code_page_437

By default, the virtual console uses the kernel built-in font with a CP437 character set,[1] but this can be easily changed.

## Keyboard Configuration

[Wiki](https://wiki.archlinux.org/index.php/Linux_console/Keyboard_configuration)

Keyboard mappings (keymaps) for virtual console, console fonts and console maps are provided by the [`kbd`](https://archlinux.org/packages/?name=kbd) package.

Use `localectl status` to view the current keyboard configurations.

The keymap files are stored in the `/usr/share/kbd/keymaps/` directory tree.

For a list of all the available keymaps, use the command:

```bash
localectl list-keymaps
```

It is possible to set a keymap just for current session.

The `loadkeys` utility is also used internally by systemd when loading the keymap configured in `/etc/vconsole.conf`. It can be used very simply for this purpose:

```bash
loadkeys <keymap>
```

A persistent keymap can be set in `/etc/vconsole.conf`, which is read by systemd on start-up. The `KEYMAP` variable is used for specifying the keymap. If the variable is empty or not set, the `us` keymap is used as default value.

`/etc/vconsole.conf`

```
KEYMAP=us
```

### Creating a Custom Keymap

One method for modifying the behavior of the keyboard is by editing the currently loaded keymap file. However, since it will be rewritten anytime the package it belongs to is updated, editing this file is discouraged. It is better to integrate the existing keymap with a personal keymap.

First, create a keymap file. This keymap file can be anywhere, but one method is to mimic the directory hierarchy in `/usr/local`:

```bash
mkdir -p /usr/local/share/kbd/keymaps
cp /usr/share/kbd/keymaps/i386/qwerty/us.map.gz /usr/local/share/kbd/keymaps/custom.map.gz
```

**Note**: What is `/usr/local`?

As a side note, it is worth noting that such a personal keymap is useful also to redefine the behaviour of keys already treated by the default keymap: when loaded with loadkeys, the directives in the default keymap will be replaced when they conflict with the new directives and conserved otherwise. This way, only changes to the keymap must be specified in the personal keymap.
