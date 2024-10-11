====================
PA-RISC Linux Kernel
====================

Kernel issues
-------------

Nothing to brag about, but it's important, so let's keep it visible:
Kernel :doc:`Hot Spots <_hot_spots>` and problems :doc:`Known Issues
<known_issues>`.

Kernel flavours
---------------

The kernel comes in two flavours: 32 bit and 64 bit. The older machines
(PA 7xxx processors) only run the 32 bit kernel. Newer machines (PA8xxx
processors) may run either 32 or 64 bit kernels. Some machines
(depending on the PDC firmware) may only run the 64 bit kernel. The user
land is currently only 32 bit ELF, which means that the **only**
interest in running a 64 bit kernel on machines capable of running 32
**and** 64 bit is accessing more than 4GB of RAM.

Low Level Kernel Code
---------------------

A collection of notes about various parts of the PA-RISC low level Linux
kernel code can be found here:

- :doc:`Virtual Memory Subsystem <virtual_memory_subsystem>`
- :doc:`SMP <_smp>` implementation
- :doc:`Discontiguous Memory Support <discontiguous_memory_support>`
- :doc:`Device Drivers <_device_drivers>` and interaction with the :doc:`Device Model <device_model>`
- :doc:`Interrupts <interrupts>` and :doc:`IO-SAPIC <io-sapic>`
- :doc:`EISA <_eisa>`, :doc:`GSC <gsc>`, :doc:`PCI <pci>` and :doc:`IO-MMU <io-mmu>` implementations
- :doc:`Futex Implementation <futex_implementation>`
- :doc:`Locks <locks>` and `Atomic Operations <_atomic_operations>`
- :doc:`Time <time>` and high-precision timers.
- :doc:`Registers <registers>` and Space Registers

Specific Device Drivers
-----------------------

Here are some drivers that have been written specially for the PA-RISC
Linux port, as they concern either PA-RISC-specific devices, or
"generic" devices that are only found in PA-RISC systems.

- :doc:`STI FrameBuffer <_sti_framebuffer>` and :doc:`STI Console <_sti_console>`
- :doc:`AD1889 <ad1889>` PCI Soundmax Controller
- :doc:`Harmony Audio <harmony_audio>`
- :doc:`SuperIO <_superio>`
- :doc:`HIL <hil>` bus and drivers

PA-RISC Hardware/Firmware
-------------------------

Also some bits about PA-RISC specific hardware/firmware and the way it
is used by the kernel:

- :doc:`Processor Dependent Code <processor_dependent_code>` (PDC)
- :doc:`Guardian Service Processor <guardian_service_processor>` (GSP)
- :doc:`Console Types <console_types>`

Other Gotchas
-------------

Bits of information related to the Linux Kernel but not specific to
PA-RISC

- :doc:`Sparse <sparse>` compile-time checks for the Linux kernel
- :doc:`Kernel Profiling <kernel_profiling>`
