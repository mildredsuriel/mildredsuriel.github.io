# NETWORKING

Document network setup. This should include locations of any files you've created or need to reference. You should include any programs you've installed or updated as well, with dates of when you've done those things. Include a short document including how you did any of the installs or updates. 

Write a script to dump network info (including ip, dns, open ports and anything else you think is useful) to the commandline and to a file.  Make sure the name of the file includes the date and the purpose.

Deliverables:

A document that is your current network setup, including notes of what is installed, the last time it was updated and any changes you've made to the defaults. 

A well commented and well tested script, and a sample run of your script on each server.  Include any instructions needed for running the script.  Such as, does it need to be run in a special folder? does it save the textfile to a special place (it should) and where that might be? Which commands you've chosen to put in the script and why.

- Running the `ip address` command will list all IP addresses for your device. You can see that there is your standard loopback IP, ethernet IP, and wlan IP (although wireless is currently disabled)

![image](https://user-images.githubusercontent.com/64757540/97744669-08485a80-1abe-11eb-9511-b490c77c8494.png)

- Running `speedtest-cli` will begin a test to a close server to determine your latency and bandwidth

![image](https://user-images.githubusercontent.com/64757540/97744724-1dbd8480-1abe-11eb-802c-f7fbd5d1b01f.png)

- using `nslookup` on a website should provide you the DNS information of your system

![image](https://user-images.githubusercontent.com/64757540/97744766-3037be00-1abe-11eb-981b-5ac0fefe1710.png)

- You can also find your DNS within `/etc/resolv.confg`

![image](https://user-images.githubusercontent.com/64757540/97744811-3fb70700-1abe-11eb-86c5-f3bbb337457e.png)

- `ss` is a netstat program replacement that can be used to get information about ports on your network.

![image](https://user-images.githubusercontent.com/64757540/97744881-5bbaa880-1abe-11eb-8ff2-4fef7ea7a6d8.png)
