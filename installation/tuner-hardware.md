# Tuner Hardware

Before you install Tvheadend software you need to have a working tuner device. There are broadly four types of Tuner device that Tvheadend can use:

* Internal PCI/PCIe tuners
* Internal i2s tuners
* External USB tuners that you plug-in
* Network tuners you connect-to over Ethernet

### PCI/PCIe Tuners

Internal PCI/PCIe tuner cards require support for the tuner in the host OS. How to install drivers and firmware is beyond the scope of this guide so please follow the recommendations and instructions of the tuner card manufacturer. Please be mindful that Tvheadend can do nothing if the tuners are not working properly. If you have problems, most original card manufacturers (but not cheap clone-card manufacturers) have active forums where you can report issues and ask for assistance.

### i2s Tuners

Internal i2s tuners are normally found in Android or Linux set-top box devices with the required drivers and firmware embedded in the OS image that runs on the device. In theory this means the box requires no hardware setup. In practice you may need to update the device to the lastest available firmware to ensure best performance. If you have problems, these need to be addressed to the box manufacturer.

### USB Tuners

External USB tuners are often cheap, work well, and are well-matched to physically-smaller boards and boxes that lack internal PCI slots. Most USB tuners need more than 500mA so will need external direct power or an external USB hub that supports higher current loads to work properly. Bandwidth can also be a problem and even fast USB3 ports can experience bandwidth problems with mulitple USB devices connected to a single port (and USB bus) on the main board. This is particularly true with Raspberry Pi 0/1/2/3/4 boards that internally share USB bus bandwidth with the Ethernet port. Multi-tuner configs often cause platforms to struggle or report errors with higher-bandwidth HD streams.

### Network Tuners

External network tuners (SAT>IP devices and similar) generally cost more than internal PCI/PCIe cards and USB devices but are the recommendation of the project team: they are easier to configure and require no fiddling with Linux kernel drivers/firmware to get a working and reliable system. The extra that you pay up-front is saved over the long-term with easier maintenance, and the devices typically have excellent support from their manufacturers. Separating the back-end tuner device from the front-end player also allows easier and lower-cost player upgrades.
