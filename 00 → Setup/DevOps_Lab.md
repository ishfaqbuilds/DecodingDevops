### My DevOps Lab Setup

I'm building a local DevOps lab on **Ubuntu 24.04** to practice real world workflows without relying on the cloud. This is my setup guide for anyone doing the same.
If you're just starting out, Welcome !!! It gets less confusing, I promise.

---

#### What We're Installing & Why

Before we start typing commands, here is why each tool matters for our journey:

| Tools | Why we need it |
|------|---------------------|
| **VirtualBox** | We use this to create virtual machines. It is our safe playground where we can break things without worrying about our actual computer. |
| **Vagrant** | This automates our VM setup. We just run one command and our entire lab environment is ready. No manual clicking through installers. |
| **Git** | This tracks every change we make. When something breaks, we can go back to when it worked. It also helps us share our work with others. |
| **OpenJDK17** | This is the Java runtime we need for tools like Jenkins and Maven to work properly. |
| **Maven** | This builds Java projects for us and handles all the dependencies automatically. We do not have to hunt for libraries manually. |
| **VS Code** | This is our main code editor. It has extensions that make DevOps work easier, like Docker support and GitHub Copilot. |
| **SublimeText** | This is a super fast editor for when we just need to quickly peek at a file without waiting for a full IDE to load. |

---

#### Installation

> 💡 **Tip:** We should run each section one at a time in a fresh terminal. If something fails, it is easier for us to spot where things went wrong.

---
<br>

### 1. VirtualBox — Our Hypervisor

VirtualBox lets us run multiple operating systems like CentOS or Ubuntu Server as virtual machines. Think of it as our sandbox where nothing can go wrong with our real system.

```bash
sudo apt update
sudo apt install curl wget gnupg2 lsb-release -y

# Trust Oracle's signing keys (so Ubuntu knows this software is legit)
curl -fsSL https://www.virtualbox.org/download/oracle_vbox_2016.asc | \
  sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/vbox.gpg

curl -fsSL https://www.virtualbox.org/download/oracle_vbox.asc | \
  sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/oracle_vbox.gpg

# Tell Ubuntu where to find VirtualBox packages
echo "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian \
$(lsb_release -sc) contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list

# Install kernel headers + VirtualBox
sudo apt update
sudo apt install -y linux-headers-$(uname -r) dkms virtualbox-7.1

# Add ourselves to the vboxusers group (needed for USB and shared folders)
sudo usermod -aG vboxusers $USER && newgrp vboxusers
```

✅ We can check with: `virtualbox --help`

---
<br>

### 2. Vagrant — VM Automation

Manually setting up a VM every time is tedious for us. Vagrant lets us describe our environment in a file called `Vagrantfile` and spin it up with `vagrant up`. This is our first taste of infrastructure as code.

```bash
# Get HashiCorp's signing key
wget -O- https://apt.releases.hashicorp.com/gpg | \
  gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

# Add their repository
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
  sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update
sudo apt install vagrant libarchive-dev libarchive-tools -y
```

✅ We can check with: `vagrant --version`

---
<br>

### 3. Git — Version Control

Git tracks every change we make to our code. If we mess something up (and we will, we all do), we can roll back. It also lets us push our work to GitHub to share or back it up.

```bash
sudo apt install git -y
```

After installing, we tell Git who we are:

```bash
git config --global user.name "Add Name"
git config --global user.email "Add Email"
```

✅ We can check with: `git --version`

---
<br>

### 4. OpenJDK 17 — Java Runtime

Many DevOps tools we will use (Jenkins, Maven, SonarQube) are built on Java. This installs the runtime they need to work.

```bash
sudo apt-get install openjdk-17-jdk -y
```

✅ We can check with: `java -version`

---
<br>

### 5. Maven — Java Build Tool

Maven handles compiling Java code, running tests, and managing libraries our project depends on. One command (`mvn package`) and it does all of that for us.

```bash
sudo apt-get install maven -y
```

✅ We can check with: `mvn -version`

---
<br>

### 6. VS Code — Main Editor

VS Code is where most of our writing happens: code, YAML configs, Dockerfiles, shell scripts. The extensions marketplace makes it very DevOps friendly for us.

```bash
sudo apt-get install wget gpg -y

wget -qO- https://packages.microsoft.com/keys/microsoft.asc | \
  gpg --dearmor > packages.microsoft.gpg

sudo install -D -o root -g root -m 644 packages.microsoft.gpg \
  /etc/apt/keyrings/packages.microsoft.gpg

echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] \
https://packages.microsoft.com/repos/code stable main" | \
  sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null

rm -f packages.microsoft.gpg
sudo apt install apt-transport-https -y && sudo apt update
sudo apt install code -y
```

✅ We can check with: `code --version`

---
<br>

### 7. Sublime Text — Lightweight Editor

Sometimes VS Code feels like overkill for a quick edit. Sublime Text opens instantly and gets out of our way.

```bash
sudo apt install dirmngr gnupg apt-transport-https ca-certificates software-properties-common -y

curl -fsSL https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo add-apt-repository "deb https://download.sublimetext.com/ apt/stable/"
sudo apt install sublime-text -y
```

✅ We can check with: `subl --version`

---
<br>

### Did Everything Install Correctly?

We can run this script to check all tools at once:

```bash
echo "=== DevOps Lab Environment Check ==="
echo "VirtualBox : $(virtualbox --help | head -1)"
echo "Vagrant    : $(vagrant --version)"
echo "Git        : $(git --version)"
echo "Java       : $(java -version 2>&1 | head -1)"
echo "Maven      : $(mvn -version | head -1)"
echo "VS Code    : $(code --version | head -1)"
echo "Sublime    : $(subl --version 2>/dev/null || echo 'Not installed')"
echo "====================================="
```

If something shows an error, we should try rerunning just that section. Most issues come from a missed step or a copy paste gone wrong.

---
<br>

*This is a living document — I update it as I learn. Feel free to use it, fork it, or suggest improvements.*