---
title: Terminal tips from PES Open Source
tags: linux, bash, compilation
---


// Start your contributions here with this format

*Contributed by: <your name>*
    
### Title for the tip/code
    insert code here (if any)
description about what your tip does with accompanying code snippet

---


*Contributed by: Akshatha Laxmi*

### Shorter way to run ./a.out
    !.
On executing command, ./a.out runs.

### Create a file with date
    touch filename`date +&d%m%y`
This command creates a file with the date of the day. %d is for the day, %m is for month, %y is for year.

---

*Contributed by: Bhargav SNV*
### Stop/Start Displaying Terminal Input  
    export PS1="MyPrompt >"  
This let's you edit your prompt text to anything you'd like! Example:
    
    root@kali:~# export PS1="MyPrompt >"  
    Myprompt >  
    
### Stop/Start Displaying Terminal Input
    stty -echo
    stty echo
When `stty -echo` is run, input in the terminal won't be displayed.
When `stty echo` is run, input in the terminal will be displayed.

### Describe Filetype of File or Directory
    file [filename or dirname]
The command describes the type of file or directory provided as an argument along with a description of its contents.

### Create a typescript of terminal session
    script [dir/filename]
On executing the command, every command typed after it is logged and added to a typescript with the name `filename` in the destination described by `dir`. When we `cat filename`, the logged commands are executed again. Example:
    
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

Here, when we run `cat script_file`, the commands logged under it are directly executed.

---

Contributed by : Akhil E ([akhil-eppa](https://github.com/akhil-eppa))  

**Undoing a commit**  
Sometimes you may commit the wrong files to the repository and may want to entirely undo a commit. This can be done using the following command  
```$ git reset --soft ^HEAD~1 ```

**Modifying a commit by adding files**  
Sometimes you may want to add an another file to the existing commit. For that you first add the file to the staging area as follows  
```$ git add filename```  
and then commit using the ammend option  
```$ git commit --amend -m "Added this file"```  

**Syncing forked repository to the original repository**  
When you fork a repository, the fork contains all the files that were present in the original repository at the time of forking. Now after a certain period if you want to sync the forked repository to the upstream one the following commands have to be executed:  
Add remote of original repository in your cloned fork repository as follows
```
$ git remote add upstream git://github.com/github_handle/repo_name_you_forked_from.git  
$ git fetch upstream  
```  
Update your fork from original repo to reflect the changes made in original repository  

    $ git pull upstream master  
Finally to reflect these changes in your remote repository from your local repository  

    $ git push

---



