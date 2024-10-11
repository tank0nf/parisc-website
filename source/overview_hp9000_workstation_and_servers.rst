Information on HP9000 Servers and Workstations
==============================================

Updated on July 2, 1997

SERIES 700 WORKSTATIONS
-----------------------

.. note::

   Information taken from current and past configuration/ordering
   guides.

::

                            CPU    --BUILT-IN SCSI--    MAX I/O SLOTS    Last OS
   MODEL/CLK   PROJECT      TYPE  SE/SCSI-CLK FWD/TYPE  EISA, GSC, PCI   Support
   ----------  -----------  ----  --------------------  --------------   -------
   705/35      Flounder     PCXS   700/35.0000  NA      0 Slots           10.20
   710/50      Bushmaster   PCXS   700/50.0000  NA      0 Slots           10.30
   712/60      Gecko        PCXL   710/40.0000  NA      0 Slots           11.X
   712/80      King Gecko   PCXL   710/40.0000  NA      0 Slots           11.X
   712/100     King Gecko   PCXL   710/40.0000  NA      0 Slots           11.X
   715/33      Scorpio Jr.  PCXT   700/33.3335  NA      1 E               10.30
   715/50      Scorpio      PCXT   700/50.0000  NA      1 E               10.30
   715/75      Scorpio Sr.  PCXT   700/37.5000  NA      1 E               10.30
   715/64      Mirage Jr.   PCXL   710/40.0000  NA      1 E (Only SE)     11.X
   715/80/D    Mirage       PCXL   710/40.0000  NA      1 E (Only SE)     11.X
   715/100/E   Mirage Sr.   PCXL   710/40.0000  NA      1 E (Only SE)     11.X
   715/100/XC  Turnip(1MB)  PCXL   710/40.0000  NA      1 E, 1 GSC        11.X 
   720/50      Cobra        PCXS   700/50.0000  NA      1 E               10.20
   725/50      Spectra      PCXT   700/50.0000  NA      4 E               10.20
   725/75      Spectra      PCXT   700/37.5000  NA      4 E               10.20
   725/100/C   Electra      PCXL   710/40.0000  720/Z   3 E, 1 GSC        11.X
   730/66      King Cobra   PCXS   700/33.????  NA      1 E               10.20
   735/99      Hardball     PCXT   700/33.0000  720/O   1 E               10.20
   735/125/B   Hardball     PCXT   700/31.2500  720/O   1 E               10.20
   750/66      Coral        PCXS   700/33.????  NA      4 E               10.20
   755/99      Coral II     PCXT   700/33.0000  720/O   4 E               10.20
   755/125     Coral II     PCXT   700/31.2500  720/O   4 E               10.20
   770/J200    Skyhawk      PCXT'  710/40.0000  720/Z   4 E(1), 3 GSC+    11.X
   770/J210    Skyhawk      PCXT'  710/40.0000  720/Z   4 E(1), 3 GSC+    11.X
   770/J210XC  Light Hawk   PCXT'  710/40.0000  720/Z   4 E(1), 3 GSC+    11.X
   777/C100    Raven T      PCXT'  710/40.0000  720/Z   (1),4 GSC         11.X
   777/C110    Raven T      PCXT'  710/40.0000  720/Z   (1),4 GSC         11.X
   778/B132L   Merlin L2    PCXL2  710/40.0000  Opt.(3) (1),1 GSC,1 PCI   11.X
   778/B160L   Merlin L2    PCXL2  710/40.0000  Opt.(3) (1),1 GSC,1 PCI   11.X
   778/B180L   Merlin L2    PCXL2  710/40.0000  Opt.(3) (1),1 GSC,1 PCI   11.X
   779/C132L   Raven L2     PCXL2  710/40.0000  Opt.    (1),2 GSC,2 PCI   11.X
   779/C160L   Raven L2     PCXL2  710/40.0000  Opt.    (1),2 GSC,2 PCI   11.X
   779/C180L   Raven L2     PCXL2  710/40.0000  Opt.    (1),2 GSC,2 PCI   11.X
   780/C160    Raven U      PCXU   710/40.0000  720/Z   (1),2 GSC,2 PCI   11.X
   780/C180    Raven U      PCXU   710/40.0000  720/Z   (1),2 GSC,2 PCI   11.X
   780/J280    FireHawk     PCXU   710/40.0000  720/Z   (1),3 GSC         11.X
   780/J282    FireHawk     PCXU   710/40.0000  720/Z   (1),3 GSC         11.X
   782/C200+   Raven U+     PCXU+  710/40.0000  875/Z   (1),2 GSC,2 PCI   11.X
   782/C240+   Raven U+     PCXU+  710/40.0000  875/Z   (1),2 GSC,2 PCI   11.X
   782/J2240   FireHawk+    PCXU+  710/40.0000  895/Z   (1),2 GSC,2 PCI   11.X

   NOTES: 1. The B, C, and J class workstations do NOT support the EISA-SCSI 
   &#9;  Fast Differential interfaces.  The other models with EISA slots 
             support the EISA-SCSI/SE (A2679A) and EISA-SCSI/FD (25525B) cards.

          2. The HP-UX 10.30 and 11.00 releases only support the GSC-SCSI/FWD 
             add-on card (Product # A4107A) and the built-in SCSI interfaces
             for the S700 models per the "limitedS700support" FCR.

          3. The B class default wide SCSI is SE875 built-in.
             Optional differential is Zalon/720 built-in.

VME INDUSTRIAL WORKSTATIONS
---------------------------

::

                                   CPU     BUILT-IN   MAX I/O SLOTS   Last OS
   MODEL/CLK/TYPE   PROJECT        TYPE    SE SCSI    EISA, VME, GSC  Supported
   --------------   ----------     ----    --------   --------------  ---------
   742i/ 50/Board   Sidewinder     PCXT    700        None            UX 10.20
   742rt/50/Board   Sidewinder     PCXT    700        None            HP-RT 2
   743i/ 64/Board   Anole-64       PCXL    710        1 VME, 2 GSC    UX 10.20
   743i/100/Board   Anole-100      PCXL    710        1 VME, 2 GSC    UX 10.20
   743rt/ 64/Board  Jason-64       PCXL    710        1 VME, 2 GSC    HP-RT 2
   743rt/100/Board  Jason-100      PCXL    710        1 VME, 2 GSC    HP-RT 2
   744/132L/Board   Anole-132L     PCXL2   710        1 VME, 2 GSC    UX 10.20
   744/165L/Board   Anole-165L     PCXL2   710        1 VME, 2 GSC    UX 10.20
   745i/ 50/Board   Pace           PCXT    700        4 E, No VME     UX 10.20
   745i/100/Board   Fast Pace      PCXT    700        4 E, No VME     UX 10.20
   747i/ 50/System  Pace           PCXT    700        2 E,6 V,1 GSC   UX 10.20
   747i/100/System  Fast Pace      PCXT    700        2 E,6 V,1 GSC   UX 10.20
   748i/ 64/System  Telepace       PCXL    710        4 E,8 V,2 GSC   UX 10.20
   748i/100/System  SuperPace      PCXL    710        4 E,8 V,2 GSC   UX 10.20

SERIES 800 SERVERS
------------------

.. note::

   Only the current 8x7, Dxxx, Exx-Ixx, Kxxx, and Txxx models are
   supported multi-user platforms for the HP-UX 11.00 release!)

::

                                         CPU    BUILT-IN      ADD-ON SCSI I/O
   MODEL STRING     PROJECT NAME        TYPE    SE, FWD/TYPE  SE, FWD, GSC-FWD
   ------------     ------------------  -----   ------------  ----------------
   822/922          SilverFox Low               NIO, None     Last Support-10.20
   825/925          Firefox                     CIO, None     Last Support-10.20
   832/932          SilverFox High              NIO, None     Last Support-10.20
   834/835/935      TopGun                      CIO, None     Last Support-10.20
   842/948          SilverBullet Low            CIO, None     Last Support-10.20
   845/945          ShoGun                      CIO, None     Last Support-10.20
   840/930          Indigo                      CIO, None     Last Support-10.20
   850/950          Cheetah                     CIO, None     Last Support-10.20
   852/958          SilverBullet High           CIO, None     Last Support-10.20
   855/955          Jaguar                      CIO, None     Last Support-10.20
   860/960          Cougar                      CIO, None     Last Support-10.20
   865/870/980      Panther                     CIO, None     Last Support-10.20
   890/990/992      Chimera                     NIO, NIO      Last Support-10.20

   8x7/F10-I40      Old Nova servers    PCXS    NIO, None     NIO(1),NIO(2),NA
   G50-I70          New Nova servers    PCXT    NIO, None     NIO(1),NIO(2),NA
   806/E25          WB Orville (48 Mhz) 7100LC  NIO, None     NIO(1),NIO(2),NA
   816/E35          WB Wilbur  (64 Mhz) 7100LC  NIO, None     NIO(1),NIO(2),NA
   826/E45          Wright Brothers 80  7100LC  NIO, None     NIO(1),NIO(2),NA
   856/E55          Wright Brothers 96  7100LC  NIO, None     NIO(1),NIO(2),NA

   801/D200/D300    UltraLight  75MHz   PCXL    710, 720/Z    EISA(3), 720/Z(4)
   811/D210/D310    UltraLight 100MHz   PCXL    710, 720/Z    EISA(3), 720/Z(4)
   803/D220         UltraLight 132MHz   PCXL2   710, 720/Z    EISA(3), 720/Z(4)
   813/D320         UltraLight 132MHz   PCXL2   710, 720/Z    EISA(3), 720/Z(4)
   823/D230         UltraLight 160MHz   PCXL2   710, 720/Z    EISA(3), 720/Z(4)
   833/D330         UltraLight 160MHz   PCXL2   710, 720/Z    EISA(3), 720/Z(4)
   821/D250/D350    UltraLight 100MHz   PCXT'   710, 720/Z    EISA(3), 720/Z(4)
   831/D250/D350    UltraLight 100MHz   PCXT'   710, 720/Z    EISA(3), 720/Z(4)
   841/D260/D360    UltraLight 120MHz   PCXT'   710, 720/Z    EISA(3), 720/Z(4)
   851/D260/D360    UltraLight 120MHz   PCXT'   710, 720/Z    EISA(3), 720/Z(4)
   861/D270/D370    UltraLight 160MHz   PCXU    710, 720/Z    EISA(3), 720/Z(4)
   871/D270/D370    UltraLight 160MHz   PCXU    710, 720/Z    EISA(3), 720/Z(4)
   810/D280/D380    UltraLight 180MHz   PCXU    710, 720/Z    EISA(3), 720/Z(4)
   820/D280/D380    UltraLight 180MHz   PCXU    710, 720/Z    EISA(3), 720/Z(4)
    
   9000/809/K100    Kittyhawk  100Mhz   PCXT'   710, 720/Z    NIO, NIO, 720/Z(5)
   9000/819/K200    Kittyhawk  100Mhz   PCXT'   710, 720/Z    NIO, NIO, 720/Z(5)
   9000/829/K400    Kittyhawk  100Mhz   PCXT'   710, 720/Z    NIO, NIO, 720/Z(5)
   9000/839/K210    Kittyhawk  120Mhz   PCXT'   710, 720/Z    NIO, NIO, 720/Z(5)
   9000/849/K410    Kittyhawk  120Mhz   PCXT'   710, 720/Z    NIO, NIO, 720/Z(5)
   9000/859/K220    Kittyhawk  120Mhz   PCXT'   710, 720/Z    NIO, NIO, 720/Z(5)
   9000/869/K420    Kittyhawk  120Mhz   PCXT'   710, 720/Z    NIO, NIO, 720/Z(5)

   9000/802/K250    Mohawk     160MHz   PCXU    710, 720/Z    NIO, NIO, 720/Z(5)
   9000/804/K450    Mohawk     160MHz   PCXU    710, 720/Z    NIO, NIO, 720/Z(5)
   9000/879/K260    Mohawk     180MHz   PCXU    710, 720/Z    NIO, NIO, 720/Z(5)
   9000/889/K460    Mohawk     180MHz   PCXU    710, 720/Z    NIO, NIO, 720/Z(5)
   9000/879/K270?   Mohawk     200MHz   PCXU    710, 720/Z    NIO, NIO, 720/Z(5)
   9000/889/K470?   Mohawk     200MHz   PCXU    710, 720/Z    NIO, NIO, 720/Z(5)
   9000/898/K370    Bravehawk  200MHz   PCXU+   710, 720/Z    NIO, NIO, 720/Z(5)
   9000/899/K570    Bravehawk  200MHz   PCXU+   710, 720/Z    NIO, NIO, 720/Z(5)

   9000/890         Emerald (1-12 Way)  PCXT    NIO, None     NIO(1),NIO(2),NA
   9000/891/T500    TNT 100 (1-12 Way)  7100    NIO, None     NIO(1),NIO(2),NA
   9000/892/T520    TNT 120 (1-12 Way)  7150    NIO, None     NIO(1),NIO(2),NA
   9000/893/T540    Jade 180 (1-12 Way) PCXU    NIO, Opt.     HSC(9)-FWD,NIO,FC
   9000/893/T600    Jade 180 (1-12 Way) PCXU    NIO, Opt.     HSC(9)-FWD,NIO,FC

   NOTES:  1. Product # 28655A is HP-PB (NIO) card with SCSI/SE interface.
           2. Product # 28696A is HP-PB (NIO) card with SCSI/FWD interface.
           3. Product # A2979A is EISA card with SCSI/SE interface
              supported only on D-class (UltraLight) servers.
           4. Product # A4107A is (Bluefish) HP-HSC card with SCSI/FWD 
              supported only on D-class (UltraLight) servers.
           5. Product # A2969A is (Shrike) HP-HSC card with SCSI/FWD 
              supported only on K-class servers.
           6. Product # 28615A is NIO/HP-FL card with fiber-optic interface
              supported only on 890, 8x7, G, H, I, T500, and T520 servers.
           7. Product # 28650A is HPIB interface card 
              supported only on 890, 8x7, F, G, H, I T500, and T520 servers.
           8. PCXT', PCXU, and PCxU+ machines use a bus converter (U2) to
              provide two HSC (GSC+) busses from the Runway bus.
           9. The Jade server supports 22 additional HSC slots for HSC-FWD 
              SCSI cards, HSC-FibreChannel cards, and HP-PB bus converters
              for NIO SCSI cards.

NOTES ON HP MODELS AND INTERFACES
---------------------------------

The above matrix lists the HP models, project names, CPU types, and SCSI
options for the three major system types. More information appears in
the "Series 700 Workstations" section since experience has shown more
differences with the Single-Ended (SE) SCSI interfaces on the S700
workstations. This data was collected from various ordering and
configuration guides, and HP-UX system specifications.

The PCXS and PCXT models include the NCR 53C700 device at various
SCSI-Clock rates for the built-in Single-Ended (SE) SCSI controller.
These older models use the NCR 53C720 (40 MHz) SCSI controller (where
supported) with the Outfield (O) chip for the built-in SCSI controller
for the Fast-Wide-Differential (FWD) SCSI bus. The PCXS and PCXT models
do not provide support for an internal PC Floppy drive.

The other CPU models use the NCR 53C710 SCSI-SE controller at 40 MHz
that is built into the multi-function LASI-I/O chip. The built-in LASI
device also provides I/O support for an internal PC Floppy drive. These
newer models use the NCR 53C720 device running at 40 MHz with the Zalon
(Z) chip on the built-in SCSI-FWD I/O and the external GSC-SCSI-FWD I/O.

The two types of EISA-SCSI cards use the NCR 53C710 SCSI controller at
50 MHz to support either Single-Ended (SE) or Fast-Differential (FD)
SCSI devices. The Series 700 Configuration Guide (November 1992 Edition)
states that the older EISA Card (model 25525A) for FD SCSI devices is
not qualified on the 715/33-50-75 models, and it recommends the 25525B
EISA card for best results on the other workstations.

Note that the EISA bus runs at a clock rate (either 16 or 33 Mhz) that
is one-third to one-half of the CPU CLK rate. At this time, the EISA bus
clock does not appear to affect our tests with SCSI devices.

The B, C, and J class workstations do NOT support the EISA-SCSI
interfaces. The other workstation models with EISA interfaces will
support the EISA-SCSI/SE and EISA-SCSI/FD cards. Only the D-class s800
models support the EISA-SCSI/SE card (model A2679A).
