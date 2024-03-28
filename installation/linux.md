# Linux

Tvheadend binary packages can be downloaded from [https://apt.tvheadend.org](https://apt.tvheadend.org) or you can configure a local package repo to install and update from by running the following shell commands:

## DEB Packages (Debian, Ubuntu, RaspiOS)

Run the following shell command to setup a local `apt` repo:

```
curl -1sLf 'https://dl.cloudsmith.io/public/tvheadend/tvheadend/setup.deb.sh' | sudo -E bash
```

## RPM Packages (Fedora, RedHat)

Run the following shell command to setup a local `dnf` or `yum` repo:

```
curl -1sLf 'https://dl.cloudsmith.io/public/tvheadend/tvheadend/setup.rpm.sh' | sudo -E bash
```

> Tvheadend aims to provide installable packages for as long as possible to extend the usable life of server and tuner hardware. In practice this means if we can still automate regular build testing for popular distributions and versions we will have binaries available.

## Source Code

Please refer to [development documentation on compiling Tvheadend from source](../development/compiling.md)
