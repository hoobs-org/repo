This is for Fedora and Debian systems. If you are running macOS please go to [macOS Remote Access](5e763f44e87d1e02b6c19d3a).

To setup remote access you will need to know how to access your router to enable port forwarding to access HOOBS remotely.

HOOBS automatically installs NGINX and routes all traffic through it. We do this to manage the network traffic. This is done when running the `sudo hoobs-init` command.

If you ran the `sudo hoobs-init` command, you need to forward port `80`.

If you opted not to run the init script, HOOBS runs from the port configured in `server.port`. The default is port `8080`.

For this guide we are assuming that you ran the `sudo hoobs-init` command, so we are using port `80`.

## Configuring your Router
Everyone has a different router, please refer to your router's manual or online help. You will need to forward port `80` to your HOOBS server.

Some routers require you to reserve the IP address to enable port forwarding.

## Hairpinning
Some routers don't have hairpinning. This is when a public domain or ip address is called within the LAN. Some routers will not direct the traffic to the local device.

In this case you will need to access HOOBS using the `http://hoobs.local` address or the devices local IP address. To test port fowarding you will need to test from a device not on the same network.

If your router supports hairpinning, you do not need to worry about this.

### Index
* [**Introduction**](5e763b10e87d1e02b6c19d29)
* [**HOOBS in a Box**](5e763d06e87d1e02b6c19d30)
* [**HOOBS on microSD**](5e763d92e87d1e02b6c19d31)
* [**HOOBS to Download**](5e8599870ab68b0344e872bd)
* [**Install HOOBS Manually**](5e763e30e87d1e02b6c19d33)
* [**HOOBS Migration Tool**](5e763dfbe87d1e02b6c19d32)
* [**Migrate Manually**](5e764226e87d1e02b6c19d3b)
* [**Installing HOOBS**](5e763e30e87d1e02b6c19d33)
* [**Remote Access**](5e763e4be87d1e02b6c19d34)
