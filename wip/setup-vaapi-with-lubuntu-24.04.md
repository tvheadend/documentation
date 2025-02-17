---
description: Setup VAAPI on x86 (64 bits) system from scrach
---

# Setup VAAPI with Lubuntu 24.04

**HW**:&#x20;

Lenovo ThinkCentre M720q element with i5-9500T

download ISO LUBUNTU 24.04:&#x20;

[https://www.cdimage.ubuntu.com/lubuntu/releases/24.04/release/lubuntu-24.04.1-desktop-amd64.iso](https://www.cdimage.ubuntu.com/lubuntu/releases/24.04/release/lubuntu-24.04.1-desktop-amd64.iso)

flash ISO to USB 32G using rufus-3.21 Note: make sure you plug the USB in USB2.0 socket (black).

Install Lubuntu to PC with default settings; connect also to internet.

Update some settings: Preference / LXQt setting / Power Management: Idle --> uncheck Enable Idleness Watcher : Close Preference / LXQt setting / Monitor Settings: 1280 x 720 : Save : Yes Preference / LXQt setting / LXQt Configuration Center : Openbox Settings --> Desktops : Number of desktops : 1 Preference / Screen Saver : Mode : Disable screen saver

**Install SSH**

open: System Tools / QTerminal

`sudo apt update sudo apt install ssh`

check status

`systemctl status ssh`

if is not working&#x20;

`sudo systemctl enable ssh`

and&#x20;

`sudo systemctl start ssh`

connect over SSH to continue:

Update to latest software

`sudo apt update`&#x20;

`sudo apt upgrade`&#x20;

`sudo reboot sudo`&#x20;

`apt autoremove --purge`

_ukn@ukn-lenovo:\~$ uname -a Linux ukn-lenovo 6.8.0-52-generic #53-Ubuntu SMP PREEMPT\_DYNAMIC Sat Jan 11 00:06:25 UTC 2025 x86\_64 x86\_64 x86\_64 GNU/Linux_

install OneVPL

Before you start let's check that GPU is supported in MSDK or OneVPL.

`sudo lspci -nn | grep -e VGA`

_ukn@ukn-lenovo:\~$ sudo lspci -nn | grep -e VGA 00:02.0 VGA compatible controller \[0300]: Intel Corporation CoffeeLake-S GT2 \[UHD Graphics 630] \[8086:**3e92**]_

you can go on: https://dgpu-docs.intel.com/devices/hardware-table.html and search for: "**3e92**" (check after \[8086:\*\*\*\*]). and see is: Intel® UHD Graphics 630 --> Gen 9 --> Coffee Lake

install vainfo to check what profiles are available

`sudo apt install vainfo`

`sudo vainfo`

$################### log output ####################&#x20;

_ukn@ukn-lenovo:\~$ sudo vainfo error: XDG\_RUNTIME\_DIR is invalid or not set in the environment. error: can't connect to X server! libva info: VA-API version 1.20.0 libva info: Trying to open /usr/lib/x86\_64-linux-gnu/dri/iHD\_drv\_video.so libva info: Found init function \_\_vaDriverInit\_1\_20 libva info: va\_openDriver() returns 0 vainfo: VA-API version: 1.20 (libva 2.12.0) vainfo: Driver version: Intel iHD driver for Intel(R) Gen Graphics - 24.1.0 () vainfo: Supported profile and entrypoints VAProfileMPEG2Simple : VAEntrypointVLD VAProfileMPEG2Main : VAEntrypointVLD VAProfileH264Main : VAEntrypointVLD VAProfileH264Main : VAEntrypointEncSliceLP VAProfileH264High : VAEntrypointVLD VAProfileH264High : VAEntrypointEncSliceLP VAProfileJPEGBaseline : VAEntrypointVLD VAProfileJPEGBaseline : VAEntrypointEncPicture VAProfileH264ConstrainedBaseline: VAEntrypointVLD VAProfileH264ConstrainedBaseline: VAEntrypointEncSliceLP VAProfileVP8Version0\_3 : VAEntrypointVLD VAProfileHEVCMain : VAEntrypointVLD VAProfileHEVCMain10 : VAEntrypointVLD VAProfileVP9Profile0 : VAEntrypointVLD VAProfileVP9Profile2 : VAEntrypointVLD_ $########################################################

instructions:&#x20;

[https://dgpu-docs.intel.com/driver/client/overview.html#installing-client-gpus-on-ubuntu-desktop-24-04-lts](https://dgpu-docs.intel.com/driver/client/overview.html#installing-client-gpus-on-ubuntu-desktop-24-04-lts)

**Install gpu driver**

Install the Intel graphics GPG public key

`wget -qO - https://repositories.intel.com/gpu/intel-graphics.key |`\
`sudo gpg --yes --dearmor --output /usr/share/keyrings/intel-graphics.gpg`

Configure the repositories.intel.com package repository

`echo "deb [arch=amd64,i386 signed-by=/usr/share/keyrings/intel-graphics.gpg] https://repositories.intel.com/gpu/ubuntu noble client" |`\
`sudo tee /etc/apt/sources.list.d/intel-gpu-noble.list`

Update the package repository meta-data

`sudo apt update`

Install the compute-related packages

`sudo apt-get install -y libze-intel-gpu1 libze1 intel-opencl-icd clinfo intel-gsc`

Install the media-related packages

`sudo apt-get install -y intel-media-va-driver-non-free libmfx1 libmfx-gen1 libvpl2 libvpl-tools libva-glx2 va-driver-all`

Update to latest software:

`sudo apt update sudo apt upgrade sudo reboot sudo apt autoremove --purge`

`sudo vainfo`

$################### log output ####################&#x20;

_ukn@ukn-lenovo:\~$ sudo vainfo Trying display: wayland error: XDG\_RUNTIME\_DIR is invalid or not set in the environment. Trying display: x11 error: can't connect to X server! Trying display: drm libva info: VA-API version 1.22.0 libva info: Trying to open /usr/lib/x86\_64-linux-gnu/dri/iHD\_drv\_video.so libva info: Found init function \_\_vaDriverInit\_1\_22 libva info: va\_openDriver() returns 0 vainfo: VA-API version: 1.22 (libva 2.22.0) vainfo: Driver version: Intel iHD driver for Intel(R) Gen Graphics - 24.3.4 () vainfo: Supported profile and entrypoints VAProfileNone : VAEntrypointVideoProc VAProfileNone : VAEntrypointStats VAProfileMPEG2Simple : VAEntrypointVLD VAProfileMPEG2Simple : VAEntrypointEncSlice VAProfileMPEG2Main : VAEntrypointVLD VAProfileMPEG2Main : VAEntrypointEncSlice VAProfileH264Main : VAEntrypointVLD VAProfileH264Main : VAEntrypointEncSlice VAProfileH264Main : VAEntrypointFEI VAProfileH264Main : VAEntrypointEncSliceLP VAProfileH264High : VAEntrypointVLD VAProfileH264High : VAEntrypointEncSlice VAProfileH264High : VAEntrypointFEI VAProfileH264High : VAEntrypointEncSliceLP VAProfileVC1Simple : VAEntrypointVLD VAProfileVC1Main : VAEntrypointVLD VAProfileVC1Advanced : VAEntrypointVLD VAProfileJPEGBaseline : VAEntrypointVLD VAProfileJPEGBaseline : VAEntrypointEncPicture VAProfileH264ConstrainedBaseline: VAEntrypointVLD VAProfileH264ConstrainedBaseline: VAEntrypointEncSlice VAProfileH264ConstrainedBaseline: VAEntrypointFEI VAProfileH264ConstrainedBaseline: VAEntrypointEncSliceLP VAProfileVP8Version0\_3 : VAEntrypointVLD VAProfileVP8Version0\_3 : VAEntrypointEncSlice VAProfileHEVCMain : VAEntrypointVLD VAProfileHEVCMain : VAEntrypointEncSlice VAProfileHEVCMain : VAEntrypointFEI VAProfileHEVCMain10 : VAEntrypointVLD VAProfileHEVCMain10 : VAEntrypointEncSlice VAProfileVP9Profile0 : VAEntrypointVLD VAProfileVP9Profile2 : VAEntrypointVLD_ $########################################################

Install developer packages:

`sudo apt-get install -y libigc-dev intel-igc-cm libigdfcl-dev libigfxcmrt-dev level-zero-dev`

**Configuring permissions for render:**

To access GPU capabilities, a user needs to have the correct permissions. The following will list the group assigned ownership of the render nodes, and list the groups the active user is a member of:

`stat -c "%G" /dev/dri/render*`

&#x20;\--> render

_ukn@ukn-lenovo:\~$ stat -c "%G" /dev/dri/render\*_&#x20;

_render_

`groups ${USER}`

_ukn@ukn-lenovo:\~$ groups ${USER} ukn : ukn adm cdrom sudo dip plugdev lpadmin sambashare_

My user doesn't have access because is not art of 'render' Now we add my user (ukn) to group (render)

`sudo gpasswd -a ${USER} render`

_ukn@ukn-lenovo:\~$ sudo gpasswd -a ${USER} render Adding user ukn to group render_

`newgrp render`

verify:&#x20;

`groups ${USER}`

_ukn@ukn-lenovo:\~$ groups ${USER} ukn : ukn adm cdrom sudo dip plugdev render lpadmin sambashare_

Now we see user is part of **render**.

`sudo vainfo`

$################### log output ####################&#x20;

_ukn@ukn-lenovo:\~$ sudo vainfo Trying display: wayland error: XDG\_RUNTIME\_DIR is invalid or not set in the environment. Trying display: x11 error: can't connect to X server! Trying display: drm libva info: VA-API version 1.22.0 libva info: Trying to open /usr/lib/x86\_64-linux-gnu/dri/iHD\_drv\_video.so libva info: Found init function \_\_vaDriverInit\_1\_22 libva info: va\_openDriver() returns 0 vainfo: VA-API version: 1.22 (libva 2.22.0) vainfo: Driver version: Intel iHD driver for Intel(R) Gen Graphics - 24.3.4 () vainfo: Supported profile and entrypoints VAProfileNone : VAEntrypointVideoProc VAProfileNone : VAEntrypointStats VAProfileMPEG2Simple : VAEntrypointVLD VAProfileMPEG2Simple : VAEntrypointEncSlice VAProfileMPEG2Main : VAEntrypointVLD VAProfileMPEG2Main : VAEntrypointEncSlice VAProfileH264Main : VAEntrypointVLD VAProfileH264Main : VAEntrypointEncSlice VAProfileH264Main : VAEntrypointFEI VAProfileH264Main : VAEntrypointEncSliceLP VAProfileH264High : VAEntrypointVLD VAProfileH264High : VAEntrypointEncSlice VAProfileH264High : VAEntrypointFEI VAProfileH264High : VAEntrypointEncSliceLP VAProfileVC1Simple : VAEntrypointVLD VAProfileVC1Main : VAEntrypointVLD VAProfileVC1Advanced : VAEntrypointVLD VAProfileJPEGBaseline : VAEntrypointVLD VAProfileJPEGBaseline : VAEntrypointEncPicture VAProfileH264ConstrainedBaseline: VAEntrypointVLD VAProfileH264ConstrainedBaseline: VAEntrypointEncSlice VAProfileH264ConstrainedBaseline: VAEntrypointFEI VAProfileH264ConstrainedBaseline: VAEntrypointEncSliceLP VAProfileVP8Version0\_3 : VAEntrypointVLD VAProfileVP8Version0\_3 : VAEntrypointEncSlice VAProfileHEVCMain : VAEntrypointVLD VAProfileHEVCMain : VAEntrypointEncSlice VAProfileHEVCMain : VAEntrypointFEI VAProfileHEVCMain10 : VAEntrypointVLD VAProfileHEVCMain10 : VAEntrypointEncSlice VAProfileVP9Profile0 : VAEntrypointVLD VAProfileVP9Profile2 : VAEntrypointVLD_ $########################################################

the data format is: CODEC/profile : Encoder/Decoder

```
  VAProfileH264High               : VAEntrypointVLD
  VAProfileH264High               : VAEntrypointEncSlice
  VAProfileH264High               : VAEntrypointFEI
  VAProfileH264High               : VAEntrypointEncSliceLP
```

This is: H264, Profile high with decoder (**VAEntrypointVLD**) , Encoder (**VAEntrypointEncSlice**) and LowPower encoder (**VAEntrypointEncSliceLP**) Is important to identify if your GPU has this low power (LP) codecs available. In my case I have low power for: H264 profiles Main, High and Constrained

`sudo apt update`&#x20;

`sudo apt upgrade`

Install gpu tools (required to check the work load on GPU):&#x20;

`sudo apt install intel-gpu-tools`

Intel GPU:&#x20;

`sudo apt install i965-va-driver-shaders`

Enable GUC firmware (this is a must for encoding with low power codec):

we need to generate a file: /etc/modprobe.d/i915.conf&#x20;

with the text (only one line) "options i915 enable\_guc=1"

`echo -e "options i915 enable_guc=1" | sudo tee -a /etc/modprobe.d/i915.conf`

`sudo update-initramfs -k all -u sudo update-grub`

`sudo reboot`

Verify GuC was enabled:&#x20;

`sudo dmesg | grep guc`

_ukn@ukn-lenovo:\~$ sudo dmesg | grep guc \[ 4.331207] Setting dangerous option enable\_guc - tainting kernel \[ 4.343052] i915 0000:00:02.0: \[drm] GT0: Incompatible option enable\_guc=1 - GuC submission is N/A \[ 4.726395] i915 0000:00:02.0: \[drm] GT0: GuC firmware i915/kbl\_guc\_70.1.1.bin version 70.1.1_

In this case we see that GuC is not available (so bit 1 is not useful).

delete the old file:&#x20;

`sudo rm /etc/modprobe.d/i915.conf`

`echo -e "options i915 enable_guc=2" | sudo tee -a /etc/modprobe.d/i915.conf`

`sudo update-initramfs -k all -u`

`sudo update-grub`

`sudo reboot`

Verify GuC was enabled:&#x20;

`sudo dmesg | grep guc`

_ukn@ukn-lenovo:\~$ sudo dmesg | grep guc \[ 2.142048] Setting dangerous option enable\_guc - tainting kernel \[ 2.502650] i915 0000:00:02.0: \[drm] GT0: GuC firmware i915/kbl\_guc\_70.1.1.bin version 70.1.1_

This setting was accepted; bit 2 was able to enable GuC

-> it sounds scary 'dangerous option' ... but is fine.

this is required to scan channels later on:&#x20;

`sudo apt update`

`sudo apt install w-scan`

`sudo apt upgrade`

clean up:

`sudo apt autoremove --purge`

## **Compile tvheadend**

`cd ~`

`git clone https://github.com/tvheadend/tvheadend.git`

`sudo apt update`

`sudo apt install cmake gettext libssl-dev liburiparser-dev libavahi-client-dev libdvbcsa-dev libva-dev debhelper`

`sudo apt install python-is-python3`

`cd tvheadend`

`./configure`

$################### log output ####################&#x20;

_ukn@ukn-lenovo:\~/tvheadend$ ./configure Checking support/features checking for cc execinfo.h ... ok checking for cc -mmmx ... ok checking for cc -msse2 ... ok checking for cc -Wunused-result ... ok checking for cc -fstack-protector ... ok checking for cc -fstack-protector-strong ... ok checking for cc -fstack-check ... ok checking for cc -fPIE ... ok checking for cc strlcat ... ok checking for cc strlcpy ... ok checking for cc fdatasync ... ok checking for cc getloadavg ... ok checking for cc atomic32 ... ok checking for cc atomic64 ... ok checking for cc atomic\_time\_t ... ok checking for cc atomic\_ptr ... ok checking for cc bitops64 ... ok checking for cc lockowner ... ok checking for cc qsort\_r ... ok checking for cc time\_ld ... ok checking for cc time\_lld ... fail ^ using time\_t format 'ld' checking for cc stime ... fail checking for cc gmtoff ... ok checking for cc recvmmsg ... ok checking for cc sendmmsg ... ok checking for cc gnu\_libiconv ... fail checking for cc libiconv ... fail ^ using build-in glibc iconv routines checking for cc ifnames ... ok checking for cc cclang\_threadsan ... fail checking for py module gzip ... ok checking for pkg-config ... ok checking for xgettext ... ok checking for msgmerge ... ok checking for gzip ... ok checking for bzip2 ... ok checking for pkg openssl ... ok (detected 3.0.13) checking for cc linux/dvb/version.h ... ok checking for pkg zlib ... ok (detected 1.3) checking for pkg libpcre2-8 ... ok (detected 10.42) checking for pkg liburiparser ... ok (detected 0.9.7) checking for pkg avahi-client ... ok (detected 0.8) checking for cmake ... ok checking for cc -lstdc++ ... ok checking for pkg libva >=0.38.0 ... ok (detected 1.22.0) checking for pkg libva-drm >=0.38.0 ... ok (detected 1.22.0) checking for cc sys/inotify.h ... ok checking for cc inotify\_init1 ... ok checking for cc dvbcsa/dvbcsa.h ... ok checking for cc -ldvbcsa ... ok fetching dvb-scan files ... ok checking for cc epoll\_create1 ... ok checking for pkg dbus-1 ... ok (detected 1.14.10)_

_Compiler: Using C compiler: cc Using LD flags: -ldvbcsa Build for arch: x86\_64_

_Binaries: Using PYTHON: python Using GZIP: gzip Using BZIP2: bzip2_

_Options: pie yes ccdebug no cardclient yes cwc yes cccam yes capmt yes constcw yes linuxdvb yes satip\_server yes satip\_client yes hdhomerun\_client yes hdhomerun\_server yes hdhomerun\_static yes iptv yes tsfile yes dvbscan yes timeshift yes trace yes avahi yes zlib yes libav yes ffmpeg\_static yes libx264 yes libx264\_static yes libx265 yes libx265\_static yes libvpx yes libvpx\_static yes libtheora yes libtheora\_static yes libvorbis yes libvorbis\_static yes libfdkaac no libfdkaac\_static no libopus yes libopus\_static yes nvenc no vaapi yes mmal no omx no inotify yes epoll yes pcre no pcre2 yes uriparser yes ccache no tvhcsa yes bundle no pngquant no kqueue no dbus\_1 yes android no gtimer\_check no slow\_memoryinfo no libsystemd\_daemon no pcloud\_cache yes ddci yes cclang\_threadsan no gperftools no execinfo yes mmx yes sse2 yes W\_unused\_result yes f\_stack\_protector yes f\_stack\_protector\_strong yes f\_stack\_check yes f\_PIE yes strlcat yes strlcpy yes fdatasync yes getloadavg yes atomic32 yes atomic64 yes atomic\_time\_t yes atomic\_ptr yes bitops64 yes lockowner yes qsort\_r yes time\_ld yes gmtoff yes recvmmsg yes sendmmsg yes ifnames yes py\_gzip yes bin\_pkg\_config yes bin\_xgettext yes bin\_msgmerge yes bin\_gzip yes bin\_bzip2 yes ssl yes linuxdvbapi yes linuxdvb\_ca yes upnp yes bin\_cmake yes stdcpp yes libogg\_static yes hwaccels yes inotify\_h yes inotify\_init1 yes dvbcsa yes epoll\_create1 yes mpegts yes mpegts\_dvb yes_

_Packages: openssl 3.0.13 zlib 1.3 libpcre2-8 10.42 liburiparser 0.9.7 avahi-client 0.8 libva 1.22.0 libva-drm 1.22.0 dbus-1 1.14.10_

_Installation paths: Prefix: /usr/local Binaries: ${prefix}/bin Libraries: ${prefix}/lib Data files: ${prefix}/share Man pages: ${datadir}/man_

_Final Binary: /home/ukn/tvheadend/build.linux/tvheadend_

_Tvheadend Data Directory: /usr/local/share/tvheadend_&#x20;

$################### log output end ####################

**Build tvheadend:**&#x20;

`./Autobuild.sh`

$################### log output ####################&#x20;

_...................................................................................._

_dpkg-deb: building package 'tvheadend-dbg' in '../tvheadend-dbg\_4.3-2375_~~_g653bd0400_~~_noble\_amd64.deb'. dpkg-deb: building package 'tvheadend' in '../tvheadend\_4.3-2375_~~_g653bd0400_~~_noble\_amd64.deb'. make\[1]: Leaving directory '/home/ukn/tvheadend' dpkg-genbuildinfo --build=binary -O../tvheadend\_4.3-2375_~~_g653bd0400_~~_noble\_amd64.buildinfo dpkg-genchanges --build=binary -O../tvheadend\_4.3-2375_~~_g653bd0400_~~_noble\_amd64.changes dpkg-genchanges: info: binary-only upload (no source code included) dpkg-source --after-build . dpkg-buildpackage: info: binary-only upload (no source included)_&#x20;

$################### log output end ####################

From this last log you need to copy the file name starting "'**tvheadend' in '../tvheadend\_4.3...**" (in your case will have a different number after '4.3-') In my case is: **tvheadend-dbg\_4.3-2375**~~**g653bd0400**~~**noble\_amd64.deb**

`cd ..`

Install tvheadend:

`sudo dpkg -i tvheadend_4.3-2375`~~`g653bd0400`~~`noble_amd64.deb`

We have to add also user hts to render (or your group that has access to GPU):

`sudo gpasswd -a hts render`

`newgrp render`

verify:&#x20;

`groups hts`

_ukn@ukn-lenovo:\~$ groups hts hts : hts render_

Now we see user is part of render.

restart:&#x20;

`sudo reboot`

**Setup VAAPI profile:**

in browser

http://\[IP\_NUMBER]:9981

Setup GPU transcoding:&#x20;

\--> make sure you have **Expert** settings selected&#x20;

\[browser menus]:&#x20;

Configuration / Stream / Codec Profiles --> Add&#x20;

Codec: h264\_vaapi

Name: h264\_vaapi

Description: ....&#x20;

Deinterlace: checked (very important)&#x20;

Height: 0&#x20;

Hardware acceleration: checked (very important)&#x20;

Device name: i915 v.1.6.0 (/dev/dri/renderD128) (very important)&#x20;

Bitrate: 0&#x20;

Buffer factor: 3 Rate&#x20;

control: 1 (CQP)&#x20;

Constant QP: 27&#x20;

Ignore B-Frames: 0&#x20;

Quality: 1

Press Create button.

\[browser menus]:&#x20;

Configuration / Stream / Stream Profiles --> Add&#x20;

Type: Transcode/av-lib&#x20;

Profile name: h264&#x20;

Enabled: checked&#x20;

Default: checked&#x20;

Comment: ...&#x20;

Data timeout: 5&#x20;

Default priority: Normal&#x20;

Force priority: 0&#x20;

Restart on error: checked&#x20;

Continue if descrambling fails: checked&#x20;

Descrembling timeout: 2000&#x20;

Switch to another service: checked&#x20;

Preferred services vide type: None&#x20;

Container: Matroska&#x20;

Video codec profile: h264\_vaapi (very important)&#x20;

Source video codec: EMPTY&#x20;

Audio codec profile: web-aac&#x20;

Source audio codec: EMPTY&#x20;

Subtitle codec profile: Copy&#x20;

Source subtitle codec: EMPTY

Press **Create** button.

Note: all 'very important' are required.

Now you are ready to test: open one stream with tvh server and check the Tvheadend log:&#x20;

_2022-12-09 10:53:37.821 transcode: 0001: 01:MPEG2VIDEO: ==> Using profile h264\_vaapi 2022-12-09 10:53:37.822 transcode: 0001: 02:AC3: ==> Using profile webtv-aac_

To confirm you are using GPU for trancoding you need to send:

`sudo intel_gpu_top`

When you don't have any streams open you will see all numbers: 0; after you open streams you should see values non-zero in: Render/3D , Video and VideoEnhance.
