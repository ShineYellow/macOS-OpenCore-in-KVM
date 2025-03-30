使用方法

opencore for macos kvm

- for Sequoia, checkout Sequoia
- for Sonoma, checkout Sonoma

diskutil list
sudo diskutil mount disk0s1
把 EFI 文件 复制进去








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



refernce
https://forum.proxmox.com/threads/anyone-can-make-bluetooth-work-on-sonoma.153301/


