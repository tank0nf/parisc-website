64-bit Userspace TODO
=====================

Listed here are the tasks required to complete a 64-bit userspace:

- Select the required 64-bit dynamic relocations.
- Implement the 64-bit relocations in linker.
- Make sure gcc can use the new 64-bit linker to create libraries and binaries.
- Implement a 64-bit glibc with the required 64-bit relocation processing.
- Test it all...

Completed Tasks:
----------------

- Binutils and the linker already support static 64-bit relocations.
- Kernel support for 64-bit tasks and VMA.

Anyone wishing to work on these tasks should contact the parisc-linux
list at http://lists.parisc-linux.org.
