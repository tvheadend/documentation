# Downloads

Tvheadend is compiled for a broad range of Linux distributions and CPU architectures and we aim to provide installable packages for as long as possible. In practice this means any distro/arch combo that we can still automate regular build testing for.&#x20;

### **Official Sources**

Binaries can be downloaded from [https://apt.tvheadend.org](https://apt.tvheadend.org) or you can configure a local repo to install and update Tvheadend from by running the following shell commands:

#### DEB Packages (Debian, Ubuntu, RaspiOS)

```
curl -1sLf 'https://dl.cloudsmith.io/public/tvheadend/tvheadend/setup.deb.sh' | sudo -E bash
```

#### RPM Packages (Fedora, RedHat)

```
curl -1sLf 'https://dl.cloudsmith.io/public/tvheadend/tvheadend/setup.rpm.sh' | sudo -E bash
```

### Community Sources

These are alternative binaries or packages provided by third-parties. The project does not provide direct support for them.

#### QNAP NAS devices

{% embed url="https://www.myqnap.org/product/tvheadend" %}

#### Synology NAS devices

{% embed url="https://synocommunity.com/package/tvheadend" %}

## Source Code

Please refer to [development documentation on compiling Tvheadend from source](../development/compiling.md)
