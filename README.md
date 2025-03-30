使用方法

opencore for macos kvm

- for Sequoia, checkout Sequoia
- for Sonoma, checkout Sonoma

diskutil list
sudo diskutil mount disk0s1
把 EFI 文件 复制进去


通过 [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools) 开启show picker
- reboot 后， 选择 reset





changes 


## 在 Sequoia, 解决dp接口的显示器 无法显示的问题:
WhateverGreen.kext up to 1.6.9
Lilu.kext up to 1.7.0
AppleALC.kext up to 1.7.0



## 修复 wifi

OSkywalkFamily.kext up to 1.1.0,

• Inject 3 extensions (Kexts folder and config.plist): IOSkywalk.kext, IO80211FamilyLegacy.kext and AirPortBrcmNIC.kext (IO80211FamilyLegacy.kext plugin) in this order, setting MinKernel to *24.0.0* to ensure they are injected only in Sonoma



Or directly edit config.plist:


## 修复 蓝牙
Go to Kernel -> Patch and add two new items as follows:

| Identifier | Base | Count | Find | Limit | Mask | Replace | Skip | Arch |
|------------|------|-------|------|-------|------|---------|------|------|
| kernel | | 1 | 68696265726E61746568696472656164790068696265726E617465636F756E7400 | 0 | | 68696265726E61746568696472656164790068765F766D6D5F70726573656E7400 | 0 | x86_64 |
| kernel | | 1 | 626F6F742073657373696F6E20555549440068765F766D6D5F70726573656E7400 | 0 | | 626F6F742073657373696F6E20555549440068696265726E617465636F756E7400 | 0 | x86_64 |





## 配置文件 Sequoia
```
/etc/pve/qemu-server/102.conf

agent: 1
args: -device isa-applesmc,osk="xxx" -smbios type=2 -device qemu-xhci -device usb-kbd -device usb-tablet -global nec-usb-xhci.msi=off  -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc,+vmx,rdtscp
bios: ovmf
boot: order=ide0;virtio0;net0
cores: 8
cpu: Skylake-Client
efidisk0: local-lvm:vm-102-disk-0,size=4M
hostpci0: 0000:01:00,pcie=1,x-vga=1
hostpci1: 0000:03:00,pcie=1
machine: q35
memory: 8048
name: Macos-Sequoia
net0: virtio=CE:29:35:A7:B1:B7,bridge=vmbr0,firewall=1
numa: 0
onboot: 1
ostype: other
scsihw: virtio-scsi-pci
smbios1: uuid=7ce35616-9bbb-46ae-b7ab-2400fd10dc47
sockets: 1
usb0: host=1-11.1,usb3=1
usb1: host=1-11.2,usb3=1
usb2: host=1-13.3.3,usb3=1
vga: none
virtio0: local-lvm:vm-102-disk-1,cache=unsafe,size=64G
vmgenid: 54217dfb-8de1-4264-a7ea-913abe9ffe5c
```


refernce
https://forum.proxmox.com/threads/anyone-can-make-bluetooth-work-on-sonoma.153301/
https://github.com/perez987/Broadcom-wifi-back-on-macOS-Sonoma-with-OCLP

