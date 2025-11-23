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
// open new terminal
// run command to download and install network manager
```
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