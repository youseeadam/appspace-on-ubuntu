# AppSpace on Ubuntu
I like using Ubuntu for this because it's free and lightweight, allowing you to run AppSpace on almost any hardware that support Ubuntu.  I tried this on a RaspberryPi 4, it didn't work too well, not enough resources availalbe. This was tested using Ubuntu Server 24.04 LTS.<br>
Special thanks to [@hotwire49]https://github.com/hotwire49 for his help on this as well
1. Install Ubuntu Server as you normally would.  It's not super complex.
2. Login whit the username you created during setup
3. Update the System
> Sudo apt update<br>
> Sudo apt upgrade
4. Create a new user, this will be used to login to the system automatcially and launch appspace-app
> sudo adduser appspace
5. Disable hibernation/sleep of the system
> sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
6. Install X, which is needed to run a GUI
> sudo apt install xinit
7. Disable blank screen
> gsettings set org.gnome.desktop.session idle-delay 0
8. Install appspace app
> sudo snap install appspace-app
9. Enable appspace to run at the start of X
> sudo nano /home/appspace/.xinitrc
10. Enter the following line
> appspace-app
* Save and exit the file using CTL-X -> Y -> ENTER
11. Configure autologin
> sudo mkdir /etc/systemd/system/getty@tty1.service.d
12.  Create and edit the override.conf file
> sudo nano /etc/systemd/system/getty@tty1.service.d/override.conf
13. Add the following lines
> [Service]<br>
> Type=simple<br>
> ExecStart=<br>
> ExecStart=-/sbin/agetty --autologin AppSpaceUser--noclear %I 38400 linux<br>
* Save and exit the file using CTL-X -> Y -> ENTER
14. Auto launch Startx
> sudo nano /home/appspace/.profile
15. Add the following lines to the end of the file
> #Startx Automatically<br>
> if [[ -z "$DISPLAY" ]] && [[ $(tty) = /dev/tty1 ]]; then<br>
> . startx<br>
> logout<br>
> fi<br>
* Save and exit the file using CTL-X -> Y -> ENTER
16. Reboot the System
> Sudo reboot
