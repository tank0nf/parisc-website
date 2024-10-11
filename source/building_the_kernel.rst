===================
Building the kernel
===================

If you are only interested in using Linux/PARISC then please see the
`software <http://www.parisc-linux.org/software/index.html>`__
information web page.

We no longer advise using the `pre-built cross compiler
<http://www.parisc-linux.org/software/index.html#xcs>`__ to build a
parisc kernel on an x86 linux host. Native compiler/linker tools are
better maintained. The old mini-howto describes how to `cross-build
kernels <http://www.parisc-linux.org/kernel/nfsroot.html>`__ for Net
Boot. Please only bother with this if you have a very slow parisc
machine and very fast x86 machine.

Prerequisites For Building Kernels
==================================

- Internet connection
- hppa-debian host properly configured so aptitude and ftp work
- http://ftp.debian-ports.org/debian and
  http://ftp.parisc-linux.org/debian-ports/debian apt sources

How To Build a Kernel
=====================

Here are details developers care about in order to **modify, build,
test** parisc-linux kernels. Note that just because a kernel option can
be select, does NOT mean it works. Trial and error is usually the only
sure way to find out. Reports of such adventures are always welcome on
the parisc-linux `mailing list <mailto:linux-parisc@vger.kernel.org>`__.

#. **Install minimal set of tools**
   ::

      aptitude install libncurses-dev bc

#. **Obtain kernel source and build tools**: Stable kernel sources are
   available via ``aptitude install linux-source-XX`` (where XX is
   something like "2.4.25-32" or "2.6.6-32"). You may also download a
   tarball from the `The Linux Kernel Archives <https://www.kernel.org/>`__
   or ``git clone`` from `Kernel.org git repositories <http://git.kernel.org/cgit/linux/kernel/git>`__. 
   The most interested repos should be: `1 <http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/>`__
   and `2 <http://git.kernel.org/cgit/linux/kernel/git/deller/parisc-linux.git/>`__.
   You may start with first, but if you need some recent PA-RISC changes
   hadn't yet been imported to the mainline, pick a second one (usually
   you would be interested in some particular branch). Note that
   ``aptitude install linux-source-``  **step is a must** (even if you
   decided to pick the sources from another place) as it will install
   most of required build tools. You may then opt-out
   ``linux-source-XX`` by issuing ``aptitude remove``, if you don't need
   these sources.

   ::

      cd /usr/src
      # verify ~350MB free
      df -h .

   - Tarball

   ::

      wget https://www.kernel.org/pub/linux/kernel/v3.x/linux-3.11.tar.xz
      tar -xJf linux-3.11.tar.xz

   - Git

   ::

      git clone git://git.kernel.org/pub/scm/linux/kernel/git/deller/parisc-linux.git
      git checkout <branch/tag/commit>

#. **Choosing toolchain version**: The good practice is to leave the one
   being installed during `#Obtain kernel source and build tools
   <#Obtain_kernel_source_and_build_tools>`__ phase. But if you can't
   sucessfully build the kernel using current toolchain version or you
   have other reasons, you may set a more fresh one.

   ::

      optionally: aptitude remove gcc-XX
      aptitude install gcc-YY

   As for installing of another ``binutils`` version, it's usually
   easier to use ``aptitude`` frontend for this purpose. *Important:*
   See how to make installed toolchain versions default ones:
   http://stackoverflow.com/a/9103299

#. **For 64-bit kernels: Install missing build tools**
   ::

      aptitude install binutils-hppa64 gcc-XX-hppa64

   Where ``XX`` usually choosen to be same version as it's 32-bit counterpart.

#. **Configure Kernel Options**
   ::

      cd /usr/src/linux-2.6
      # clone the nearest _config to start with
      cp arch/parisc/configs/b180_config .config
      # You can also "make config" or "make menuconfig" here
      # to adjust the .config if kernel defaults don't suit you.
      make oldconfig # ARCH=parisc when cross-compiling

On Debian with systemd you need to use Debian stock config as basis

::

   cd /usrc/src
   xz -d linux-config-XX/config.hppa_none-flavor.xz
   cp config.hppa_none-flavor linux-source-XX/.config

**Build Kernel Executables**

::

   make -j<N> # ARCH=parisc CROSS_COMPILE=...
   # must be root user
   make modules_install

``N`` is number of parallel processes there. You may add ``V=1`` to get verbose output of build process.

**Installing the kernel** The resulting kernel image is ``/usr/src/linux-2.6/vmlinux``. Normally, x86-linux will save the existing vmlinux and install the new kernel with ``make install``. The "dpkg -i" steps above do about the same thing. Here is one way to do it manually:

::

   cd /boot
   mv vmlinux vmlinux.old
   mv System.map System.map.old
   cd /usr/src/linux-2.6
   cp System.map vmlinux /boot/
   sync
   reboot

*NOTE: One does not need to run palo when replacing an existing kernel.*

Another way is to rename ``vmlinux`` with revision info, reboot, interrupt autoboot and specify interactive boot, specify the new kernel via palo, and finally once the new kernel is booted, modify ``/etc/palo.conf`` to match (and run ``palo`` again). Start with something like:

::

   cp vmlinux /boot/vmlinux-2.6.6-pa1
   cp System.map /boot/System.map-2.6.6-pa1
   cp .config /boot/config-2.6.6-pa1
   sync
   reboot
   ...
