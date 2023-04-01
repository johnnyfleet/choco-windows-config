# Windows 10 Guest VM notes
This information outlines the settings I've used to successfully set up the guest VM for Windows. 

## First Install
When creating the VM for the first time, set the following up using VirtManager. 

### CPU Topologies
Copy host configuration
Topology
Sockets 1
Cores 4
Threads 3

### Memory
Set to `8192 MB`


### Configure Disk
Ultimately we want to have as Virtio drivers, but needs the drivers. 
Start with Sata

Install

## After installation

### Virtio drivers
Get the latest ISO for the [virtio drivers here](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/?C=M;O=D)

Add them in virt-manager as a cd. 

### Switch to Virtio disk & NIC
Go to safeboot mode `bcdedit /set {default} safeboot network`
Shutdown
Add a second disk as Virtio
Switch to virtio for network card too
Boot
Install drivers - from the Virtio guest iso
Switch back to normal boot `bcdedit /deletevalue {default} safeboot`
Shutdown
Remove 2nd driver
Switch boot drive to Virtio

### NIC
Make sure Virtio set as drivers for nic. 

### Guest Utils
You may also need to install Virtio guest utils. You can get from the same location [same location here](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/?C=M;O=D).

## Post Virtio setup
Install [spice-guest-tools](https://www.spice-space.org/download.html) for windows on guest. 

Shutdown

### Video
Configure video to be QXL
Ensure spice server added: Spice server
Ensure there is a spice channel (to enable copy/paste)

Specific XML to sort scaling. Add the following to the Video QXL xml tab (replacing what is there)
``` xml
<video>
  <model type="qxl" ram="131072" vram="131072" vgamem="32768" heads="1" primary="yes"/>
  <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x0"/>
</video>
```
## Windows guest
Install virtio tools (from iso)
Install spice client tools
Install chocolatey
