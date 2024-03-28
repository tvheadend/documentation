# Requirements

Tvheadend has physical and software considerations:

* Intel compatible (i386/x86\_64) or ARM (arm/aarch64) CPU
* Minimum 1GB RAM
* Minimum 1GB storage for app/configuration data
* Large capacity storage for recordings
* Tuner device(s) with suitable power and connectivity
* Operating System that supports the tuners

## Server Hardware

Tvheadend runs on Intel compatible i386/x86\_64 CPUs and ARM SoC arm/aarch64 processor. It will need a minimum of 1GB disk space for application binaries and configuration data, although the total required will depend on the number and type of tuners you have, the number of channels received, the choice of programme guide data, etc.

Tvheadend is intended to be lightweight and will run in less than 1GB RAM on low-powered NAS and Single Board Computer devices. Many users run Tvheadend on older Raspberry Pi boards with 512MB physical RAM and perhaps only 256MB free memory: although more is sensible and will result in a better user experience. Note that transcoding is CPU intensive and this feature runs best on powerful multi-core systems.

Recordings consume large amounts of disk storage. SD quality MPEG2 video will typically use 1GB of disk per-hour, while higher-bitrate HD quality H264 will often consume 5GB+ per-hour. Most users who use Tvheadend to record will plan and provision their Tvheadend server with large capacity local HDD or remote-mounted NAS storage.

You will need one or more tuner devices to receive Cable, Satellite, or Terrestrial broadcast sources, or IP sources. Tuner options are [discussed in more detail here](tuners.md).

## Server Software

Tvheadend is designed for use on Linux and we provide general purpose binary pacakges and Docker containers that can be used with a large range of Linux distributions and distro versions:

* Debian derivatives (Debian, Raspberry Pi, Ubuntu, Mint, etc.)
* RedHat derivatives (Fedora, RHEL)

> Tvheadend is available as an installable add-on for the Kodi focussed distro LibreELEC

Users needing a more specific combination of Tvheadend capabilities can also compile their own binaries or build containers from our public source code.

## Connectivity

Internet access is essential for installation and maintenance of Tvheadend, but is not essential during use. Tvheadend needs an accurate clock for EPG timers to work, but this can be synchronised from the broadcast signal if `ntp` services are not available. Most broadcast services also provide some form of EPG data "over the air" alongside the broadcast signal.&#x20;

Server hardware and perhaps tuner hardware will require power and physical access to a broadcast feed from aerial, dish, or cable; or via the LAN if you are using SAT>IP, network tuners, or IP sources.&#x20;

## Architecture

Tvheadend can be run in a single-host configuration where the Tvheadend server runs on the same host as client software, e.g. Kodi, and with media recordings stored locally on the same disk. This is common with compact or lower-budget Tvheadend setups with a smaller number of tuners.

In a multi-host configuration Tvheadend runs on a dedicated server, with client software on a separate device. This allows a compact client device to sit alongside the TV while the Tvheadend server (usually a larger device with multiple tuners) is located somewhere else with convenient access to the physical aerial, dish or coax cables that provide input to your tuners
