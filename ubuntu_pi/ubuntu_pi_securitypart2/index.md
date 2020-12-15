# SECURITY PART 2

1. Take a snapshot of users every hour (Use a cron job for this) to see if there is any suspicious adding/removing of users 

2. Write a document that will show how to control what daemons run on boot and how to change that.  assume your audience is technically inclined, but not an expert. 

3. Find out how to boot into emergency mode for both your servers.  Write a one page (or less) document on how to do that. Include 1 paragraph executive summary on why you might want to. 

# DAEMONS
 
- To determine what daemons are available on your system and the status of each, the following command can be used to print out a list: `systemctl list-unit-files --type service`

- Running that command will print a long list of daemon processes that are available:

![image](https://user-images.githubusercontent.com/64757540/102260337-4ff43b80-3ede-11eb-8d4c-89515549a3f5.png)

![image](https://user-images.githubusercontent.com/64757540/102260445-71edbe00-3ede-11eb-82e2-e829b089f373.png)

![image](https://user-images.githubusercontent.com/64757540/102260487-82059d80-3ede-11eb-87ac-1a8247f0c4a3.png)

![image](https://user-images.githubusercontent.com/64757540/102260531-947fd700-3ede-11eb-8995-b508c1b9f9c4.png)

![image](https://user-images.githubusercontent.com/64757540/102260755-d872dc00-3ede-11eb-8592-16f0f68287a6.png)

- With so many processes listed, it can become overwhelming. We can also execute the `systemctl status` command as another alternative, which lists the processes in a tree structure instead. This tree structure does not list any static processes, nor does it list processes that are enabled but failed to run.

![image](https://user-images.githubusercontent.com/64757540/102260885-eaed1580-3ede-11eb-8adc-60e5f9a492b7.png)

![image](https://user-images.githubusercontent.com/64757540/102260919-f9d3c800-3ede-11eb-988c-24b18626fbe6.png)

![image](https://user-images.githubusercontent.com/64757540/102260987-0e17c500-3edf-11eb-8653-75fdf3cfd351.png)

- As an example, the mdmonitor process is listed as enabled within the list of all services, although when checking the status it is not listed. If we check the status of the process, we can see that the process is inactive for some reason, which is something that can be looked into separately if needed.

- Enabling aa daemon at boot is as simple as issuing the enable commands to for the process. When enabling a daemon, it will ask which user credentials you would like to use, so we will select our profile and provide our password.


- After enabling the service we can grep to see that it appears as enabled now


- The same process can be done for disabling a daemon and verifying that it was disabled.

# EMERGENCY MODE

- Emergency mode is a mode that provides the most minimal environment possible to still boot, which should allow for the system to boot when it is unable to in other modes, allowing you to repair the issues that are stopping you from booting. Emergency mode will the root file system will be mounted as read-only and no other local file systems are mounted and the network interface is not active. Typically, emergency mode should only be accessed if rescue mode is not accessible. Rescue mode is similar to Emergency mode, excep that Rescue mode also tries to mount local file systems, so if there is an issue within the local file systems, rescue mode may not be accessible, while emergency mode is.

- When booting CentOS, we will be presented with the GRUB menu to select the operating system. If we click 'e' to edit, we will open up a boot script that we will need to modify.

- To enter recovery mode, we must modify the line that begins with 'linux'

- I have added systemd.unit=\emergency.target to the line. Once added, we may press Ctrl-x to start with the applied settings

- Upon boot, we should see that we are placed in emergency mode

- We are able to log in using our same credentials, but within a much more minimal environment

