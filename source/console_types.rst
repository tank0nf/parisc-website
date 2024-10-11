=============
Console Types
=============

We need to sort out our console setup so it's in a mergeable state for
upstream, and functional for us.

A console is the 'back end' of ``printk()``. Its job is to get
characters from the kernel to the user. There are several kinds of
console supported:

- PDC
- 8250 serial

  - GSC
  - SuperIO
  - Diva

- MUX serial
- STI graphics
- Framebuffer

  - STI
  - possibly other

The Emerald serial console is not yet supported. Linux has some other
fun consoles we haven't played with yet like the parallel port console
and netconsole.

The PDC console is available at all times on all PA-RISC hardware. We
use it as an early debug console and as a system panic console. It's not
suited for use as a general purpose console as it has limited facilities
for console input.

In order to initialize the GSC 8250 console, we need to find the GSC
8250 serial port which happens quite late in boot. The same is true for
the MUX console. The Diva 8250 console is similar, though it is a PCI
device. SuperIO 8250 console gets initialized quite early as we know it
is accessible at ``0x3f8``. The graphics consoles also happen a bit
later during boot.

Issues
~~~~~~

In order for us to get output as soon as possible, we should register
the PDC console ASAP. As other consoles come up, they are supposed to
take over using the ``CON_BOOT`` mechanism (this has not been merged
upstream yet).

We export the ``con_start`` and ``log_end`` variables from ``printk.c``
so we avoid printing stuff twice. Maybe we could use the
:doc:`PDC Stable Storage <pdc_stable_storage>` driver to figure out
which device was the real console and clear that device's
``CON_PRINTBUFFER`` flag?

``pdc_console_die()`` appears to be an unused function.
