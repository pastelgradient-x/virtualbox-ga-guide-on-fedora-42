# virtualbox-ga-on-fedora-42
Guide: Remove Fedora’s Default VirtualBox Guest Additions & Reinstall from ISO on Fedora 42 Workstation
Introduction
Fedora Workstation sometimes comes with the default "virtualbox-guest-additions" package pre-installed, but for better compatibility (clipboard integration, auto-resize, seamless mode, etc.), it's often recommended to remove it and reinstall the official version from the VirtualBox ISO.
With the following commands, you will be able to ensure removing everything related to VirtualBox—including default Guest Additions packages and any other VirtualBox components—which helps prevent potential conflicts during the ISO-based reinstallation.
