---
id: Hardware
title: Resources, hardware
sidebar_label: Hardware
---

Recommended hardware profile:
* 16+ GiB of RAM (some client combinations benefit from 24 GiB)
* Quad Core CPU
* 2TB "mainstream" SSD - neither QLC nor DRAMless (1TB can work with some client combinations; 2TB affords more room for growth)

Generally, 8 GiB of RAM is a very tight fit, and 16+ GiB is recommended.

4 CPU cores are recommended to deal with spikes in processing. An SSD is required for storage because the node databases
are so IOPS-heavy. The Geth execution client would require around 500GiB of storage by
itself initially, which can fill a 1TB SSD within 6 months. Offline pruning is available.

Other execution clients grow at different rates, see [resource use](../Usage/ResourceUsage.md).

The consensus client database is small, around 20-100 GiB, but we don't know what growth will
look like once the merge with PoW is done.

If you are running a slasher, that might be another 100 to 300 GiB by itself.

Two home server builds that I like and am happy to recommend are below. Both support
IPMI, which means they can be managed and power-cycled remotely and need neither
a GPU nor monitor. Both support ECC RAM, though the AMD option as of Sept 2020
was unable to report ECC errors via IPMI, only OS-level reporting worked.

**Intel**

* mITX: 
  * SuperMicro X11SCL-IF(-O) (1 NVMe)
* uATX:
  * SuperMicro X11SCL-F(-O) (1 NVMe) or X11SCH-F(-O) (2 NVMe)
* Common components:
  * Intel i3-9100F or Intel Xeon E-2xxx (i5/7 do not support ECC)
  * 16+ GiB of Micron or Samsung DDR4 UDIMM ECC RAM (unbuffered, **not** registered)
  * 2TB M.2 NVMe SSD or SATA SSD, e.g. WD Red SN700 or Samsung 870 EVO

**AMD**

* mITX:
  * AsRock Rack X570D4I-2T (1 NVMe)
* uATX:
  * AsRock Rack X470D4U or X570D4U (2 NVMe both)
* Common components:
  * AMD Ryzen CPU, but not APU (APUs do not support ECC)
  * 16+ GiB of Micron or Samsung DDR4 UDIMM ECC RAM (unbuffered, **not** registered)
  * 2TB M.2 NVMe SSD or SATA SSD, e.g. WD Red SN700 or Samsung 870 EVO

Plus, obviously, a case, PSU, case fans. Pick your own. Well-liked
options are Node 304 (mITX) and Node 804 (uATX) with Seasonic PSUs,
but really any quality case that won't cook your components will do.
For a small uATX form factor, consider Silverstone ML04B.

[Joe's hardware roundup](https://github.com/jclapis/rocketpool.github.io/blob/main/src/guides/local/hardware.md) has additional build ideas.

On SSD size, 2TB is conservative and assumes you are running
an execution client as well, which currently takes about 500-700 GiB initially depending on client chosen and keeps
growing. The consensus client db is expected to be far smaller, though exact figures
won't be seen until the merge with Ethereum PoW is complete.

You'll want decent write endurance. WD Red SN700 and SK Hynix Gold P31 are good NVMe choices as of early 2022,
and Samsung 870 EVO, WD Blue 3D NAND or Crucial MX500 are good SATA 2.5" choices.
Intel SSDs are also well-liked: Their data center SSDs are quite reliable, if a bit pricey.

You may also consider getting two SSDs and running them in a software mirror
(RAID-1) setup, in the OS. That way, data loss becomes less likely for the
chain databases, reducing potential down time because of hardware issues.

Why ECC? This is a personal preference. The cost difference is minimal,
and the potential time savings huge. An Ethereum staking full node does not require
ECC RAM; I maintain it is very nice to have regardless.

With non-ECC RAM, if your RAM goes bad, you will be troubleshooting server
crashes, and potentially spending days with RAM testing tools.

With ECC RAM, if your RAM goes bad, your OS and, if Intel, IPMI, will alert
you to corrected (or uncorrected) RAM errors. You'll want to have set up
email alerts for this. You then buy replacement RAM and schedule downtime.
No RAM troubleshooting required, you will know whether your RAM is functional or has issues
because it will report this to you, and correct single-bit errors.

I am so protective of my time these days that I build even my
home PCs with ECC RAM. You know your own tolerance for troubleshooting
RAM best.
