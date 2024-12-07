# Virtualisation - Proxmox

Tvheadend can be installed either as a VM (linux guest OS) or as an LXC container.

The TV tuner must be passed through to the VM/container



## Proxmox VM - Debian

* Host OS: Proxmox 8.3.1
* Guest OS: Debian 12.8 (bookworm) amd64

Note: the TV tuner is passed through from the Host to Guest (PCI or USB pass through) - installation of the tuner is done on the VM/Guest OS

1. Install Debian as a VM with at least the minimum requirements - command-line only installs (without desktop environment) recommended to minimise resource usage
2. Update Debian to latest package versions with&#x20;

```sh
# apt update
# apt upgrade
```

3. Install Curl package to allow set up of Apt repository

```bash
# apt install curl
```

4. Set up Apt repository - for DEB packages using Curl

```bash
# curl -1sLf 'https://dl.cloudsmith.io/public/tvheadend/tvheadend/setup.deb.sh' | sudo -E bash
```

5. Update Apt package list

<pre class="language-bash"><code class="lang-bash"><strong># apt update
</strong></code></pre>

6. Install Tvheadend

```bash
# apt install tvheadend
```

7. Passthrough TV tuner hardware to VM guest OS\
   (this can be done through the proxmox web GUI)
8. Install the TV tuner on the VM guest OS
9. Access the Tvheadend web configuration interface at:\
   https://\<yourtvhserverip>:9981
10. Continue setup/configuration (in next section)



## Proxmox  LXC - Debian

* Host OS: Proxmox 8.3.1
* Container Template (Guest OS): Debian 12 standard (12.2-1-amd64)

Note: the TV tuner is first installed on the Host OS (Proxmox) and then passed through to the LXC container (see below) - the pass through must be the whole enumerated device in /dev/dvb/adapter0/\<files> and not /dev/usb or /dev/pci as the LXC does not have the kernel modules to install the device.

1. Set up an LXC container with at least the minimum requirements\
   The Debian 12 standard LXC template can be downloaded from the Proxmox web GUI
2. Update Debian packages to latest version\
   Note: a lot of packages will be updated as the Proxmox LXC template is quite old

```bash
# apt update
# apt upgrade
```

3. Install Curl package to allow set up of Apt repository

```bash
# apt install curl
```

4. Set up Apt repository - for DEB packages using Curl

```bash
# curl -1sLf 'https://dl.cloudsmith.io/public/tvheadend/tvheadend/setup.deb.sh' | sudo -E bash
```

5. Update Apt package list

<pre class="language-bash"><code class="lang-bash"><strong># apt update
</strong></code></pre>

6. Install Tvheadend

```bash
 # apt install tvheadend
```

7. Passthrough TV tuner hardware to VM guest OS\
   \
   Passthrough all the devices files under /dev/dvb/adapter0/\
   Set UID=0 (root) and GID=44 (video) for all devices\
   \
   \- GUI method:\
   From web GUI, nagivate to container, resources, add, pass through - add the devices:\
   \
   /dev/dvb/adapter0/demux0\
   /dev/dvb/adapter0/dvr0\
   /dev/dvb/adapter0/frontend0\
   /dev/dvb/adapter0/net0\
   \
   OR\
   \
   \- Command-line method:\
   Manually edit the LXC config file at:  /etc/pve/lxc/\<containerid>.conf\
   Add in the following lines\
   &#x20;\
   /dev/dvb/adapter0/demux0,gid=44,uid=0\
   /dev/dvb/adapter0/dvr0,gid=44,uid=0\
   /dev/dvb/adapter0/frontend0,gid=44,uid=0\
   /dev/dvb/adapter0/net0,gid=44,uid=0\

8. Restart LXC container to allow passthrough
9. Access the Tvheadend web configuration interface at:\
   https://\<yourtvhserverip>:9981
10. Continue setup/configuration (in next section)



