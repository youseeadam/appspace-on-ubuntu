# AppSpace on Ubuntu
I like using Ubuntu for this because it's free and lightweight, allowing you to run AppSpace on almost any hardware that support Ubuntu.  I tried this on a RaspberryPi 4, it didn't work too well, not enough resources availalbe. This was tested using Ubuntu Server 24.04 LTS
1. Install Ubuntu Server as you normally would.  It's not super complex.
2. During the setup, you are asked for a username and password.  For the purposes of this documentation, we will use this account for running AppSpace
3. Login wht the username you created during setup
4. Update the System
> Sudo apt update<br>
> Sudo apt upgrade
5. Disable hibernation/sleep of the system
> sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
6. Install X, which is needed to run a GUI
> sudo apt install xinit
7. Install appspace app
> sudo snap install appspace-app
8. Enable appspace to run at the start of X
> nano ~\.xinitrc
9. Enter the following line
> appspace-app
* Save and exit the file using CTL-X -> Y -> ENTER
10. Configure autologin
> sudo mkdir /etc/systemd/system/getty@tty1.service.d
11. Create and edit the override.conf file
> sudo nano /etc/systemd/system/getty@tty1.service.d/override.conf
12. Add the following lines <br>
Replace *yourusername* with the current logged in user
> [Service]<br>
> Type=simple<br>
> ExecStart=<br>
> ExecStart=-/sbin/agetty --autologin *yourusername* --noclear %I 38400 linux<br>
* Save and exit the file using CTL-X -> Y -> ENTER
13. Auto launch Startx
> nano ~/.profile
14. Add the following lines to the end of the file
> #Startx Automatically<br>
> if [[ -z "$DISPLAY" ]] && [[ $(tty) = /dev/tty1 ]]; then<br>
> . startx<br>
> logout<br>
> fi<br>
* Save and exit the file using CTL-X -> Y -> ENTER
15. Reboot the System
> Sudo reboot
