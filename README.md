# virtualbox-ga-guide-on-fedora-42
**pastelgradient's** Guide — How to Fix Issues with VirtualBox Guest Additions Caused by an Incorrect Build (or the preinstalled Guest Additions) and How to Reinstall Them Using the Official VirtualBox Guest Additions ISO on Fedora 42 Workstation (GNOME).

**Short story** — This guide was created because Guest Additions can be a nightmare to install/build when using VirtualBox on Fedora (or other Linux distributions). I struggled to find real solutions online; most either didn't work or suggested incorrect procedures. This guide aims to solve that problem by providing reliable, tested steps to make Guest Additions work properly. Additionally, when Fedora updated my kernel to the most recent version, it consistently failed to build a proper version of the Guest Additions.

**Introduction** — Fedora Workstation 42 comes with the default "virtualbox-guest-additions" package pre-installed. For better compatibility (clipboard integration, auto-resize, seamless mode, etc.), It is recommended to use the latest version for several reasons, so you should remove the default package and reinstall Guest Additions from the official VirtualBox ISO.
With the following commands, it is possible to ensure that everything related to VirtualBox—including default Guest Additions packages and any other VirtualBox components—is removed, which helps prevent potential conflicts during the ISO-based reinstallation.

[***Uninstall***](https://github.com/pastelgradient-x/virtualbox-ga-guide-on-fedora-42/blob/main/uninstall-ga) Virtualbox's Guest Additions.

[***Install***](https://github.com/pastelgradient-x/virtualbox-ga-guide-on-fedora-42/blob/main/install-ga) Virtualbox's Guest Additions.

[***Tuning***](https://github.com/pastelgradient-x/virtualbox-ga-guide-on-fedora-42/blob/main/tuning.md) Incoming Update in progress.

Thank you for using this guide! If you found it helpful or have ideas for improvement, contributions and feedback are always welcome. Don’t hesitate to suggest changes or share your experiences with the guide!

I will be maintaining and upgrading this guide over time—just keep checking back,
**pastelgradient** !
