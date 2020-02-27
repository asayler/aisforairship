---
layout: single
author_profile: true
toc: true
---

Like many folks who make bad life decisions, I operate a [home
lab](https://www.reddit.com/r/homelab/) filled with server and network
infrastructure. Some of this is so I can do things like operate
over-complicated home network setups, but mostly it's just a chance to
futz around with computers. Hey, everyone needs a hobby.

Because my home lab isn't exactly... critical infrastructure, and because
I'd still like to live on this planet in 40 years, my most recent
home lab overhaul involved optimizing my compute systems for minimal
power consumption -- while still maintaining reasonable compute
power. While large scale datacenter operators have long [prioritized power
efficiency](https://www.google.com/about/datacenters/efficiency/),
it's a less explored space at the small-scale, home-lab
level. Thus, I found myself testing and reviewing the power output of
a range of home-lab-scale server platforms, the results of which I
present here, for the benefit of Interwebs!

The Candidates
==============

I wound up testing a range of items, some of which I simply had lying
around, and some because I was curious as to how they'd preform. The
full list of tested components includes:

| Motherboard       |  CPU/SoC         |  Year  |  Cores  |  Threads  |  [TDP]  |
| ----------------- | ---------------- | :----: | :-----: | :-------: | :-----: |
| [Raspberry Pi 4B] | [BCM2711]        |  2019  |   4     |   4       |   4 W   |
| [A1SRi-2758F-O]   | [Atom C2758]     |  2013  |   8     |   8       |  20 W   |
| [A2SDi-TP8F]      | [Atom C3858]     |  2017  |  12     |  12       |  25 W   |
| [X9SCM-F]         | [Xeon E3-1240v2] |  2012  |   4     |   8       |  69 W   |
| [X10SLH-F]        | [Xeon E3-1246v3] |  2014  |   4     |   8       |  84 W   |
| [X10SDV-TLN4F]    | [Xeon D-1541]    |  2015  |   8     |  16       |  45 W   |
| [M11SDV-8CT-LN4F] | [EPYC 3201]      |  2018  |   8     |   8       |  30 W   |

[TDP]: https://en.wikipedia.org/wiki/Thermal_design_power

[Raspberry Pi 4B]: https://www.raspberrypi.org/products/raspberry-pi-4-model-b/specifications/
[BCM2711]: https://www.raspberrypi.org/documentation/hardware/raspberrypi/bcm2711/README.md

[A1SRi-2758F-O]: https://www.supermicro.com/products/motherboard/ATOM/X10/A1SRi-2758F.cfm
[Atom C2758]: https://ark.intel.com/content/www/us/en/ark/products/77988/intel-atom-processor-c2758-4m-cache-2-40-ghz.html

[A2SDi-TP8F]: https://www.supermicro.com/en/products/motherboard/A2SDi-TP8F
[Atom C3858]: https://ark.intel.com/content/www/us/en/ark/products/97936/intel-atom-processor-c3858-12m-cache-up-to-2-0-ghz.html

[X9SCM-F]: https://www.supermicro.com/products/motherboard/Xeon/C202_C204/X9SCM-F.cfm
[Xeon E3-1240v2]: https://ark.intel.com/content/www/us/en/ark/products/65730/intel-xeon-processor-e3-1240-v2-8m-cache-3-40-ghz.html

[X10SLH-F]: https://www.supermicro.com/en/products/motherboard/x10slh-f
[Xeon E3-1246v3]: https://ark.intel.com/content/www/us/en/ark/products/80916/intel-xeon-processor-e3-1246-v3-8m-cache-3-50-ghz.html

[X10SDV-TLN4F]: https://www.supermicro.com/en/products/motherboard/X10SDV-TLN4F
[Xeon D-1541]: https://ark.intel.com/content/www/us/en/ark/products/91199/intel-xeon-processor-d-1541-12m-cache-2-10-ghz.html

[M11SDV-8CT-LN4F]: https://www.supermicro.com/en/products/motherboard/M11SDV-8CT-LN4F
[EPYC 3201]: https://www.amd.com/en/products/embedded-epyc-3000-series

Details on each of the candidates are included below.

Raspberry Pi 4 Model B
----------------------

The [Raspberry Pi 4 Model
B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/specifications/)
is the latest Raspberry Pi board (as of February 2020). It comes in
1GB, 2GB, and 4GB RAM versions and includes a [BCM2711]
system-on-a-chip (SoC) featuring an embedded quad-core Cortex-A72 (ARM
v8) 64-bit SoC clocked at 1.5GHz. For the purpose of this test, I used
a *4GB version* of the board which [retails for
$55](https://www.pishop.us/product/raspberry-pi-4-model-b-4gb/).

For the test, the Pi was running the *32-bit* version of
[Raspian](https://www.raspbian.org/) from the [07/10/19
image](http://downloads.raspberrypi.org/raspbian/release_notes.txt)
using the 4.19.66-v7l Linux kernel. There are a number of ways to
power the Pi, most commonly a USB C connection. For this test, the Pi
was powered via the [official PoE
hat](https://www.raspberrypi.org/products/poe-hat/) connected to an
[802.3af](https://en.wikipedia.org/wiki/Power_over_Ethernet) PoE
switch from [Ubiquiti](https://www.ui.com/).

Supermicro A1SRi-2758F-O
------------------------

The Supermicro [A1SRi-2758F-O] is
[mini-ITX](https://en.wikipedia.org/wiki/Mini-ITX) motherboard
designed for networking applications (e.g. router, middlebox, etc). It
features an embedded Intel [Atom C2758] CPU, which is an 8-core, 2.40
GHz low-power (20W TDP) x86 processor released in 2013. The board
retailed for around $300 in 2014 when I purchased it.


For the test, this board was coupled with 16GB (2x 8GB) of ECC RAM, a
a 750W [80 Plus Gold](https://en.wikipedia.org/wiki/80_Plus) (87%+
efficiency) power supply, and a single SSD. The tests were run on a
fresh 64-bit install of Ubuntu 18.04.3 with the 5.0.0-25 Linux kernel.

Supermicro A2SDi-TP8F
---------------------

The Supermicro [A2SDi-TP8F] is another mini-ITX motherboard. It's the
generational successor to the A1SRi-2758F noted above. It includes an
embedded x86 Intel [Atom C3858] CPU, which includes 12-cores running
at 2.00 GHz with a 25W TDP. The C3858 was released in 2017 as one of
the successors to the C2XXX line. This board retails for about $750
today.

For the test, this board was coupled with 16GB (2x 8GB) of ECC RAM,
and the same 750W power supply and SSD as the A1SRi-2758F. The tests
were run on a fresh 64-bit install of Ubuntu 18.04.3 with the 5.0.0-25
Linux kernel.

