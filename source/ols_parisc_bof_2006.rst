OLS PARISC BOF 2006
===================

BOF Topics
----------

#. PA8800
#. NPTL Debugging
#. State of the kernel
#. tmpalias flushing
#. Git
#. H/W Support
#. 64-bit Userspace
#. Debian Etch

PA8800
~~~~~~

- Random insn run.
- 2 sockets HPMC (L2 Error?)
- Logging TLB inserts?
- sshd and telnetd are repeatable triggers
- Make and Bash will sometimes segfault
- Force prefetches?
- Disable L2 (Grant)

NPTL Debugging
~~~~~~~~~~~~~~

- More debugging required
- Mutex, lowlevellock, and futex should be reviewed

State of the Kernel
~~~~~~~~~~~~~~~~~~~

- Good!
- Tulip?
- USB?
- Missing futex routines?
- pselect / ppoll!
- gen irq!!
- Kernel headers
- Header installs
- Soft lockups gcc 3.4 vs gcc?
- RW locks broken? RW lock testsuite?
- Signals bug?
- process stuck in read()?
- mremap fails?

tmplalias flushing
~~~~~~~~~~~~~~~~~~

No comments.

GIT
~~~

- Shutdown CVS
- Migrate to?
- Where do we put userspace/ web/ linux-2.6/ build-tools/?

H/W Support
~~~~~~~~~~~

Some people poke fun at other people with really old hardware.

64-bit Userspace
~~~~~~~~~~~~~~~~

Some people poke fun at Carlos.

Debian Etch
~~~~~~~~~~~

Raise the SEP field!
