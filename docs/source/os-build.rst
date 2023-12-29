Build a Yocto Linux Image (MAPIO OS)
=====================================

The MAPIO OS distribution is build using Yocto (more information on https://yoctoproject.org).

System Requirements
--------------------

To build your own distribution you will need a build machine with the following requirements:

* Linux machine
* At least 90Go of free disk
* At least 8Go of RAM and at least a 4 CPU cores
* Follow the following README https://github.com/pcurt/yocto-build/blob/main/README.md to install:
    * Git
    * Docker
    * CQFD 


Get project and configure the build
-------------------------------------

Clone the build repository

.. code-block:: console

    $ git clone git@github.com:pcurt/yocto-build.git
    $ cd yocto-build

Build the build docker image

.. code-block:: console

    $ cqfd init

Build MAPIO OS
---------------

Start MAPIO OS build

.. code-block:: console

    $ cqfd init

The build may takes several hours depending on your build machine characteristics.
Only the first build is very long, next builds will be very fast (for example less than 2 minutes if you change an applicative package).

The output image is located here

.. code-block:: console

    $ yocto-build/build/tmp/deploy/images/mapio-cm4-64/mapio-image-mapio-cm4-64.wic.bz2

Build MAPIO OS bundle
----------------------

MAPIO OS can be updated using a bundle (see :doc:`OS Update <os-update>`).
Here are the steps to produce your own bundle update.

The bundle is signed using OpenSSL (signatures based on x.509 certificates).
In your build directory we can execute a script to generate certificates, private and public keys

.. code-block:: console

    $ yocto-build/layers/meta-rauc/scripts/openssl-ca.sh

Replace the existing ca.cert.pem and private key  with your own :

.. code-block:: console

    $ cp yocto-build/layers/meta-rauc/scripts/openssl-ca/dev/ca.cert.pem yocto-build/layers/meta-mapio-bsp/recipes-core/rauc/files/ca.cert.pem
    $ cp yocto-build/layers/meta-rauc/scripts/openssl-ca/dev/development-1.cert.pem yocto-build/development-1.cert.pem
    $ cp yocto-build/layers/meta-rauc/scripts/openssl-ca/dev/private/development-1.key.pem yocto-build/development-1.key.pem

Generate your bundle

.. code-block:: console

    $ cqfd -b bundle

The output bundle is located here

.. code-block:: console

    $ yocto-build/build/tmp/deploy/images/mapio-cm4-64/mapio-bundle-image-mapio-cm4-64.raucb

You can now update your MAPIO OS following these instructions :doc:`OS Update <os-update>`
