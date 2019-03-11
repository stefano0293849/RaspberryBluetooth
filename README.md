# RaspberryBluetoothSurf
In this simple guide you will learn how to set up your raspberry pi 3 as a bluetooth hotspot able to share his internet connection thought the bluetooth instead of the wifi and that will let you surf with every device able to navigate on the internet connected to the raspberry. The raspberry will need to be connected to the router throught the ethernet cable, and it will share his connection using the bluetooth instead of the wifi to every devices connected to it.

```
Router       Raspberry pi 3           Bluetooth connection           Devices
 __   eth0    __                                                    _   _   _
|  | ------- |  |  -    -     -      -     -     -    -    -   -   | | | | | |
```


1) You'll need to set the raspberry pi 3 as an hotspot able to share his internet connection thought the wifi first, and an android (with android version > 4.4 ) phone 

now follow this step starting from a clean install of Raspbian: 

2) 


```sudo update```
3)
follow the guide on https://github.com/ykasidit/ecodroidlink with the below configuration
4)

follow http://raspberrypi.stackexchange.com/questions/41776/failed-to-connect-to-sdp-server-on-ffffff000000-no-such-file-or-directory
5)
and check if it gives the same parameters of http://www.hkepc.com/forum/viewthread.php?tid=1710030
6)
use the following interface configuration :
```
source-directory /etc/network/interfaces.d
auto lo
iface lo inet loopback
iface eth0 inet manual
auto br0
iface br0 inet static
address 192.168.1.110
netmask 255.255.255.0
gateway 192.168.1.1
bridge_ports eth0
#dovrebbe funzionare anche senza questi 3 per ora li tolgo
#allow-hotplug bnep0
#iface bnep0 inet dhcp
allow-hotplug wlan0
iface wlan0 inet manual
    wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
allow-hotplug wlan1
iface wlan1 inet manual
    wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
 ```
 
7) in the ecodroidlink configuration use this row:
```
/home/pi/ecodroidlink/edl_main --use_existing_bridge br0 &
```
8) write in terminal:
```sudo apt-get install dnsmasq```

-sudo nano /etc/dhcpcd.conf and add:


interface=br0      # Use interface wlan0
#listen-address=172.24.1.1 # Explicitly specify the address to listen on
bind-interfaces      # Bind to the interface to make sure we aren't sending thi$
server=8.8.8.8       # Forward DNS requests to Google DNS
domain-needed        # Don't forward short names
bogus-priv           # Never forward addresses in the non-routed address spaces$
dhcp-range=192.168.1.111,192.168.1.150,12h



-connect your phone to the raspberry bluetooth and now you can surf the internet with your phone using the connection  of the raspberry py 3 with out using the wifi.

-bluetooth is very slow but it can be helpfull to use it in iot devices becouse it consume less power.


