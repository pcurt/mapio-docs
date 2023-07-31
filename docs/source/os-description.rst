MAPIO OS description
==================================

MAPIO OS is generated using yocto tool, see the dedicated page for more information (:doc:`OS build <os-build>`.)

See :ref:`os-build:Build a Yocto Linux Image (MAPIO OS)`.

The goal of this OS is to provide Docker to launch the services you want.


Services running on the host
-----------------------------
Some services are running on the host, here is the list of this services and their role:

* Global services:
    * docker.service:
         Docker is used to launch ever specific software on MAPIO OS (see :doc:`Examples <examples>`)
    
    * mosquitto.service:
         This is the MQTT broker used by docker services to communicate each over.

    * rauc.service:
        MAPIO uses RAUC tool to manage OTA updates(see :doc:`OS Update <os-update>`)

    * usr-local-nvme.automount/usr-local-nvme.mount:
        It uses sytemd automount feature to mount the NVMe disk if the SSD is present

* Custom services:
    * mapio-init.service:
         It is executed at first boot or after OTA update, it resizes the last eMMC partition to its maximal size.
    
    * mapio-display.service:
        It drives the epaper screen. And manages the physical buttons.
        It uses a custom python package that can be found here: https://github.com/pcurt/mapio_display
    
    * mapio-gpio-ha.service:
        It exposes some hardware resources (GPIOs and GPU) on a MQTT broker using the Home Assistant protocol.
        It uses a custom python package that can be found here: https://github.com/pcurt/mapio_gpio_ha
      
    * mapio-setup-wizard.service
        It start a local webserver to facilitate some MAPIO OS setup (see :doc:`OS Configure <os-configure>`).
        It uses a custom python package that can be found here: https://github.com/pcurt/mapio-setup-wizard


