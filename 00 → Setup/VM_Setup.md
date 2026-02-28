
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
---

#### Vagrant Commands

| Command                 | Use                                                           | 
| ----------------------- | ------------------------------------------------------------- | 
| `vagrant up`            | Start VM                                                      | 
| `vagrant ssh`           | Log into VM                                                   | 
| `exit`                  | Exit VM session                                               | 
| `sudo -i`               | Switch to root inside VM                                      | 
| `vagrant halt`          | Stop VM (power off)                                           | 
| `vagrant reload`        | Restart VM (apply changes) / Reload with new network settings | 
| `vagrant destroy`       | Delete VM completely                                          | 
| `vagrant status`        | Check VM status in current folder                             | 
| `vagrant global-status` | List all VMs on system                                        | 
| `vagrant suspend`       | Suspend VM (pause state)                                      | 
| `vagrant resume`        | Resume VM (after suspend)                                     | 
| `vagrant rsync`         | Resync shared folder manually                                 | 
| `vagrant provision`     | Force provisioning (rerun setup scripts)                      | 
| `vagrant ssh-config`    | Show SSH config details (IP, port, keys)                      | 
| `vagrant box list`      | Show Vagrant box details                                      |
