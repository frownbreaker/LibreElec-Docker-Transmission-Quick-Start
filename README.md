# LibreElec-Docker-Transmission-Quick-Start
Quickstart for setting up LibreElec with Docker running Transmission as a low footprint RP4 based daily driver 


Docker is installable as an add-on from LibreElec

The recommendation from the LE team is to use Docker and Portainer. I've found that option did not work that well. I got only 1 or 2 months uptime.
The portainer setting fetched updates nightly and I don't need the instabiltiy that caused me. Sometimes I'd have to reboot, finally it crashed transmission.
I've had Theoria's tranmission running for years with no outages on an old RP 2 Model B, I get the odd lock up but have a remote monitor and a remote control PSU to hard reset if the Transmission web interface is not visible for an extended period. This gives me zero touch transmission on old hardware

So why this update? I've a 4k Tv and noticed some content was taking a long time as the RP2B only has 100meg networking. RP4 has USB3 and 1g Networking.

BEFORE YOU START don't try to use USB Flash drives or SD cards for this. Use SSDs or HDs there is a lot of IO and SD cards and flash cannot take the write intensity plus there cannot keep up with SUSTAINED writes and concurrent reads.

Using the offical repo install docker (its under Add-ons services) then restart the RPI4, connect via SSH from a PC and enter the command below. Edit the -v commands to fit your setup in my case I've a USB drive plugged into a USB3 port on the RP4 (2m RAM) running of SD. Note how all my temp files are on the USB HD.


docker run -d \
--name=9091-transmission \
--net=host \
-e PUID=0 \
-e PGID=0 \
-e TZ=Europe/London \
-e USER=admin \
-e PASS=secret \
-p 9091:9091 \
-p 51413:51413 \
-p 51413:51413/udp \
-v /var/media/10TB/_dockerrp4avroom/.config/dockers/transmission/config:/config \
-v /var/media/10TB/:/downloads \
-v /var/media/10TB/watch:/watch \
-v /storage:/storage \
-v /media:/media \
--restart unless-stopped \
linuxserver/transmission
