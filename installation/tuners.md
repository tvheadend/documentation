# Tuners

Before you install Tvheadend software you need to have a working tuner device. There are four types of tuner hardware that Tvheadend can use:

* Internal PCI/PCIe tuners
* Internal i2s tuners
* External USB tuners
* Network tuners

> IP sources can also be used. These are discussed elsewhere in our documentation.

### PCI/PCIe Tuners

Internal PCI/PCIe tuner cards require support for the tuner in the host OS. Most cards require a driver and separate firmware to work. Some cards will be supported through drivers and firmware available in the upstream Linux kernel and will be able to run on any current Linux distro and version. Other cards require downstream/vendor drivers and these may dictate which distro and version must be used to have support. How to install the right drivers and firmware for your hardware is beyond the scope of this guide so please follow the instructions of the tuner card manufacturer.&#x20;

> Tvheadend can do nothing if tuners are not installed working properly. If you have problems, most original card manufacturers (but not cheap clone-card manufacturers) have active forums where you can report issues and ask for assistance.

### i2s Tuners

Internal i2s tuners are normally found in Android or Linux set-top box devices with the required drivers and firmware embedded in the OS image that runs on the device. In theory this means the box requires no hardware setup: which is appealing to users. In practice you may need to update the device to the lastest available firmware to ensure best performance, and client software options may be limited to specific pre-installed or embedded versions of popular apps.

> Firmware update options for Android set-top boxes are often limited. If you have problems with internal i2s tuners the original box manufacturer must resolve them.

### USB Tuners

External USB tuners are often cheap, work well, and are well-matched to smaller boards and boxes that lack internal PCI slots. However, most USB tuners need more than 500mA so will need external direct power or an external USB hub that supports higher current loads to work properly. Bandwidth can also be a problem and even fast USB3 ports can experience bandwidth problems with mulitple USB devices chained from a single port (and USB bus).

> Raspberry Pi 0/1/2/3/4 boards internally share USB bus bandwidth with Ethernet. Multiple USB tuner configs and higher-bandwidth HD streams often run into bandwidth issues.

### Network Tuners

External network tuners (SAT>IP devices and similar) cost more than internal PCI/PCIe cards and USB devices but are the firm recommendation of the project team: they are easier to configure and require no fiddling with Linux kernel drivers/firmware to create and maintain a working and reliable system.

> The extra up-front cost is saved over time with easier maintenance, and the devices typically have excellent and long-term support from their manufacturers.
