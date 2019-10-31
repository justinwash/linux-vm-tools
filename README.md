# Linux VM Tools for Arch

## Full Install Instructions for Manjaro

* Create a Hyper-V Virtual Machine, make sure to disable Secure Boot
* On startup, press ```ctrl+alt+F2``` to get to a shell and log in with the default username/password
* Install basic video drivers to get the X server to start:
```
$ su
$ pacman –Sy 
$ pacman –S xf86-video-fbdev
$ systemctl restart lightdm
```
* Install Manjaro
* Reboot then press ```ctrl+alt+F2``` again. Install ```linux-vm-tools``` from this repo
```
$ sudo pacman –Sy
$ sudo pacman –S git
$ cd Downloads (or wherever you want to download it to)
$ git clone https://github.com/justinwash/linux-vm-tools-arch.git // this repo
$ cd linux-vm-tools-arch/arch
$ ./makepkg.sh
$ sudo ./install.sh
```
* Edit this line in .xinitrc (```nano ~/.xinitrc```)
```
local dbus_args=(--sh-syntax --exit-with-session)
```

The edited line should read
```
local dbus_args=(--sh-syntax)
```
* Add ```xrdp``` to the ```IgnorePkg``` line in your pacman configuration so it doesn't update and break itself. ```sudo nano /etc/pacman.conf```
* Shut down your VM and issue this Windows PowerShell command to enable Enhanced Session mode for your VM.
```
Set-VM -VMName _Your_Manjaro_VM_ -EnhancedSessionTransportType HvSocket
```

