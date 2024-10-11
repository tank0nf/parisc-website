Stack Unwinding
===============

HP unwinding information
------------------------

Following HPUX, all proper PA-RISC Linux functions are generated with
unwind information. The runtime documents (e.g.
http://ftp.parisc-linux.org/docs/arch/pa-runtime-32-SOM.pdf) describes
this in some detail.

Essentially, each binary contains an ELF section named .PARISC.unwind
which contains unwind records for each function in an executable. The
unwind record contains, amongst other things, the start and end
addresses of a function, the size of the stack frame created when this
function is called, and some flags which indicate the layout of the
stack frame. Thus, to unwind regular functions, it is typically
sufficient to consult the unwind record of the present function, and
adjust the stack pointer and instruction pointer based on the
information stored in the unwind record and the current stack frame.

DWARF2 Unwinding
----------------

The HP unwinding infrastructure is used by gdb as the main unwinding
method; however, the PA-RISC linux toolchain also supports dwarf2
unwinding. Recent versions of gcc can generate dwarf2 records for
exception handling. This is used by various languages (e.g. C++, java)
to unwind the stack when an exception happens. (TODO: explain the dwarf2
unwinding mechanism here).

Signal Frame Unwinding
----------------------

Some applications also need to be able to unwind through a signal frame.
As is the case for several other architectures, this is done in a rather
ad-hoc way by examining fixed locations in the stack. The kernel lays
down a specific signal frame when a signal handler is called. The signal
frame contains the values of all the registers that were saved when the
signal was triggered. By decoding the signal frame, it is possible to
determine which function was being called when the signal was delivered.

In order to determine if one is currently in a signal frame, the
instructions pointed to by the return pointer of the signal handler can
be examined. With a 2.4 kernel, the return pointer should point directly
at the signal trampoline, which is 4 words in length.

In 2.6 kernels there are two trampolines, one for restartable syscalls
and the other for signals. The signal trampoline is still 4 words in
length, and the return pointer points at the 5th word in the trampoline
structure. (Early versions of the 2.6 kernel had a bug where the rp
would point to the 4th word, this was fixed in 2.6.5-rc2-pa4).

The signal return trampoline contains the following instructions::

       3419000x ldi 0, %r25 or ldi 1, %r25   (x = 0 or 2)
       3414015a ldi __NR_rt_sigreturn, %r20
       e4008200 be,l 0x100(%sr2, %r0), %sr0, %r31
       08000240 nop

Some good references of how to do signal frame unwinding can be found in
the gcc source code (gcc/config/pa/pa32-linux.h) and in the gdb source
code (hppa-linux-tdep.c)

Virtual Dynamic Shared Objects (vDSO) and signal frame unwinding
----------------------------------------------------------------

There is recent development of a patch that has the kernel generating a
DSO in memory and mapping this into every process space. The DSO is
added to the glibc search path, has unwind information, and provides
entry points for all types of trampolines. Thus gdb need not have any
special case handling code for unwinding. The return pointer in the
signal handler will point to a virtual DSO instead of the stack, and gdb
will use the stored DWARF2 or PARISC.unwind information.

This is highly experimental as of February 2005. The vDSO is also able
to provide optimized function calls that can override glibc functions.
This is particularly useful for cpu specific gettimeofday or locking
primitives.
