# virtualbox-ga-guide-on-fedora-42
**pastelgradient's** Guide — How To Remove Fedora’s Default VirtualBox Guest Additions & Reinstall Them from ISO on Fedora 42 Workstation. 

Introduction :  
Fedora Workstation 42 comes with the default "virtualbox-guest-additions" package pre-installed. For better compatibility (clipboard integration, auto-resize, seamless mode, etc.), it is recommended to use the latest version by removing the default package and reinstalling the Guest Additions from the official VirtualBox ISO.  
With the following commands, it is possible to ensure that everything related to VirtualBox—including default Guest Additions packages and any other VirtualBox components—is removed, which helps prevent potential conflicts during the ISO-based reinstallation.

# Commands
```bash
# 1. Remove Fedora's Default Guest Additions Packages (and possible leftovers)
sudo dnf remove virtualbox-guest-additions*

# 2. Install Required Build Tools & Libraries (needed to build kernel modules)
sudo dnf install gcc make perl dkms kernel-devel kernel-headers elfutils-libelf-devel bzip2

# 3. Ensure ISO is mounted, otherwise remount
#    (Via VirtualBox Menu: Devices > Insert Guest Additions CD image)
#    (Also possible by adding it before booting the VM, i recommand this step over the first one)
cd /run/media/$(whoami)/VBox_GAs_7.2.2

# 4. Uninstall Any Existing Guest Additions (from previous installs)
sudo sh ./VBoxLinuxAdditions.run uninstall

# 5. Delete Residual Files and Directories (for a clean slate)
sudo rm -rf /var/lib/VBoxGuestAdditions
sudo rm -rf /opt/VBoxGuestAdditions-*
sudo rm -rf /usr/share/distribution-gpg-keys/virtualbox

# 6. Clean Up Repository and Keys (if present)
rpm -q gpg-pubkey --qf "%{NAME}-%{VERSION}-%{RELEASE}\t%{SUMMARY}\n"   # List registered GPG keys
sudo rm /etc/yum.repos.d/virtualbox.repo                              # Remove VirtualBox repo if exists

# 7. Remove User from Shared Folders Group (if previously added)
sudo gpasswd -d $(whoami) vboxsf

# 8. Verify Removal (optional but recommended)
rpm -qa | grep -i virtualbox   # Output should be empty, or only unrelated VirtualBox packages

# 9. Reboot to Complete Removal & Unload Modules
sudo reboot -f

# -------- Post-Reboot Steps --------

# 10. Ensure ISO is still mounted, otherwise remount
cd /run/media/$(whoami)/VBox_GAs_7.2.2

# 11. Install Official Guest Additions from ISO
sudo sh ./VBoxLinuxAdditions.run

# 12. Add User to vboxsf Group (to enable shared folders)
sudo usermod -aG vboxsf $(whoami)

# 13. Final Reboot (to load fresh modules and group settings)
sudo reboot -f

```
Thank you for consulting this guide! If you found it helpful or have ideas for improvement, contributions and feedback are always welcome. Don’t hesitate to suggest changes or share your experiences!
