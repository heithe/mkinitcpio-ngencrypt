## encrypt-hook

I wrote this mkinitcpio-hook because the original hook in ArchLinux didn't provide a way to unlock a LUKS encrypted device with a detached header. Additionaly with this script you can adjust the flow of the unlock, you get a more detailed error description and the whole process is just a little more interactive.

### Parameter
As in the old encrypt-hook you can pass various options through the boot parameter line. New are `cryptheader` through which you can pass the path to a detached header and `cryptflow` which controls the flow of the script and unlock process.

##### cryptdevice
Specify the encrypted device and the name the unlocked device will be mapped to (same syntax as in ArchLinux current encrypt-hook).  
**Format:** `<device>:<name>`  
  
- **device:** the encrypted device (/dev/* - e.g. /dev/sda or /dev/disk/by-uuid/..)
- **name:** the target mapping name (e.g. luks_main)

##### cryptheader
Specify the external header (new with this hook).  
**Format:** `rootfs:<path-name>`, `<device>:<filesystem-type>:<path-name>` or `<device>:<offset>:<length>`

- **rootfs/device:** the device which contains the header. (rootfs = inside initcpio, /dev/* - e.g. /dev/sdb1)
- **filesystem-type:** the filesystem-type of the device (e.g. ext2)
- **path-name:** the path to the file (/path/to/file - e.g. /header.bin)
- **offset:** the start offset in bytes (e.g. 1024)
- **length:** the byte length to copy starting at offset 

##### cryptkey
Specify the key (same as in ArchLinux current encrypt-hook).   
**Format:** `rootfs:<path-name>`, `<device>:<filesystem-type>:<path-name>` or `<device>:<offset>:<length>`

- **rootfs/device:** the device which contains the key. (rootfs = inside initcpio, /dev/* - e.g. /dev/sdb1)
- **filesystem-type:** the filesystem-type of the device (e.g. ext2)
- **path-name:** the path to the file (/path/to/file - e.g. /key.bin)
- **offset:** the start offset in bytes (e.g. 1024)
- **length:** the byte length to copy starting at offset

##### cryptflow
Specify the flow built with characters which have a special meaning (new with this hook). The uppercase ones are only valid at the end of a flow-string and reapat the action infinite till success.  
**Format:** `<header-flow>:<unlock-flow>` or `<header-flow>:` or `:<unlock-flow>`

- **i**: use internal header. Valid in header-flow
- **e**: use external header (cryptheader). Valid in header-flow
- **k** | **K**: try to use cryptkey. Valid in unlock-flow
- **p** | **P**: prompt to enter passphrase. Valid in unlock-flow
- **f** | **F**: fake prompt to enter passphrase but don't use it to unlock. Valid in unlock-flow
- **m** | **M**: show menu. Valid in both flows 

The default values are `ieM` (header-flow) and `kM` (unlock-flow)  
