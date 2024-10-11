Notes on porting Mono
=====================

This document captures some experiences I had porting Mono to the HP
PA-RISC platform. It is meant to provide some more details about porting
Mono to a new platform.

Preparation
-----------

- Read the Mono Porting page http://www.mono-project.com/Porting. Read
  it again for good measure.

- Good platform instruction set reference, including binary encoding

- Platform ABI definition - mono needs to synthesize calls to both
  managed and unmanaged routines. All (?) of the existing ports use a
  unified calling convention for both cases. This is probably the
  easiest. Things that mono will need to know include:

  - What are the caller-save and callee-save registers

  - How are arguments passed to functions? On RISC architectures,
    usually the first arguments are passed in registers, and additional
    arguments are passed on the stack. Also, note how arguments smaller
    or larger than the register size are handled. For arguments smaller
    than the register size, is the argument passed left-aligned or right
    aligned? For arguments larger than the register size, are they
    passed on register pairs? Are they passed on the stack?

  - How are results returned from functions? For arguments larger than a
    register, are they returned on the stack or a caller allocated area?

  - If libffi has been ported to your platform, it is a good reference.
    It also has a good testsuite.

Getting Started
---------------

- Grab the sources from svn http://www.mono-project.com/AnonSVN. Make
  sure you have all the build-dependencies installed. To get started,
  you will need at least:

  - automake, autoconf, libtool
  - glib 2.0
  - bison
  - zlib

- Edit configure.in and add/edit a section for your host/target. For
  example, for hppa-linux, I have
  ::

    hppa*linux*)
            TARGET=HPPA;
            AC_DEFINE(MONO_ARCH_REGPARMS,1,[Architecture uses registers for Parameters])
            arch_target=hppa;
            ACCESS_UNALIGNED="no"
            JIT_SUPPORTED=yes
            jit_wanted=true

  configure.in also contains a platform conditional flag that may be
  useful in other makefiles. Look for the definition of AM_CONDITIONAL
  in the configure file and edit accordingly.

- Run autogen.sh

- Go to the mono/arch directory. Create a subdirectory for your
  platform. (e.g. hppa).

  - Create a file named -codegen.h. This file will contain inline
    functions or macros to emit code for the JIT. For now, create a file
    with an enum of registers in your architecture. For example, for
    hppa, we have "HPPAIntRegister" and "HPPAFloatRegister". The order
    of the register in the enum should correspond to how the register
    gets encoded in the instruction set.

  - Create a Makefile.am that contains something like the following.
    Note that existing platforms may have a tramp.c that was used for
    the now deprecated mono interpreter. This is no longer required::

        INCLUDES = $(GLIB_CFLAGS) -I$(top_srcdir)
        noinst_LTLIBRARIES = libmonoarch-hppa.la
        libmonoarch_hppa_la_SOURCES = hppa-codegen.h

- Go to the mono/mini directory. Create the following files. For now
  they can be empty.
