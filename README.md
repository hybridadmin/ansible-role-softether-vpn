sa-vpn-softether
================

[![Build Status](https://travis-ci.org/softasap/sa-vpn-softether.svg?branch=master)](https://travis-ci.org/softasap/sa-vpn-softether)


Example of use: check box-example

Configuration:
```YAML

```

Simple:

```YAML


     - {
         role: "sa-vpn-softether"
       }

```


Advanced:

```YAML


     - {
         role: "sa-vpn-softether"
       }

```


Connecting to OpenVPN from client box
=====================================

If you executed last step of play, you have now cer file for ipsec + zip with openvpn configuration.

Once unpacked, ensure you have GUI ready for openvpn. If menu "Import saved vpn configuration" missing, proceed with


```bash
sudo apt install network-manager-openvpn network-manager-openvpn-gnome network-manager-pptp network-manager-vpnc
```

After logout/login or reboot you will have menu option "Import saved vpn configuration".

Import file named `openvpn_remote_access_l3.ovpn`

use your user@vpn , for example `test@vpn` followed by password, like `test`


To troubleshoot you might use interactive session native ovpn client, like

`openvpn --config my.ovpn`


Connecting to OpenVPN full story
================================

1. About Files
--------------

When you open the ZIP archive, the following files with the
structured-directory will be expanded.
Extract there files including sub-directory structure toward any destination
directory, and use parts according to your necessary.

< The Configuration File for L3 (IP Routing) >
  openvpn_remote_access_l3.ovpn

< The Configuration File for L2 (Ethernet Bridging) >
  openvpn_site_to_site_bridge_l2.ovpn

The extension ".ovpn" means a configuration file. You can specify the
configuration file into OpenVPN to initiate a VPN connection.


2. How Different between L3 and L2?
-----------------------------------

Use L3 (IP Routing) if you want to install OpenVPN on the normal computer (for
example, a lap top PC), and make it connect to PacketiX VPN Server or SoftEther
VPN Server for the purpose of establishing a "Remote-Access VPN Connection" .
In this case, the IP address will be assigned on the virtual network adapter
of OpenVPN automatically when the OpenVPN will connect to the Virtual HUB on
the VPN Server successfully and request an IP address and other network
parameters (e.g. DNS server address).

In other hand, if you want to build a "Site-to-Site VPN Connection" ,
use L2 (Ethernet Bridging) for OpenVPN on the computer which is set up on the
remote place for bridging. No IP-specific treatment will be done. All Ethernet
packets (MAC frames) will exchanged transparently between two or more sites.
Any computers or network equipments (e.g. routers) will be able to communicate
to other sites mutually.

VPN Server will treat a virtual VPN session from L3-mode OpenVPN as
a "VPN Client" session.
VPN Server will treat a virtual VPN session from L2-mode OpenVPN as
a "VPN Bridge" session.


3. How to Specify the Username and Password?
--------------------------------------------

The prompt of username and password will be shown when you try to use this
configuration. You have to enter the same username and password which has
already been defined on the Virtual HUB of VPN Server.

Please note that you have to create an user on the Virtual HUB in advance.

If there are two or more Virtual HUBs on the VPN Server, you have to specify
the username as:

  "Username@Virtual-HUB-Name"

or:

  "Virtual-HUB-Name\Username"

to choose which Virtual HUB to be connected. You can also choose which
Virtual HUB should be elected as a "Default HUB" when the specification of
the name of Virtual HUB will be omitted.

Please be advised that you can make OpenVPN to enter the username and password
automatically without showing a prompt. How to do it is described on the
OpenVPN manual.


* 4. About Protocol and Port Number
Both TCP and UDP are available to connect to the VPN Server by OpenVPN.

If you use TCP, the port number is same as any of the "TCP Listener Port" on
the VPN Server which is originally defined in order to accept inbound
TCP-based VPN Client session.

If you use UDP, the port number must be one of UDP ports which are defined on
the VPN Server configuration in advance. Do not confuse between TCP and UDP
since they are not concerned mutually.

You can also specify the proxy-server address if the connection should be
relayed by the proxy-server. Specify it on the configuration file.



Copyright and license
---------------------

Copyright - Vyacheslav Voronenko

Code licensed under the [BSD 3 clause] (https://opensource.org/licenses/BSD-3-Clause) or the [MIT License] (http://opensource.org/licenses/MIT).

Subscribe for roles updates at [FB] (https://www.facebook.com/SoftAsap/)
