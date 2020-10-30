- Change the name Jon to Jonathan.
	This is a simple substitute of Jon for Jonathan.
 
![image](https://user-images.githubusercontent.com/64757540/97745187-d97eb400-1abe-11eb-844f-05b5809a4e4a.png)

2. Delete the first four lines.
	Deleting lines is as simple as specifying the line range followed by a d
 
![image](https://user-images.githubusercontent.com/64757540/97745205-e3a0b280-1abe-11eb-902f-e15d1108fe00.png)

3. Print lines 7 through 11 .
	Printing lines is as simple as specifying the line range followed by a p. We also need -n when we are printing, otherwise all lines will be printed in the process.

![image](https://user-images.githubusercontent.com/64757540/97745229-ebf8ed80-1abe-11eb-8e58-ee64223af82c.png)
 
4. Delete lines containing Lane .
	Deleting lines with certain phrases just requires searching for the string and marking it with d for delete.

![image](https://user-images.githubusercontent.com/64757540/97745252-f87d4600-1abe-11eb-9d5c-24a3b70c1103.png)

5. Print all lines where the birthdays are in October or December .
	This required finding where the birthdays were in the file. All birthdays are after a colon and are in MM/DD/YY format. So, if we search for a colon and the months of Oct+Dec (10 and 12), we can print out these lines specifically (don’t forget -n for printing). Also note, the backslash is a special character for sed, so it must be escaped with a forward slash first to search for it. 

![image](https://user-images.githubusercontent.com/64757540/97745271-00d58100-1abf-11eb-8f5b-96de5fd4aca4.png)

6. Append three asterisks to the end of lines starting with Fred
	To append to the end of the lines starting with Fred, we look for lines that begin with Fred and are followed by anything (Fred.*), we then use the & to print the regex string found, and add our 3 asterisks to the end.
  
![image](https://user-images.githubusercontent.com/64757540/97745296-0a5ee900-1abf-11eb-8d52-138271541413.png)

	NOTE : I was using bash for windows to complete the other commands, but that resulted in the wrong output in this case, so I had to use an actual Linux system instead. Here is the wrong output in the windows for bash environment.

![image](https://user-images.githubusercontent.com/64757540/97745310-10ed6080-1abf-11eb-8144-8e4403e6c796.png) 

7. Replace the line containing Jose with JOSE HAS RETIRED .
	Search for any string with Jose in it, and replace the whole string with JOSE HAS RETIRED.
 
![image](https://user-images.githubusercontent.com/64757540/97745329-19459b80-1abf-11eb-8d85-af663e55ce01.png)

8. Change Popeye 's birthday to 11/14/99 . Assume you don't know Popeye's original birthday. Use a regular expression to search for it.
	All birthdays are in the format of “:MM/DD/YY:”, so if we look for a colon, a string of numbers, a slash, another string of numbers, another slash, and a final string of numbers, we can replace that found birthday string with our own birthday.
 
![image](https://user-images.githubusercontent.com/64757540/97745349-206ca980-1abf-11eb-90cc-3136ce281379.png)

9. Delete all blank lines.
	This command uses the start of line character ^ and the end of line character $ to search for a string that doesn’t contain any characters between (aka blank line), and then deletes them.

![image](https://user-images.githubusercontent.com/64757540/97745368-25315d80-1abf-11eb-8c91-1fe2a4028bbe.png)

10. Write a sed script that will
a. Insert above the first line the title  - PERSONNEL FILE -.
b. Remove the salaries ending in  6 00 .
c. Print the contents of the file with the last names and first names reversed .
d. Append at the end of the file  THE END .
 
![image](https://user-images.githubusercontent.com/64757540/97745398-2f535c00-1abf-11eb-850f-cffbd728b301.png)

Sources:
https://flylib.com/books/en/4.356.1.40/1/
https://www.cyberciti.biz/faq/using-sed-to-delete-empty-lines/
https://youtu.be/YMqOocY0ovs
https://www.gnu.org/software/sed/manual/html_node/Escapes.html

