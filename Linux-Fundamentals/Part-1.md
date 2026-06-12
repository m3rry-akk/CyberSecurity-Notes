# Linux Fundamentals Part 1 🐧

Welcome to my comprehensive study notes for Linux Fundamentals Part 1. This document captures every concept, command, terminal snippet, and practical example covered in the module.

---

## 🐧 Introduction to the Linux Terminal

A large selling point of using Operating Systems (OSs) such as **Ubuntu** is how lightweight they can be. However, this advantage comes with its disadvantages; for example, often there is no **GUI (Graphical User Interface)** or what is also known as a desktop environment that we can use to interact with the machine (unless it has been installed). 

A large part of interacting with these systems is using the **Terminal**. The Terminal is purely text-based and can be intimidating at first. However, if we break down some of the commands, after some time, you quickly become familiar with using it.

### 🖥️ Terminal Interface Preview
```text
tryhackme@linux1:~$ enter commands here

🔑 Essential Core Commands
Command	Description
echo	Output any text that we provide
whoami	Find out what user we're currently logged in as!
  
💻 Command Snippets & Examples
1. Using echo

If we want to "echo" a single word, we don't need to use double quotes. However, the string should be enclosed within double quotes if one or more spaces are present.  

    Single Word Example:
    Bash

tryhackme@linux1:~$ echo Hello
Hello

Multiple Words Example:
Bash

    tryhackme@linux1:~$ echo "Hello Friend!"
    Hello Friend!

2. Using whoami

This command can be used to find the username of the account we are currently logged in as.
Bash

tryhackme@linux1:~$ whoami
tryhackme

📂 Interacting With the Filesystem

Being able to navigate the machine that you are logged into without relying on a desktop environment is pretty important. After all, what's the point of logging in if we can't go anywhere?
🛠️ Filesystem Navigation Commands
Command	Full Name	Description
ls	listing	List contents of the current directory
cd	change directory	Change the current working directory
cat	concatenate	Output the contents of a file
pwd	print working directory	Print the full path of the current directory
💻 Practical Navigation Examples
1. Listing Files in Our Current Directory (ls)

Before we can do anything such as finding out the contents of any files or folders, we need to know what exists in the first place.
Bash

tryhackme@linux1:~$ ls
'Important Files' 'My Documents' Notes Pictures

Based on the output above, the current directory contains the following folders:

    Important Files

    My Documents

    Notes

    Pictures

    💡 Pro Tip: You can list the contents of a directory without having to navigate to it by using ls followed by the name of the directory. (e.g., ls Pictures).

2. Changing Our Current Directory (cd)

Now that we know what folders exist, we use the cd command to change to that directory. If we want to open the "Pictures" directory and see its contents:
Bash

tryhackme@linux1:~$ cd Pictures
tryhackme@linux1:~/Pictures$ ls
dog_picture1.jpg dog_picture2.jpg dog_picture3.jpg dog_picture4.jpg

In this case, it looks like there are 4 pictures of dogs!
3. Outputting the Contents of a File (cat)

Whilst knowing about the existence of files is great — it's not all that useful unless we're able to view the contents of them. cat (short for concatenating) is a fantastic way for us to output the contents of text files (and other files as well!).

Example of listing and viewing files inside the "Documents" directory:
Bash

tryhackme@linux1:~/Documents$ ls
todo.txt
tryhackme@linux1:~/Documents$ cat todo.txt
Here's something important for me to do later!

    Step 1: Used ls to see what files are available in the Documents folder (found todo.txt).

    Step 2: Used cat todo.txt to output its contents, which are: "Here's something important for me to do later!"

    💡 Pro Tip: You can use cat to output the contents of a file within directories without having to navigate to it by using its full path. (e.g., cat /home/ubuntu/Documents/todo.txt).

    📌 Note: Sometimes things like usernames, passwords (yes - really...), flags, or configuration settings are stored within files where cat can be used to retrieve them.

4. Finding out the full Path to our Current Working Directory (pwd)

As you progress through navigating your Linux machine, the name of the directory that you are currently working in will be listed in your terminal. However, it's easy to lose track of where we are on the filesystem exactly, which is why we use pwd.
Bash

tryhackme@linux1:~/Documents$ pwd
/home/ubuntu/Documents

    The terminal indicates we are in "Documents", but pwd reveals its absolute position on the filesystem tree.

    The full file path is /home/ubuntu/Documents.

    In the future, if we find ourselves in a different location, we can easily return here by running: cd /home/ubuntu/Documents.

🔍 Advanced Searching & Efficiency

One of the redeeming features of Linux is truly how efficient you can be with it. You can use a set of commands to quickly search for files across the entire system that your user has access to. No need to consistently use cd and ls to find out what is where. Instead, we can use commands such as find and grep to automate things!
🛠️ Search & Filter Utilities
1. Using find

The find command can be used both very simply or rather complex depending upon what you want to do exactly.

Let's assume we have these directories available:
Bash

tryhackme@linux1:~$ ls
Desktop Documents Pictures folder1

Directories can contain even more subdirectories within themselves. If we remember a filename but can't remember where it is stored (e.g., passwords.txt), we can use the -name flag:
Bash

tryhackme@linux1:~$ find -name passwords.txt
./folder1/passwords.txt

The file has been located inside folder1/passwords.txt.
Using Wildcards (*) with Find

If we do not know the exact filename but want to find every file that has a specific extension such as .txt, we use a wildcard (*):
Bash

tryhackme@linux1:~$ find -name *.txt
./folder1/passwords.txt
./Documents/todo.txt

find successfully located all text files across different folders.
2. Using grep

The grep command allows us to search the contents of files for specific values that we are looking for.

Imagine a web server's access log (access.log) that contains 244 entries. We can verify the line count using the wc -l command:
Bash

tryhackme@linux1:~$ wc -l access.log
244 access.log

Looking through 244 entries manually with cat is highly inefficient. If we want to see everything that a specific fictional IP address (81.143.211.90) visited, we use grep:
Bash

tryhackme@linux1:~$ grep "81.143.211.90" access.log
81.143.211.90 - - [25/Mar/2021:11:17 + 0000] "GET / HTTP/1.1" 200 417 "-" "Mozilla/5.0 (Linux; Android 7.0; Moto G(4))"

grep successfully isolated and displayed only the entry matching that specific IP address.
3. Searching Recursively with grep -R

Sometimes, the information we are looking for is spread across multiple files inside a directory. Instead of checking each file individually, we use the -R (recursive) option to search through all files and subdirectories.

Example of searching for a variable name across the /etc/ directory:
Bash

tryhackme@linux1:~$ grep -R "PRETTY_NAME" /etc/
grep: /etc/sudoers: Permission denied
/etc/os-release:PRETTY_NAME="Ubuntu"

    The file path is shown before the matching line, making it easy to identify where the result was found.

    Inaccessible files will return a Permission denied notice, but matching results (like in /etc/os-release) will print out successfully.

⚡ Powering Up with Shell Operators

Operators are a fantastic way to power up your knowledge of working with Linux. They allow you to chain commands and control outputs in bite-sized chunks.
🛠️ Core Shell Operators
Symbol / Operator	Description
&	Allows you to run commands in the background of your terminal.
&&	Allows you to combine multiple commands together in one line of your terminal.
>	An output redirector - takes output from a command and directs it elsewhere (overwrites).
>>	An output redirector that appends the output rather than replacing (nothing is overwritten).
💻 Operator Breakdown & Behavior
1. Operator &

Allows us to execute commands in the background. For example, copying a large file can take a long time and leave us unable to do anything else. Running it with & pushes the process to the background, freeing up the terminal instantly for other tasks.
2. Operator &&

Unlike its single counterpart, && is used to chain a list of commands together (e.g., command1 && command2). It is worth noting that command2 will only run if command1 executes successfully.
3. Operator >

An output redirector that takes the results of a command and sends them somewhere else, such as a new file. Running echo howdy just returns the text to the terminal. Redirecting it allows file creation:
Bash

tryhackme@linux1:~$ echo hey > welcome
tryhackme@linux1:~$ cat welcome
hey

    ⚠️ Note: If the target file (e.g., welcome) already exists, its contents will be completely overwritten!

4. Operator >>

This is also an output redirector, but instead of overwriting existing contents, it places the new output at the very end (bottom) of the file.

If we have a file named welcome containing "hey", using > to add "hello" would wipe out "hey". Using >> appends it properly:
Bash

tryhackme@linux1:~$ echo hello >> welcome
tryhackme@linux1:~$ cat welcome
hey
hello

🏁 Conclusion & Recap

Nice work on getting to this stage! These are the most essential commands and functions you are going to use whenever you interact with a Linux machine. Because of how often you will be using them, they will become muscle-memory very quickly.
📋 Summary of Covered Concepts:

    Linux Environment: Understood why Linux machines are so commonplace today and interacted with a text-based terminal.

    Core Functions: Ran some of the most fundamental commands (echo, whoami).

    Navigation: Learned to navigate around the filesystem (ls, cd, cat, pwd).

    Search Tools: Utilized tools like find and grep to make finding data across files and logs highly efficient.

    Operators: Powered up command execution by utilizing shell operators (&, &&, >, >>).

When you feel comfortable with these tools, progress onto Linux Fundamentals Part 2!
