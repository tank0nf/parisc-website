================
Kernel Profiling
================

Using readprofile
-----------------

- Compile your kernel with ``CONFIG_PROFILING=y``
- boot your kernel with profile=2 on the palo command line
- as root:

  - ``readprofile -r`` # clears the profile counters
  - run your test
  - ``readprofile -m /path/to/System.map -d /path/to/vmlinux > /tmp/profile.txt``

- you might want to sort the results using "sort -nr +2"

Using oprofile
--------------

- Compile your kernel with ``CONFIG_OPROFILE=y`` (or as a module)
- (to be written)
