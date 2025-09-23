# virtualbox-ga-on-fedora-42
Guide: Remove Fedora’s Default VirtualBox Guest Additions & Reinstall from ISO on Fedora 42 Workstation
Introduction
Fedora Workstation sometimes comes with the default "virtualbox-guest-additions" package pre-installed, but for better compatibility (clipboard integration, auto-resize, seamless mode, etc.), it's often recommended to remove it and reinstall the official version from the VirtualBox ISO.
With the following commands, you will be able to ensure removing everything related to VirtualBox—including default Guest Additions packages and any other VirtualBox components—which helps prevent potential conflicts during the ISO-based reinstallation.

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
