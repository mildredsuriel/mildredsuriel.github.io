# INSTALLATION

Your first task:

1. We need two Linux systems that are servers. The servers can be done on a Raspberry Pi, a persistent boot USB or on a second virtual machine on your laptop. Virtual machines are the recommended option.
2. You will need to use 2 different Linux Distros, one for each setup.  One must be CentOS, the other can be another server distro of your choice such as Ubuntu Server, Debian, OpenSUSE or Fedora.  Ubuntu Server or Debian is strongly recommended
3. Do not use the GUI or the minimal install. Make sure you turn on the Internet. When you are doing the installs use the commandline mode. Include a way to share files (such as Smartie)

Deliverables:
1. A short document showing how you did installs.  Target market is someone trying to follow along with you to make their own machines, assume some technical knowledge but not expertise.  Screenshots are helpful to go with your descriptions.
2. A short document saying what you have included in your installs, including any software you've added and any configurations you've changed. 


The majority of the instructions for setting up the Raspberry Pi server were followed from [the following guide](https://pimylifeup.com/ubuntu-server-raspberry-pi/).

1. Download Raspberry Pi Ubuntu server
2. Plug SD and ethernet into Raspberry PI and boot up
3. Sign in with default username and password (both are ubuntu), update password
4. Update/Upgrade the system: sudo apt update && sudo apt upgrade
5. Execute following commands to enable ssh:
```
sudo apt install openssh-server
sudo service ssh enable
sudo service ssh start
```
6. Install ifconfig : 

```
sudo apt-get install net-tools
```

7. Run ifconfig to get your IP address, then you can SSH from Putty or a command line on another PC:
```
ssh ubuntu@192.168.1.23
```
8. Installation Putty: https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe 
9. Launch Putty > Insert IP address > Click Open

![image](https://user-images.githubusercontent.com/64757540/97362700-c8903180-1877-11eb-8287-0953f2fea79f.png)

10. Insert your credentials to sign in.

![image](https://user-images.githubusercontent.com/64757540/97362755-dc3b9800-1877-11eb-80c2-dea857dea3d1.png)




