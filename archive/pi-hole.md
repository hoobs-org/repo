![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/logo.png)
### HOOBS Pi-Hole Installer

This script will install Pi-Hole for HOOBS 3 for v3.1.1 or higher

go to hoobs.local -> top right menu -> Terminal 
![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/system/terminal.png)
The terminal is the command line for the device HOOBS is running on. 
This works on the HOOBS Image, Raspbian, all other Linux Distros and MacOS. 
This option is not available on Docker


Run the following command:

```wget -q -O - https://git.io/J3fno | sudo bash -```

Copy this command all in one line

This will setup Pi-Hole for you.


After the installation you can access Pi-Hole as following:

**Pi-Hole Interface is reachable at "hoobs.local:1882/admin"**

**Pi-Hole Password is "hoobsadmin"**


**CLICK ON ENABLE TO START BLOCKING**

![](https://raw.githubusercontent.com/hoobs-org/hoobs-images/master/docs/step-by-step/pihole10.png)

# Gather your network requirements

Pi-hole needs a static IP address in order to function properly. By default your router will most likely give your device a different IP address every time it connects to the network or after a period of 30 days. What we need is for the IP address to never change when the Pi-hole is connected to your router, otherwise you would have to re-configure the Pi-hole settings every so often, and this is not practical. 

There are two ways in which you can set a static IP address on your router; you can either set it as a static address or you can use Dynamic Host Control Protocol (DHCP) reservation. The easiest and most convenient way to set a static IP is using DHCP reservation.

Logon to your router's web interface. This is usually a static IP address in which you put into the web browser and can be found in either your routers manual or on a sticker on the reverse side of the router hardware. You will also be required to enter a password.

In the web interface navigate and locate a section called DHCP settings or something similar.

Look for a reservations setting

You should see a full list of connected devices from a list
Click on the small tick box next to the HOOBS and add the reservation


The Pi-hole IP address should now be added to the reserved list, where the IP address will always be assigned to the Pi-hole. Make sure you take note of the IP address as we will need it later on in this guide.

# Use Pi-hole as your DNS server

Now that we have set the Pi-hole to use a static IP address on the local network we need to make sure that every device on the network will now use the Pi-hole as its DNS server:

Enter your router's configuration page and depending on on your router's interface you should see a setting or menu that says static DNS or DNS server.

Here you need to enter the IP address of your HOOBS Device, which we set earlier in the DHCP section.
