Hardware troubleshooting and repair guide
================================================

My MAPIO doesn't start
-----------------------------

You don't see any of the two LEDs embedded on PCB1. Follow the next steps until you find the root cause.

* With a multimeter, check that 5V is present on J1001 connector
* Remove PCB2 and try to power your MAPIO. If the MAPIO can start now, your PCB2 is defective. Please check your PCB2 with the following guide.
* Check that jumpers on P1003 and P1005 are correctly installed, as described in the Getting Started guide.
* With a multimeter, check if 5V is present on P1003 connector, pin 3. If absent, check the fuse F1000.
* Check that the Compute Module is correctly installed. Ideally, test with another Compute Module.

My USB device is not detected
--------------------------------

The relay doesn't work
--------------------------------

The optocoupler doesn't work
--------------------------------

My PCB2 prevents my MAPIO from starting
-----------------------------------------

Replacement parts
-----------------------------------------

+--------------------+-------------------+--------------------------+
| Item               | Manufacturer      | Reference                |
+====================+===================+==========================+
| Fuse (F1000)       | Bel               | 0ABB-3500-TM             |
+--------------------+-------------------+--------------------------+
| Relay (K800)       | Omron             | G5LE-14 DC5              |
+--------------------+-------------------+--------------------------+
| 3                  | Test              |                          |
+--------------------+-------------------+--------------------------+