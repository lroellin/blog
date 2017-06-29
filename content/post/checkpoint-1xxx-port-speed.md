+++
title = "Serial speed on Check Point 1xxx Series (e.g. 1100, 1430/1450, etc.)"
date = 2014-02-23T01:30:42+02:00
+++

I recently had to connect to one of the new Check Point 1100 Appliances. This is the successor series of the old Edge boxes, and features a new OS (Embedded Gaia), an ARMv9 CPU and a new WebUI. **UPDATE: this also works on other 1xxx series devices, like the 1430.**

To connect via serial, I used the kind-of standard 9600 baud (bits/s), but that only displayed garbage.
To successfully connect, use `115200` baud, 8N1, no parity and XON/XOFF flow control (standard PuTTY). Additionally, use a Cisco serial cable, but they're pretty common too.

If you have no idea what I'm talking about, the connector shown below actually does have its use:

![](/post/serial.jpg)

PS: I like this WebUI!