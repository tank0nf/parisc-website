INSTALLING PA-RISC Linux
========================

These days PA-RISC Linux is installed using a fairly standard `Debian
Linux <http://www.debian.org/>`__ installer, usually from a CD. If you
can't use the standard CD-ROM install, there are several other methods
(network, tape, etc...). This `PA-RISC/linux-boot HOWTO
<http://www.pateam.org/doc.html>`__ by the `ESIEE
<http://www.pateam.org/>`__ team in France may be helpful. And if you
get stuck please ask the `parisc-linux
<mailto:linux-parisc@vger.kernel.org>`__ mailing list. You might want to
`join it <http://vger.kernel.org/vger-lists.html#linux-parisc>`__ too.

The old completely unautomated method is described below for people with
special situations where no Debian install works.

This document explains some of the ways that PA-RISC Linux is different
from other Debian Linuces so you can be better prepared during the
installation process -- **this is not an installation manual**. Since
most things are common between PA-RISC and other flavors of Debian
Linux, you can use the fine documentation at `www.debian.org
<http://www.debian.org/>`__.

HP-UX and Linux on a Single PA-RISC Box
---------------------------------------

You'll need a separate disk drive for Linux from HP-UX. Sorry for that
limitation but it's the way things are.

During the installation process, you will need to partition a disk and
you need to choose the right one! Start by interrupting the boot process
following the instructions, either pressing ESCAPE or "any key" within a
certain time limit.

Once you're talking to the boot firmware, type "path". This will give
you a message like::

    Primary:    FWSCSI.6.0

That tells you your current boot path is the disk at SCSI address 6
(it's almost always 6). To see what disks are present, ask the firmware
to "search". After a while it will give a list of bootable devices it
found which may include disks, tape, cd-rom(IDE), and network(LAN),
including the disk mentioned by the "path" command above.

Linux names SCSI disks /dev/sda, /dev/sdb, etc... starting with the
**LOWEST** SCSI ID, so from the list above you can figure out what names
Linux will assign and be sure to avoid the ones imporant to HP-UX.

Our Boot Loader isn't Lilo
--------------------------

Our boot loader is *palo*, not *lilo*. The `palo README
<http://ftp.parisc-linux.org/cgi-bin/cvslite/palo/README.html>`__ is a
bit out of date but still useful if you want to know the icky details.
For installation you need to know palo is different from lilo in two
important ways:

#. palo can boot a kernel right out of a normal Linux "ext2" disk
   partition -- no need to run palo every time the kernel changes.

#. palo needs a special disk partition for itself because of the way
   PA-RISC firmware works, so read the next section.

Disk Partitions
---------------

During your Debian install, you will be asked to partition a disk. If
you have multiple disks, you might want to read the information about
disk names in the "HP-UX and Linux" section above.

**You must place two special partitions on your boot disk** and **they
must fit entirely within the first 2Gbytes of your disk**. The first
special partition is the "palo" partition, which will hold the secondary
boot loader image and a Linux kernel. We usually call this the
"recovery" kernel because you'll usually boot a kernel out of a normal
partition, but in an emergency you can use this one.

I usually recommend 16Mb for the palo partition because it can
optionally hold a second kernel and a ramdisk image, but 8Mb is just
fine if you want to save space. The numeric (hex) code for the palo
partition is "f0". When you are in the disk partitioning tool you must
change the type of your intended palo partition to "f0".

The next special partition is the one which will be a normal ext2 file
system where you'll be storing your kernel. If your disk is larger than
2Gbytes, it's convenient to make a small partition which will be mounted
as /boot which is contained within the first 2Gbytes of the disk. I
often use a 32-Mbyte /boot partition so I can keep several kernels
around.

After this you'll want to add the usual Linux partitions -- one or more
swap partitions and one or more ext2 partitions. They are not required
to be within the first 2 Gbytes or anything. Here's a working setup as
shown by **cfdisk**, the partitioning program used by the Debian
installer.

::

                                  Disk Drive: /dev/sda
                                Size: 73407865856 bytes
                  Heads: 255   Sectors per Track: 63   Cylinders: 8924
        Name        Flags      Part Type  FS Type          [Label]        Size (MB)
     ------------------------------------------------------------------------------
        sda1                    Primary   Linux/PA-RISC boot                  24.68
        sda2                    Primary   Linux ext2                          41.13
        sda3                    Primary   Linux swap                         542.87
        sda5                    Logical   Linux ext3                        2155.03
        sda6                    Logical   Linux ext3                        2155.03
        sda7                    Logical   Linux ext3                       68483.69
