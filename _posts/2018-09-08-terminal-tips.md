---
title: Terminal tips from PES Open Source
tags: linux, bash, compilation
---

// Start your contributions here
### Title for the tip/code
    insert code here (if any)
*Contributed by: <your name>*
description about what your tip does with accompanying code snippet

---
### Stop/Start Displaying Terminal Input
    stty -echo
    stty echo
*Contributed by: Bhargav SNV*
When `stty -echo` is done, input in the terminal won't be displayed.
When `stty echo` is done, input in the terminal will be displayed.

---

### Describe Filetype of File or Directory
    file [file/dir]
*Contributed by: Bhargav SNV*
The command describes the type of file/directory provided as a n argument along with a description of its contents.

---

### Create a typescript of terminal session
    script [dir/filename]
*Contributed by: Bhargav SNV*
On executing the command, every command typed after it is logged and added to a typescript with the name `filename` in the destination described by `dir`.

---
