
### VM Setup (Ubuntu + CentOS with Vagrant + VirtualBox)
---
#### 1. Install Prerequisites
We need the prerequisites first [My DevOps Lab](https://github.com/ishfaqbuilds/DecodingDevops/blob/main/00%20%E2%86%92%20Setup/DevOps_Lab.md).

#### 2. Create Project Directory
```bash
mkdir ~/vagrant-vms
cd ~/vagrant-vms
mkdir ubuntu centos
```

#### 3. Initialize Vagrant Boxes

Ubuntu 22.04 (Jammy Jellyfish)
```bash
cd ~/vagrant-vms/ubuntu
vagrant init ubuntu/jammy64
```

CentOS Stream 9
```bash
cd ~/vagrant-vms/centos
vagrant init eurolinux-vagrant/centos-stream-9
```



