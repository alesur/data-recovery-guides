# VMware VMDK -Deltas access fix
### Last CHILD data can't be mounted

Connect to VMware Hypervisor via SSH

**cd** (change directory) to your VMDK files, (default **/vmfs/volumes/** etc.)

locate your files structure like:

* HostName.vmdk
* HostName-flat.vmdk
* HostName-ctk.vmdk
* HostName-000001.vmdk  **<- Trouble one**
* HostName-000001-delta.vmdk
* HostName-000001-ctk.vmdk
* 
* 
* 

Run vmkfstools command: `vmkfstools -e -v10 HostName-000001.vmdk` (..and point to your trouble .vmdk)
