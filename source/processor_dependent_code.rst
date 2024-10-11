========================
Processor Dependent Code
========================

What is the PDC?
================

The Processor Dependent Code (aka "PDC") is a firmware executable that
lives in the machine's PROM, and, among other things, handles basic
initialization during boot up and provides a :doc:`Boot Console Handler
<_boot_console_handler>` (BCH). It could be considered as a sort of BIOS
for the PA-RISC architecture.

When the machines starts, it loads the PDC that then performs various
hardware checks, and finally shows the user a limited interface (the
BCH) through which information can be collected about the hardware, and
some settings can be changed (such as *Paths*, *Fast Boot*, *Fan
Choice*, etc). For more details about how to use that PDC interface, one
can look at the corresponding section of the `PA-RISC/Linux Boot HOWTO
<http://www.pateam.org/parisc-linux-boot/PA-RISC-Linux-Boot-HOWTO/bootadmin.html>`__.

Aside these boot-time facilities, the PDC is also responsible for
providing a set of low-level routines that can be accessed by the
operating system of the running machine.

Linux on PA-RISC uses these routines for various tasks, including device
discovery, *chassis log* reporting and *stable storage* accessing. Some
of the kernel hooks to access the PDC are documented here.

PDC comes in several flavours, that behaves differently when dealing
with device initialization. More about that on the :doc:`PCI <pci>` and
:doc:`IO-SAPIC <io-sapic>` pages.

Code Documentation
------------------

- :doc:`PDC Chassis <pdc_chassis>` / :doc:`PDC Chassis Log <pdc_chassis_log>`
- :doc:`PDC Stable Storage <pdc_stable_storage>`
