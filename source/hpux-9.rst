======
HPUX-9
======

.. note::

   This information is taken from:
   https://web-docs.gsi.de/~kraemer/COLLECTION/HPUX/scratch.html

HP-UX 9.x/8.x installation from scratch
=======================================

Prerequisites
-------------

HP-UX 9.x/8.x does not install on disks larger than 2GB (exactly). It
may boot off the ``Install`` media, but the subsequent ``CoreOS``
installation will fail. The typical message is a complaint about at
least 55MB which have to be free for swap space.

HP-UX 9.x installs trouble-free only on disks listed in
`/etc/disktab/
<https://web-docs.gsi.de/~kraemer/COLLECTION/HPUX/disktab9x.txt>`__, the
larger ones being:

- Quantum PD425S
- Quantum LPS525S
- Quantum PD1050S
- Micropolis 1588[T], 660MB
- Micropolis 1528, 1.4GB
- Micropolis 1924, largeish ?
- Seagate ST3600N, 525MB
- HP C3010
- HP C2247, 1GB
- HP C2235, 420MB

HP-UX 8.x is even more restrictive, `/etc/disktab/
<https://web-docs.gsi.de/~kraemer/COLLECTION/HPUX/disktab8x.txt>`__. I
had to resort to the antique Seagate ST3600N to get it to install.

Some disks not listed in ``/etc/disktab/`` are installable too, after
some warnings (which can be ignored in my experience) from the
installation procedure:

- IBM/Quantum Fireball 1280
- IBM DPES 31080
- Seagate ST11200N

HP-UX 9.x takes at least 200MB, >330MB with NLS support, plus 55MB for
swap space, thus a 400 to 420MB disk is minimum. If the LaserROM
documentation should reside on the same disk it would have to be as
large as 1GB. In this case disk space is very tight, so one might
consider to install the LaserROM on a separate second disk, if possible.
| All this doesn't include user and freeware filesystems.

Base system
-----------

From CD
~~~~~~~

#. Straightforward. Insert ``Install`` CD, cycle power. During startup
   press ``ESC`` to allow boot media select.

   - On 300/400 series:

     - (soon to come)

   - On 700/800 series:

     - A bootable device list appears.
     - On some models a ``BOOT_ADMIN`` console will allow further actions.
     - Anyway, ``boot scsi.x`` where ``x`` is the CD's SCSI address
     - Answer the questions and accept the defaults. One may alter some
       of the root filesystem parameters, e.g. increase swap space
       beyond the proposed value (but not larger than 128MB if LaserROM
       should coexist on the same 1GB disk).
     - Leave/set date below Y2K.

#. On request (update): insert ``Core OS`` CD and proceed. For external
   CD-ROM drives this might involve power cycling.

   - If this does not work (as experienced e.g. with series 400 systems):

     #. press ``Reset``, reboot and press ``ESC`` to allow selection of
        a minimal system (``SYSHPUX``).

     #. Then
        ::

         mount /dev/bsrc /UPDATE_CDROM; rm /update.lock; /etc/update

     #. Accept proposed default terminal.

#. In the presented menu choose ``Change Source/Destination`` and select
   CD-ROM, no password. Press ``Done``/``F4``

   - In the presented menu choose installation method. In my experience
     one may ``Select all filesets`` and install just everything (ca.
     160 MB)

   - Apply Y2K patches (HP-UX 9.1 for series 300/400 only):

     - Insert CD, power cycle CD-ROM drive and::

           mount /dev/bsrc /UPDATE_CDROM; rm /update.lock; /etc/update

     - If the mount fails, reboot and repeat.
     - Alternative mount method::

          mount -r -t cdfs /dev/dsk/cEd3s0 /UPDATE_CDROM  # CD with SCSI ID=3
          rm /update.lock; /etc/update                    # or use VUE toolbox, if active

     - In the presented menu change installation source to CD-ROM and
       select/install all filesets.

#. If available, Tools and Languages (C,Pascal,FORTRAN):

   - reboot with CD inserted, (alternatively try switch off/on CD
     drive)::

       mount /dev/bsrc /UPDATE_CDROM; rm /update.lock; /etc/update

   - or::

       mount -r -t cdfs /dev/dsk/cEd3s0 /UPDATE_CDROM  # CD with SCSI ID=3 
       rm /update.lock; /etc/update                    # or use VUE toolbox, if active 

   - Select/install all filesets, may skip NLS stuff

#. On request and if the machine is already connected to a network one
   may configure it already during installation. Just answer the
   questions on

   - network mask (e.g. 255.255.255.0)
   - and Gateway address (e.g. 192.168.1.1 for a router), a (dummy) name
     must also be given.

#. After (``root``) login start multi-user level, includes starting
   VUE::

       init 3 

#. Note that if one chooses to leave the date as is, to avoid Y2K
   issues, one might have to fix SAM's other date related problems.

