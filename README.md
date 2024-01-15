# Use-Regular-Expressions-to-Find-Patterns-in-Python

<h2>Introduction</h2>

Security analysts often analyze log files, including those that contain information about login attempts. For example as an analyst, I might flag IP addresses that relate to unusual attempts to log in to the system.

Another area of focus in cybersecurity is detecting devices that require updates. Software updates help prevent security issues due to vulnerabilities.

Using regular expressions in Python can help automate the processes involved in both of these areas of cybersecurity. Regular expression patterns and functions can be used to efficiently extract important information from strings and files.

In this lab, I'll write regular expressions to extract information such as device IDs or IP addresses.

<h2>Scenario</h2>

In this lab, I'm working as a security analyst and my main tasks are as follows:

extracting device IDs containing certain characters from a log; these characters correspond with a certain operating system that requires an update.

extracting all IP addresses from a log and then comparing them to those that are flagged in a list.

<h2>Task 1</h2>

To work with regular expressions in Python, start by importing the ```re``` module. This module contains many functions that will help me work with regular expressions. By running the following code cell, the module will be available through the rest of the notebook.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/52641177-cd2d-4337-84c3-6863ec0ebb56)

<h2>Task 2</h2>

Currently, I am looking for device IDs that begin with "r15". These characters indicate that the device is running an operating system that must be updated.

I'm given a log of device IDs, stored in a variable named devices. My eventual goal is to extract the device IDs that start with the characters "r15". For now, display the contents of the whole string to examine what it contains.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/2ac1b4da-598f-422e-b090-c3d803444914)

<h2>Task 3</h2>

In this task, I'll write a pattern to find devices that start with the character combination of "r15".

Use the regular expression symbols \w and + to create the pattern, and store it as a string in a variable named target_pattern.

Note that the code cell will contain only variable assignments, so running it will not produce an output.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/5b706ab7-a0ec-4961-b26a-a077ef27a7d1)

The regular expression pattern used was "r15\w+". Without the r15, the pattern will not match with device IDs that start with the characters "r15". Without the \w, the pattern will not match with alphanumeric characters following "r15". Without the +, the pattern will match with only the first alphanumeric character that occurs after "r15".

<h2>Task 4</h2>

Use the findall() function from the re module to find the device IDs that the target_pattern matches with. 

Note: To use re.findall() in Tasks 4, 7, 8, 9, and 11, I must have previously run the code import re in Task 1.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/8c289793-fdd6-4e0c-869a-d32d9e0b0e55)

<h2>Task 5</h2>

Now, the next task I'm responsible for is analyzing a network security log file and determining which IP addresses have been flagged for unusual activity.

I'm given the log file as a string stored in a variable named log_file. There are some invalid IP addresses in the log file due to issues in data collection. My eventual goal is to use regular expressions to extract the valid IP addresses from the string.

Start by displaying the contents of the log_file to examine the details inside.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/6cc28872-236a-423b-abff-c72cb70a78e9)

hint: Recall that this task's focus is on IP addresses in the form of xxx.xxx.xxx.xxx, where each x is a digit. In other words, these addresses have the following format: three digits followed by a period, three digits followed by a period, three digits followed by a period, three digits.

To build a pattern that matches with IP addresses in this form, use the \d symbol for every digit and the \. for every period that should be in the IP address.

<h2>Task 6</h2>

In this task, I'll build a regular expression pattern that I can use later on to extract IP addresses that are in the form of xxx.xxx.xxx.xxx. In other words, I'll extract all IP addresses that contain four segments of three digits that are separated by periods.

Write a regular expression pattern that will match with these IP addresses and store it in a variable named pattern. Use the regular expression symbols \d and \. in my pattern. Note that the symbol \d matches with digits, in other words, any integer between 0 and 9. Since I'll just build the pattern here, there won't be any output when I run this cell.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/29b63d4d-4dc6-4e1b-961c-bc65aca2d248)

<h2>Task 7</h2>

In this task, I'll use the re.findall() function on the regular expression pattern stored in the pattern variable and the provided log_file to extract the corresponding IP addresses. Afterward, run the cell and take note of what it outputs.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/4aa35f5e-e9d4-49b9-b4b2-7cc89f61d251)

Examples of IP addresses that were extracted include "192.168.152.148" and "192.168.190.178". Examples of IP addresses that were not extracted include "192.168.22.115" and "1923.1689.3.24". IP addresses that have fewer than three digits per segment, such as "192.168.22.115" (which has two digits in the third segment and three digits in each of the other segments), are valid IP addresses but were not extracted.

<h2>Task 8</h2>

There are some valid IP addresses in the log_file that I haven't extracted yet. This is because each segment of digits in a valid IP address can have anywhere between one and three digits.

Adjust the regular expression in the pattern to allow for variation in the number of digits in each segment. I can do this by using the + symbol after the \d symbol. Afterwards, use the updated pattern to extract the remaining IP addresses. Then, run the cell to analyze the results.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/57b29a2a-6498-4100-be40-4df2288eb1e1)

Now, extracted IP addresses include those with exactly three digits per segment (such as "192.168.152.148"), those with fewer than three digits per segment (such as "192.168.22.115"), and those with more than three digits per segment (such as "1923.1689.3.24"). Not all of the extracted IP addresses have between one and three digits in every segment.

<h2>Task 9</h2>

Note that all the IP addresses are now extracted but they also include invalid IP addresses with more than three digits per segment.

In this task, I'll update the pattern using curly brackets instead of the + symbol. In regular expressions, curly brackets can be used to represent an exact number of repetitions between two numbers. For example, {2,4} in a regular expression means between 2 and 4 occurrences of something. Applying this to an example, \w{2,4} would match with two, three, or four alphanumeric characters. Afterward, I'll call the re.findall() function on the updated pattern and the log_file and store the output in a variable named valid_ip_addresses.

Then, display the contents of valid_ip_addresses and run the cell to analyze the results.

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/74ed95e5-bd06-4fe8-9af1-095ceeba1c21)

Here, the extracted IP addresses all have between one and three digits per segment. Recall that in Task 7, only IP addresses with exactly three digits per segment were extracted. And in Task 8, IP addresses with more than three digits per segment were also extracted.

<h2>Task 10</h2>

Now, all of the valid IP addresses have been extracted. The next step is to identify flagged IP addresses.

I'm given a list of IP addresses that have been previously flagged for unusual activity, stored in a variable named flagged_addresses. When these addresses are encountered, they should be investigated further. This list is just for educational purposes and contains examples of private IP addresses that are found only within internal networks.

Display this list and examine what it contains by running the cell. 

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/df6de045-1128-4145-8e25-565b13658ab8)

<h2>Task 11</h2>

Finally, I will write an iterative statement that loops through the valid_ip_addresses list and checks if each IP address is flagged. In the following code, the address will be the loop variable. Also, include a conditional that checks if the address belongs to the flagged_addresses list. If so, it should display "The IP address ______ has been flagged for further analysis." If not, it should display "The IP address ______ does not require further analysis."

![image](https://github.com/n8som/Use-Regular-Expressions-to-Find-Patterns-in-Python/assets/110139109/b376bcd6-0aab-46db-b81d-3066926191ad)

<h2>Conclusion</h2>

What are the key takeaways from this lab?

- Regular expressions in Python allow me to create patterns that I can then use to find important strings.
- Regular expression patterns can be built to match specific characters and character combinations.
- Examples of regular expression symbols practiced in this lab:
  - ```\w``` represents any alphanumeric character.
  - ```+``` represents one or more occurrences of the previous character in the regular expression.
  - ```\d``` represents any digit.
  - ```\.``` represents a period.
  - ```{x,y}``` represents anywhere between x and y number of occurrences of the previous character in the regular expression. The x and y can be replaced with any two positive integers to indicate an exact range for the number of occurrences.
- The ```re``` module in Python contains functions that are useful when working with regular expressions.
  - One example is the ```re.findall()``` function, which takes in a regular expression pattern as well as a string, checks for all instances in the string that match with the pattern and outputs a list of the matches.

