# INSTALLATION

Your first task:

1. We need two Linux systems that are servers. The servers can be done on a Raspberry Pi, a persistent boot USB or on a second virtual machine on your laptop. Virtual machines are the recommended option.
2. You will need to use 2 different Linux Distros, one for each setup.  One must be CentOS, the other can be another server distro of your choice such as Ubuntu Server, Debian, OpenSUSE or Fedora.  Ubuntu Server or Debian is strongly recommended
3. Do not use the GUI or the minimal install. Make sure you turn on the Internet. When you are doing the installs use the commandline mode. Include a way to share files (such as Smartie)

Deliverables:
1. A short document showing how you did installs.  Target market is someone trying to follow along with you to make their own machines, assume some technical knowledge but not expertise.  Screenshots are helpful to go with your descriptions.
2. A short document saying what you have included in your installs, including any software you've added and any configurations you've changed. =

- Plug the SD card into your PC and download Raspberry Pi Ubuntu Server. Here is an article that will explain the process, as well as provide links to the downloads : 

- https://pimylifeup.com/ubuntu-server-raspberry-pi/ 

![image](https://user-images.githubusercontent.com/64757540/101853067-03e77680-3b2d-11eb-80dd-b122e24b655c.png)

- Once installed, you will need to download Etcher (https://www.balena.io/etcher/) to copy the OS to the SD card 

![image](https://user-images.githubusercontent.com/64757540/101853230-414c0400-3b2d-11eb-8356-a8ca2bf9f2f9.png)

- Once Etcher is installed, launch the executable and locate the downloaded OS within Etcher. 

![image](https://user-images.githubusercontent.com/64757540/101853515-b7506b00-3b2d-11eb-8b16-4d96c72a1fe8.png)

- Select the SD card you would like to install it on, and click Flash.

![image](https://user-images.githubusercontent.com/64757540/101853810-41003880-3b2e-11eb-9d2e-774cd7d0e26b.png)

- Plug the SD card in to your Raspberry Pi once the operating system has completed its installation. 

![image](https://user-images.githubusercontent.com/64757540/101852128-ec0ef300-3b2a-11eb-8771-273163f8418c.png)

- Plug in an HDMI cable to connect the Raspberry Pi up to a display.

![image](https://user-images.githubusercontent.com/64757540/101852575-009fbb00-3b2c-11eb-8d33-05cc843dc8b0.png)

- Connect an ethernet port to your Raspberry Pi from your router so that we do not have to worry about wireless configuration. You will also need a keyboard/mouse for initial configuration. For my setup, I used a wireless keyboard/trackpad combo.

![image](https://user-images.githubusercontent.com/64757540/101852760-5bd1ad80-3b2c-11eb-8f35-59cf16b3aabd.png)

- Once all cables are connected, plug a micro-usb power supply into the Raspberry Pi.

![image](https://user-images.githubusercontent.com/64757540/101852223-25476300-3b2b-11eb-9851-1d02fc860ec6.png)

- The Raspberry Pi should begin to boot as soon as power is plugged in.

![image](https://user-images.githubusercontent.com/64757540/101852831-80c62080-3b2c-11eb-9ae6-c272deac7e4a.png)

- Sign in with default username and password (both are ubuntu), update password
- Update/Upgrade the system: sudo apt update && sudo apt upgrade

- Set up SSH and get our IP address so that we can access our device remotely.

![image](https://user-images.githubusercontent.com/64757540/101853880-71e06d80-3b2e-11eb-8aaa-73fbe99999b2.png)

![image](https://user-images.githubusercontent.com/64757540/101854176-fd59fe80-3b2e-11eb-9291-1c247836e97e.png)

- Run ifconfig to get your IP address, then you can SSH from Putty or a command line on another PC: 

![image](https://user-images.githubusercontent.com/64757540/97491412-824ed700-1938-11eb-8dcf-21e433090ef0.png)

- Install Putty: https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe 
- Launch Putty > Insert IP address > Click Open

![image](https://user-images.githubusercontent.com/64757540/97491341-64817200-1938-11eb-8b42-5ceae3bf23b6.png)

- Insert your credentials to connect

![image](https://user-images.githubusercontent.com/64757540/97491451-8f6bc600-1938-11eb-8791-5bd52492f238.png)


