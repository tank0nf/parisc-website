PA-RISC Linux Register Conventions
==================================

A file in the kernel tree describes the :doc:`Registers <registers>`
specified by the ABI.

A stack frame for a function in the 32-bit runtime looks like this::

       Offset
            [ Variable args ]
       SP = (4*(n+9))       arg word N
       ...
       SP-52                arg word 4
            [ Fixed args ]
       SP-48                arg word 3
       SP-44                arg word 2
       SP-40                arg word 1
       SP-36                arg word 0
            [ Frame marker ]
       ...
       SP-20                RP
       SP-4                 previous SP

- First 4 non-FP 32-bit args are passed in ``gr26``, ``gr25``, ``gr24``
  and ``gr23``

- First 2 non-FP 64-bit args are passed in register pairs, starting on
  an even numbered register (i.e. ``r26/r25`` and ``r24+r23``)

- First 4 FP 32-bit arguments are passed in ``fr4L``, ``fr5L``, ``fr6L``
  and ``fr7L``

- First 2 FP 64-bit arguments are passed in ``fr5`` and ``fr7``

- The rest are passed on the stack starting at ``SP-52``, but 64-bit
  arguments need to be aligned to an 8-byte boundary
