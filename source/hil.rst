The HIL bus and HIL drivers
===========================

HIL overview
------------

HIL stands for "Human Interface Loop" and was used on older PARISC
machines and HP300 (m68k processor) series machines to connect
keyboards, mice and other kind of input devices to the machine.

Nowadays you maybe could compare the HIL bus with an very ancient
predecessor of the USB bus.

The PARISC kernel provides two different inplementations to support the
HIL bus, which are

- a very simple HIL keyboard-only driver (no other HIL devices
  supported)

- a complete HIL stack which supports HIL keyboards, HIL mice, HIL
  tablets and other HIL devices.

HIL technical overview
----------------------

The HIL bus is pretty complex, and accessing the HIL devices in a sane
manner from Linux is very hard. Especially correct timing on the HIL bus
needs much care.

The HIL bus consists of the following components:

- SDC - System Device Controller
- MLC - Machine Loop Controller
- HIL devices

The simple HIL keyboard-only driver
-----------------------------------

The simple HIL keyboard-only driver just consists of one single kernel
module which is named "hilkbd" (note that there is no underscore in the
driver name). This driver is a very basic HP Human Interface Loop (HIL)
driver which handles the keyboard on HP300 (m68k) and on some HP700
(parisc) series machines. This driver is pretty stable, reliable and has
very little performance overhead. If you don't need to support HIL mice
or want to use your machine as a desktop machine, you should prefer this
driver. If you need mouse support, use the full HIL driver instead.

The full HIL-driver for keyboards, mice, tablets and others
-----------------------------------------------------------

The full HIL-drivers were originally written by Brian S. Julin
<bri@calyx.com>.

The following Linux kernel modules implement the HIL bus on PARISC:

- hp_sdc - driver for the HP System Domain Controller.
- hp_sdc_mlc - provides access to the HIL MLC through the HP System
  Device Controller.
- hil_mlc - provides HIL MLC state machine and serio interface driver
- hil_kbd - HIL keyboard driver
- hil_ptr - HIL mouse and tablet driver

hp_sdc, hp_sdc_mlc and hil_mlc are the main drivers which need to be
loaded first. After that, any of the other drivers may be loaded at any
time.

Debian Linux distribution and HIL devices
-----------------------------------------

All Debian Linux distributions up to and including "Lenny" have had
problems with HIL devices. Lenny for example still uses the simple HIL
keyboard-only driver for installation, because the autodetection of
attached HIL devices was missing in the Linux kernel 2.6.28. With kernel
2.6.29 we hope to have all missing pieces in the kernel implemented, so
that further Debian releases will work out of the box with the full HIL
stack instead.

If you want to use HIL mice as well, you need to configure Debian to
load the full HIL driver instead (after installation).

High CPU load with HIL drivers, ksoftirqd uses 70-100 percent of the CPU time
-----------------------------------------------------------------------------

This is a known problem and we are working on it. The problem is related
to how the HIL drivers poll the HIL bus, and how the interrupts and
kernel tasklets interact with each other. Currently we try to solve this
issue by migrating the HIL drivers to use kernel workqueues and kernel
threads instead.

Guy Martin posted once a `patch <http://article.gmane.org/gmane.linux.ports.parisc/278/match=use+lower+nice+level+ksoftirqd+hil+enabled>`__
to the parisc mailing list, which temporarily solves this issue, but
this patch will not be accepted upstream.
