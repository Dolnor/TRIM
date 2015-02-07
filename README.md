## TRIM Support for non-Apple SSDs

Patch IOAHCIBlockStorage to support TRIM functionality on non-Apple SSDs.

Automatically detects (and performs, if needed) whether patching out APPLE SSD is required or not. 

### Installation

Make sure to have nvram boot-args variable set to allow unsigned kext (for Yosemite)

		sudo nvram boot-args=kext-dev-mode=1

Follow the catalog hierarchy to install files in respective folders

### Finishing touches

1. Log folder requires 755 perms

		sudo chmod 755 /Library/Logs/TRIM

2. RC script require execution perms, while the parent folder requires 644 perms

		sudo chmod 644 /etc/rc.boot.d
		sudo chmod +x /etc/rc.boot.d/*

3. Daemon config plist requires 644 perms + root ownership in wheel group

		sudo chmod 644 /Library/LaunchDaemons/org.tw.trim.daemon.plist
		sudo chown root:wheel /Library/LaunchDaemons/org.tw.trim.daemon.plist