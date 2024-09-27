# Important Softwares

After just installing, I mostly found these missing
1. Dolphin
2. Firefox
3. Kwrite/kate
4. openSSH
5. Bluetooth
6. Connect to iPhone

## 1, 2, 3, 4 To install them just do,
```
sudo pacman -S dolphin firefox kate openssh
```

## 5 Bluetooth
```
sudo pacman -S bluez bluez-utils blueman
sudo modprobe btusb
sudo systemctl start bluetooth.service
sudo systemctl enable bluetooth.service
sudo systemctl status bluetooth.service
```
Then you can use any GUI for easy interface, or also a CLI which comes with Blueman it's your wish.

## 6. Connect to iPhone
Install the required packages to allow your arch to detect your iPhone,
```
sudo pacman -S ifuse usbmuxd libplist libimobiledevice
```
and done!
