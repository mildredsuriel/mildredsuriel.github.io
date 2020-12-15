# SECURITY PART 2

1. Take a snapshot of users every hour (Use a cron job for this) to see if there is any suspicious adding/removing of users 

2. Write a document that will show how to control what daemons run on boot and how to change that.  assume your audience is technically inclined, but not an expert. 

3. Find out how to boot into emergency mode for both your servers.  Write a one page (or less) document on how to do that. Include 1 paragraph executive summary on why you might want to. 

# CRON

- A list of all users can be generated using the compgen command

![image](https://user-images.githubusercontent.com/64757540/102265989-de1ff000-3ee5-11eb-9d19-29306c9f98bd.png)

- By having a list of the users, we can write a script to check the list every hour and identify any changes to the users. 

```
# Get a list of all of the users for the new hourly snapshot
compgen -u > users_new_hourly

# Compare the new hourly snapshot to the previous hour snapshot
diff users_last_hourly users_new_hourly > user_changes

# Check if the file is empty. If the string returned from the find command is empty, it means that the file being looked at isn't empty, signifying their are user changes
if [ -z "$(find -empty -name user_changes)" ]
then
    echo "User changes detected!"
    file=$(date +"%m_%d_%Y_H%H_user_changes")
    # Print all but the first and last lines since they don't contain the username changes, and save it to an hourly snapshot file
    sed '1d;$d' user_changes | tee $file
# Otherwise if the string returned is empty, then there are no differences
else
    echo "No user changes detected."
fi

cp users_new_hourly users_last_hourly
``` 

- Navigate to the directory that you want to install the script in. The following command can be used to download the script:

`wget https://raw.githubusercontent.com/mildredsuriel/mildredsuriel/master/bash/linuxadmin/user_cron.sh`

![image](https://user-images.githubusercontent.com/64757540/102266262-32c36b00-3ee6-11eb-92fe-761e6c993213.png)

- To verify the script works, we can generate the last hourly manually, and run the script to see what it does:

![image](https://user-images.githubusercontent.com/64757540/102266756-df9de800-3ee6-11eb-99d8-ffa42de38eb8.png)

- As expected, no user changes were detected. We can add/delete a user and run it to see that the appropriate log file is generated with the different user.

![image](https://user-images.githubusercontent.com/64757540/102267027-4d4a1400-3ee7-11eb-8d03-c9c05112ee21.png)

- To ensure that the script is run every hour, we can add the script to cron by running `sudo crontab -e`, which will launch an editor. At the bottom of the file, we can add `@hourly /path/to/script.sh` to have the cron job added.

![image](https://user-images.githubusercontent.com/64757540/102268346-34426280-3ee9-11eb-9cdc-35d1e5864409.png)

- Another easier alternative is to move the script to the cron.hourly directory. If placed within this directory, we do not need to reference the path to the file, as it was live in this directory instead.

![image](https://user-images.githubusercontent.com/64757540/102267183-82eefd00-3ee7-11eb-9bfd-6c6d5d5c3dc9.png)

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

- Enabling a daemon at boot is as simple as issuing the enable commands to for the process. When enabling a daemon, it will ask which user credentials you would like to use, so we will select our profile and provide our password.

![image](https://user-images.githubusercontent.com/64757540/102264191-49b48e00-3ee3-11eb-8a23-be1c889fca5b.png)

- After enabling the service we can grep to see that it appears as enabled now

![image](https://user-images.githubusercontent.com/64757540/102264112-2f7ab000-3ee3-11eb-974d-036aa44236e3.png)

- The same process can be done for disabling a daemon and verifying that it was disabled.

![image](https://user-images.githubusercontent.com/64757540/102264281-68b32000-3ee3-11eb-8a20-3f9001eca794.png)

![image](https://user-images.githubusercontent.com/64757540/102264358-85e7ee80-3ee3-11eb-846a-650673493b7c.png)

# EMERGENCY MODE

- Emergency mode is a mode that provides the most minimal environment possible to still boot, which should allow for the system to boot when it is unable to in other modes, allowing you to repair the issues that are stopping you from booting. Emergency mode will the root file system will be mounted as read-only and no other local file systems are mounted and the network interface is not active. Typically, emergency mode should only be accessed if rescue mode is not accessible. Rescue mode is similar to Emergency mode, excep that Rescue mode also tries to mount local file systems, so if there is an issue within the local file systems, rescue mode may not be accessible, while emergency mode is.

- When booting Ubuntu, we need to hold shift while booting, which we will be presented with the GRUB menu to select the operating system. If we click 'e' to edit, we will open up a boot script that we will need to modify.

![image](https://user-images.githubusercontent.com/64757540/102264489-b760ba00-3ee3-11eb-8a81-94bc082d0bb4.png)

- To enter recovery mode, we must modify the line that begins with 'linux'. I have added systemd.unit=emergency.target to the line. Once added, we may press Ctrl-x to start with the applied settings
 
![image](https://user-images.githubusercontent.com/64757540/102264673-f68f0b00-3ee3-11eb-8d24-e7a585f73ed9.png)

- Upon boot, we should see that we are placed in emergency mode. By issuing the Ctrl-D option, we will continue into emergency mode and be prompted to login.

![image](https://user-images.githubusercontent.com/64757540/102264737-09a1db00-3ee4-11eb-8ee0-85e587f10b33.png)


