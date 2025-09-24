# virtualbox-ga-guide-on-fedora-42
**pastelgradient's** Guide — How To Remove Fedora’s Default VirtualBox Guest Additions & Reinstall Them from ISO on Fedora 42 Workstation. 

Introduction :  
Fedora Workstation 42 comes with the default "virtualbox-guest-additions" package pre-installed. For better compatibility (clipboard integration, auto-resize, seamless mode, etc.), it is recommended to use the latest version by removing the default package and reinstalling the Guest Additions from the official VirtualBox ISO.  
With the following commands, it is possible to ensure that everything related to VirtualBox—including default Guest Additions packages and any other VirtualBox components—is removed, which helps prevent potential conflicts during the ISO-based reinstallation.

# Commands
```bash
sudo dnf remove virtualbox-guest-additions*
cd /run/media/$(whoami)/VBox_GAs_7.2.2
sudo dnf install gcc make perl dkms kernel-devel kernel-headers elfutils-libelf-devel bzip2
sudo sh ./VBoxLinuxAdditions.run uninstall
sudo rm -rf /var/lib/VBoxGuestAdditions
sudo rm -rf /opt/VBoxGuestAdditions-*
sudo rm -rf /usr/share/distribution-gpg-keys/virtualbox
rpm -q gpg-pubkey --qf "%{NAME}-%{VERSION}-%{RELEASE}\t%{SUMMARY}\n"
sudo rm /etc/yum.repos.d/virtualbox.repo
sudo gpasswd -d $(whoami) vboxsf
sudo reboot -f
cd /run/media/$(whoami)/VBox_GAs_7.2.2
sudo sh ./VBoxLinuxAdditions.run
sudo usermod -aG vboxsf $(whoami)
sudo reboot -f
```
Thanks for using my Guide and don't hesitate to contribute to it !
