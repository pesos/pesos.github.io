---
title: Terminal tips from PES Open Source
tags: linux, bash, compilation
---

// Start your contributions here
---

*Contributed by: Ramya *
### Compressing multiple files using gzip
    cat [file1] [file2] | gzip > [file3.gz]
'gzip' command is used to compress/truncate and decompress files. To compress multiple files together you can use the 'cat' and 'gzip' command with pipe command(lets you use two or more commands such that output of one command serves as the input of the other).This command create a compressed file file3.gz which has contents of both the files.

---

### Checking the success status of a command
    echo $?
 This command is run to check if your previous command was successful or not.It returns 0 on success.
 
---
 
### Abbreviating a command
    alias alias_name='command'
alias command helps to launch any command or group of commands by entering a pre-set string.

---
