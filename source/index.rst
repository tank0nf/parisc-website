Linux on PA-RISC
================

.. image:: media/parisc-powered.png
   :width: 100px
   :align: right

- The PA-RISC project provides a *native* port of Linux to the PA-RISC
  architecture.

- Linux on PA-RISC is stable and runs on most PA-RISC machines and in
  a virtual :doc:`Qemu <qemu>` machine.

- Check the :doc:`PARISC FAQ <parisc_faq>` and :doc:`Hardware support
  <hardware_support>` if you have trouble installing Linux.

Linux distributions for PA-RISC machines
----------------------------------------

.. image:: media/Debian_logo.png
   :width: 100
   :align: right

Debian Linux
~~~~~~~~~~~~

- PA-RISC is a non-release architecture in the `Debian Ports
  <http://www.debian-ports.org>`__ project with more than
  12,000 Debian packages available.
- You may download the latest installation ISO `here
  <https://cdimage.debian.org/cdimage/ports/snapshots/2022-12-09/>`__ or
  `here <http://ftp.parisc-linux.org/debian-cd/>`__.

.. image:: media/Gentoo-logo.png
   :width: 100
   :align: right

Gentoo Linux
~~~~~~~~~~~~

- PA-RISC is a fully supported architecture of Gentoo Linux.
- The `Gentoo hppa team <https://wiki.gentoo.org/wiki/Project:HPPA>`__
  provides `Gentoo Linux installation ISOs available for download
  <http://www.gentoo.org/main/en/where.xml>`__ and a
  `Handbook on how to install Gentoo Linux for PA-RISC
  <http://www.gentoo.org/doc/en/handbook/handbook-hppa.xml>`__.

.. image:: media/t2logo.png
   :width: 100
   :align: right

T2 System Development Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The `T2 System Development Environment <https://t2sde.org/>`__ Linux
distribution provides a port to PA-RISC which you may download `here.
<http://dl.t2sde.org/binary/>`__

Our sponsors
------------

Corporate sponsors
~~~~~~~~~~~~~~~~~~

- `Cypress Technology Inc <http://www.cypress-tech.com>`__ (`Jesse
  Dougherty <mailto:jesse@cypress-tech.com>`__) sponsored a `HP J6700 workstation
  <https://www.openpa.net/systems/hp-visualize_j6000_j6700.html>`__ with
  2 x 750MHz PA8700 CPUs, 4GB RAM and a 72GB disc. (Oct 2022)

  - This machine is used as `Debian buildd and Porterbox machine
    "parisc" <https://db.debian.org/machines.cgi?sortby=purpose&sortorder=dsc>`__.

- `GALL EDV-Systeme GmbH <http://www.gall.de/>`__ (info@gall.de)
  sponsored `HP Visualize FX-2, FX-4 and FX-6 grahics cards
  <https://www.openpa.net/pa-risc_graphics.html#visfx>`__ (June 2023)

  - Those will be used to further develop the Visualize-FX fbdev and
    DRM graphics drivers.

Organizations and private sponsors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Oregon State University Open Source Lab <http://osuosl.org>`__

- Hosting and support for the physical parisc servers "parisc" (since
  2014) and "panama" (since 2017)
- Hosting of a x86 virtual machine for the qemu-user based parisc build
  server "pasta" (since Jan 2021)

`Roberto C. Sánchez <mailto:roberto@debian.org>`__ sponsored a `HP
rp3410 server
<http://www.openpa.net/systems/hp-9000_rp3410_rp3440.html>`__ with one
800 MHz PA8900 CPU. (May 2017)

- This machine is used as `Debian buildd and Porterbox machine "panama"
  <https://db.debian.org/machines.cgi?sortby=purpose&sortorder=dsc>`__.

.. note::

   If you want to sponsor HP physical machines, graphics-cards or other
   hardware, or hosting services for virtual (x86) or physical (parisc)
   machines, please contact `me <mailto:deller@gmx.de>`__

Resources
---------

.. toctree::
   :maxdepth: 2

   faq
   documentation
   tool_chain

External Resources
------------------

- http://www.gentoo.org/doc/en/handbook/handbook-hppa.xml - Gentoo Linux Installation
- http://www.openpa.net/index.html - The OpenPA Project
- http://www.wikiwand.com/en/HP_9000 and http://www.wikiwand.com/en/PA-RISC - Good overview of PA-RISC, HP-UX, CDE, ...
- http://web.archive.org/web/20040202003152/http://www.cpus.hp.com/technical_references/parisc.shtml - Historic PA-RISC Documentation from HP.com (2004)
- https://www.hpl.hp.com/hpjournal/pdfs/IssuePDFs/1987-03.pdf - technical documentattion of first PA-RISC processors
- http://www.3kranger.com/HP3000/mpeix/hard.shtm#PA-RISC - PA-RISC arch & HP3000 docs
- http://www.debian.org/ports/hppa/ - Debian HPPA port page
- http://www.gentoo.org/doc/en/handbook/handbook-hppa.xml - Gentoo HPPA Handbook
- http://www.hpmuseum.net/collection_document.php - HP Computer Museum
- http://computermuseum.informatik.uni-stuttgart.de/dev/hp9000_840/ - Uni Stuttgart Computermuseum - HP 9000/840 (first PA-RISC machine)
- http://tenox.pdp-11.ru/hpux/ - HP/UX ressources
- http://psg.skinforum.org/hpux.html - Tin Ho's "Sys Admin Pocket Survival Guide - HP-UX"
- http://www.mach-linux.org/ - OSF Mach-Linux
- http://www.unixnerd.demon.co.uk/hp_unix.html - UnixNerds/HPUX
- https://github.com/larsbrinkhoff/awesome-cpus - All CPUs documented
- http://git.kernel.org/cgit/linux/kernel/git/deller/parisc-linux.git - Helge's PARISC Linux Kernel git tree
- https://patchwork.kernel.org/project/linux-parisc/list - PARISC Linux Patchwork
- http://git.kernel.org/cgit/linux/kernel/git/deller/palo.git - PALO boot loader source code

Archived historical webpages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Snapshot of former Wiki on kernel.org (2014-2024): https://web.archive.org/web/20240917210505/https://parisc.wiki.kernel.org/index.php/Main_Page
- Old website until 2014: http://www.parisc-linux.org/index.html - The former and now historical PA-RISC/Linux website
- http://pateam.parisc-linux.org - The PA/Linux ESIEE Team (former www.pateam.org webpage until 2014)

PA-RISC Linux NEWS
------------------

Oct 2024
~~~~~~~~
- Upon request from the kernel.org website admin, the PA-RISC Wiki is converted
  to a ReadTheDocs static website and is moved to https://parisc.docs.kernel.org
- `Dmitry Sibirtsev <mailto:sibirtsevdl@gmail.com>`__ added support for
  the HPPA/PA-RISC architecture to the `Capstone
  disassembly/disassembler framework
  <https://github.com/capstone-engine/capstone/commit/9daa1ffbac35f553c4b2c0428af0b5cfdd6850d7#diff-c579e1e2290a10e71b47294265bc0be7b553b8c9fea1d3bd5b9b9546417ff5f5R2>`__.
  Capstone is used by by QEMU and other projects.

Sep 2024
~~~~~~~~
- Qemu v9.1.0 released. Needs at least `one patch for system-mode
  <https://gitlab.com/qemu-project/qemu/-/commit/ead5078cf1a5f11d16e3e8462154c859620bcc7e>`__
  and `one patch for user-mode
  <https://gitlab.com/qemu-project/qemu/-/commit/d33d3adb573794903380e03e767e06470514cefe>`__
  to run stable with 64-bit CPUs.

- Some patches for Linux kernel to fix 64-bit userspace issues.

Jul 2024
~~~~~~~~
- The `Debian 64-bit time_t transition
  <https://wiki.debian.org/ReleaseGoals/64bit-time>`__ has finished and
  stability of PA-Linux has improved greatly. Important next milestones
  will be to port rust to hppa, and maybe to add a LLVM backend for
  parisc.

Jun 2024
~~~~~~~~
- `Dave Anglin contributed a patch
  <https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=72d95924ee35c8cd16ef52f912483ee938a34d49>`__
  which prevents the random segfaults we faced on PA8800 and PA8900 CPU
  machines. It is included in kernel 6.6.35, 6.9.6, and 6.10.0 (and
  higher).
- Work has started to add clock_gettime() syscalls in kernel vDSO.

Apr 2024
~~~~~~~~
- The `Debian 64-bit time_t transition
  <https://wiki.debian.org/ReleaseGoals/64bit-time>`__ is going very
  well. Upgrades were broken until now, but since end of april 2024 it's
  possible again to upgrade most existing debian hppa installations to
  the new binaries from the debian-ports archive. Since now 64-bit
  time_t is enabled by default, and since the LFS64 filesystem calls are
  enabled by default as well, we expect much lesss problems running
  debian hppa.
- `Qemu 9.0 was released. <https://wiki.qemu.org/ChangeLog/9.0>`__ Note
  that the 64-bit hppa emulation is still incomplete and may work with
  Linux guests only.

Mar 2024
~~~~~~~~

- Improving 64-bit CPU emulation in Qemu, e.g. with `CPU fixes from
  Richard <https://lists.nongnu.org/archive/html/qemu-devel/2024-03/msg06872.html>`__
  and `HP-UX 11 64-bit support fixes from Sven
  <https://lists.nongnu.org/archive/html/qemu-devel/2024-03/msg06020.html>`__.
- The `Offline_Diagnostic_Environment\_(ODE)
  <Offline_Diagnostic_Environment_(ODE)>`__ CD-ROM is helpful to verify
  quality of Qemu CPU emulation.
- `Debian 64-bit time transition is ongoing
  <https://wiki.debian.org/ReleaseGoals/64bit-time>`__. Lots of hppa
  packages have to be bootstrapped again.

Jan 2024
~~~~~~~~
- `Initial rust libc support for hppa
  <https://github.com/rust-lang/libc/pull/3539>`__ was added (and
  temporarily removed again).

Nov 2023
~~~~~~~~
- Upcoming Qemu v8.2 will support booting a 64-bit Linux kernel.

Sep 2023
~~~~~~~~
- `Kernel 6.6
  <https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=847165d7c83ddb32aefab3ad4e7424fad919eb05>`__
  and `Qemu 8.2 <https://gitlab.com/qemu-project/qemu/-/commit/cb8a8b2ca9b25fdf561b0fd887df8344fe7927fd>`__
  with `SeaBIOS-hppa v9 <https://github.com/hdeller/seabios-hppa/commit/feb446728ae83f2973b58d9542bf25491dbf888d>`__
  supports Block-TLBs (BTLB) on 32-bit kernels.
- Kernel 6.6 includes `native eBPF JIT compiler for 32- and 64-bit
  kernels <https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=48d25d382643a9d8867f8eb13af231268ab10db5>`__.
- `Dave fixed glibc v2.38 to prevent ``unaligned access to 0xf7ebadcd at
  ip 0xf5f7e307`` syslog warnings <https://sourceware.org/bugzilla/show_bug.cgi?id=30750>`__
- Development to support 64-bit PA-RISC CPU emulation and Astro/Elroy
  PCI-Bridge emulated device in QEMU started. Goal is to (hopefully)
  allow booting a 64-bit Linux kernel and HP/UX 11 with 64-bit support
  in QEMU.
- The `T2 System Development Environment <https://t2sde.org/>`__ Linux
  distribution added support for 32- and 64-bit PA-RISC.

Aug 2023
~~~~~~~~
- `Qemu 8.1.0 released <https://www.qemu.org/>`__.
- `Found a 10-year old bug (since kernel 3.11) which affected 32-bit parisc
  kernels <https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=382d4cd1847517ffcb1800fd462b625db7b2ebea>`__.
- Many kernel bugs fixed in aio, ...

Jul 2023
~~~~~~~~
- `Qemu 8.0.3 released with many parisc fixes (SMP CPU fixes, graphics fixes) <https://www.qemu.org/>`__.

Jun 2023
~~~~~~~~
- Work started to implement native eBPF for Linux kernel.

May 2023
~~~~~~~~
- `palo version 2.24 <https://git.kernel.org/pub/scm/linux/kernel/git/deller/palo.git/>`__
  released.
- `STI text console support on 64-bit machines
  <https://patchwork.kernel.org/project/linux-parisc/patch/ZFKAK7Z4oi8f/ro4@p100/>`__,
  e.g. this allows using all original HP graphics cards in text-mode on
  C8000 workstations.
- `Fix palo to speed up printing the IPL menu on C8000 workstations
  <https://git.kernel.org/pub/scm/linux/kernel/git/deller/palo.git/commit/?h=devel&id=37481ef2e3776292d15883b9f4aa855d4090ee2d>`__.

Apr 2023
~~~~~~~~
- Debian-12 (Bookworm) preparations, with `more than 13,000 pre-built
  packages <https://buildd.debian.org/status/architecture.php?a=hppa&suite=sid>`__.
- Progress on an `upcoming Visualize-FX5 fbdev graphics driver
  <https://patchwork.kernel.org/project/linux-parisc/patch/ZEWqkJekzyIlhBlW@p100/>`__.

Mar 2023
~~~~~~~~
- `More than 12,900 pre-built Debian packages available.
  <https://buildd.debian.org/status/architecture.php?a=hppa&suite=sid>`__

Jan 2023
~~~~~~~~
- Availability of a new `HP J6700
  <https://www.openpa.net/systems/hp-visualize_j6000_j6700.html>`__
  dual-core debian porterbox `parisc.debian.net
  <https://db.debian.org/machines.cgi?host=parisc>`__, sponsored by
  `Cypress Technology Inc <http://www.cypress-tech.com>`__. This
  machines was upgraded to 8 GB RAM and 2 x 300GB discs with parts of
  the former "parisc" `HP A500-44
  <https://www.openpa.net/systems/hp_a400_a500.html>`__ server.

1998-2022
~~~~~~~~~
- See :doc:`PA-RISC_Linux_Project_History <pa-risc_linux_project_history>` for older news.

