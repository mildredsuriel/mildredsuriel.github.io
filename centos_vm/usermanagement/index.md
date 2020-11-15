You have been asked to add to your system four groups of users: admin, developers, staff and temp. Each should have their own group and an associated folder that they have access to. Within each groups folder should be a read only folder for policies and such. There should also be a public read only folder for general company policy.  

You should add users for testing from the attached user lists. Any repetitive task should be scripted (shell or Python or hybrid). Admin users should be added to sudo with full permission. Each group should have a skeleton directory. The developers should default to c shell. Temps should have a limit to their disk usage.

Turn in any scripts you have written, a link to your GitHub where you have posted your scripts, and  screenshot(s) that best shows you were able to complete this task successfully. Use your own best judgment for how many you need, but remember this will be added to your documentation.

Test your scripts on both levels of UserNames attached to this lab. For adding to groups, any users can be added to any group, split it up however you like but document who's in which group. This lab is considered complete when both UserNames are added to both your servers using the scripts you've made, including the group add.

Deliverables:

A well commented script (or set of scripts) that achieves the set out tasks as outlined above including  A link to your GitHub where you've posted your scripts.

A short document explaining how you decided to set up your username rules (first letter last name, first name only, random characters and last name, etc) as well as a list of who is in which group. And any extra rules or regulations you've decided are important for each group.  You should also include any dicumentation needed for how to run your scripts.  Do they  need any special files? Any special formats expected? Any assumptions you've made as you're writing your scripts?

A short document showing you've been able to successfully add all users from both levels to both your distros.  Can be done with screenshots or a textfile taken from your servers

- Creating groups is simply a `groupadd` command for the group you want. I can quickly create all the groups now (although we will automate this in the script, and we really only care about the admin group existing at this point which it should by default.

![image](https://user-images.githubusercontent.com/64757540/98878115-26b03d80-2450-11eb-9b8f-43102a870f92.png)

- You can verify your groups exist by grepping in /etc/group

![image](https://user-images.githubusercontent.com/64757540/98878137-392a7700-2450-11eb-8b6a-f1e8dc767a2c.png)

- Lets go ahead and add ourselves as a user to the admin group. We can verify that we are member of the group using getent

<p align="center">
  <img src="https://user-images.githubusercontent.com/64757540/98878198-6119da80-2450-11eb-91de-715132ce90ed.png">
</p>

- Lets get the scripts to create all of the other users. You can download the scripts I used with the following `wget` commands to whatever directory you choose (I recommend placing it within a scripts directory somewhere, like I have)

```
sudo wget https://raw.githubusercontent.com/mildredsuriel/mildredsuriel/master/bash/linuxadmin/create_users.sh
sudo wget https://raw.githubusercontent.com/mildredsuriel/mildredsuriel/master/bash/linuxadmin/create_groups.sh
```

<p align="center">
  <img src="https://user-images.githubusercontent.com/64757540/98878281-958d9680-2450-11eb-96d4-2884b5b7a30d.png">
</p>

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

![image](https://user-images.githubusercontent.com/64757540/99195702-48157000-2755-11eb-9c5d-a6ecfc541f70.png)

- Our create_users scripts does several things at once

```bash
# List of possible groups to add users to
groups=("temp" "staff" "developers" "admin")

# Keep track of which group we're adding a user to
i=0

# Get the OS name to determine what program to install
os=$(hostnamectl | awk -F ' ' '/Operating System:/ {print $3}')

# Default name of sudo group is usually sudo
sudo_group="sudo"

if [ $os == "CentOS" ]
then
	# The default sudo group in CentOS is called wheel
	sudo_group="wheel"
fi

# Take in the first argument as the file to open and loop through each line of the file
while IFS= read -r line; do
        # Assign the user a group
        group=${groups[$i]}
		# Remove spaces from name
        username=${line//[[:blank:]]/}
		# Remove hyphens from name
        username=${username//-/}
		# Make username first 20 characters of name
        username=${username:0:20}

        echo "Creating a user and assign them a group : sudo useradd -m -c \"$line\" -s/bin/bash -G $group $username"
        sudo useradd -m -c "$line" -s/bin/bash -G $group $username -p Linux2020

        # Require the username to update the default password when signing in
        sudo passwd -e $username

        echo "Creating a user file in their group : sudo mkdir groups/$group/$username"
        sudo mkdir /home/shared/groups/$group/$username

        # Grant users of admin group sudo permissions
        if [ $group == "admin" ]
        then
                echo "Granting sudo priveleges to $username  : sudo usermod -a -G $sudo_group $username"
                sudo usermod -a -G $sudo_group $username
        fi

        # Set developer shells to C shell
        if [ $group == "developers" ]
        then
                echo "Setting C shell as default for developer $username : sudo chsh --shell /bin/sh $username"
                sudo chsh --shell /bin/sh $username
        fi

        # Increment value so that next user is in a different group (even distribution across each group, % 4 handles going back to the first value
        let "i++"
        i=$((i%4))
done < "$1"
```

- Run the create_user script at this time, and the user will be created with their associated group. The output of the script for each type of group will will look like the following

![image](https://user-images.githubusercontent.com/64757540/99195736-9dea1800-2755-11eb-92f4-247caeb5c330.png)

- Once users have been created from both files, we can view all of users' home directories that have been added

![image](https://user-images.githubusercontent.com/64757540/99195750-b35f4200-2755-11eb-8a61-6bd2903a2f02.png)

- We can also see the associated folders for each user within their associated group directory

![image](https://user-images.githubusercontent.com/64757540/99195764-c70aa880-2755-11eb-90fe-0a6042093b82.png)

![image](https://user-images.githubusercontent.com/64757540/99195766-cd008980-2755-11eb-968e-da34867b2c3a.png)

- We can also run our `getent` command again to see that the members of each group match the directories that were created

![image](https://user-images.githubusercontent.com/64757540/99195770-d558c480-2755-11eb-8750-88f325325b9d.png)

- Log back into your account, and verify that your account has the appropriate permissions still. You should be able to make changes in the admin folder without sudo. 

![image](https://user-images.githubusercontent.com/64757540/99195824-210b6e00-2756-11eb-8519-d67112acb310.png)

- You shouldn't be able to make changes in the temp/developers/staff folders without using sudo.

![image](https://user-images.githubusercontent.com/64757540/99195831-2c5e9980-2756-11eb-8b3d-fdc1345477a6.png)

- Exit your account and log into a developer account. Verify that they are using /bin/sh (C shell) instead of /bin/bash (bash shell)

![image](https://user-images.githubusercontent.com/64757540/99195843-45ffe100-2756-11eb-9411-e3ba95beebbe.png)

- Verify the quota limits of each of our created groups. We can see that temp is the only one with soft and hard quotas set.

![image](https://user-images.githubusercontent.com/64757540/99195848-4c8e5880-2756-11eb-8ba6-aca13af1581f.png)



