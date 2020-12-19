# Use the OV13850_camera for the FriendlyElec NanoPC-T4 SBC on an upstream kernel
This is a port of the OV13850 camera sensor ([CAM1320](http://wiki.friendlyarm.com/wiki/index.php/Matrix_-_CAM1320)) from the rockchip-kernel(https://github.com/friendlyarm/kernel-rockchip/) to the 5.10-rc6 Kernel.

I keep this repository to show the current development state, while I work on upstreaming the patch to the mainline kernel.

### Motivation

I required a system with a rk3399 SoC as it contains the rkisp1 Image Signal Processor. The NanoPC-T4 is a great Single Board Computer, it just has a few flaws, for example, a lot of functionality is found on the BSP(Board Specific Programming) [Kernel from friendlyElec](https://github.com/friendlyarm/kernel-rockchip), which is based on the 4.4 Kernel (2016). This on its own is not a major problem, but it gets problematic as soon as you want to do upstream development for the Linux Kernel. The MIPI CSI-2 & CSI-1 sockets of the board have a special width, which makes it impossible to insert for example the raspberry pi [camera module v2](https://www.raspberrypi.org/products/camera-module-v2/?resellerType=home) with the [Sony IMX219](https://www.arducam.com/downloads/modules/RaspberryPi_camera/IMX219DS.PDF) image sensor. The only two cameras that I was able to find, which fit those sockets are the [CAM1320](https://www.friendlyarm.com/index.php?route=product/product&product_id=228) with the OV13850 image sensor & the [MCAM-400](https://www.friendlyarm.com/index.php?route=product/product&product_id=247) with the OV4689 image sensor and in contrast to the IMX219 these cameras have no upstream driver.

If you want more details, I have created a blog post about the whole endeavor, [here](https://sebastianfricke.me) **TODO - not finished yet**

## Setup

In order to play around with this patch, you will have to apply it to the target kernel version tree and create an image for the NanoPC-T4. If you use the Armbian method described below, the procedure of adding this driver is simple just put the patch file into the `userpatches/kernel/rockchip64-dev` folder of the armbian build repository.

### Creating the kernel

There are 3 major ways of creating an image for the NanoPC-T4 with an upstream kernel: [Armbian](https://github.com/armbian/build), [Buildroot](https://github.com/buildroot/buildroot), [Yocto Project](https://www.yoctoproject.org/).
My pick was armbian simply because I heard it was the fastest to set up. Now there is a little bit of learning involved in order to learn how to create an armbian image with upstream sources but it is possible. If you want to learn how: I describe that in [this project](https://github.com/initBasti/NanoPC-T4_armbian_configuration) together with the latest configurations and patches, that I use to build the image.
