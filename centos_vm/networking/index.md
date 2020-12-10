# NETWORKING

Document network setup. This should include locations of any files you've created or need to reference. You should include any programs you've installed or updated as well, with dates of when you've done those things. Include a short document including how you did any of the installs or updates. 

Write a script to dump network info (including ip, dns, open ports and anything else you think is useful) to the commandline and to a file.  Make sure the name of the file includes the date and the purpose.

Deliverables:

A document that is your current network setup, including notes of what is installed, the last time it was updated and any changes you've made to the defaults. 

A well commented and well tested script, and a sample run of your script on each server.  Include any instructions needed for running the script.  Such as, does it need to be run in a special folder? does it save the textfile to a special place (it should) and where that might be? Which commands you've chosen to put in the script and why.

- Running the `ip address` command will list all IP addresses for your device. You can see that there is your standard loopback IP, ethernet IP, and wlan IP (although wireless is currently disabled)

![image](https://user-images.githubusercontent.com/64757540/100123651-c1dde580-2e48-11eb-9973-55b2209e03c0.png)

- Speedtest is not downloadable via yum, so we will use wget to grab it from online

![image](https://user-images.githubusercontent.com/64757540/100123756-dc17c380-2e48-11eb-9014-8d8bb1384c6f.png)

- Running `speedtest-cli` will begin a test to a close server to determine your latency and bandwidth

![image](https://user-images.githubusercontent.com/64757540/100123788-e20da480-2e48-11eb-84c1-2aaff8f8b2b5.png)

- using `nslookup` on a website should provide you the DNS information of your system

![image](https://user-images.githubusercontent.com/64757540/100123814-e8038580-2e48-11eb-9af7-b66e5c4b650d.png)

- You can also find your DNS within `/etc/resolv.confg`

![image](https://user-images.githubusercontent.com/64757540/100123855-f05bc080-2e48-11eb-9a4c-3bbc66681098.png)

- `ss` is a netstat program replacement that can be used to get information about ports on your network.

![image](https://user-images.githubusercontent.com/64757540/100123876-f5b90b00-2e48-11eb-98c4-cfb078c992d5.png)

- All of the above commands can be executed by downloading the network script.

![image](https://user-images.githubusercontent.com/17841536/101684644-c0a9dc80-3a34-11eb-88e9-67a0957e2200.png)

![image](https://user-images.githubusercontent.com/17841536/101684833-0070c400-3a35-11eb-9c28-024cfb59bad1.png)

![image](https://user-images.githubusercontent.com/17841536/101684860-0b2b5900-3a35-11eb-99e1-f7450b4eea9e.png)

- After running the script, we can see that the output is split up between several files for easier parsing 

![image](https://user-images.githubusercontent.com/17841536/101684882-141c2a80-3a35-11eb-84b4-ddb823edfbb0.png)

