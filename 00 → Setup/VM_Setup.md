
### VM Setup (Ubuntu + CentOS with Vagrant + VirtualBox)

#### 1. Install Prerequisites
- Install Oracle VirtualBox → https://www.virtualbox.org
- Install Vagrant → https://developer.hashicorp.com/vagrant

- Verify installation:
  ```bash
  vagrant --version
  ```

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



