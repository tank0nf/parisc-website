PA-RISC Linux Runtime Conventions
=================================

The PA-RISC Linux runtime is very similar to what was designed for HPUX,
as described in the HP runtime documents:
http://ftp.parisc-linux.org/docs/arch/pa-runtime-32-SOM.pdf and
http://ftp.parisc-linux.org/docs/arch/pa64rt.pdf

:doc:`Register Conventions <register_conventions>` explains how
registers are used and how they are passed to functions.

Like HPUX, PA-RISC Linux has a stack that grows up instead of down. This
has some advantages (not as easy to get stack overflow exploits), but
sometimes creates some porting issues.
