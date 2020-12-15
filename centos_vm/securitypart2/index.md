# SECURITY PART 2

1. Take a snapshot of users every hour (Use a cron job for this) to see if there is any suspicious adding/removing of users 

2. Write a document that will show how to control what daemons run on boot and how to change that.  assume your audience is technically inclined, but not an expert. 

3. Find out how to boot into emergency mode for both your servers.  Write a one page (or less) document on how to do that. Include 1 paragraph executive summary on why you might want to. 

# CRON

- A list of all users can be generated using the compgen command (we pipe the head command to just print the first 10 users here, as the list is much longer)

![image](https://user-images.githubusercontent.com/64757540/102267324-bb8ed680-3ee7-11eb-817b-4fdfa1ea14ef.png)

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

![image](https://user-images.githubusercontent.com/64757540/102267649-3c4dd280-3ee8-11eb-8414-0f220478ba51.png)

- To verify the script works, we can generate the last hourly manually, and run the script to see what it does:

![image](https://user-images.githubusercontent.com/64757540/102267774-60111880-3ee8-11eb-9830-cd5ac8916a26.png)

- As expected, no user changes were detected. We can add/delete a user and run it to see that the appropriate log file is generated with the different user.

![image](https://user-images.githubusercontent.com/64757540/102267953-9e0e3c80-3ee8-11eb-8281-e152db5b41d4.png)

- To ensure that the script is run every hour, we can add the script to cron by running `sudo crontab -e`, which will launch an editor. At the bottom of the file, we can add `@hourly /path/to/script.sh` to have the cron job added.

![image](https://user-images.githubusercontent.com/64757540/102268346-34426280-3ee9-11eb-9cdc-35d1e5864409.png)

- Another easier alternative is to move the script to the cron.hourly directory. If placed within this directory, we do not need to reference the path to the file, as it was live in this directory instead.

![image](https://user-images.githubusercontent.com/64757540/102268047-c1d18280-3ee8-11eb-8eba-86f75dd21d49.png)


# DAEMONS
 
- To determine what daemons are available on your system and the status of each, the following command can be used to print out a list: `systemctl list-unit-files --type service`

![image](https://user-images.githubusercontent.com/64757540/102255644-567fb480-3ed8-11eb-8091-3d62f61fa0fb.png)

- Running that command will print a long list of daemon processes that are available:

![image](https://user-images.githubusercontent.com/64757540/102255690-65666700-3ed8-11eb-9b61-ebf20db2f097.png)

![image](https://user-images.githubusercontent.com/64757540/102255701-69928480-3ed8-11eb-9fa8-5c1343039b67.png)

![image](https://user-images.githubusercontent.com/64757540/102255713-6d260b80-3ed8-11eb-85b3-08b248b52562.png)

![image](https://user-images.githubusercontent.com/64757540/102255730-71eabf80-3ed8-11eb-8786-e9ebb63e1645.png)

![image](https://user-images.githubusercontent.com/64757540/102255738-757e4680-3ed8-11eb-8fb4-f3705cc095ae.png)

![image](https://user-images.githubusercontent.com/64757540/102255748-79aa6400-3ed8-11eb-9de5-942d5d14818e.png)

- With so many processes listed, it can become overwhelming. We can also execute the `systemctl status` command as another alternative, which lists the processes in a tree structure instead. This tree structure does not list any static processes, nor does it list processes that are enabled but failed to run.

![image](https://user-images.githubusercontent.com/64757540/102256926-07d31a00-3eda-11eb-90f4-1af5292f9b8d.png)

![image](https://user-images.githubusercontent.com/64757540/102256942-0dc8fb00-3eda-11eb-82aa-98c8d8cfcc5b.png)

- As an example, the mdmonitor process is listed as enabled within the list of all services, although when checking the status it is not listed. If we check the status of the process, we can see that the process is inactive for some reason, which is something that can be looked into separately if needed.

![image](https://user-images.githubusercontent.com/64757540/102257191-6e583800-3eda-11eb-9f63-09a8c0fcec6c.png)

- Enabling aa daemon at boot is as simple as issuing the enable commands to for the process. When enabling a daemon, it will ask which user credentials you would like to use, so we will select our profile and provide our password.

![image](https://user-images.githubusercontent.com/64757540/102258106-909e8580-3edb-11eb-8cef-061e6c44b96b.png)

![image](https://user-images.githubusercontent.com/64757540/102258074-84b2c380-3edb-11eb-93eb-a3b1dec76eef.png)

- After enabling the service we can grep to see that it appears as enabled now

![image](https://user-images.githubusercontent.com/64757540/102257868-4a492680-3edb-11eb-85ff-e1c8e9d648d4.png)

- The same process can be done for disabling a daemon and verifying that it was disabled.

![image](https://user-images.githubusercontent.com/64757540/102258198-a9a73680-3edb-11eb-8cf7-4a7905199e04.png)

![image](https://user-images.githubusercontent.com/64757540/102258304-cba0b900-3edb-11eb-987e-a367aedc53a2.png)

# EMERGENCY MODE

- Emergency mode is a mode that provides the most minimal environment possible to still boot, which should allow for the system to boot when it is unable to in other modes, allowing you to repair the issues that are stopping you from booting. Emergency mode will the root file system will be mounted as read-only and no other local file systems are mounted and the network interface is not active. Typically, emergency mode should only be accessed if rescue mode is not accessible. Rescue mode is similar to Emergency mode, excep that Rescue mode also tries to mount local file systems, so if there is an issue within the local file systems, rescue mode may not be accessible, while emergency mode is.

- When booting CentOS, we will be presented with the GRUB menu to select the operating system. If we click 'e' to edit, we will open up a boot script that we will need to modify.

![image](https://user-images.githubusercontent.com/64757540/102248564-48796600-3ecf-11eb-89c7-81f6a2670f17.png)

- To enter recovery mode, we must modify the line that begins with 'linux'

![image](https://user-images.githubusercontent.com/64757540/102248663-69da5200-3ecf-11eb-9734-23f5eb8b1fa1.png)

- I have added systemd.unit=\emergency.target to the line. Once added, we may press Ctrl-x to start with the applied settings

![image](https://user-images.githubusercontent.com/64757540/102249202-1ae0ec80-3ed0-11eb-958c-eede7c8494de.png)

- Upon boot, we should see that we are placed in emergency mode

![image](https://user-images.githubusercontent.com/64757540/102249264-2c29f900-3ed0-11eb-9b06-c63fddaded33.png)

- We are able to log in using our same credentials, but within a much more minimal environment

![image](https://user-images.githubusercontent.com/64757540/102249316-3c41d880-3ed0-11eb-8f18-9fdd620cc51a.png)
