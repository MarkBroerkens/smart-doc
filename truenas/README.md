

# TrueNAS on Proxmox
## Why ?
* ZFS for Snapshots
* UI for NAS config
* no dedecated hardware
* TrueNAS CORE because we use Proxmox for VMs

## Prerequisit
enable iommu by setting kernel parameter
(required for SATA Co ntroller pass through)

## Installation
* download iso of TrueNAS CORE: https://www.truenas.com/truenas-core/
* upload to Proxmox 
 * local -> ISO Images -> Upload
* Create Virtual Machine
  * consider [hardware requirements](https://www.truenas.com/docs/core/gettingstarted/corehardwareguide/)
  * [General] Hostname: truenas
  * [OS] ISO Image: TrueNAS-13.0-U5.1.iso
  * [System]
  * [Disks] Disk Size: 32GB (min 16GB), SSD Emulation: true
  * [CPU] Cores: 2 (min 2), Type: host
  * [Momory] 16384 (min 8GB), Balooning Device: false
  * [Network]
  * => finish (don't select 'start after creation')
  
* in VM Settings
 * [Hardware] Add -> PCI Device (SATÀ Controller, all functions: true) 
 * [Options] use local time for RTC: false
 * Start VM
 * Open Console

* in TrueNAS Console Setup
 * 1. Install / Upgrade
 * Destination Media: QEMU Harddisk - 32 GB
 * Confirm deletion of 32GB disk
 * set password
 * Boot via UEFI
 * in VM Settings: Edit - Hardware -> CD/DVD Drive -> "do not use any media"
 * Reboot

* In TrueNAS web interface:
 * navigate to [http://truenas.local](http://truenas.local)
 * Accounts -> Users -> Create New user with Samba Authentication
 * System -> General -> set timezone

 
 
 

## Optimizations
### on Proxmox level
apt install ethtools
ethtool eno1
=> make sure speed is 1000Mb/s
=> if not: replace cable