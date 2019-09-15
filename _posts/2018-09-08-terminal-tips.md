---
title: Terminal tips from PES Open Source
tags: linux, bash, compilation
---

// Start your contributions here

*Contributed by: Shivansh*

### Counting number of lines in a file:
  command: wc <filename>
  Description:The output prints 3 numbers with the filename. The three numbers represent number of lines, words and charecters in that file.
  
### Counting number of files and sub-directories in a directory
  command: ls | wc
  Description: This gives 3 numbers as output again, representing total number of files and sub-directories, the number of words in the names of these files and sub-directories and the number of charecters in the names of these files and sub-directories.
  
  command ls | wc > <filename>
  Description: This command redirects the output of the previous command to the the filename. The filename should be present in the same directory whose number of files and sub-directories is being found.
