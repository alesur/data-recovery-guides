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

In output result find a line with message like this **Content ID mismatch (parentCID 5ad259c6 != 0cb205b1)**

it point that parentCID doesnt match on that VMDK in this case it is expecting **0cb205b1** but current value is **5ad259c6**

So we need to fix that:

open in any text editor current trouble file **HostName-000001.vmdk** 

we will get file structure like this:
```
# Disk DescriptorFile
version=2
encoding="UTF-8"
CID=d9c73e0a
parentCID=5ad259c6
isNativeSnapshot="no"
createType="vmfsSparse"
parentFileNameHint="HostName.vmdk"
# Extent description
RW 1048576000 VMFSSPARSE "HostName-000001-delta.vmdk"

# The Disk Data Base 
#DDB

ddb.longContentID = "29441754bee7ae3d9cc80a26d9c73e0a"
```

So now we need to change 
parentCID=**5ad259c6** line value to **0cb205b1**

so final result will look like this 

```
# Disk DescriptorFile
version=2
encoding="UTF-8"
CID=d9c73e0a
parentCID=0cb205b1
isNativeSnapshot="no"
createType="vmfsSparse"
parentFileNameHint="HostName.vmdk"
# Extent description
RW 1048576000 VMFSSPARSE "HostName-000001-delta.vmdk"

# The Disk Data Base 
#DDB

ddb.longContentID = "29441754bee7ae3d9cc80a26d9c73e0a"
```

Save the file and close it.

Now rerun check command once more on this file `vmkfstools -e -v10 HostName-000001.vmdk`

it should now pass sucessfully

Now at this point don't mount it to same HOST!
Create new Virtual Machine and mount it to this disk to it to access the data.


