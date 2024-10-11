Discontiguous Memory Support
============================

Several PA-RISC machines have large memory holes in their memory maps.
e.g. Astro-based machines, the N-class, and the new zx1-based PA8800
machines.

We have these possible memory map layouts::

     * Astro: 0-3.75, 67.75-68, 4-64
     * zx1: 0-1, 257-260, 4-256
     * Stretch (N-class): 0-2, 4-32, 34-xxx

Normally Linux uses a single contiguous memory map to address all the
physical memory in a machine. In order to support discontiguous memory,
several memory maps representing each contiguous segment of memory are
created. Each of these segments is called a "node". From the above
memory maps, we can see that each 1GB can only belong to one region
(node), so we can create an index table for pfn to nid lookup.

`Discussing <http://lists.parisc-linux.org/pipermail/parisc-linux/2003-October/021216.html>`__
PA-RISC hardware implementations and issues around N-class machines,
MatthewWilcox also explained:

    A500/L1000/L2000 use Astro/Elroy just like the B/C/J class.
    L1500/L3000/N use Ike and Stretch in place of Astro. I once
    downloaded an N-class PDF which I've subsequently lost. If I
    remember correctly, it looked like
    ::

             CPU --+-- CPU          RAM          CPU --+-- CPU
                  DEW              |||||              DEW
          +--------+--------+---- Stretch ----+--------+------+
         IKE               DEW               DEW             IKE
        |||||         CPU --+-- CPU     CPU --+-- CPU       |||||
        Ropes                                               Ropes
     

    (Elroys on the end of the ropes, of course)

    My understanding is that Stretch is the problem. We don't follow the
    rules for non-coherent aliases and Stretch isn't as lenient as other
    memory controllers.
