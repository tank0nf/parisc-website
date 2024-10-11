GSC
===

GSC, the **General** (or Gonzo) **System Connect** is the primary I/O
bus of the early HP workstations. On PA7100LC and PA7300LC systems, the
processor also sometimes sits on the GSC bus. The bus is 32-bits wide
and comes in several flavours. GSC cards are available in many different
form factors to fit in various different chassis sizes.

- GSC-1x: The original GSC bus implemented on PCX-L and used in the
  Gecko, Mirage and Electra computers. Peak Bandwidth 142MB/s w/DMA, 106
  MB/s with PIO writes.

- GSC+: Enhancements added for KittyHawk/SkyHawk (U2 chip) that allow
  for pending transactions. GSC+ enhancements are orthogonal to the
  GSC-1.5X and GSC-2X enhancements. Aka "Extended GSC" or "EGSC".

- GSC-1.5x: GSC-1X with an additional variable length write transaction.

- GSC-2x: GSC-1.5X with a protocol enhancement to allow data to be sent
  at double the GCLK rate (Peak bandwidth = 256 MB/s.)

Misc Notes
----------

- All versions of the K-Class systems operate the GSC bus at the same
  speed. The core I/O slots all run at 32MHz. The other slots connected
  to the Harrier board all run at 40MHz.
