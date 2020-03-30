# linux-kernel
requirements to compile kernel
This link will give you the minimal requirements for kernel compilation
https://github.com/torvalds/linux/blob/master/Documentation/process/changes.rst


# How to compile and install Linux Kernel 5.4.1 from source code

**Step 1. Get the latest Linux kernel source code**

[Download Latest kernel](https://www.kernel.org/)

**Step 2. Extract tar.xz file**
You really don’t have to extract the source code in /usr/src. You can extract the source code in your $HOME directory or any other directory using the following unzx command or xz command:

$ tar xvf linux-5.4.1.tar

**Step 3. Configure the Linux kernel features and modules**

Before start building the kernel, one must configure Linux kernel features. You must also specify which kernel modules (drivers) needed for your system. The task can be overwhelming for a new user. I suggest that you copy existing config file using the cp 

$ cd linux-5.6
$ cp -v /boot/config-$(uname -r) .config


**Step 4. Install the required compilers and other tools**
**How to install GCC and development tools on a Debian/Ubuntu Linux**

$ sudo apt-get install build-essential libncurses-dev bison flex libssl-dev libelf-dev


**Installing compilers using apt command**


$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install build-essential


**Verify installation**

$ whereis gcc make
$ gcc --version
$ make -v


**Installing the dev man pages on a Ubuntu Linux**


$ sudo apt-get install manpages-dev man-db manpages-posix-dev


**Installing the X11 development compilers**

$ sudo apt install libx11-dev


**Step 5. Configuring the kernel**

**$ make menuconfig** – Text based color menus, radiolists & dialogs. This option also useful on remote server if you wanna compile kernel remotely.

You have to select different options as per your need. Each configuration option has HELP button associated with it so select help button to get help. Please note that ‘make menuconfig’ is optional. I used it here to demonstration purpose only. You can enable or disable certain features or kernel driver with this option. It is easy to remove support for a device driver or option and end up with a broken kernel. For example, if the ext4 driver is removed from the kernel configuration file, a system may not boot. When in doubt, just leave support in the kernel.

**Step 5. How to compile a Linux Kernel**

Start compiling and tocreate a compressed kernel image, enter:
$ make

or

**To speed up compile time, pass the -j as follows:**
## use 4 core/thread ##
$ make -j 4

or

## get thread or cpu core count using nproc command ##
$ make -j $(nproc)


**Install the Linux kernel modules**

$ sudo make modules_install 


**Install the Linux kernel**

So far we have compiled the Linux kernel and installed kernel modules. It is time to install the kernel itself:
$ sudo make install 


**It will install three files into /boot directory as well as modification to your kernel grub configuration file:**

    - initramfs-5.4.1.img
    - System.map-5.4.1
    - vmlinuz-5.4.1

**Step 6. Update grub config**

You need to modify Grub 2 boot loader configurations. Type the following command at a shell prompt as per your Linux distro:


## Debian/Ubuntu Linux


**The following commands are optional as make install does everything for your but included here for historical reasons only:**
$ sudo update-initramfs -c -k 5.4.1
$ sudo update-grub

**How to build and install the latest Linux kernel from source code**

You have compiled a Linux kernel. The process takes some time, however now you have a custom Linux kernel for your system. Let us reboot the system.
Reboot Linux computer and boot into your new kernel

**Just issue the reboot command or shutdown command:**
# reboot

**Verify new Linux kernel version after reboot:**
$ uname -mrs
