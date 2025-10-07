# virtualbox-ga-guide-on-fedora-42
**pastelgradient's** Guide — How to Fix Issues with VirtualBox Guest Additions Caused by an Incorrect Build (or the preinstalled Guest Additions) and How to Reinstall Them Using the Official VirtualBox Guest Additions ISO on Fedora 42 Workstation (GNOME).

**Short story** — This guide was created because Guest Additions can be a nightmare to install/build when using VirtualBox on Fedora (or other Linux distributions). I struggled to find real solutions online; most either didn't work or suggested incorrect procedures. This guide aims to solve that problem by providing reliable, tested steps to make Guest Additions work properly. Additionally, when Fedora updated my kernel to the most recent version, it consistently failed to build a proper version of the Guest Additions.

**Introduction** — Fedora Workstation 42 comes with the default "virtualbox-guest-additions" package pre-installed. For better compatibility (clipboard integration, auto-resize, seamless mode, etc.), It is recommended to use the latest version for several reasons, so you should remove the default package and reinstall Guest Additions from the official VirtualBox ISO.
With the following commands, it is possible to ensure that everything related to VirtualBox—including default Guest Additions packages and any other VirtualBox components—is removed, which helps prevent potential conflicts during the ISO-based reinstallation.

# Commands
```bash

# -------- Uninstall Guest Additions --------

# 1. Remove Fedora's Default Guest Additions Packages (and possible leftovers).
sudo dnf remove virtualbox-guest-additions*

# 2. Install Required Build Tools & Libraries (needed to build kernel modules).
sudo dnf install gcc make perl dkms kernel-devel kernel-headers elfutils-libelf-devel bzip2

# 3. Ensure ISO is mounted, otherwise remount.
#    (Via VirtualBox Menu: Devices > Insert Guest Additions CD image).
#    (Also possible by adding it before booting the VM, i recommand this step over the first one).
cd /run/media/$(whoami)/VBox_GAs_7.2.2

# 4. Uninstall Any Existing Guest Additions (from previous installs).
sudo sh ./VBoxLinuxAdditions.run uninstall

# 5. Delete Residual Files and Directories (for a clean slate).
sudo rm -rf /var/lib/VBoxGuestAdditions
sudo rm -rf /opt/VBoxGuestAdditions-*
sudo rm -rf /usr/share/distribution-gpg-keys/virtualbox # optional

# 6. Clean Up Repository and Keys (optional).
rpm -q gpg-pubkey --qf "%{NAME}-%{VERSION}-%{RELEASE}\t%{SUMMARY}\n"   # List registered GPG keys
sudo rm /etc/yum.repos.d/virtualbox.repo                              # Remove VirtualBox repo if exists

# 7. Remove User from Shared Folders Group (if previously added).
sudo gpasswd -d $(whoami) vboxsf
# Optional (Attention: In rare cases with multiple users or typos, it is safer to use 'sudo groupdel vboxsf,' as this command deletes the entire group and its members. It is safe to use because the Bash installer will recreate the group during the installation process.).

# 8. Verify Removal (optional but recommended).
rpm -qa | grep -i virtualbox   # Output should be empty, or only unrelated VirtualBox packages

# 9. Reboot to Complete Removal & Unload Modules.
sudo reboot
# sudo reboot -f (if not working).

# -------- Install Guest Additions --------

# 1. Ensure ISO is still mounted, otherwise remount.
cd /run/media/$(whoami)/VBox_GAs_7.2.2

# 2. Uninstall Any Existing Guest Additions Again (in some rare cases, I found Guest Additions still present, and this fixed the issue).
sudo sh ./VBoxLinuxAdditions.run uninstall

# 3. Install Official Guest Additions from ISO.
sudo sh ./VBoxLinuxAdditions.run

# 4. Add User to vboxsf Group (to enable shared folders).
sudo usermod -aG vboxsf $(whoami)

# 5. Final Reboot (to load fresh modules and group settings).
sudo reboot
# sudo reboot -f (if not working).

```
Thank you for using this guide! If you found it helpful or have ideas for improvement, contributions and feedback are always welcome. Don’t hesitate to suggest changes or share your experiences with the guide!

I will be maintaining and upgrading this guide over time—just keep checking back,
**pastelgradient** !
