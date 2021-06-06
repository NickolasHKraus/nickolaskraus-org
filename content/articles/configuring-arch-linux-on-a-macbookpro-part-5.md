---
title: "Configuring Arch Linux on a MacBookPro - Part 5"
date: 2021-04-02T12:00:00-06:00
draft: false
description: This is part five of a five part series on how to configure Arch Linux on a MacBookPro11,3.
---

## Overview
This is part five of a five part series on how to configure Arch Linux on a MacBookPro11,3:

* [Configuring Arch Linux on a MacBookPro - Part 1](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-1/)
* [Configuring Arch Linux on a MacBookPro - Part 2](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-2/)
* [Configuring Arch Linux on a MacBookPro - Part 3](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-3/)
* [Configuring Arch Linux on a MacBookPro - Part 4](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-4/)
* [Configuring Arch Linux on a MacBookPro - Part 5](https://nickolaskraus.org/articles/configuring-arch-linux-on-a-macbookpro-part-5/)

## Hardware Video Acceleration

What is hardware video acceleration?

Linux kernel KMS driver (nouveau)

https://wiki.archlinux.org/index.php/Hardware_video_acceleration

https://wiki.archlinux.org/index.php/Nouveau

https://nouveau.freedesktop.org/index.html

https://nouveau.freedesktop.org/VideoAcceleration.html

https://nouveau.freedesktop.org/FeatureMatrix.html

https://nouveau.freedesktop.org/KernelModeSetting.html

For the DDX driver (which provides 2D acceleration in Xorg), install the xf86-video-nouveau package.

[Hardware video acceleration](https://en.wikipedia.org/wiki/Graphics_processing_unit#GPU_accelerated_video_decoding) makes it possible for the video card to decode/encode video, thus offloading the CPU and saving power.

There are several ways to achieve this on Linux:

* [Video Acceleration API](https://www.freedesktop.org/wiki/Software/vaapi/) (VA-API) is a specification and open source library to provide both hardware accelerated video encoding and decoding, developed by Intel.

* [Video Decode and Presentation API for Unix](https://www.freedesktop.org/wiki/Software/VDPAU/) (VDPAU) is an open source library and API to offload portions of the video decoding process and video post-processing to the GPU video-hardware, developed by NVIDIA.

    * [Nouveau](https://wiki.archlinux.org/index.php/Nouveau) open-source driver supports both VA-API and VDPAU:

    * GeForce 8 series and newer GPUs up until GeForce GTX 750 are supported by [libva-mesa-driver](https://archlinux.org/packages/?name=libva-mesa-driver) and [mesa-vdpau](https://archlinux.org/packages/?name=mesa-vdpau).

    * [Requires](https://nouveau.freedesktop.org/wiki/VideoAcceleration/#firmware) [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/) AUR firmware package, presently extracted from the NVIDIA binary driver.

VP6: NV117-NV124 (GeForce 750; GeForce 800, 900 series; corresponds to VDPAU feature set E)

### Display drivers
The default modesetting display driver will work with most video cards, but performance may be improved and additional features harnessed by installing the appropriate driver for AMD or NVIDIA products.

## mpv

https://mpv.io/manual/stable/#options-hwdec

