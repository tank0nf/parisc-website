==========
Test Cases
==========

Kernel Testcases
================

Math test case
--------------

should return 0.0: (hppa floating point error)

.. code-block:: cpp

    #include <stdio.h>
    #include <math.h>
    int
    main (void) {
     double result = exp (-4.3682654441477153e+19);
     printf ("%g\n", result);
     if (result != 0.0)
      return 1;
     return 0;
    }

Futex wait failure
------------------

No testcase.

Threads and fork on VIPT-WB machines
------------------------------------

- Affects `#561203 <http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=561203>`__.
- Discussed on `this thread <http://thread.gmane.org/gmane.linux.ports.parisc/2503>`__ and `this thread <http://thread.gmane.org/gmane.linux.ports.parisc/2751>`__

Summary from `JDA <http://article.gmane.org/gmane.linux.ports.parisc/2823>`__:

    *The minifail bug is a "Threads and fork" problem arising from cache
    corruption. Mainly, copy_user_page is broken when copying memory
    shared by more than one process. There are also issues in PTE/TLB
    management on SMP systems. Probably, the vfork/execve bug is caused
    by the same problem.*

Initial patch `syscall.S.d.1 <http://marc.info/?l=linux-parisc&m=126202676424518&q=p3>`__ from `JDA <http://article.gmane.org/gmane.linux.ports.parisc/2524>`__

First testcase `minifail.cpp <http://bugs.debian.org/cgi-bin/bugreport.cgi?msg=25;filename=minifail.cpp;att=1;bug=561203>`__

Build with::

    g++ -I/usr/include/qt4 -lQtCore minifail.cpp -o minifail -O0 -g

Fails occasionally with::

    $ i=0; while true; do i=$(($i+1)); echo Run $i; ./minifail; done;
    $ i=0; while true; do i=$(($i+1)); echo Run $i; ./minifail qt; done;

Typical observed failure::

    Run 21
    Segmentation fault
    Run 22
    Child OK.
    Thread OK.
    Run 23
    Thread OK.
    Segmentation fault


- Reduced `minifail6.cpp <http://marc.info/?l=linux-parisc&m=126503924510791&q=p4>`__, from `this post <http://article.gmane.org/gmane.linux.ports.parisc/2606>`__
- Tentative `patch <http://marc.info/?l=linux-parisc&m=126514540817084&q=p3>`__], see this `post <http://article.gmane.org/gmane.linux.ports.parisc/2615>`__
- Other version `minifail3.c <http://marc.info/?l=linux-parisc&m=126523464015510&q=p3>`__ from `Helge Deller <http://article.gmane.org/gmane.linux.ports.parisc/2618>`__
- Other version `1 <http://marc.info/?l=linux-parisc&m=126835038716389&q=p3%7Cminifail9.cpp>`__ from `JDA <http://article.gmane.org/gmane.linux.ports.parisc/2685>`__
- Other version `minifail12.cpp <http://marc.info/?l=linux-parisc&m=126919558329853&q=p3>`__ from `JDA <http://article.gmane.org/gmane.linux.ports.parisc/2693>`__
- **Final** (?) version `minifail_dave.cpp <http://marc.info/?l=linux-parisc&m=127275273129566&q=p3>`__ from `Helge Deller <http://article.gmane.org/gmane.linux.ports.parisc/2824>`__

Other testcase from `JDA <http://article.gmane.org/gmane.linux.ports.parisc/2774>`__:

Compile with ``-static`` to link with libc.a. Testcase prints incorrect
parent pid.:

.. code-block:: cpp

    #!cplusplus
    #include <stdio.h>
    #include <stdlib.h>
    #include <errno.h>
    #include <sys/types.h>
    #include <unistd.h>

    #define CALL_EXIT 0

    int main (void)
    {
      pid_t child;
      pid_t parent;
      char *cmd[] = { "bash", "-c", "echo In child $$;", (char *)0 };
      char *env[] = { "HOME=/tmp", (char *)0 };
      int ret;

      child = vfork();

      if (child == 0)
        {
          ret = execve("/bin/bash", cmd, env);
          // printf ("ret = %d\n", ret);
          _exit(1);
        }
      else
        {
          // printf("child != 0\n");
        }

      parent = getpid();
      printf("parent is %d\n", (unsigned int)parent);
      printf("child is %d\n", (unsigned int)child);

      return 0;
    }

Patches
~~~~~~~

- `parisc_lock_v2.patch <https://patchwork.kernel.org/patch/76829/>`__ from Helge Deller - Not Applicable (not-upstream)

- `entry.S.patch <https://patchwork.kernel.org/patch/85865/>`__ from JDA (not-upstream)

- `patch1 <https://patchwork.kernel.org/patch/90467/>`__ from JDA - Superseded by patch2 (not-upstream)

- `patch2 <https://patchwork.kernel.org/patch/90596/>`__ from JDA - Included in patch3 (not-upstream)

- `bundle patch3 <https://patchwork.kernel.org/patch/91525/>`__ from JDA - Partially split into

  - `Call pagefault_disable/pagefault_enable in kmap_atomic/kunmap_atomic <https://patchwork.kernel.org/patch/91916/>`__ (on-buildds)

  - `Remove unnecessary macros from entry.S <https://patchwork.kernel.org/patch/91918/>`__ (on-buildds)

  - `Delete unnecessary nop's in entry.S <https://patchwork.kernel.org/patch/91919/>`__ (on-buildds)

  - `Avoid interruption in critical region in entry.S <https://patchwork.kernel.org/patch/91922/>`__ (on-buildds)

  - `LWS fixes for syscall.S <https://patchwork.kernel.org/patch/91924/>`__ (on-buildds)

  - **Note:** some bits from patch3 have not be separately submitted (futex.h, etc) - Needs review

- `pgtable.h patch update <https://patchwork.kernel.org/patch/91933/>`__, initially found in patch3 from JDA (not-upstream)

- `bundle patch4 <https://patchwork.kernel.org/patch/93520/>`__ aka ``pte.2.d`` from JDA, updating parts of patch3 (not-upstream)

- `patch <https://patchwork.kernel.org/patch/95969/>`__] from James Bottomley for kmap issues fixing **minifail6.cpp** (not-upstream)

- `bundle patch5 <https://patchwork.kernel.org/patch/97971/>`__ from JDA with a slightly modified version of James' patch (not-upstream)

- `bundle patch6 <https://patchwork.kernel.org/patch/99861/>`__ from JDA, with apparently good results both on pa8800 and previous CPUs (not-upstream)

- `bundle patch7 <https://patchwork.kernel.org/patch/101741/>`__ from JDA, with reworked pacache.s and cache.c (not-upstream)

vfork/execve
------------

- Affects `#558905 <http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=558905>`__

- Discussed by Carlos O'Donell in `this thread
  <http://thread.gmane.org/gmane.linux.ports.parisc/2403>`__:

    *I have constructed a vfork test case which shows some of the
    problems I have using vfork reliably. This fails every time on my
    PA8700 system running 2.6.32-rc6. It appears as though r28 (ret0) in
    the parent is being corrupted.*

The intent of the testcase is to do the following:

#. vfork
#. Launch "ls -l" in the vfork'd child.
#. Print some information in the parent.

.. code-block:: cpp

    /* vfork.c */
    #include <stdio.h>
    #include <stdlib.h>
    #include <errno.h>

    int main (void)
    {
      pid_t child;
      char *cmd[] = { "ls", "-l", (char *)0 };
      char *env[] = { "HOME=/tmp", (char *)0 };

      child = vfork();

      if (child == 0)
        {
          execve("/bin/ls", cmd, env);
        }
      else
        {
          printf("child != 0\n");
        }

      printf("child is 0x%x\n", (unsigned int)child);

      return 0;
    }

Compile this test case twice:

#. ``gcc -O1 -g -o vfork-O1 vfork.c``
#. ``gcc -O0 -g -o vfork-O0 vfork.c``

The return from vfork is corrupted in the parent. This gets worse at
``-O0``.

To remove the C library from the loop I attach a complete vfork
implementation as used by glibc. `pt-vfork.s
<http://marc.info/?l=linux-parisc&m=126013436326095&q=p3>`__

You can compile the test case using: ``cc -O1 -g -o vfork-O1 vfork.c
pt-vfork.s``

In summary:

- Test case works on x86.
- Test case fails on hppa.
- Test case works on hppa under strace.

More discussion by Carlos O'Donell in `this thread
<http://thread.gmane.org/gmane.linux.ports.parisc/2725>`__

- Other testcase `vforktest.tgz <http://marc.info/?l=linux-parisc&m=126979720816005&q=p3>`__ by Carlos O'Donell

- Updated (?) testcase `vforktest.tgz <http://marc.info/?l=linux-parisc&m=126980206121937&q=p3>`__ by Carlos O'Donell

Patches
~~~~~~~

- `Patch <https://patchwork.kernel.org/patch/90144/>`__ from JDA (not-upstream)

- `Patch <https://patchwork.kernel.org/patch/90018/>`__ from Carlos O'Donell - Comments/cleanup (on-buildds)

floating point SIGFPE not trapped
---------------------------------

- Affects `#559406 <http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=559406>`__

- Testcase `fputest.c <http://bugs.debian.org/cgi-bin/bugreport.cgi?msg=33;filename=fputest.c;att=1;bug=559406>`__

Patches
~~~~~~~

- `Patch <https://patchwork.kernel.org/patch/96558/>`__ from Helge Deller (in-debian, on-buildds)

GCC TestCases
=============

MMAP
----

- Affects `PR40505 <http://gcc.gnu.org/bugzilla/show_bug.cgi?id=40505>`__.

- Discussed by Carlos O'Donell on `this thread <http://thread.gmane.org/gmane.linux.debian.devel.release/30830/focus=31039>`__.

- Testcase `test-mmap.c <http://marc.info/?l=linux-parisc&m=124689818116647&q=p3>`__ from Carlos O'Donell

GLIBC TestCases
===============

Segmentation fault in \__libc_start_main with -static
-----------------------------------------------------

Discussed in `this thread <http://thread.gmane.org/gmane.linux.ports.parisc/2585>`__

Testcase from `JDA <http://marc.info/?l=linux-parisc&m=126477688209053>`__: Compile with ``g++ -o xx -static -pthread xx.C``

.. code-block:: cpp

    // This test only applies to glibc (NPTL) targets.
    // { dg-do run { target *-*-linux* } }
    // { dg-options "-pthread" }

    #include <pthread.h>
    #include <cxxabi.h>
    extern "C" int printf (const char *, ...);

    int main()
    {
      try
        {
          pthread_exit (0);
        }
      catch (abi::__forced_unwind &)
        {
          printf ("caught forced unwind\n");
          throw;
        }
      catch (...)
        {
          printf ("caught ...\n");
          return 1;
        }
    }

