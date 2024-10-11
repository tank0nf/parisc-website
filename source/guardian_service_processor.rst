==========================
Guardian Service Processor
==========================

This page needs improvement, but for now it contains some useful info
about using the GSP with Linux.

Using the GSP card with Linux
=============================

The *Guardian Service Processor* card (recently renamed to *Management
Processor*) can be a little confusing at first. This document attempts
to explain how to use it to best effect under Linux. There is extensive
online help available to you via the ``HE`` command, but it doesn't
explain how it integrates with Linux (only HP-UX and MPE/ix ;-).

There have been several versions of this card; some are integrated onto
the motherboard but most are PCI cards. This doesn't mean you can use
them in a different slot, or in a different machine from the one they
came in -- there are hardware dependencies.

There are 4 physical connectors (ports) to the GSP. One is the LAN port,
the other three are RS232 serial ports. If you attach the so-called *W*
cable to the 25-way socket on the back of the machine, you get all three
(labelled **Console**, **Remote** and **UPS** or **AUX**). If you
connect a regular 25-to-9-pin cable or adapter to the port, you get the
**Console** port, which is incredibly cool.

On the software side, there are either 4 or 5 UARTs, depending on which
version of the GSP you have. They are: **Console**, **UPS/AUX**,
**Remote Session**, **Internal** (not present on all cards) and **Local
Session**. I do not discuss the **Internal** UART in this document as I
don't know how to use it, and it's removed from later cards anyway. How
the UARTs map to the ports is partially under the control of the GSP
card.

The UPS/AUX UART is always connected to the **UPS/AUX** port. By
default, all the other ports are connected to the **Console** UART.
Sending a ``^B`` to this UART breaks you into the GSP card interface.
The intent is that you connect a serial console to the **Console** port
and a modem to the **Remote** port. If you connect to either of these
ports, break into the GSP interface and use the ``SE`` (session)
command, it will attempt to connect you to either the local or remote
session (depending if you're connected to the console or remote port,
respectively).

In order to make use of the session, you'll need to make sure there are
gettys running on the appropriate serial ports. If you look at dmesg,
you'll see something like::

    ttyS00 at iomem 0xfffffffff8000000 (irq = 132) is a 16550A
    ttyS01 at iomem 0xfffffffff8000008 (irq = 132) is a 16450
    ttyS02 at iomem 0xfffffffff8000010 (irq = 132) is a 16550A
    ttyS03 at iomem 0xfffffffff8000038 (irq = 132) is a 16550A

``ttyS0`` is the mirrored console UART, ``ttyS1`` is the UPS/AUX UART,
``ttyS2`` is the remote session and ``ttyS3`` is the local session. So
take a look in ``/etc/inittab`` and you'll see something like::

    T0:23:respawn:/sbin/getty -L ttyS0 9600 vt100

Just add a couple of lines below this, changing them appropriately::

    T0:23:respawn:/sbin/getty -L ttyS0 9600 vt100
    T2:23:respawn:/sbin/getty -L ttyS2 9600 vt100
    T3:23:respawn:/sbin/getty -L ttyS3 9600 vt100

Now restart init with ``telinit q`` and you'll be able to start
sessions. To disconnect from the session, just log out. The GSP detects
the line drop and puts you back into the mirrored console UART.

Remote Power On on B2600 and J6000 machines
===========================================

The B2600 and J6700 workstations have a remote power-on feature that
allows you to power up and shut down your workstation remotely through
the RS232 port. The RS232 receive line is monitored by the system board
Remote Power Controller (RPC). This controller responds to the following
commands:

.. list-table::
   :header-rows: 1

   - 

      - Press:
      - Type:
      - Description
   - 

      - Esc
      - rsys^on
      - Turns the system on
   - 

      - Esc
      - rsys^off
      - Turns the system off
   - 

      - Esc
      - rsys^ton
      - Turns the system off without soft-power down
   - 

      - Esc
      - pic^sleep
      - Causes RPC to stop responding to commands
