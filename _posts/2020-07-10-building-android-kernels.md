---
 title: "Building Android kernels"
 tags: android kernel xda
 author: Niranjan Bhaskar K
 show_author_profile: true
---

Introduction
============

What is an Android kernel?
--------------------------

We often hear that flashing custom ROMs like LineageOS (formerly known as Cyanogenmod), ResurrectionRemix, etc., can improve our Android experience. However, there is a misconception that ROMs are the ones that greatly impact the performance and battery life of an Android device.

Well, leaving aside the hardware limitations of the device, it is the kernel that is responsible for increased performance gains and enhanced battery life!
Literally everything we do on our device involves the kernel. 

**For instance,** 
 - Android does not directly notify the speakers to increase the volume. Instead, it tells the kernel that it wants to increase the volume, and the kernel informs the speaker to increase its output.
 - Android does not directly influence the CPU to operate within a specified frequency. It tells that to the kernel who then tells it to the CPU.
 
Therefore, the kernel acts as middleman between the operating system and the hardware components.

Summing up, **an Android kernel is a bridge between the operating system and the device hardware.**

From [Wikipedia](https://en.wikipedia.org/wiki/Kernel_(operating_system)),
![android-flowchart](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Kernel_Layout.svg/1200px-Kernel_Layout.svg.png)

A ROM on the other hand, is a bit more all-encompassing. It is the operating system we use on our device. All ROMs come with a kernel installed but we can 
install another one of our own. 

**Android kernels are based on Linux. What?**

Android uses the Linux kernel under the hood. Because Linux is open-source, Android developers can modify the Linux kernel to fit their needs. 
Linux gives the Android developers a pre-built, already maintained operating system kernel to start with so they do not have to write their own kernel 
from scratch.

From [source.android.com](source.android.com),  
> "While the Linux kernel contains code for all the different chip architectures and hardware drivers it supports, an individual system runs only a fraction 
of the codebase. An average laptop uses around 2 million lines of kernel code from 5 thousand files to function properly, while the Pixel phone uses 3.2 
million lines of kernel code from 6 thousand files (due to the increased complexity of an SoC)."

![android-framework](https://source.android.com/images/android_framework_details.png)

Here's why you should consider installing a custom Android kernel
-----------------------------------------------------------------

Before digging deeper, let's make clear some of the commonly used terminologies below: 
 - Stock kernels are the kernels that originally come with your device
 - Custom kernels are basically modified stock kernels
 
Custom Android kernels can do a lot for our device, ranging from enhanced battery life to significant performance gains.
 
But that is not all, custom kernels make it possible to add a bunch of features to our devices ranging from improving the WiFi driver to efficient sound control.
Here are a **few** possibilities to tweak our custom kernel: 

 - **Overclock/Underclock:**
 
	In a very basic sense, higher clock speeds bring in greater performance whereas lower clock speeds bring in increased battery life.
	However, increasing clock speeds (overclocking) above a certain frequency (which is usually way greater than the "safe" frequency values used by stock kernels) 
	may ruin the device's battery life. And similarily, decreasing clock speeds (underclocking) may have adverse effects on the performance of the device. 
	
 - **Increase/Decrease minimum and maximum voltages:**
 
	As specified earlier higher clock speeds use up more battery, that is essentially because they require more voltage and hence reducing these voltages 
	while increasing the clock speeds can help achieve a stable battery-performance balance.
	However, during the kernel's testing phase it is not advised to overclock to high frequencies or increase the maximum voltages to an enormous value. 
	The perfect clock frequency or voltages are usually selected by slowly incrementing in steps of low frequencies.
	
 - **CPU governor:**
 
	It controls how the CPU raises and lowers its frequency in response to the demands the user is placing on their device. Governors are especially 
	important in smartphones and tablets because they have a large impact on the apparent fluidity of the interface and the battery life of the device
	over a charge.
	
 - **I/O Scheduler:**
 
	In a very basic sense, the kernel controls how the input and output is handled using the I/O scheduler. This helps improve memory management 
	and thereby comes into significant effect when you're multi-tasking.

Hands on: Building a stock Android kernel from source
=====================================================

Prerequisites
-------------
 
 - A Linux environment 
 - Familiar with navigating via the Linux terminal
 - A rooted android device with a custom recovery installed

Some terminologies
------------------

 - **Cross-compiler:**
	Generally speaking, a cross-compiler is a compiler that runs on platform A (our Linux environment), but generates executables for platform B	
	(our android device).

 - **Toolchain:**
	A toolchain is the set of compiler + linker + loader + any other tools you need to produce executables (+ shared libraries, etc.) for the target.

 - **defconfig:**
	The defconfig is a file that contains a list of all the device-specific configurations. Summing up, it tells the compiler the list of all the drivers 
	used in that particular device (including the battery, chipset, sound drivers, etc.). This is done so that the toolchain builds only the relevant files 
	for our device from the enormous kernel source code. 
	
What this post will cover
-------------------------

 1. Downloading the kernel source code
 2. Downloading a Toolchain
 3. Building the Android kernel
 4. Flashing the Android kernel
 
What this post will **not** cover
---------------------------------

 - Tweaking your Android kernel 
 - Building kernels for the Google Pixel (It is a slightly different process)
 - Building kernels for devices with no opensource code

Downloading the stock kernel source code
----------------------------------------

Most devices have their kernel source codes uploaded on the following sites
 - [Google](https://opensource.google/)
 - [Samsung](https://opensource.samsung.com/)
 - [LG](http://opensource.lge.com/)
 - [HTC](https://www.htcdev.com/devcenter/downloads/)
 - [OnePlus](https://github.com/OnePlusOSS)
 - [Motorola](https://github.com/MotorolaMobilityLLC)
 - [Sony](https://github.com/sonyxperiadev/kernel)

*Unfortunately, some devices such as the ones using the MediaTek SoC do not upload their source codes :(*
 
Clone/Download the appropriate kernel source code for your device model from above.

Downloading a GCC toolchain
---------------------------

Before we proceed further, let us take note of our device architecture (arm or arm64) since the building process is quite different for 
the both of them. So we need to download/clone the right GCC toolchain from below
 - [arm UBERTC Toolchain](https://bitbucket.org/matthewdalex/arm-eabi-4.9/src/master/)
 - [arm64 UBERTC Toolchain](https://bitbucket.org/matthewdalex/aarch64-linux-android-4.9/src/master/)

**Enough with the downloading, Let's get to building!**

Building the Android kernel
---------------------------

Let's get started!

First, navigate to the directory where the downloaded kernel source code resides via the **terminal**.

Tell the Makefile the architecture of the device

	export ARCH=<arch>

For instance, say I need to build the kernel for a device with an ARM architecture, I would input

	export ARCH=arm

Point the location of the downloaded toolchain to the Makefile

	export CROSS_COMPILE=<toolchain>
	
For instance, say my ARM toolchain resides in a folder named Toolchains in the current working directory, I would input

	export CROSS_COMPILE=$(pwd)/Toolchains/bin/arm-eabi-
	
Now, let's create a directory where our final kernel builds will reside after the build process

	mkdir output
	
Point your device's defconfig to the Makefile

	make O=output <defconfig_filename>

The defconfig is located in `$(pwd)/arch/$ARCH/configs` where, **$ARCH is your device's architecture**.

And finally, build it!

	make O=output -j$(nproc --all)

**In this stage, you may encounter compile errors where you'll have to fix some headers or other issues.**

Flashing the Android kernel
---------------------------

Assuming you were able to build the kernel successfully, you will now have a `zImage` inside the `/output` directory you created earlier.

Let's build a flashable zip for your newly built stock kernel!

 1. Clone/Download [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
 2. Copy the final zImage into AnyKernel3's root directory
 3. Zip up the entire AnyKernel3 folder and push the zip into your device
 4. Reboot into your custom recovery and flash the zip!
 
**And Voila! You've just built a bootable stock Android kernel for your device!**
