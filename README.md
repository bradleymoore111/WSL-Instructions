## Basic Installation
# Extract Arch.zip to C:\Users\USERNAME\Documents\Arch
# Run C:\Users\USERNAME\Documents\Arch\Arch.exe the first time to install
# Run Arch.exe again to spawn a shell

# add a new user
useradd -m -g users -G adm,ftp,games,http,log,rfkill,sys,systemd-journal,uucp,wheel -s /bin/bash USERNAME

passwd USERNAME

# enable sudo by uncommenting '%wheel ALL=(ALL) ALL'
EDITOR=nano visudo

# close Arch.exe and run the following in windows cmd
Arch.exe config --default-user USERNAME

# then run Arch.exe again

# update system. say no to installing fakeroot
sudo pacman-key --init
sudo pacman-key --populate
sudo pacman -Syyu base-devel wget git

## install Yet another Yogurt AUR helper
cd ~/
git clone https://aur.archlinux.org/fakeroot-tcp.git
cd fakeroot-tcp
makepkg -si

cd ~/
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si

## X11 Forwarding (Allow gui from linux)
# install VcXsrv for windows
https://sourceforge.net/projects/vcxsrv/

# On startup choose multiple windows, display 0, start no client, disable native opengl. Save the configuration to C:\Users\USERNAME\Documents

# enable x11 forwarding
echo export DISPLAY=:0 >> .bashrc

## Create start menu shortcut for Arch.exe
# navigate to C:\Users\USERNAME\Documents\Arch
# right click Arch.exe and select copy
# make sure Hidden Items are shown in Windows Explorer
# navigate to C:\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs
# right click -> Paste shortcut
# rename the shortcut to 'Arch Shell'

## Automatically start VcXsrv
# navigate to C:\Users\USERNAME\Documents
# right click config.xlaunch and select copy
# make sure Hidden Items are shown in Windows Explorer
# navigate to C:\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
# right click -> Paste shortcut
# rename the file and remove - shortcut

