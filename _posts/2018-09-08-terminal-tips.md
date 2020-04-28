---
title: Terminal tips from PES Open Source
tags: linux, bash, compilation
---

## Short tricks for long commands
*Contributed by: Aditi*  
- Use `Ctrl+A` and `Ctrl+E` to navigate to the beginning and end of the line respectively.   
- Hit `Ctrl+R` and enter a word/phrase from a previously used super long command and it will retrieve the last used command with the term.  

---  

## Reusing previous commands
*Contributed by: Aditi*  
- `!!` is always substituted by the previous command.  
```sh
$ sh /etc/script.sh
mv: cannot execute '/etc/script.sh': Permission denied
$ sudo !!
Script executed.
``` 
It's the command equivalent of the upper arrow key! 

---  

## Bash history
*Contributed by: Aditi*  
To avoid having a command added to your .bash_history file, prefix it with a space i.e. go with `  [command]` instead of <code>&nbsp;[command]</code>.    

---  

## Pausing and running commands
*Contributed by: Aditi*  
Say, you have a terminal text editor open and you're in the process of editing it. You realize you want to test something out on the terminal.   
Instead of closing and re-opening it, you could use `Ctrl+Z` to pause the application and return to the terminal; followed by the `fg` command to return to it.

---  

## Running commands after logging out of an SSH session
*Contributed by: Aditi*  
This one's for long commands in an SSH session.     
Nohup stands for 'no hangups'.   
Prefixing `nohup` lets you run time-taking commands in an SSH session after log out too.   
So a time-taking script.sh can be run remotely as `nohup sh script.sh`.

---  

## Returning to a previous directory without a pwd
*Contributed by: Aditi*  
Say you accidentally change directories and want to return to the previous directory you were working in.     
`cd -` takes you back to it.    

---

## Undoing a commit
_Contributed by : Akhil E ([akhil-eppa](https://github.com/akhil-eppa))_  
Sometimes you may commit the wrong files to the repository and may want to entirely undo a commit. This can be done using the following command  
```sh
$ git reset --soft ^HEAD~1
```

---  

## Modifying a commit by adding files
_Contributed by : Akhil E ([akhil-eppa](https://github.com/akhil-eppa))_  
Sometimes you may want to add an another file to the existing commit. For that you first add the file to the staging area as follows  
```sh
$ git add filename
```  
and then commit using the ammend option  
```sh
$ git commit --amend -m "Added this file"
```  

---  

## Syncing forked repository to the original repository
_Consributed by : Akhil E ([akhil-eppa](https://github.com/akhil-eppa))_  
When you fork a repository, the fork contains all the files that were present in the original repository at the time of forking. Now after a certain period if you want to sync the forked repository to the upstream one the following commands have to be executed:  
Add remote of original repository in your cloned fork repository as follows
```sh
$ git remote add upstream git://github.com/github_handle/repo_name_you_forked_from.git  
$ git fetch upstream  
```  
Update your fork from original repo to reflect the changes made in original repository  
```sh
$ git pull upstream master
```  
Finally to reflect these changes in your remote repository from your local repository  
```sh
$ git push
```  

---  

## Stop/Start Displaying Terminal Input
*Contributed by: Bhargav SNV*  
```sh
stty -echo
stty echo
```
When `stty -echo` is done, input in the terminal won't be displayed.
When `stty echo` is done, input in the terminal will be displayed.

---

## Describe Filetype of File or Directory
*Contributed by: Bhargav SNV*  
```sh
file [filetype or dirname]
```
The command describes the type of file/directory provided as a n argument along with a description of its contents.

---

## Create a typescript of terminal session
*Contributed by: Bhargav SNV*  
```sh
script [dir/filename]
```
On executing the command, every command typed after it is logged and added to a typescript with the name `filename` in the destination described by `dir`. When we `cat filename`, the logged commands are executed again. Example:
    
```sh
~$ script script_file 
Script started, file is script_file
~$ echo "hi this is in the script"
hi this is in the script
~$echo "hello"
hello
~$ exit
exit
Script done, file is script_file
~$
~$ cat script_file
Script started on 2019-09-14 08:34:06+05:30
~$ echo "hi this is in the script"
hi this is in the script
~$ echo "hello"
hello
# exit
exit

Script done on 2019-09-14 08:35:51+05:30
```

Here, when we run `cat script_file`, the commands logged under it are directly executed.

---

## Change command prompt
*Contributed by: Bhargav SNV*  
```sh
export PS1="MyPrompt >"  
```
This let's you edit your prompt text to anything you'd like! Example:

```sh
root@ubuntu:~# export PS1="MyPrompt >"  
Myprompt >  
```

---

## Shorter way to run ./a.out
*Contributed by: Akshatha Laxmi*  
```sh
!.
```
On executing command, ./a.out runs.

---

## Create a file with date
*Contributed by: Akshatha Laxmi*  
```sh
touch filename`date +&d%m%y`
```
This command creates a file with the date of the day. %d is for the day, %m is for month, %y is for year.

---

## Display certain parts of a text file
*Contributed by: Akshatha Laxmi*  
```sh
cat -n filename.txt | sed '11d'
cat -. filename.txt | sed '11!d'
```
The first command prints everything but line number 11.   
The second command prints only line number 11.

---

## Compressing multiple files using gzip
*Contributed by: Ramya*  
```sh
cat [file1] [file2] | gzip > [file3.gz]
```
'gzip' command is used to compress/truncate and decompress files. To compress multiple files together you can use the 'cat' and 'gzip' command with pipe command(lets you use two or more commands such that output of one command serves as the input of the other).This command create a compressed file file3.gz which has contents of both the files.

---

## Checking the success status of a command
*Contributed by: Ramya*  
```sh
echo $?
```
 This command is run to check if your previous command was successful or not.It returns 0 on success.

---
 
## Abbreviating a command
*Contributed by: Ramya*  
```sh
alias alias_name='command'
```
alias command helps to launch any command or group of commands by entering a pre-set string.

---

**Note: Please copy this format for further tips. Place your tip before this sample**  

## Title for the tip/code
*Contributed by: <your name>*  
```sh
insert code here (if any)
```
description about what your tip does with accompanying code snippet

---
