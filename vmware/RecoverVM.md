# VMware VMDK -Deltas access fix
### Last CHILD data can't be mounted

Connect to VMware Hypervisor via SSH

**cd** (change directory) to your VMDK files, (default **/vmfs/volumes/** etc.)

locate your disk structure files like:

*HostName.vmdk
*HostName-flat.vmdk
*HostName-ctk.vmdk
*HostName-000001.vmdk
*HostName-000001-delta.vmdk
*HostName-000001-ctk.vmdk
*.
*.
*.



