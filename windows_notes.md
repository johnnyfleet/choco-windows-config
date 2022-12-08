# Windows 10 Vm notes

## CPU Topologies
Copy host configuration
Topology
Sockers 1
Cores 4
Threads 3

## Memory
8192 MB


## Virtio Disk
Start with Sata
Go to safeboot mode `bcdedit /set {default} safeboot network`
Shutdown
Add a second disk
(Add NIC virtio)
Boot
Install drivers
Switch back to normal boot `bcdedit /deletevalue {default} safeboot`
Shutdown
Remove 2nd driver
Switch boot drive to Virtio

## NIC
Virtio

## Video
QXL
Spize server

Specific XML to sort scaling
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
