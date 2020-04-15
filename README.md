# Enable WSL
Open powershell as administrator and run the following
```
> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

# Installation
- Download the latest Arch.zip release from the ArchWSL repo https://github.com/yuk7/ArchWSL
- Extract Arch.zip to C:\Users\USERNAME\Documents\Arch
- Run C:\Users\USERNAME\Documents\Arch\Arch.exe the first time to install
- Run Arch.exe again to spawn a shell

Add a new user
```
# useradd -m -g users -G adm,ftp,games,http,log,rfkill,sys,systemd-journal,uucp,wheel -s /bin/bash USERNAME
# passwd USERNAME
```

Enable sudo by uncommenting '%wheel ALL=(ALL) ALL'
```
# EDITOR=nano visudo
```
Close Arch.exe and run the following in windows cmd
```
> Arch.exe config --default-user USERNAME
```

Then run Arch.exe again

Update the system. Say no to installing fakeroot
```
$ sudo pacman-key --init
$ sudo pacman-key --populate
$ sudo pacman -Syyu base-devel wget git
```

# AUR helper
First install fakeroot-tcp, since systemd wont work here
```
$ cd ~/
$ git clone https://aur.archlinux.org/fakeroot-tcp.git
$ cd fakeroot-tcp
$ makepkg -si
```

Then install Yet another Yogurt AUR helper
```
$ cd ~/
$ git clone https://aur.archlinux.org/yay.git
$ cd yay
$ makepkg -si
```

# X11 Forwarding
Allows spawning GUI or applications in Windows

Install VcXsrv for windows<br>
https://sourceforge.net/projects/vcxsrv/

On startup choose multiple windows, display 0, start no client, disable native opengl.<br>
Save the configuration to C:\Users\USERNAME\Documents

Enable X11 forwarding 
```
$ echo export DISPLAY=:0 >> .bashrc
```

To test if X11 forwarding is working
```
$ sudo pacman -S mesa-demos
$ glxgears
```
# Automatically start VcXsrv
Load your configuration on Windows startup
- Navigate to C:\Users\USERNAME\Documents
- Right click config.xlaunch and select copy
- Make sure Hidden Items are shown in Windows Explorer
- Navigate to C:\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
- Right click -> Paste shortcut
- Rename the file and remove - shortcut

# Start menu shortcut for Arch.exe
Useful if you're going to spawn a shell from the start menu
- Navigate to C:\Users\USERNAME\Documents\Arch
- Right click Arch.exe and select copy
- Make sure Hidden Items are shown in Windows Explorer
- Navigate to C:\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs
- Right click -> Paste shortcut
- Rename the shortcut to 'Arch Shell'

# Increasing IO performance
Disabling real time scanning of the WSL folders increases read/write access, but possibly reduces security.<br>
https://gist.github.com/noelbundick/9c804a710eb76e1d6a234b14abf42a52#file-excludewsl-ps1

To allow unsigned powershell scripts, run
```
> Set-ExecutionPolicy unrestricted
```

After you finish, it is recommended to change the policy to something more secure
```
> Set-ExecutionPolicy remotesigned
```
# Additional WSL configurations
Fixes the ugly green ntfs directories due to improper filesystem metadata<br>
https://docs.microsoft.com/en-us/windows/wsl/wsl-config

Create /etc/wsl.conf and copy the following into it
```
[automount]
enabled = true
root = /mnt/
options = "metadata,umask=22,fmask=11"
mountFsTab = false

[network]
generateHosts = true
generateResolvConf = true
```
run the following in powershell as administrator to restart the WSL management service
```
> Restart-Service -Name "LxssManager"
```

# Disable tab-completion bell
uncomment `set bell-style none` in /etc/inputrc

# Managing git line endings
https://code.visualstudio.com/docs/remote/troubleshooting#_resolving-git-line-ending-issues-in-containers-resulting-in-many-modified-files

Git on windows usually has autocrlf enabled. You can just enable line ending conversion to match the windows setting.
```
$ git config --global core.autocrlf true
```

# Recommended programs
- bash-completion

# Better right click context menu
Fixes the missing icon and customizes text.

Open regedit.exe and change the ownership of the following registry folders to Administrators (dont forget to hit `Check Names`):
```
Computer\HKEY_CLASSES_ROOT\Directory\Background\shell\WSL
Computer\HKEY_CLASSES_ROOT\Directory\shell\WSL
Computer\HKEY_CLASSES_ROOT\Drive\shell\WSL
```
Also `Enable inheritance` and `Replace all child object permissions entries...`<br>
Ensure Administrators have `Full Control` checked.

Import the appropriate registry file from the github source.

# Uninstalling Arch WSL
Run the following in the command line.
```
> Arch.exe clean
```
