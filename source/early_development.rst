=================
Early Development
=================

Year 1999
=========

**December 31st, 1999**

- LASI Serial driver
- HIL keyboard driver (Matthew)
- PS/2 LASI keyboard driver (Philipp)
- Extensive MM work (Philipp)
- LASI Sound (Philipp)

**October 7, 1999**

The following is a list of what has been accomplished in the PA-RISC Linux project over the past few months:

- interrupt handling now works
- the start of Virtual Memory has been completed
- hardware discovery through PDC works
- PCI bus walking with the Dino contoller is functional
- IO and MMIO space for the Dino PCI bus has been started
- we've moved to kernel version 2.2.13 as our base
- a shell loads and dies

**June 25, 1999**

- The kernel boots and promptly dies after displaying version information.

**May 1, 1999**

- The kernel builds! Work begins on getting the kernel to boot using a modified boot loader.

**March, 1999**

- Jason Eckhardt gets the boot loader working. Work starts on modifying the kernel for elementary parisc support.

**October, 1998**

- Martin Petersen, Alex deVries and Christopher Beard dream up the project at Atlanta Linux Showcase.

.. _year_2000:

Year 2000
=========

**18 December 2000**

- Fix user stacks so they start at a reasonable address and grow upwards. (Matthew)

**15 December 2000**

- Added chassis LED- and LCD-driver. (`Helge <mailto:deller@gmx.de>`__)

**5 December 2000**

- Initial merge with Linus, including a few tidy-ups to our tree. (Alan Cox, Matthew Wilcox)

**29 November 2000**

- Fixed parallel port driver to not crash kernel on early ASP based machines. (`Helge <mailto:deller@gmx.de>`__)

**10 November 2000**

- Fixed remaining \__FUNCTION\_\_ usage to be complaint w/gcc definition (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- Merge to linux-2.4.0-test10 completed (`Paul Bame <mailto:bame@puffin.external.hp.com>`__)
- palinux-linux v0.5 beta ISO published! (`Paul Lahaie <mailto:pjlahaie@puffin.external.hp.com>`__)
- Fixed strace (`Richard <mailto:rhirst@linuxcare.com>`__)

**7 November 2000**

- 64-bit: PCI Interrupt Routing (iosapic support) (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- 64-bit: PCI Resource init/mngt (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- "reboot" command works on c3k/j5k (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- PS/2 keyboard driver is missing various important keysyms (`Thomas Marteau (ESIEE Team) <mailto:marteaut@esiee.fr>`__)

(No - I'm not the only person working on this port - just happen to muck with this list more than anyone else. :^) -grant)

**24 October 2000**

- 64-bit: Fixed PDC wrappers so upper half of "callee saves" register don't get trashed `Paul <mailto:bame@puffin.external.hp.com>`__)
- VM: Paging now works (`John <mailto:john_marvin@hp.com>`__)
- VM: Fixed most outstanding bugs! A180 is quite stable now... (`John <mailto:john_marvin@hp.com>`__)
- PA1.1 Hand-Tuned/Optimised asm IP checksum code (`Randolph <mailto:tausq@tausq.org>`__)
- SMP : add cpuinfo_parisc cpu_data[] and fix boot_cpu_data usage (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- update /proc/interrupts info (`Helge <mailto:deller@gmx.de>`__)
- Added "bits_wide" parameter to txn_alloc_data(). (`Grant <mailto:grundler@puffin.external.hp.com>`__)

**17 October 2000**

- dynamic user stack. ( `Richard <mailto:rhirst@linuxcare.com>`__/ `David <mailto:dhd@puffin.external.hp.com>`__ )
- Finish ptrace(2) implementation. (`Thomas <mailto:tsbogend@alpha.franken.de>`__)
- STI fbcon driver - STI console works (`David <mailto:dhd@puffin.external.hp.com>`__)
- update "How-To Build the Kernel" recipe (`Alan Modra <mailto:amodra@linuxcare.com>`__)
- 64-bit kernel : PAT PDC device discovery (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- Smarter resource mgmt in ccio driver (`Ryan <mailto:rbradetich@uswest.net>`__)
- Smarter resource mgmt in sba driver (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- Implement kernel module loading (this is half userspace work). ( `Richard <mailto:rhirst@linuxcare.com>`__/ `David <mailto:dhd@puffin.external.hp.com>`__ )

**10 October 2000**

- Kernel built/booted all native! (`Richard <mailto:rhirst@linuxcare.com>`__)
- base/glibc/gcc/etc debs are now available (`David <mailto:dhd@puffin.external.hp.com>`__)
- STI console driver(`Helge <mailto:deller@gmx.de>`__ and `Paul <mailto:bame@puffin.external.hp.com>`__)
- Smarter resource mgmt in ccio driver (`Ryan <mailto:rbradetich@uswest.net>`__)
- merged rbrad's changes into sba (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- User stack grows dynamically! (`Richard <mailto:rhirst@linuxcare.com>`__)
- flush_kernel_dcache_range(): off-by-one bug found/fixed by fleedwood/jsm
- SBA I/O MMU: LCI bug fixed w/help from chada/jsm
- 64-bit kernel almost gets to user space on c3k

**28 August 2000**

- Linux syscalls (`John <mailto:john_marvin@hp.com>`__)
- Signals (`David <mailto:dhd@puffin.external.hp.com>`__)
- Check other arches for new syscalls we don't have and add them. (`Matthew <mailto:matthew@wil.cx>`__)
- WAX EISA adapter. (`Helge <mailto:deller@gmx.de>`__)
- Symbios 8xx SCSI driver (`Richard <mailto:rhirst@linuxcare.com>`__)
- NCR 720 Zalon SCSI driver (`Richard <mailto:rhirst@linuxcare.com>`__)

**11 March 2000** **Kernel**

- NCR710 driver (`Gyula <mailto:gyula_matics@hp.com>`__)
- pci_consistent() interfaces implementation (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- ELF-reenable the kernel (`Sam <mailto:sammy@sammy.net>`__)

**13 February 2000**

Kernel

- IO SAPIC support (Grant)
- C3000/J5000 PCI support (Grant)
- Tulip driver
- LASI Apricot ethernet (Sammy)
- IP checksum code in C (Thomas)
- console termios setup (Martin)
- Moved to Kernel 2.3.42

Userland

- Sash 3.4 works (Matthew)
- ifconf (Matthew)
- httpd (Josh)

.. _year_2001:

Year 2001
=========

**February 28, 2001**

Kernel

- rewrite semaphores -- both read/write and ordinary (Matthew)
- Create an IO tree to support multiple I/O MMUs. (`Ryan <mailto:rbradetich@uswest.net>`__)
- SuperIO Serial (`Martin Petersen <mailto:mkp@mkp.net>`__ and Alex deVries)
- fix fbcon-sti.c bugs and X11? (`David <mailto:dhd@puffin.external.hp.com>`__)
- Kernel Memory dumps on crash. See `SGI's LKCD <http://oss.sgi.com/projects/lkcd/>`__. (`Bruno Vidal? <mailto:bruno_vidal@hpfrcu03.france.hp.com>`__)
- HIL keyboard driver needs updating (`Brian <mailto:bri@mojo.calyx.net>`__ and `Alex <mailto:alex@linuxcare.com>`__ has access to HIL documentation)
- Coalesce DMA pages in sba_map_sg() (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- Coalesce DMA pages in ccio_map_sg() (`Ryan <mailto:rbradetich@uswest.net>`__)
- LASI Floppy controller (`Dave Kennedy <mailto:dkennedy@linuxcare.com>`__)
- WAX EISA bus addapter (`Alex deVries <mailto:alex@linuxcare.com>`__)
- Harmony audio driver completion (`Alex deVries <mailto:alex@linuxcare.com>`__)
- AD1889 PCI Audio driver (`Alex deVries <mailto:alex@linuxcare.com>`__)
- SMP support

  - build/test w/CONFIG_SMP (`ggg <mailto:ggg@cup.hp.com>`__)
  - Interrupt Distribution (even CPU loading) w/CONFIG_SMP (`ggg <mailto:ggg@cup.hp.com>`__)
  - asm-parisc/cache.h defines L1_CACHE_BYTES - issue w/32-bit on PA2.0 (`ggg <mailto:ggg@cup.hp.com>`__)

- 64-bit kernel

  - VM (`John <mailto:john_marvin@hp.com>`__)
  - PA2.0 Hand-Tuned/Optimised asm IP checksum code (`Randolph <mailto:tausq@tausq.org>`__)
  - Syscalls/ioctl (`John <mailto:john_marvin@hp.com>`__, `Paul <mailto:bame@puffin.external.hp.com>`__, George, Ringo, **Cast of Thousands**)
  - defconfig and friends
  - check/fix sim700 driver compile warnings (needed to support Cxxx boxes in wide mode, if we ever want to) (`Ryan <mailto:rbradetich@uswest.net>`__)
  - 64-to-32-bit translator for PDC firmware calls on Cxxx boxen (enable more people to test wide kernels) (`Ryan <mailto:rbradetich@uswest.net>`__)
  - Change 'unsigned long sversion:28' to unsigned int in hardware.h? Change hardware.c functions which take hversion/sversion args?
  - Do the right thing with macro elf_check_arch() for wide/narrow kernels (see include/asm-parisc/elf.h)
  - Fix 'hwclock' problem (probably a broken or missing ioctl32.c translation).

- Kernel debugger - KWDB (`Grant <mailto:grundler@puffin.external.hp.com>`__)
- Fix cache/TLB flushing. (`John <mailto:john_marvin@hp.com>`__)
- Finish ptrace(2) implementation. (`Thomas <mailto:tsbogend@alpha.franken.de>`__)
- Unaligned trap handler. (`Volunteer? <mailto:Volunteer>`__)
- Finish floating point completion and trap handler. (`Volunteer? <mailto:Volunteer>`__)
- Verify floating point trap behaviour is correct (`Volunteer? <mailto:Volunteer>`__)
- Remove kbd_read_status() dependency on CONFIG_GSC_PS2. (`Volunteer? <mailto:Volunteer>`__)
- <include/asm-parisc/types.h> defines dma_addr_t as 32-bit. PCI/Elroy supports 64-bit. "typedef ulong_t dma_addr_t"? (`Volunteer? <mailto:Volunteer>`__)
- Update Documentation/parisc/registers (`Volunteer? <mailto:Volunteer>`__)
- PA1.1 SR can be 16-32 bits wide - only using 16-bits. (`Volunteer? <mailto:Volunteer>`__)
- rewrite kernel_thread (`Matthew <mailto:matthew@wil.cx>`__)
- Dino/100BT: Use "Good Dog" Timer to limit GSC bus tenancy instead of limiting tulip DMA burst length. (`Volunteer? <mailto:Volunteer>`__)
   (JSM has tried this - it didn't work. GGG thinks it should.)
- remove asm-parisc/real.h fixing dependencies on it
- Verify and fix the existing code in led.c for LCD displays (`Volunteer? <mailto:Volunteer>`__)

Userland:

- Test/Debug floating point environment support in GNU libc. (`Volunteer? <mailto:Volunteer>`__)
- Debug floating point environment and trap handling. (`Volunteer? <mailto:Volunteer>`__)
- Write open version of required 64-bit libmilli routines. (`Volunteer? <mailto:Volunteer>`__)
