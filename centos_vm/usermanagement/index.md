You have been asked to add to your system four groups of users: admin, developers, staff and temp. Each should have their own group and an associated folder that they have access to. Within each groups folder should be a read only folder for policies and such. There should also be a public read only folder for general company policy.  

You should add users for testing from the attached user lists. Any repetitive task should be scripted (shell or Python or hybrid). Admin users should be added to sudo with full permission. Each group should have a skeleton directory. The developers should default to c shell. Temps should have a limit to their disk usage.

Turn in any scripts you have written, a link to your GitHub where you have posted your scripts, and  screenshot(s) that best shows you were able to complete this task successfully. Use your own best judgment for how many you need, but remember this will be added to your documentation.

Test your scripts on both levels of UserNames attached to this lab. For adding to groups, any users can be added to any group, split it up however you like but document who's in which group. This lab is considered complete when both UserNames are added to both your servers using the scripts you've made, including the group add.

Deliverables:

A well commented script (or set of scripts) that achieves the set out tasks as outlined above including  A link to your GitHub where you've posted your scripts.

A short document explaining how you decided to set up your username rules (first letter last name, first name only, random characters and last name, etc) as well as a list of who is in which group. And any extra rules or regulations you've decided are important for each group.  You should also include any dicumentation needed for how to run your scripts.  Do they  need any special files? Any special formats expected? Any assumptions you've made as you're writing your scripts?

A short document showing you've been able to successfully add all users from both levels to both your distros.  Can be done with screenshots or a textfile taken from your servers

- First, we should create an account for us that will have admin rights and then run our scripts to configure the other users and the groups. We want to make our account an admin account so that we can perform all of our duties.

- Creating groups is simply a `groupadd` command for the group you want. I can quickly create all the groups now (although we will automate this in the script, and we really only care about the admin group existing at this point which it should by default.

![image](https://user-images.githubusercontent.com/64757540/98878115-26b03d80-2450-11eb-9b8f-43102a870f92.png)

- You can verify your groups exist by grepping in /etc/group

![image](https://user-images.githubusercontent.com/64757540/98878137-392a7700-2450-11eb-8b6a-f1e8dc767a2c.png)

- Lets go ahead and add ourselves as a user to the admin group. We can verify that we are member of the group using getent

<p align="center">
  <img width="720" height="450" src="https://user-images.githubusercontent.com/64757540/98878198-6119da80-2450-11eb-91de-715132ce90ed.png">
</p>


![image](https://user-images.githubusercontent.com/64757540/98878198-6119da80-2450-11eb-91de-715132ce90ed.png)

- Lets get the scripts to create all of the other users. You can download the scripts I used with the following `wget` commands to whatever directory you choose (I recommend placing it within a scripts directory somewhere, like I have)

```
sudo wget https://raw.githubusercontent.com/mildredsuriel/mildredsuriel/master/bash/linuxadmin/create_users.sh
sudo wget https://raw.githubusercontent.com/mildredsuriel/mildredsuriel/master/bash/linuxadmin/create_groups.sh
```

<p align="center">
  <img width="720" height="450" src="https://user-images.githubusercontent.com/64757540/98878281-958d9680-2450-11eb-96d4-2884b5b7a30d.png">
</p>

test test test

![image](https://user-images.githubusercontent.com/64757540/98878281-958d9680-2450-11eb-96d4-2884b5b7a30d.png)

- Our create_groups scripts does several things at once

```bash
# Create top level policies
sudo mkdir -p /home/shared/policies
# Make file read only
sudo chmod a=rx /home/shared/policies

# List of possible groups to add users to
groups=("temp" "staff" "developers" "admin")
# Loop over each group and create files with set permissions
for group in $groups; do
	# Create a group
	sudo groupadd $group
	# Create the group directory
	sudo mkdir -p /home/shared/groups/$group
	# Assign the group directory to the group
	sudo chgrp -R $group /home/shared/groups/$group
	# Only users who are a part of this group can write / execute
	sudo chmod -R 2775 /home/shared/groups/$group
	# Make policy folder for each group
	sudo mkdir -p /home/shared/groups/$group/policies
	# Make each policy folder read only
	sudo chmod a=rx /home/shared/groups/$group/policies
done

# Get the OS name to determine what program to install
os=$(hostnamectl | awk -F ' ' '/Operating System:/ {print $3}')

if [ $os == "Ubuntu" ]
then
	# Get quota support
	sudo apt-get install quota
	# Install quota_v1.ko and quota_v2.ko dependencies
	sudo apt-get install linux-image-extra-virtual	
fi

if [ $os == "CentOS" ]
then
	# Get quota support
	sudo yum install quota
fi

# Find the line within /etc/fstab that contains the "/" mount, and print the line number
line_num=$(awk -F ' ' '$2 == "\/" {print NR}' /etc/fstab)
# Get the mount name 
mount=$(awk -F ' ' '$2 == "\/" {print $1}' /etc/fstab)
# Get the format type
format=$(awk -F ' ' '$2 == "\/" {print $3}' /etc/fstab)

# Update "/" fstab mount to support user and group quotas
sudo sed -i "$line_num s/defaults/defaults,usrquota,grpquota/" /etc/fstab
# Remount disk with new quota rules
sudo mount -o remount /

# XFS partitions take special effort to support quotas
if [ $format == "xfs" ]
then
	# Install grub2 on the partition
	sudo grub2-install $mount --skip-fs-probe
	# Configure grub
	sudo grub2-mkconfig -o /boot/efi/EFI/${os,,}/grub.cfg
else
	# Run quotacheck to create aquota.group and aquota.user files
	sudo quotacheck -ugm /
fi

# Turn quota on
sudo quotaon -v /
# Set the quota limit to 10G for temp group
sudo setquota -g temp 9G 10G 0 0 /

```


- Run the create_groups script at this time, and the groups will be created with their associated directories and read-only protected policies directories. Re-run the same commands as before to verify groups, and lets check the permissions of the folders to verify that they're read-only (NOTE: they also have to be executable, otherwise you cannot `cd` into the directory)

- Our create_users scripts does several things at once

- Run the create_user script at this time, and the user will be created with their associated group.

- The output of the script for each type of group will will look like the following

- Once users have been created from both files, we can view all of users' home directories that have been added



- We can also see the associated folders for each user within their associated group directory



- We can also run our members command again to see that the members of each group match the directories that were created



- Log back into your account, and verify that your account has the appropriate permissions still. You should be able to make changes in the admin folder without sudo. You shouldn't be able to make changes in the temp/developers/staff folders without using sudo.


- Exit your account and log into a developer account. Verify that they are required to change their password, verify that they are using /bin/sh (C shell) instead of /bin/bash (bash shell)



- Verify the quota limits of each of our created groups. We can see that temp is the only one with soft and hard quotas set.




