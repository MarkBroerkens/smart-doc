# Installation in Proxmox #
1. Download latest [ISO Image](https://sourceforge.net/projects/openmediavault/files/)
1. Upload ISO to proxmox server: Datacenter/pve/local -> ISO -> Upload
1. Create Virtual Machine
 2. [General] Hostname: nas-vm
 2. [OS] ISO Image: openmediavault_6.0.24-amd64.iso
 2. [System]
 2. [Disks] Disk Size 12GB
 2. [CPU] Cores 1
 2. [Momory] 2048
 2. [Network]
3. in VM 
 4. [Options] select use 
 
 => finish (don't select 'start after creation')
 
1.  find the disk by id
 2. ```lsblk -o +MODEL,SERIAL,WWN```
 3. ```ls -l /dev/dev/by-id```

1. attach disk to new vm
 2. ```qm set [VM_ID] -scsi1 /dev/disk/by-id/[FULL_ID_OF_DISK]```

1. start the vm "nas-vm"
2. connect to console
3. select language "english"


enable iommu by setting kernel parameter
pass through sata
enables hdd quality

  
apt install ethtools
ethtool eno1
=> make sure speed is 1000Mb/s
=> if not: replace cable


apt update
apt install pve-kernel-6.2
reboot

=> omv: latest kernel
apt update
apt dist-upgrade
reboot


debug smb version
smbutil statshares -a

