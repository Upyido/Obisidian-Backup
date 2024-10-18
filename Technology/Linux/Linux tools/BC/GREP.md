- [  
    Menu](https://www.hostbillo.com/blog/how-to-use-grep-command-in-linux/#)

[![Hostbillo Blog - Web Hosting, Devops, Tech, and more](https://hostbillo.com/blog/wp-content/uploads/2022/03/hostbillo-logo.webp)](https://www.hostbillo.com/blog/ "Hostbillo Blog - Web Hosting, Devops, Tech, and more")

- [Search for](https://www.hostbillo.com/blog/how-to-use-grep-command-in-linux/#)

[Linux](https://www.hostbillo.com/blog/category/linux/)

# How To Use Grep Command In Linux/Unix?

 [![Photo of Arpit Saini](https://secure.gravatar.com/avatar/3934089db88200cab70e7bdd61787776?s=140&d=mm&r=g)](https://www.hostbillo.com/blog/author/arpit-saini/)Arpit SainiMay 7, 2024

0 628 6 minutes read

![How To Use Grep Command In Linux/Unix?](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/How-To-Use-Grep-Command-In-Linux_Unix.png)

Grep Command is a tool that is used to identify and match the string of characters in a file. It filters the content present in the files to make searching easy and efficient. So, you can effortlessly search any type of file in your system. Furthermore, the **Grep Command in Linux** is pre-installed for every Linux distribution. So, you can effectively use it in Ubuntu, Unix, and Debian OS.  

Through this guide, we let you know how to use the Grep command in Linux with examples to search the files from the terminal windows. Let’s get started!

## **Requirements**

– Linux or UNIX-like system

-Access to a terminal

-Access to a command line

-A user with access to files and directories

## **Explain Grep Command**

Grep is an important command-line tool in Linux / Unix. It is used to search and match the string of characters in a file. The word “**Grep**” implies “**Global Regular Expression Print”.**  The text search pattern in Grep Command Linux is also known as the **“Regular Expression”**. So, when you search for any query, then it finds the match in your file to print the line with your desired output. The command is very user-friendly and easy to use. That’s why you can search the string of characters through log files with a couple of clicks.

Also Read: [How to use top Command in Linux](https://www.hostbillo.com/blog/how-to-use-top-command-in-linux/)

## **Use Case of Grep Commands in Linux with Examples**

![Use Case of Grep Commands in Linux with Examples](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/Use-Case-of-Grep-Commands-in-Linux-with-Examples.png)

The Grep Command in Linux comprises three primary parts. The first or initial part begins with the **_grep_** Command. Then, it follows the search pattern to search the string in the file. 

The simplest Grep Command Syntax is:

![simplest Grep Command Syntax](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-91.png)

The above Grep Command in Linux contains so many options, pattern variables, and file names. Therefore, combine an ample range of options to get your desired output.  So, here we introduce you to the most popular Grep commands in Linux with Examples. 

### **#1. To search a File**

Use the syntax below to print a single line from a large file encompassing a specific character pattern. 

```
Grep ABC Sample1
```

![To search a File](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-90.png)

In this syntax, the ABC in the Sample 1 file displays all the lines from the “ABC” File content once it is executed. This command does not show you the accurate command but lists all the content with the name “ABC.” Instead of that, the terminal prints all the lines in which your entered character string is mentioned. See the example:

### **#2. To Search Multiple Files**

To search a number of files using the Linux Grep Command, insert the respective filenames you want to search in the file and separate it with a space character. 

In our case, the Grep Command in Linux to match the word ABC in three files sample, sample2, and sample3 look like this example:

```
grep ABC sample sample2 sample3
```

![To Search Multiple Files](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-96.png)

The terminal window prints every file name, and solid lines are contained in which it finds your searched string of characters.

You are free to append multiple files as needed. The terminal window prints a completely new line along with a filename for your search.

### **#3. Search All Files in Directory**

To search files in the present directory, use “*” instead of a filename in Grep Command Linux’s end.

In the example, we use XYZ as a search criterion:

```
Grep XYZ* sample
```

![Search All Files in Directory](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-102.png)

The output shows that the list of file names starts with XYZ and returns the entire line.  

### **#4. To Find Whole Words Only**

Grep Command Linux enables you to identify and print the results for the entire string. To search for the word ABC in all the files in your present directory, use the grep command “-w” to append.

```
grep -w ABC *
```

![To Find Whole Words Only](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-99.png)

This command only prints the lines which comprise the complete word of your search result. 

If you miss the “-w” command or omit it from the code, the grep command still runs and displays a search pattern even if it contains the substring of another word. 

### **#5. To ignore cases in Grep Searches**

**Grep Commands are case-sensitive**. One of the most useful operators used in the grep searches for searching string of characters is “**-i.**”  Instead of printing the output or showing results in lowercase, the terminal displays both uppercase and lowercase results. The final output includes the line of both cases.

Example:

```
grep -i ABC* sample
```

![To ignore cases in Grep Searches](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-100.png)

When we use the **-i** operator to search the files in the directory you are working now for ABC, the output you’ll see on your terminal windows be like:

### **#6. To Search Subdirectories**

Use the “-r” operator to the grep command you are using now to include the subdirectories in a search.

```
grep -r ABC *
```

![To Search Subdirectories](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-97.png)

When you run the above command, it prints all the related matches for all files present in your current directory, subdirectories, and accurate path with the filename. We also include the -w operator to show you the entire string of characters in the below instance. But the format of the output will be the same.

### **#7. Inverse grep Search**

To print all the lines that are unmatched with your search pattern of characters, use the grep command. Also, to invert the search, use the append **-v** operator to a grep command.

To omit all the lines that contain ABC, enter.

```
grep -v ABC sample
```

![Inverse grep Search](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-99.png)

Using this syntax, ensure the terminal prints all the lines that do not contain your search word. To ignore the case-sensitive outputs, use “-i.”

### **#8. To Show Lines That Exactly Match a Search String**

The Grep Command prints the entire line when it finds the result of your match. If you want the command to only display the output comprising the complete match of your search, then use the -X option.  

```
grep -x "ABC number3" *
```

![To Show Lines That Exactly Match a Search String](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-97.png)

In the output, you’ll get the lines of your exact match. If other characters or strings are included on the line, then Grep Command in Linux does not include them in the search results. Always consider using quotation marks whenever necessary in a space or a symbol in a search pattern.

Here we show you a comparison with or without the -x operator in our Linux Grep Command.

### **#9. To List Names of Matching Files**

Sometimes, you want to see only file names containing content by eliminating the actual lines in the files in your current directory. For that, you should use the “**-l”** operator.

```
grep -l ABC *
```

![To List Names of Matching Files](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-101.png)

You’ll get the exact filenames on your terminal window to contain ABC in the present directory in the output. But the operator does not show you the corresponding word mentioned in the line. 

In addition, you can use the **-r** operator to include all subdirectories in your search.

### **#10. To Count, the Number of Matches**

Grep Command in Linux displays the exact number of lines and filenames to identify the accurate match for your word. 

To count the number of matches, use the **_-c_** operator:

```
grep -c ABC *
```

![To Count, the Number of Matches](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-92.png)

### **#11. To Display the Number of Lines Before or After a Search String**

Sometimes, you require more content when you want to search for the most relevant results. 

Add the following operators to add the desired lines before and after the match or sometimes both:

#### **Use “-A” operator and a number of lines to display after a match:**

```
grep -A 1 ABC sample 
```

![To Display the Number of Lines Before or After a Search String](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-95.png)

The command you use above prints three lines after a match. 

#### **_Use “-B” operator and a number of lines to display before a match_****:**

```
Grep "-B" 2 ABC Sample
```

![To Display the Number of Lines Before a match](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-94.png)

The use of this operator along with numerical value “2” prints two lines before the match.

#### **_Use the “-C” operator and several lines to display before and after the match:_** 

```
grep -C 2 ABC sample
```

![](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-103.png)

The use of command in Linux grep Commands to print two lines before and after the match.

### **12. To Display Line Numbers with grep Matches**

When grep prints results with multiple matches, it’s easy to see the line numbers. 

So, to append the matches, use the “**-n**” operator with any grep command. It will display the line numbers. 

We will search for the ABC in the directory we are working on and display the output as two lines before and after the matches with their line numbers. 

```
grep -n -C 2 ABC sample
```

![To Display Line Numbers with grep Matches](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-98.png)

### **#13. Limit grep Output to a Fixed Number of Lines**

For grep search patterns, files similar to log can contain multiple matches. Limit the number of lines in the grep output by appending the “**-m**” option and a number to the command.  

```
grep -m 2 ABC sample
```

![Limit grep Output to a Fixed Number of Lines](https://www.hostbillo.com/blog/wp-content/uploads/2024/05/image-93.png)

When you execute this command, it will display the terminal prints with the first 2 matches identified in the sample file. 

If you do not declare the files in the current directory, the output automatically fetches the first two results from every file and the filename containing the respective matches.