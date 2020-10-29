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

![image](https://user-images.githubusercontent.com/64757540/97641052-67ec2a80-1a18-11eb-8d15-677d3571e561.png)

- You can verify your groups exist by grepping in /etc/group

![image](https://user-images.githubusercontent.com/64757540/97641107-8a7e4380-1a18-11eb-98cf-c67bad52f2ab.png)

- You can also install members so that you can view members of groups (we'll verify our account once we create it next)

![image](https://user-images.githubusercontent.com/64757540/97641381-2019d300-1a19-11eb-8ab4-ee89c4a2d8aa.png)

- Create a new account for yourself using useradd. Assign our user to the admin group at the same time. Notice that our account is listed as a member of the admin group.

![image](https://user-images.githubusercontent.com/64757540/97641738-f3b28680-1a19-11eb-9edd-3509b2b4622b.png)

- We also want to give ourselves sudo permisions so that we can make admin changes (admin accounts may get this by default, but it doesn't hurt to run still)

![image](https://user-images.githubusercontent.com/64757540/97641674-d1206d80-1a19-11eb-8236-9da7fda7f173.png)

- Set a temp password for your new account, and then make it required that you update when you log in (it may seem pointless now, but the script will do this for every other user besides you). You are now logged in on your account.

![image](https://user-images.githubusercontent.com/64757540/97642085-b8fd1e00-1a1a-11eb-81ba-77f9edd0af4b.png)

- You can always exit your user account to return to the main ubuntu account by running exit. Both accounts have similar permissions, so the rest of this can be run on either account.

![image](https://user-images.githubusercontent.com/64757540/97643569-750c1800-1a1e-11eb-9ee7-04bfa362bedf.png)

- Now that your user account exists, lets get the scripts to create all of the other users. You can download the scripts I used with the following `wget` commands to whatever directory you choose (I recommend placing it within a scripts directory somewhere, like I have)

![image](https://user-images.githubusercontent.com/64757540/97643693-d16f3780-1a1e-11eb-88f5-3e165f778357.png)

- Our create_groups scripts does several things at once

![image](https://user-images.githubusercontent.com/64757540/97643962-62dea980-1a1f-11eb-91d2-5fedda487833.png)

- Run the create_groups script at this time, and the groups will be created with their associated directories and read-only protected policies directories. Re-run the same commands as before to verify groups, and lets check the permissions of the folders to verify that they're read-only (NOTE: they also have to be executable, otherwise you cannot `cd` into the directory)



- Our create_users scripts does several things at once

![image](https://user-images.githubusercontent.com/64757540/97643929-4e9aac80-1a1f-11eb-8fb9-cb2f27a1ed1c.png)

- Run the create_user script at this time, and the user will be created with their associated group.

![image](https://user-images.githubusercontent.com/64757540/97642944-ce734780-1a1c-11eb-8c36-e67d10f2aa4d.png)

- The output of the script for each type of group will will look like the following

![image](https://user-images.githubusercontent.com/64757540/97642520-c23aba80-1a1b-11eb-9cef-611de0c9d38f.png)

- Once users have been created from both files, we can view all of users' home directories that have been added

![image](https://user-images.githubusercontent.com/64757540/97642545-da123e80-1a1b-11eb-9a7f-7cd321f0e2f6.png)

- We can also see the associated folders for each user within their associated group directory

![image](https://user-images.githubusercontent.com/64757540/97642598-f8783a00-1a1b-11eb-9f63-1905aa97dc30.png)

- We can also run our members command again to see that the members of each group match the directories that were created

![image](https://user-images.githubusercontent.com/64757540/97642632-12198180-1a1c-11eb-9f4e-35bbc329888b.png)

- Log back into your account, and verify that your account has the appropriate permissions still. You should be able to make changes in the admin folder without sudo. You shouldn't be able to make changes in the temp/developers/staff folders without using sudo.

![image](https://user-images.githubusercontent.com/64757540/97642256-1b561e80-1a1b-11eb-9b6b-07c2673b910d.png)

- Exit your account and log into a developer account. Verify that they are required to change their password, verify that they are using /bin/sh (C shell) instead of /bin/bash (bash shell)

![image](https://user-images.githubusercontent.com/64757540/97642823-82280780-1a1c-11eb-8e66-91462681dbce.png)

![image](https://user-images.githubusercontent.com/64757540/97642831-86542500-1a1c-11eb-9c31-09983f907907.png)




