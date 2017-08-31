+++
title = "Printing to HP LaserJet over a firewall"
date = 2015-01-12T14:24:49+02:00
+++

This shouldn't be so surprising, but it took us a good bit of searching to get everything together. Here is what you need for the following to work:

*   Printing
    *   TCP/9100
*   Configuration and driver search
    *   HTTP
    *   SNMPv2
*   Diagnostics
    *   Ping

Your printer won't be seen though by the automatic search, you have to add it as a TCP/IP device manually. But once given the IP, everything works.