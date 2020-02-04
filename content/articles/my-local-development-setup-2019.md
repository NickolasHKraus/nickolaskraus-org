---
title: "My Local Development Setup - 2019"
date: 2020-01-19T12:00:00-06:00
draft: false
description: A comprehensive walk through of the tools and productivity modifications that I use. Updated for 2019.
---

## Automatic Configuration

This year, instead of semi-manually installing and configuring my local development environment, I created a CLI, [`nhk-mac`](https://github.com/NickolasHKraus/nhk-mac), to do it automatically.

`nhk-mac` will do the following:

* Set the hostname to `computer`.
* Set the desktop wallpaper to `#1c1c1c`.
* Configure macOS.
    * Set `InitialKeyRepeat` to 10 (very short).
    * Set `KeyRepeat` to 1 (very short).
* Configure the Dock.
    * Set `autohide` to `true`.
    * Set `autohide-delay` to `0`.
    * Set `autohide-time-modifier` to `0`.
    * Set `show-recent` to `false`.
    * Set `tilesize` (Dock size) to `32`.
    * Set `orientation` (Dock position) to `left`.
    * Remove all persistent and recent applications.
* Install Xcode Developer Tools ([Git](https://git-scm.com/)).
* Install [Homebrew](https://brew.sh/).
* Install [Homebrew Bundle](https://github.com/Homebrew/homebrew-bundle).
    * Installs [tmux](https://github.com/tmux/tmux) and [Vim](https://www.vim.org/).
* Install [iTerm2](https://www.iterm2.com/).
* Install [Spectacle](https://www.spectacleapp.com/).
* Install [Zsh](https://ohmyz.sh/)
* Install [Vundle](https://github.com/VundleVim/Vundle.vim).
* Install [Powerline fonts](https://github.com/powerline/fonts).
* Create SSH keys.
* Create `~/Workspace`.
* Install Python 2 and Python 3.
* Install virtual environment tooling.
* Install Python packages.
* Install my [Vim scripts](https://github.com/NickolasHKraus/dotfiles/blob/master/.vimrc).
* Install my [Vim plugins](https://github.com/NickolasHKraus/dotfiles/blob/master/.vimrc).

## What's New?

### [Homebrew Bundle](https://github.com/Homebrew/homebrew-bundle).

## Manuall Configuration

### macOS

### Rebind Caps Lock to Control

To rebind Caps Lock (⇪) to Control (⌃) go to **System Preferences** > **Keyboard** > **Modifier Keys…** and change **Caps Lock (⇪) Key:** to **^ Control**.

### Configure shortcuts

To configure macOS shortcuts, go to **System Preferences** > **Keyboard** > **Shortcuts**.

For macOS, my shortcuts are as follows:

| | |
|-----------------------|-----------|
| Show Spotlight search | `^Space`  |

To configure application shortcuts, go to **App Shortcuts** > **+** and enter the **Menu Title** as given in the application and the desired keyboard shortcut.

For Chrome, my shortcuts are as follows:

| Menu Title          |  Shortcut   |
|---------------------|-------------|
| New Tab             |  `^T`       |
| Select Next Tab     |  `^K`       |
| Select Previous Tab |  `^J`       |
| Close Tab           |  `^W`       |
| Find...             |  `^F`       |
| Find Next           |  `^G`       |
| Find Previous       |  `^B`       |
| New Window          |  `^N`       |
| Close Window        |  `^Q`       |
| Open Location...    |  `^L`       |
| Reload This Page    |  `^R`       |
