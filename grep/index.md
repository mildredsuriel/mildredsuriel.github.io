- Print all lines containing the string San

This is just a basic grep command with the string and file specified.

![image](https://user-images.githubusercontent.com/64757540/97485902-1e74e000-1931-11eb-82cb-fe2e281fe363.png)

- Print all lines where the person's first name starts with J. 

This command uses the ^ key to signify to check the beginning of a line for a J.

![image](https://user-images.githubusercontent.com/64757540/97485944-2af93880-1931-11eb-9500-ceaf82289a0c.png)

- Print all lines ending in 700. 

This command uses the $ at the end to signify searching at the end of the line.

![image](https://user-images.githubusercontent.com/64757540/97485962-30ef1980-1931-11eb-9bd9-0f9be9b6ed4f.png)

- Print all lines that don't contain 834.

The -v option searches for lines not containing a pattern.  We use grep twice and pipe since blank lines count within the search, and so it made the screenshot hard to see all of the results.

![image](https://user-images.githubusercontent.com/64757540/97485997-39dfeb00-1931-11eb-8197-30a32fa7ecb3.png)

- Print all lines where birthdays are in January.

All January birthdays begin with a colon (following the zip code), and then have “1/” 

![image](https://user-images.githubusercontent.com/64757540/97486025-4401e980-1931-11eb-9275-3b1934419310.png)

- Print all lines where the phone number is in the 408 area code.

All phone numbers are followed by a colon and the 408- area code.

![image](https://user-images.githubusercontent.com/64757540/97486045-49f7ca80-1931-11eb-9557-ebb1ae45c597.png)

- Print all lines containing an uppercase letter, followed by four lowercase letters , a comma, a space, and one uppercase letter.

Greps for an upper case character [A-Z], followed by 4 lower cases letters, a comma, space and other uppercase.

![image](https://user-images.githubusercontent.com/64757540/97486060-50864200-1931-11eb-9ddf-b75cea15dd57.png)

- Print lines where the last name begins with k or K, s or S .

We look for uppercase or lowercase k and s. To skip the first name, we look for the first space within the line, signifying the end of the first name.

![image](https://user-images.githubusercontent.com/64757540/97486079-57ad5000-1931-11eb-94b4-0390af135277.png)

- Print lines preceded by a line number where the salary is a six-figure number.

All salaries are at the end of the line and contain at least 6 numbers after a colon.

![image](https://user-images.githubusercontent.com/64757540/97486095-5da33100-1931-11eb-87cb-48ccb6fbf2a8.png)

- Print lines containing Lincoln or lincoln (remember that grep is insensitive to case)

The -i option makes the search case insensitive.

![image](https://user-images.githubusercontent.com/64757540/97486122-6562d580-1931-11eb-8b51-3288fc713a41.png)


