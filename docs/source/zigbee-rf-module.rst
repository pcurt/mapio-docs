Zigbee RF module
===================

The zigbee RF module is based on a **TI CC2652**
It can be inserted on any off the RF location (A, B or C).

+--------------------+-------------------+
| RF location        | Serial port       |
+====================+===================+
| A                  | ttyS1 or ttyAMA3  |
+--------------------+-------------------+
| B                  | ttyAMA5           |
+--------------------+-------------------+
| C                  | ttyS1 or ttyAMA3  |
+--------------------+-------------------+


Flash or update
---------------------

You can flash the module directly from MAPIO.
Connect to the gateway using SSH, stop the services that are currently using the module.
Get the latest binary from official firmawares
https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator/Z-Stack_3.x.0/bin

Then transfert the binary with an scp command.

For example:

.. code-block:: console

    scp CC1352P2_CC2652P_launchpad_coordinator_20230507.hex root@192.168.1.10:/tmp


Go the the directory 

.. code-block:: console

    cd /home/root/tools


Execute the following command (select the correct serial port corresponding to your setup)

.. code-block:: console

    python cc2538-bsl.py -p /dev/ttyAMA5 -e -w /tmp/CC1352P2_CC2652P_launchpad_coordinator_20230507.hex 


Your module is up to date, you can check the communication using the command

.. code-block:: console

    python cc2538-bsl.py -p /dev/ttyAMA5