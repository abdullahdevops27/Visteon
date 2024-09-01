# Visteon
Setting Up Ubuntu 20.04 VM
Overview
This document outlines the steps required to set up an Ubuntu 20.04 virtual machine (VM) for development and specific use cases, including installing essential packages, handling errors, and configuring the repo tool.

Prerequisites
Ensure you have an Ubuntu 20.04 VM up and running. You will need administrative access to perform installations and configurations.

1. System Update
Start by updating the package lists:



sudo apt update
2. Install Essential Packages
Install the required packages and utilities:



sudo apt install -y software-properties-common unzip curl git build-essential zip uuid-dev
Troubleshooting
Error:

kotlin

Package build-essential is not available, but is referred to by another package.
Package zip is not available, but is referred to by another package.
Resolution:

Update Package Lists:



sudo apt update
sudo apt upgrade -y
Enable Universe Repository:



sudo add-apt-repository universe
sudo apt update
Reinstall Required Packages:



sudo apt install -y software-properties-common unzip curl git build-essential zip uuid-dev
Additional Troubleshooting:

Check Package Sources:



cat /etc/apt/sources.list
Reconfigure Package Manager:



sudo apt-get clean
sudo apt-get update
sudo apt-get install -f
sudo add-apt-repository main
sudo add-apt-repository universe
sudo add-apt-repository restricted
sudo add-apt-repository multiverse
sudo apt-get update
Manual Installation (if necessary):



sudo apt install -y gcc g++ make
sudo apt install -y gzip unzip
3. Install Development Libraries and Tools


sudo apt install -y uuid-dev unzip liblz-dev liblzo2-2 liblzo2-dev lzop git mtd-tools device-tree-compiler gdisk \
gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev zlib1g-dev lib32z-dev \
lib32z1-dev clang openjdk-8-jdk libssl-dev gnupg build-essential curl bc libgl1-mesa-dev libxml2-utils python \
libtinfo5 libncurses5 liblocal-lib-perl cpanminus libxml-simple-perl cpio python3-pip python-dev libffi-dev \
libjpeg8-dev uuid u-boot-tools mtd-utils bison zip xsltproc python3-networkx libxml2-dev libxslt1-dev \
android-sdk-libsparse-utils android-sdk-ext4-utils
Troubleshooting
Error:

vbnet

Some packages could not be installed. The following packages have unmet dependencies: python-dev-is-python2 : Depends: python2-dev but it is not going to be installed
Resolution:

Fix Broken Packages:



sudo apt --fix-broken install
Install Python 3 Development Packages:



sudo apt install -y python3-dev python3-pip
Remove Python 2 Packages:



sudo apt purge -y python-dev-is-python2
Reinstall Remaining Packages:



sudo apt install -y liblz-dev lzop mtd-utils device-tree-compiler gcc-multilib g++-multilib libc6-dev-i386 \
lib32ncurses-dev clang openjdk-8-jdk libssl-dev libtinfo5 libncurses5 liblocal-lib-perl cpanminus libxml-simple-perl \
u-boot-tools bison xsltproc libxml2-dev libxslt1-dev
Clean Up:



sudo apt autoremove -y
sudo apt clean
sudo apt update
4. Setup Configuration Files
Copy the .nerc, .rc, and .gitconfig files from existing working machines to the new VM.

5. Install repo Tool
Download repo Tool:



curl https://storage.googleapis.com/git-repo-downloads/repo > ~/repo
Make repo Tool Executable:



chmod +x ~/repo
Move repo Tool to /usr/local/bin:



sudo mv ~/repo /usr/local/bin/repo
Verify Installation:



repo --version
6. Initialize Repository
Navigate to the /data partition and create a test folder:



mkdir -p /data/testfolder
cd /data/testfolder
repo init -u https://git.visteon.com/snapdragonseries/visteon/s220/manifest.git -b mah_s220_w502_cs2_int -m mah_s220_w502_product/mah_s220_w502_6155.xml --repo-url=http://git.pune.visteon.com/repo-tools/repo-v2.8 --no-clone-bundle --no-repo-verify --depth=1
7. Synchronize Repository


repo sync --optimized-fetch --no-tags --no-clone-bundle --force-sync -j16
Conclusion
Following these steps will set up your Ubuntu 20.04 VM with the necessary packages, tools, and configurations. Ensure to address any errors as described to successfully complete the setup.
