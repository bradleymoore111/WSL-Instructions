# Installation
Download the latest Arch.zip release from the ArchWSL repo https://github.com/yuk7/ArchWSL<br>
Extract Arch.zip to C:\Users\USERNAME\Documents\Arch<br>
Run C:\Users\USERNAME\Documents\Arch\Arch.exe the first time to install<br>
Run Arch.exe again to spawn a shell<br>

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

# Uninstalling Arch WSL
Run the following in the command line.
```
Arch.exe clean
```
