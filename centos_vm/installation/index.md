# INSTALLATION

Your first task:

1. We need two Linux systems that are servers. The servers can be done on a Raspberry Pi, a persistent boot USB or on a second virtual machine on your laptop. Virtual machines are the recommended option.
2. You will need to use 2 different Linux Distros, one for each setup.  One must be CentOS, the other can be another server distro of your choice such as Ubuntu Server, Debian, OpenSUSE or Fedora.  Ubuntu Server or Debian is strongly recommended
3. Do not use the GUI or the minimal install. Make sure you turn on the Internet. When you are doing the installs use the commandline mode. Include a way to share files (such as Smartie)

Deliverables:
1. A short document showing how you did installs.  Target market is someone trying to follow along with you to make their own machines, assume some technical knowledge but not expertise.  Screenshots are helpful to go with your descriptions.
2. A short document saying what you have included in your installs, including any software you've added and any configurations you've changed. 

1. Download the .iso file - http://mirrors.seas.harvard.edu/centos/7.8.2003/isos/x86_64/CentOS-7-x86_64-DVD-2003.iso 
2. Launch VMWare Workstation
3. Select "Create a new virtual machine"
![image](https://user-images.githubusercontent.com/64757540/97351882-bbb81180-1868-11eb-95db-be3c7f3dc372.png)
4. Select Typical configuration and click next
![image](https://user-images.githubusercontent.com/64757540/97351937-cd99b480-1868-11eb-8d50-8e6d39254da1.png)
5. Select "Installer disc image file" and browse for your downloaded ISO file
![image](https://user-images.githubusercontent.com/64757540/97351997-e3a77500-1868-11eb-8677-888cef9c1b25.png)
6. Select your disk size and store the virtual disk as a single file
![image](https://user-images.githubusercontent.com/64757540/97352014-e904bf80-1868-11eb-94f0-1dfa2af60238.png)
7. Click finish
![image](https://user-images.githubusercontent.com/64757540/97352034-edc97380-1868-11eb-99eb-c97295696c80.png)
8. Launch the virtual machine and choose Install CentOS 7
![image](https://user-images.githubusercontent.com/64757540/97352053-f4f08180-1868-11eb-90b9-1a2df0ba7a26.png)
9. Select your preferred language
![image](https://user-images.githubusercontent.com/64757540/97352070-fa4dcc00-1868-11eb-8d71-31d27f35f597.png)
10. Select File and Print Server and click Done.
![image](https://user-images.githubusercontent.com/64757540/97352090-0043ad00-1869-11eb-8e98-a0ac0331b924.png)
11. Click Installation Destination and apply the following settings.
![image](https://user-images.githubusercontent.com/64757540/97352234-0c2f6f00-1869-11eb-9703-15872b0b45ad.png)
12. Select Network & Host Name and toggle Ethernet on
![image](https://user-images.githubusercontent.com/64757540/97352338-12255000-1869-11eb-8b9d-40899acb33d1.png)
13. Select User Creation and create a user with desired credentials
![image](https://user-images.githubusercontent.com/64757540/97352437-19e4f480-1869-11eb-881d-2791a30ae861.png)
14. Select Root Password and provide the desired credentials
![image](https://user-images.githubusercontent.com/64757540/97352494-1fdad580-1869-11eb-8991-5f33fce619af.png)
15. Once finished, reboot and you will be prompted for your user credentials
![image](https://user-images.githubusercontent.com/64757540/97352525-26694d00-1869-11eb-9eba-d0ce07ea8da4.png)