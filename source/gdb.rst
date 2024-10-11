GDB - The GNU Debugger
======================

Upstream webpage: http://sources.redhat.com/gdb/

gdb support for hppa-linux was merged upstream in GDB version 6.2.
Currently, there is no official maintainer for the hppa port. Would
anybody like to volunteer?

Details about the hppa implementation
-------------------------------------

:doc:`Stack Unwinding <stack_unwinding>` describes the stack layout on
hppa and how unwinding works.

A description of the DWARF debug format can be found at
http://www.eagercon.com/dwarf/dwarf3std.htm

Currently there is a known problem in gdb with unwinding through static
functions.
