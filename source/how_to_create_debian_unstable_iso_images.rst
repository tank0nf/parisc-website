========================================
How to create Debian unstable iso images
========================================

PA-RISC is not any longer an official Debian distribution and as such,
Debian ISO install images are not produced any longer by the Debian
developers.

This website describes the basic steps how you can create such images
yourself. The instructions should - with minor modifcations - work for
other architectures like alpha or sparc too.

What you need to know
---------------------

Prebuilt debian unstable packages are available at the repository at
http://ftp.debian-ports.org/debian/ . In most cases it's not possible to
install from the debian ports repository, because:

#. it is a moving target, which means that the Linux kernel udeb
   packages which are needed by the kernel on the ISO/liffile may not be
   available any longer at a later date, and

#. the bootloader (e.g. palo for parisc, aboot for alpha, silo for
   sparc) is not available there (because those architectures are not
   any longer release architectures, so the bootloaders are not being
   built any long), and

#. the partitioning tools during installation for the architecture might
   be missing for the same reason (e.g. partman-palo for parisc).

Basic steps
-----------

#. Create a local copy of the debian-ports repository
#. Build the debian-installer packages
#. Add missing boot loader / partitioning tools packages to the repository
#. Build the final iso image

Create a local copy of the debian-ports repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Install reprepro (apt-get install reprepro)
#. Create a directory which will hold the copied packages (around 60 GB
   storage needed!). You will need
   :download:`Reprepro-conf-alpha.zip <media/Reprepro-conf-alpha.zip>`
   for one of the steps below::

        apt-get install reprepro
        mkdir -p /extra/deller/debian-alpha-archive/
        cd /extra/deller/debian-alpha-archive/
        # curl/wget the Repro-conf-alpha.zip file
        unzip Reprepro-conf-alpha.zip
        rm Reprepro-conf-alpha.zip

        # now modify the files in conf/* to your needs
        # now run "reprepro update" to pull all files from debian-ports
        reprepro update

Build the debian-installer packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Read `how to check out the debian installer
   <https://wiki.debian.org/DebianInstaller/CheckOut%7Con>`__. It's done
   below::

        apt-get install mr myrepos git curl fakeroot
        apt-get build-dep debian-installer
        mkdir -p /extra/deller/DEBIAN_INSTALLER/{TEMP,bootstrap}

        # See: https://wiki.debian.org/DebianInstaller/CheckOut
        cd /extra/deller/DEBIAN_INSTALLER/
        git clone https://salsa.debian.org/installer-team/d-i.git debian-installer
        cd debian-installer
        scripts/git-setup
        mr checkout 

        # check out other packes for your architecture into the packages directory
        # for a list see here:
        # https://alioth.debian.org/plugins/scmgit/cgi-bin/gitweb.cgi?a=project_list;pf=d-i

        cd /extra/deller/DEBIAN_INSTALLER/debian-installer/packages

        # in the past, for alpha:
        # git clone https://anonscm.debian.org/git/d-i/attic/aboot.git
        # git clone https://anonscm.debian.org/git/d-i/attic/aboot-installer.git
        # for parisc:
        # git clone https://alioth.debian.org/anonscm/git/d-i/attic/palo-installer.git
        # git clone https://alioth.debian.org/anonscm/git/d-i/attic/partman-palo.git
        # for sparc:
        # git clone https://alioth.debian.org/anonscm/git/d-i/attic/silo-installer.git
        # palo and aboot are now in the unreleased repositories:
        # http://ftp.ports.debian.org/debian-ports/pool-hppa/main/p/palo-installer/
        # http://ftp.ports.debian.org/debian-ports/pool-alpha/main/a/aboot-installer/
        # https://salsa.debian.org/debian/aboot
        # then build the debian-installer with all packages
        cd /extra/deller/DEBIAN_INSTALLER/debian-installer/installer
        export ONLINE=n
        dpkg-buildpackage

Add boot loader installer and partitioning tools packages to the repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The architecture-specific packages (palo-installer, silo-installer, ...)
were built above. Install them into your local reprepro archive
directory::

    cd /extra/deller/debian-alpha-archive/
    reprepro includeudeb unstable \
        /extra/deller/DEBIAN_INSTALLER/debian-installer/installer/build/apt.udeb/cache/archives/*udeb

Build your platform boot loader
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Build the boot loader for your platform (palo, silo, ...) and install
the deb package as done above (use includedeb instead of includeudeb)::

    cd /extra/deller/debian-alpha-archive/
    reprepro includedeb unstable

Set up debian-cd
~~~~~~~~~~~~~~~~

debian-cd will build the installer images. Download it, configure it and
let it build the image. You will need to download
:download:`Debian-cd.patch.txt <media/Debian-cd.patch.txt>` first.

::

    cd /extra/deller/DEBIAN_INSTALLER
    git clone https://alioth.debian.org/anonscm/git/debian-cd/debian-cd.git

    # patch debian-cd
    cd debian-cd
    # curl or wget the Debian-cd.patch.txt file
    patch -p1 -s < Debian-cd.patch.txt

    # after patching check changes with "git diff" and modify as needed
    # adjust the kernel options (KERNEL_PARAMS in CONF.sh)
    # modify DI_DIR in easy-build.sh to point to the cdrom directory
    # (instead of netboot dir)

Build the final iso image
~~~~~~~~~~~~~~~~~~~~~~~~~

::

    cd /extra/deller/DEBIAN_INSTALLER/debian-cd

    ./easy-build.sh NETINST $HOSTTYPE
    ./easy-build.sh CD $HOSTTYPE

External HOWTOs
~~~~~~~~~~~~~~~

https://wiki.debian.org/PortsDocs/CreateDebianInstallerImages

Other prebuilt files for parisc:

- http://parisc.osuosl.org/debian/palo-installer_0.0.15_hppa.udeb
- http://parisc.osuosl.org/debian/partman-palo_20_hppa.udeb
