---
title: Terminal tips from PES Open Source
tags: linux, bash, compilation
---

// Start your contributions here
*Contributed by: <your name>*
### Title for the tip/code
    insert code here (if any)
description about what your tip does with accompanying code snippet

---

*Contributed by: Bhargav SNV*
### Stop/Start Displaying Terminal Input
    stty -echo
    stty echo
When `stty -echo` is done, input in the terminal won't be displayed.
When `stty echo` is done, input in the terminal will be displayed.

### Describe Filetype of File or Directory
    file [file/dir]
The command describes the type of file/directory provided as a n argument along with a description of its contents.

### Create a typescript of terminal session
    script [dir/filename]
On executing the command, every command typed after it is logged and added to a typescript with the name `filename` in the destination described by `dir`.

---

*Contributed by: Akshatha Laxmi*

### Shorter way to run ./a.out
    !.
On executing command, ./a.out runs.

### Create a file with date
    touch filename`date +&d%m%y`
This command creates a file with the date of the day. %d is for the day, %m is for month, %y is for year.

---
