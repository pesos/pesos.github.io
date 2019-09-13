---
title: Terminal tips from PES Open Source
tags: linux, bash, compilation
---

// Start your contributions here

**Undoing a commit**  
Contributed by : Akhil E ([akhil-eppa](https://github.com/akhil-eppa))  
Sometimes you may commit the wrong files to the repository and may want to entirely undo a commit. This can be done using the following command  
```$ git reset --soft ^HEAD~1 ```

----  

**Modifying a commit by adding files**  
Contributed by : Akhil E ([akhil-eppa](https://github.com/akhil-eppa))  
Sometimes you may want to add an another file to the existing commit. For that you first add the file to the staging area as follows  
```$ git add filename```  
and then commit using the ammend option  
```$ git commit --amend -m "Added this file"```  

----  

**Syncing forked repository to the original repository**  
Contributed by : Akhil E ([akhil-eppa](https://github.com/akhil-eppa))  
When you fork a repository, the fork contains all the files that were present in the original repository at the time of forking. Now after a certain period if you want to sync the forked repository to the upstream one the following commands have to be executed:  
Add remote of original repository in your cloned fork repository as follows
```
$ git remote add upstream git://github.com/github_handle/repo_name_you_forked_from.git  
$ git fetch upstream  
```  
Update your fork from original repo to reflect the changes made in original repository  
```$ git pull upstream master```  
Fianlly to reflect these changes in your remote repository from your local repository  
```$ git push```  

----  
