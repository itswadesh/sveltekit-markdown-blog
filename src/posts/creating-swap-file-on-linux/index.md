---
title: Creating SWAP file on Linux
published: '2015-12-18T00:00:00.000+08:00'
updated: '2015-12-18T12:00:00.000+08:00'
tags: ['ubuntu', 'centos', 'linux']
series: false
cover: ./angularcode-swap-file-linux.png
coverStyle: 'TOP'
canonical_url: false
summary: "There are the steps to create a swap file which will act as RAM when sufficient space not available in RAM"
---

Show active swap: 
```
swapon --show
```
Show free space: 
```
free -h
```
Check available HDD space: 
```
df -h
```

Create swap: 
```
fallocate -l 3G /swapfile
```
Modify permissions: 
```
chmod 600 /swapfile
```
Make swap: 
```
mkswap /swapfile
```
Enable swap: 
```
swapon /swapfile
```

Initialize on startup: 
```
echo '/swapfile none swap sw 0 0' | tee -a /etc/fstab
```

Improve speed & swappiness: 
```
nano /etc/sysctl.conf
```
Add the following at bottom of file:
```
## Swap Configuration
vm.swappiness=10
vm.vfs_cache_pressure=50
```