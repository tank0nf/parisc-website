IO-MMU
======

There are two primary types of IO-MMU supported by parisc-linux.

The first is U2/U-Turn, found on machines with PA7200 and PA8000/8200
processors. On these machines, as I understand it, U2/U-Turn act as a
Runway-to-GSC bus bridge. (TODO: Writeup U2/U-Turn info on another page)

The second type of IO-MMU is Astro. Astro (or the successor IKE and
Pluto) is found on all machines with PA8500 and newer processors. (TODO:
Better Astro description on another page)

There are a few more types of IO-MMU found on PA-RISC machines, such as
the JAVA IO-MMU found on T600 servers. However these are not supported,
and quite likely will never be, because the chipset is not IO-Coherent.
