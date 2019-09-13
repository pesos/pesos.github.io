---
title: Terminal tips from PES Open Source
tags: linux, bash, compilation
---

*Contributed by: Aditi*		      
## Short tricks for long commands:     
- Use `Ctrl+A` and `Ctrl+E` to navigate to the beginning and end of the line respectively.   
- Hit `Ctrl+R` and enter a word/phrase from a previously used super long command and it will retrieve the last used command with the term.  

## Reusing previous commands
- `!!` is handy for reusing the previous command with the current one.  
- `!?` uses the argument of the previous command with the current one.

## Bash history
To avoid having a command added to your .bash_history file, prefix it with a space i.e. go with `  [command]` instead of `[command]`.

## Switching between an application and the (same) terminal
Say, you have a terminal text editor open and you're in the process of editting it. You relaise you want to test something out on the terminal.   
Instead of closing and re-opening it, you could use `Ctrl+Z` to suspend the application and return to the terminal; followd by the `fg` command to exit from it once done.



