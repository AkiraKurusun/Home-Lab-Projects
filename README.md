### Description

* This repository documents my home lab environment, including network analysis, security tool configuration, and hands-on cybersecurity practice using Kali Linux and industry-standard tooling.

### 

### Host Machine

* Device: Microsoft Surface Pro 7
* Architecture: ARM64
* Storage: 1TB SSD
* RAM: 32GB
* OS: Windows 11 Pro

### 

### Access to Kali Linux

* Kali Linux runs via Windows Subsystem for Linux 2 (WSL2), installed directly from the Microsoft Store.
* GUI access is provided through Win-KeX (Windows + Kali Desktop Experience).

  * Due to the ARM64 architecture of the host device, Win-KeX operates exclusively in Enhanced Session Mode — the only supported GUI mode on non-x86 hardware.
  * Standard Win-KeX modes (Window Mode, Seamless Mode) are not available on ARM64 platforms. Enhanced Session Mode leverages RDP internally and remains fully functional for GUI-based tooling and workflows.

