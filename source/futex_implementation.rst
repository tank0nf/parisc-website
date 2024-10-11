The Implementation of Futexes on PA-RISC
========================================

Original author: James Bottomley

Introduction
------------

A futex is a fast user mutex, first described by Franke et al. in [1].
The idea is to optimise the uncontested mutex case so that it can be
done entirely at user level, thus dispensing with a kernel context
switch.

Futex Implementations
---------------------

The classic futex implementation described in [1] and subsequently honed
for glibc in [2] calls for the use of two atomic operations, to be
provided by the CPU, in the user level implementation of futexes:
Compare and exchange and atomic increment. Unfortunately, PA-RISC
possesses only a single atomic operation: Load and Clear Word (ldcw)
which cannot be used to substitute for either required operation. The
object of this paper is to explore whether futexes can be implemented on
the PA-RISC architecture with only the provided ldcw primitive.

Potential PA-RISC implementations
---------------------------------

The final stage futex described in "Mutex, Take 3" of [2] describes a
three state object alone. Since ldcw is a binary operation (the atomic
states being either clear, or not clear), it is worth while exploring
whether the futex can be implemented with \*two\* ldcw variables.

In the following implementation, val0 represents the lock state (1 ==
unlocked, 0 == locked) and val1 represents the waiters (1 == no waiters,
0 == one or more waiters). A summary of the states of the values is::

    val0    val1
    1   1   Unlocked
    0   1   Locked, No waiters
    0   0   Locked with waiters,
    1   0   Transitional intermediate state in unlock().
     

Thus, we propose the implementation of mutex3 as being:

.. code-block:: cpp

    class mutex {
    private:
        int val0;
        int val1;
    public:
        mutex() : val0(1), val1(1) {
        }
    
        void lock() {
            while (!ldcw(&val0) {
                /* lock not acquired; wait; if we're the first
                 * waiter, just retry the lock again */
                if (!ldcw(&val1)) {
                    futex_wait(&val0, &val1, 0, 0)
                    /* we don't know how many waiters
                     * there actually were, so must wake
                     * when we exit */
                    val1 = 0;
                }
            }
            /* lock acquired */
        }
        void unlock() {
            val0 = 1;
            /* here futex_wait with 0,0 would be disallowed, so
             * any failure of futex_wait because of this will
             * acquire the lock.  Val1 must be clear if we have
             * any sleepers. It is possible that the lock could already
             * be acquired here with waiters, but in that case we
             * simpley do a spurious wake. */
            if (!val1) {
                val1 = 1;
                /* in the final case, there will be no-one to 
                 * wake and we will proceed with val1 == 1,
                 * otherwise val1 will be reset to zero by the
                 * awoken process */
                futex_wake(&val0, &val1, 1)
            }
        }
    }
     

It should be noted that the above implementation requires kernel level
changes to sys_futex: as noted in [1] and [2] for FUTEX_WAIT and
FUTEX_WAKE, the second argument is ignored. For parisc we require that
the second argument form part of the comparison. For backwards
compatibility, the second argument would still be ignored, but only if
it were NULL, which should allow all the non-parisc implementations to
function as they did before.

Once the above changes are made, the algorithm is provably secure, since
the locking process will \*only\* be allowed to sleep if both val0 and
val1 are zero, which signifies that a wake will be done. The seting of
val0 to one before the check of val1 ensures this. The semantics are
preserved by the fact that the lock may \*only\* clear val1 and the
unlock may only set it if it is also going to do a wake.

The price of all this is that in the contested case, we do one more
syscall for wakeup than is actually necessary. However, this is a
reasonable price to pay for a syscall free uncontended case which it is
the goal of the futex to optimise.

Conclusion
----------

Simply changing the kernel sys_futex implementation to respect the
second argument for FUTEX_WAIT and FUTEX_WAKE will be sufficient to
permit the simple (and for the most part, efficient) implementation of
futexes on PA-RISC.

References
----------

[1] Hubertus Franke, Rusty Russell and Matthew Kirkwood; Fuss, Futexes
and Furwocks: Fast User Level Locking in Linux; Proceedings of the
Ottawa Linux Symposium 2002, pp 479--491.
http://www.parisc-linux.org/~carlos/docs/ols2002_proceedings.pdf

[2] Ulrich Drepper; Futexes are Tricky;
http://people.redhat.com/drepper/futex.pdf 27 June 2004
