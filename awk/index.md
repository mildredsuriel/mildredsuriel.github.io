# AWK

Lab3
1. Print all the phone numbers.
```
awk -F ':' '{print $2}' lab3.data
```
2. Print Dan's phone number.	
```
	awk -F ':' '/Dan/ {print $2}' lab3.data
```
3. Print Susan's name and phone number.
```
	awk -F ':' '/Susan/ {print $1 $2}' lab3.data
```
4. Print all last names beginning with S .
```
	awk '{print $2}' lab3.data | awk -F ":" '/S/ {print $1}'
```
5. Print all first names beginning with either a C or J.
```
	awk '/[CJ]/ {print $1}' lab3.data
```
6. Print all first names containing only four characters.
```
	awk 'length($1) == 4 {print $1}' lab3.data
```
7. Print the first names of all those in the 916 area code.
```
	awk '/916/ {print $1}' lab3.data
```
8. Print Mike 's campaign contributions. Each value should be printed with a leading dollar sign; e.g., $250 $100 $175.
```
	awk -F ':' '/Mike/ {print "$" $3 " $" $4 " $" $5}' lab3.data
```
9. Print last names followed by a comma and the first name.
```
	awk -F ':' '{print $1}' lab4.data | awk '{print $2 "," $1}'
```
10. Write an awk script called facts that
- Prints full names and phone numbers for the Savages .
- Prints Chet 's contributions.
- Prints all those who contributed $50 the first month.
```
	awk -F ':' -f facts.awk lab4.data
```	

Lab4
```
	awk -F ':' '$4 > 110 {print $1}' lab4.data
	awk -F ':' '$5 < 75 {print $1 $2}' lab4.data
	awk -F ':' '$3 > 75 && $3 < 150 {print $1}' lab4.data
	awk -F ':' '$3 + $4 + $5 < 700 {print $1}' lab4.data
	awk -F ':' '($3 + $4 + $5) / 3 > 100 {print $1}' lab4.data
	awk -F ':' '!/\(916/ {print $1}' lab4.data
	awk '{print NR,$0}' lab4.data
	awk -F ':' '{print $1 " - $" $3+$4+$5}' lab4.data
	awk -F ':' '{variable=$4; if ($1 == "Chet Main") variable=$4+10; $4=variable; print $0}' lab4.data
	awk -F ':' '{variable=$1; if ($1 == "Nancy McNeil") variable="Doris Shutt"; $1=variable; print $0}' lab4.data
```











Lab4
The database contains the names , phone numbers , and money contributions to the party campaign for the past three months.
Print the first and last names of those who contributed more than $110 in the second month.
Print the names and phone numbers of those who contributed less than $75 in the last month.
Print the names of those who contributed between $75 and $150 in the first month.
Print the names of those who contributed less than $700 over the three-month period.
Print the names and addresses of those with an average monthly contribution greater than $100 .
Print the first name of those not in the 916 area code.
Print each record preceded by the number of the record.
Print the name and total contribution of each person.
Add $10 to Chet 's second contribution.
Change Nancy McNeil 's name to Doris Shutt.