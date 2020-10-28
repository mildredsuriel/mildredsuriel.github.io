# INSTALLATION

Your first task:

1. We need two Linux systems that are servers. The servers can be done on a Raspberry Pi, a persistent boot USB or on a second virtual machine on your laptop. Virtual machines are the recommended option.
2. You will need to use 2 different Linux Distros, one for each setup.  One must be CentOS, the other can be another server distro of your choice such as Ubuntu Server, Debian, OpenSUSE or Fedora.  Ubuntu Server or Debian is strongly recommended
3. Do not use the GUI or the minimal install. Make sure you turn on the Internet. When you are doing the installs use the commandline mode. Include a way to share files (such as Smartie)

Deliverables:
1. A short document showing how you did installs.  Target market is someone trying to follow along with you to make their own machines, assume some technical knowledge but not expertise.  Screenshots are helpful to go with your descriptions.
2. A short document saying what you have included in your installs, including any software you've added and any configurations you've changed. =

- download Raspberry Pi Ubuntu server : https://pimylifeup.com/ubuntu-server-raspberry-pi/ 
- Plug SD and ethernet into Raspberry PI and boot up
- Sign in with default username and password (both are ubuntu), update password
- Update/Upgrade the system: sudo apt update && sudo apt upgrade
- Execute following commands to enable ssh:
```
sudo apt install openssh-server
sudo service ssh enable
sudo service ssh start
```
- Install ifconfig : 

```
sudo apt-get install net-tools
```

- Run ifconfig to get your IP address, then you can SSH from Putty or a command line on another PC: 

![image](https://user-images.githubusercontent.com/64757540/97491412-824ed700-1938-11eb-8dcf-21e433090ef0.png)

- Install Putty: https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe 
- Launch Putty > Insert IP address > Click Open

![image](https://user-images.githubusercontent.com/64757540/97491341-64817200-1938-11eb-8b42-5ceae3bf23b6.png)

- Insert your credentials to connect

![image](https://user-images.githubusercontent.com/64757540/97491451-8f6bc600-1938-11eb-8791-5bd52492f238.png)


