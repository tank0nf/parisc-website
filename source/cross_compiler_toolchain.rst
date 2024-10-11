Cross compiler toolchain
========================

Cross compiling the Linux kernel for PA-RISC is easy nowadays:

Debian
------
::

    apt install gcc-hppa-linux-gnu gcc-hppa64-linux-gnu

Fedora
------
::

    yum install gcc-hppa64-linux-gnu gcc-hppa-linux-gnu binutils-hppa64-linux-gnu binutils-hppa-linux-gnu

Download prebuilt cross compilers for PA-RISC
---------------------------------------------

- `Latest cross-compilers on kernel.org by Arnd Bergmann <https://www.kernel.org/pub/tools/crosstool/>`__
- `Segher Boessenkool toolchain <http://git.infradead.org/users/segher/buildall.git>`__

How to build the kernel
-----------------------
::

    make ARCH=parisc menuconfig
    make ARCH=parisc

Before Kernel v5.17 you need to give CROSS_COMPILE= on the command line
when cross-compiling, e.g.::

    make ARCH=parisc CROSS_COMPILE=hppa64-linux-gnu-   # to build a 32- or 64-bit kernel (depending on the value in the .config file)

Starting with Kernel v5.17 you don't need to give CROSS_COMPILE= on the
command line any longer, just run::

     make ARCH=parisc  # to build a 32-bit kernel

or::

     make ARCH=parisc64  # to build a 64-bit kernel
