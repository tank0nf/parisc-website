Virtual Memory
==============

If you don't feel very comfortable with the Linux Virtual Memory
Management, you might want to take a look here:
http://www.informit.com/articles/article.asp?p=336868 This article
explain the general concepts underlying the way Linux deals with Virtual
Memory (VM).

PA-RISC VIPT caches
-------------------

See this article for a good overview of the various caching
architectures: https://www.linuxjournal.com/article/7105

PA-RISC equivalent and non-equivalent aliasing issues
-----------------------------------------------------

Jerry Huck <huck@cup.hp.com> provided information about equivalent and
non-equivalent aliasing issues on PA-RISC. The full email is here:
https://lore.kernel.org/all/199912161642.IAA11478@lucy.cup.hp.com/

::

   From: Jerry Huck <huck@cup.hp.com>
   To: parisc-linux@thepuffingroup.com
   Subject: [parisc-linux] Comments on non-equivalent aliasing and PA-RISC
   Date: Thu, 16 Dec 1999 08:42:01 -0800 (PST)
   Message-ID: <199912161642.IAA11478@lucy.cup.hp.com>

   I would like to comment on the discussion related to equivalent and
   non-equivalent aliasing issues on PA-RISC.

   In summary, I think the 2.0 and 1.1e3 architecture book is overly
   restrictive on aliasing between physical and virtual addresses.  We
   are investigating prior designs to ensure that we can restate the
   rules to allow transitivity in the equivalent aliasing rules.  We hope
   to post updated documentation and a collection of errata to the PA
   RISC 2.0 manual in the January timeframe.  (as an aside, I do like the
   model where kernel addresses are the same for virtual or physical
   accesses; it does get much easier in PA2.0.)

   The remainder of this note describes some of the history of PA-RISC on
   how we got where we are.  People not interested in virtual memory
   aliasing architecture can skip the following.

   I've been involved in the PA-RISC architecture development process
   since 1983.  The virtual memory model was heavily influenced by the
   single-level store work by IBM (in System 3x).  But, that influence
   was heavily tempered by hardware designers trying to squeeze it into
   very modest LSI.  The big dilemma was the HW interest in having big
   virtual-indexed caches to avoid putting the TLB lookup in the critical
   path.  There are ways to have big caches and full aliasing support
   but it does take effort and reduces performance.

   PA-RISC defines a virtual memory model based on global virtual
   addresses (GVA).  A virtual address is first transformed into a global
   virtual address (via a simple space register lookup and concatenation
   for PA1.x) and that address is used to lookup in the TLB.  This allows
   a single page table to hold translations for all processes.  A
   different mechanism is used to provide protection (protection IDs).  A
   specialization of this approach is address space IDs used in some
   other RISC architectures.  This augments the per-process address space
   to avoid TLB purging on context switch.

   When data is not shared between processes, then everything is simple.
   Sharing on traditional page-table per process architectures is done via
   aliasing.  Sharing on PA-RISC is done by using the same GVA.

   Single address space models didn't normally require aliasing.  A
   process was always given a global address to the data.  Protection is
   done using the Protection IDs.  This works very well when you can
   control the system call semantics.  Sharing is easy and the tough
   things (like very different access rights to the same VA range) are
   just outlawed.  Unix process semantics that suggested aliasing (like
   fork) could be easily implemented using shared global addresses.  The
   text segment is directly shared by using the same space register ID.
   Data segment sharing is done via copy-on-access instead of
   copy-on-write.  Sharing is done with SR6 and SR7 being common between
   all processes.

   The other nice aspect of single address space models is the sharing of
   TLB entries.  Sharing is done by using the same global virtual address
   - hence it's covered by the same TLB entry.  The OS can keep a single
   data structure for that object and just record the processes that
   attach to it.  For example, there is a single text segment for all the
   "vi" processes.  They all share the same page table and TLB entries for
   that segment.

   Single address spaces are not without problems.  The biggest in
   PA-RISC was the 1G limit for each of the quadrants.  An aliased model
   allows a flexible boundary between stack, heap, text, shared data,
   etc.  We had to make special hacks to get around the problems - some
   that encouraged some limited aliasing.  IBM's RS6000 has a little bit
   of the same issue but had 16 space-like registers (upper 4-bits of
   each 32-bit offset).  They could more easily adjust boundaries to
   allow flexible sizing of process address space.  As many people have
   said in the past, "this is not a problem for the 2.0 architecture
   since a 62-bit offset is more than enough for the future - or at
   least until I retire".

   Our second problem with single address spaces that we didn't fix
   until PA2.0, was good support for instruction stream space crossing.
   The Apollo folks tried to get better shared library support in 1.1
   ('89ish) but the design (PA7000) was too far along and we just did the
   FP part of their proposal.  Also, I didn't have a good handle on
   shared library design to support the proposal.

   A final general problem is the ability to incorporate other designs
   into our "different" environment.  For example, a 3rd party file
   system might be designed to coordinate between mapped files and the
   buffer pool using aliasing.  While it is not hard to manage coherence
   using GVAs, it will involve a lot of rework to use.

   For this discussion, I'm ignoring aliasing support where all aliased
   translations are ping-ponged between the different aliases via
   protection faults.  We can handle any kind of alias if you're willing to
   take the time to remap the page.  Some minimization of the ping-ponging
   must be considered.

   So the rest of the note is a little chronology of the how the aliasing
   architecture evolved to the current definition.

   The first specs completely outlawed all aliasing.  It was/is expected
   that the OS flush the range whenever a virtual address (VA) needed to
   be changed.  An early change was made to allow PA=VA aliasing in '84.  The
   OS couldn't begin to manage the page tables if that aliasing wasn't
   allowed.

   The first 1.1 book (11/90) defined the first virtual aliasing model -
   limited space aliasing.  It allows space aliasing if certain bits
   match between the addresses.  For PCX-S, this means you have just 4
   bits that can be used as an alias. For example, address
   0x1234.00000000 (space register contents = 0x1234, offset = 00000000)
   can be aliased to address 0x2234.00000000.  This change was encouraged
   by some of the Apollo engineers that wanted to enable some amount of
   aliasing to help with Domain needs (they wanted more).  Several of the
   machines used the low-order space bits as part of the cache-index
   computation.  So two addresses like 0x1.00000000 and 0x2.0000000 would
   definitely NOT be in the same spot in the cache.

   This wasn't enough, by the last 1.1 book (1.1e3 published 2/94) we
   added 1MByte offset aliasing (page 3-6).  We also included a PDC call
   to disable space hashing on the newer machines.  Once disabled, SW
   could then alias any 2 virtual addresses provided the low 20-bits were
   equal.  HP-UX never used this feature since it cut performance in high
   multi-programmed environments (ex. TPC-A at the time).

   We also introduced "non-equivalent" aliasing in the 1.1e3 book.  It
   allows aliasing down to the 4k boundary if some very special rules
   were followed.  In all the old designs, read-only aliasing did happen
   to work, but the PA7200 had a little wrinkle that would HPMC if you didn't
   carefully transition a page from read-only to read-write.

   The 2.0 architecture extended the architecture to support 64-bit
   offsets.  Space registers were extended to 64-bits in width (although
   today's PA8xxx processors only implement 32-bits).  Aliasing rules
   were changed in a small way (2.0 page F-6).  First, the space bits
   that could be used in cache hashing were moved from 3 different places
   to a continuous group above the low 48-bits of the GVA.  The PDC call
   to disable space hashing remains.

   More recently, we changed the aliasing boundary to be a range from
   4K-16M that the machine communicates through PDC_CACHE.D_conf.alias.
   Machines either return 0 which means "can't count on offset
   aliasing" or the offset aliasing boundary.

   One additional comment, a couple of recent designs do not fully meet
   the read-only non-equivalent aliasing rules.  We're having some
   internal discussion on how to best document the architecture.  If you
   don't absolutely need the non-equivalent aliasing, avoid it or send me
   mail to figure out a solution.

   So, what does this mean to the PA-RISC Linux port.  I would try to
   think about a 2 level approach.  The first level is a "use the global
   address space if it's easy".  This would mimic the current simple HP-UX
   address space layout.  If the process uses < 1Gbyte for text, data,
   and shared structures (SR4, SR5, and SR6 respectively), then great.
   Once a process needs resources or sharing that isn't easily
   accommodated, then switch to an "all or nearly all alias" model.
   In the alias model, encourage aliases that don't require flushing,
   otherwise ping-pong the translations as needed.  If you use a
   page-table translation SW cache in front of the real page tables,
   you can use the hardware walker, avoid lots of virtual mode references
   in TLB miss handler, and manage these aliases in one spot.  No doubt
   some coordination problems will exist.  Just some thoughts.

   Hope this helps.  As an additional FYI, we are preparing a set of
   errata pages to augment the 2.0 Kane book and will post them to the web
   once we complete them.  Included will be clarifications on this
   non-equivalent aliasing issue.

   Jerry Huck (jerry_huck@hp.com)
   PA-RISC and IA-64 Architecture
   Hewlett-Packard

Page Tables
-----------

Currently, only 4k pages are supported.

PA-RISC Linux uses different page table layouts for 32-bit vs 64-bit
kernels.

On 32-bit, the page table has 2 levels. We use 9 bits to index the Page
Table Entry (PTE), 0 bits for the Page Middle Directory (PMD), and 11
bits to index the Page Global Directory (PGD).

On 64-bit, the page table has 3 levels. We use 9 bits to index the PTE,
11 bits to index the PMD, and 11 bits to index the PGD.

A hybrid approach is used to optimize page table lookups for processes
that address <4GB of memory -- the PGD is allocated together with the
first PMD for the process. The PGD/PMDs are sized so that if the Virtual
Address (VA) is <4GB, the PMD can be located by doing an offset-load
from the PGD, instead of an extra level of pointer dereference.

An additional trick is used to reduce the amount of memory required to
store the PMD/PTE pointers in the page table. This also has the
advantage of making the code paths for 32-bit and 64-bit kernels more
similar because they always use pointers of the same size -- PMD/PTE
pointers are always stored in a 32-bit pointer. We take advantage of the
fact that in a 64-bit PMD/PTE pointer, the lower 12 bits (offset) are
always zero. Normally these bits are used to store some page flags. In
the case of the PMD/PTE pointers, we do not need the full set of page
flags, so only 4 bits are reserved for flags. This means that we can
right-shift a PMD/PTE pointer by 8 bits before storing it into the
PGD/PMD. This allows us to address 40 bits (1TB) of physical space with
a 32-bit pointer.

VM Initialization
-----------------

:doc:`Device Inventory <_device_inventory>` during bootup creates a
physical memory map of the system. For each memory region, the starting
physical address and the extent are saved to ``pmem_ranges``.

If ``CONFIG_DISCONTIGMEM`` is not set, then only the first of these
memory regions will be initialized, and a linear ``mem_map`` is used.
Otherwise, if :doc:`Discontiguous Memory Support
<discontiguous_memory_support>` is enabled, multiple "nodes" are created
to represent each of the memory regions.

.. admonition:: todo

   Put something here about vmalloc space is allocated on parisc?

A gateway page is also initialized during VM initialization. The page is
not mapped into userspace, but instead resides in kernel space (sr2) at
address 0x0. During the initialization process the page is copied from
the kernel text address 'linux_gateway_page' into place at address 0x0.
All references in that gateway page must be relocatable and hence PIC in
some way. The page is used for raising the priority of a process during
kernel entry for syscalls, light-weight-syscalls, and setting the thread
register (NOTE: Technically setting the thread register should have been
a light-weight-syscall but it was fixed as part of the ABI before LWS
was available).

Page Fault Handling
-------------------

TODO

translation_exists()
--------------------

PA-RISC is a **VIPT** architecture, so that would ordinarily entail a
lot of cache flushing through process spaces for shared pages. However,
we use an optimisation of making all user space shared pages congruent,
so flushing a single one makes the cache coherent for all the others
(this is also a cache usage optimisation).

So, what our ``flush_dcache_page()`` does is it selects the first user
page it comes across to flush knowing that flushing this is sufficient
to flush all the others.

Unfortunately, there's a catch: the page we're flushing must have been
mapped into the user process (not guaranteed even if the area is in the
vma list) otherwise the flush has no effect (a VIPT cache flush must
know the translation of the page it's flushing), so we have to check the
validity of the translation before doing the flush.

On parisc, if we try to flush a page without a translation, it's picked
up by our software *tlb miss handlers*, which actually nullify the
instruction (but since we have to flush a page as a set of non
interlocking cache line flushes [about 128 of them per page with a cache
width of 32]) and the tlb handler is invoked for every flush instruction
(because the translation continues not to exist) it makes that flush
operation extremely slow. (128 interruptions of the execution stream per
flush)

So, the uses of ``translation_exists()`` are threefold

#. Make sure we execute ``flush_dcache_page()`` correctly (rather than
   executing a flush that has no effect)

#. Optimise single page flushing: don't excite the tlb miss handlers if
   there's no translation

#. Optimise pte lookup (that's why ``translation_exists()`` returns the
   pte pointer); since we already have to walk the page tables to answer
   the question, the return value may as well be the pte entry or
   ``NULL`` rather than true or false.

