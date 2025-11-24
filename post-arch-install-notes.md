# POST ARCH INSTALL NOTES  

## SET UP NetworkManager  
1. connect temporarily with iwd (basic default network service) so that you can download NetworkManager  
```
$ iwctl  
//show devices you can use
[iwd]# device list  
// i only have one so shows device wlan0  
// you'll also need to have your wifi's SSID a.k.a the name of your wifi network (just google how to find it... if you don't know it)  
[iwd]# station wlan0 connect my-cool-wifi  
// open another terminal  
// send a ping to see if you have internets  
$ ping google.com  
// if shows packets being transmitted it works  
// shutdown the ping  
$ ctrl + c  
// close the other terminal running iwctl
```

2. install networkmanager  
```
// open new terminal
// run command to download and install network manager
$ sudo pacman -S networkmanager  
```

3. stop / disable iwd service before enabling NetworkManager to prevent service conflicts (this will shutdown internets so make sure you have everything you need... i mean you can always re-enable iwd but why go through that)  
```
$ sudo systemctl stop iwd  
$ sudo systemctl disable iwd  
```

4. enable NetworkManager  
```
$ sudo systemctl enable --now NetworkManager  
```

5. reboot system  
```
$ reboot
```

6. configure networkmanager  
```
// open terminal and start the network manager terminal UI configurator
$ nmtui
// select 'Activate a connection'
// select your wifi ssid
// enter wifi password
// once connected hit 'back'
// and then 'Quit' the tui

// confirm the network connection so start a new terminal
$ ping google.com
// you should see packet are transferring and then stop ping
$ ctrl + c
// reboot system to confirm that the service runs on startup and connection persists
$ reboot
// once rebooted and logged in open a terminal session
$ ping google.com
// you should see packet are transferring and then stop ping
$ ctrl + c
```
### YAY IT WORKS!  

---
---

## SET UP AUR HELPER (paru) 

https://github.com/Morganamilo/paru  

1. install requirements  
```
// the needed flag is to check if the package is already installed and ignore
sudo pacman -S --needed base-devel git
```

2. clone and build paru (anywhere works as the location since we'll clean it all up anyway but i usually have a temp folder off the home dir for all my garbage so i clone it there)  
```
// -si flags tell makepkg to install dependencies and install the package after building
// you may be prompted to pick a rust dependency either 'rust' or 'rustup'.. rustup is a toolchain manager so if you're not going to be developing in rust just choose the base 'rust' package
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```

3. clean up build dir (don't be a messy bessy)  
```
cd ..
rm -rf paru
```

4. test paru with a search  
```
paru -Ss firefox
```

5. optional things  
```
// i like to install 'bat' to enable syntax highlighting during PKGBUILD review
pacman -S bat

// i like to have color enabled in my paru outputs
// uncomment '#color' in pacman configuration
vim /etc/pacman.conf
```