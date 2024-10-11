Toolchain
=========

.. toctree::
   :maxdepth: 1

   gcc
   binutils
   glibc
   gdb
   userspace64
   runtime_conventions
   cross_compiler_toolchain

In order to build applications you need:

- A compiler: :doc:`gcc <gcc>` has built parisc-linux targets since
  version 3.x

- A linker: GNU :doc:`binutils <binutils>` supplies the linker, assembler
  and various binary utilities

- A library: GNU :doc:`glibc <glibc>` supplies this

- And maybe a debugger: :doc:`gdb <gdb>` in case you want to figure out
  why "it's not working?!"

These elements are called the "tool chain." The palinux tool chain is
somewhat temperamental. However, palinux builds are now self hosting
(the installed system can compile and build itself)

Currently, only 32-bit userspace is well-supported. There has been some
discussions to implement a 64-bit userspace (:doc:`userspace64
<userspace64>`), but a lot of work still needs to be done.

While there are some documents that describe the PA-RISC runtime, there
is also a lot of undocumented pieces. Some information is collected
below:

- The PA-RISC Linux 32-bit ELF runtime is based heavily on the HPUX
  32-bit `SOM runtime <http://ftp.parisc-linux.org/docs/arch/pa-runtime-32-SOM.pdf>`__.

- Summary of the :doc:`Runtime Conventions <runtime_conventions>`

- The 32-bit and 64-bit ELF relocations are described in the
  `Processor-specific supplement for PA-RISC
  <http://ftp.parisc-linux.org/docs/arch/elf-pa-hp.pdf>`__. Not all the
  relocations described in that document are implemented currently.

- :doc:`Stack Unwinding <stack_unwinding>` explains how stack frames are
  setup on palinux, and how to unwind through them

Currently, we are working on supporting :doc:`Thread Local Storage
<thread_local_storage>` and NPTL for glibc.

There is also a :doc:`Mono Porting <mono_porting>` effort underway.
