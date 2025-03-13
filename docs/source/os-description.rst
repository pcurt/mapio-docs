OS description
==================================

MAPIO OS is generated using yocto tool, see the dedicated page for more information (:doc:`OS build <os-build>`.)

See :ref:`os-build:Build a Yocto Linux Image (MAPIO OS)`.

The goal of this OS is to provide Docker to launch the services you want.


Services running on the host
-----------------------------
Some services are running on the host, here is the list of this services and their role:

* Global services:
    * docker.service:
         Docker is used to launch ever specific software on MAPIO OS
    
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
      
    * mapio-webserver-back.service
        It starts the backend used by web server to facilitate some MAPIO OS setup (see :doc:`OS Configure <os-configure>`).
        It uses a custom python package that can be found here: https://github.com/pcurt/mapio-webserver-back


Docker compose services
------------------------
MAPIO OS is delivered with some basic docker configuration. This configuration is in the file /home/root/mapio/docker-compose.yml.
This file defines the following services:

* homeassistant: an open source home automation system
* zigbee2mqtt: to control zigbee network and devices
* caddy: a reverse proxy
* jellyfin: a media center
* samba: for network file sharing
* nextcloud: an open source file hosting service
* domoticz: a lightweight home automation 
* resticprofile: a backup service
* teleinfo2mqtt: a service to read the Linky TIC port data and send it to HA using the MQTT broker
* matter-server: a service to control matter devices
* otbr: a service to control thread devices
* wireguard: a service to create a VPN

These services can be controlled by the web server (see :doc:`OS Configure <os-configure>`).
From the web server you can:

* start, stop, a service
* create a service
* pull and update a service
* see the logs of the services
* check the status of the services
* check for updates
* see ports used by the services


.. warning::
    The file /home/root/mapio/docker-compose.yml is overwritten during an update. If you modify it, you can replace the file by a symbolic link and keep your modified file in data partition (mounted on /usr/local).


Security
--------
There is only a root user installed on the MAPIO OS. The SSH login by password is disabled. The only way to connect to your gateway is to add you SSH private key from the web server (see :doc:`OS Configure <os-configure>`). 
We advise you to keep these security rules especially if you authorize external access. MAPIO is not connected to any custom cloud service, you have total control of your data.
