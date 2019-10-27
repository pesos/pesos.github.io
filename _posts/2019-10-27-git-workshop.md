---
title: "Summary: Git Workshop at 16th October"
tags: git workshop
author: true
---

PESOS conducted its first workshop, one to learn git and get started with using it effectively.

Here is a brief reference for the workshop conducted on 16th October, 2019.

Version control systems help in efficiently tracking changes to source code over time, especially in codebases with multiple collaborators.  Apart from this, developers can also ‘reset’ their source code to an earlier stage, reversing recent changes.

One such widely used free and open source version control system is git.

## Let’s git started!

Create a new folder called git_playground.
Linux and MacOS users, this is just `mkdir git_playground`.

Here are a few git commands to help you get started:
Navigate to the git_playground folder.

1. `git init`

    The folder is now initialised with a .git folder and is a git repository. 
    Linux and MacOS users, an `ls -a` will show the newly created .git folder.

2. `git status`

    This, true to its name, shows the status of your local repo, including details like which branch you are working on and changes staged for commit.

3. Creating a README

    A README is essentially a document providing details about your repo such as usage, installation, requirements, contributing guides, etc. Mostly written in markdown (.md) format. 
    A good README is an important starting point for documentation of the repo, which is especially useful when working with collaborators/contributing to a project.
    
    The Working Tree, in this context, refers to the area where you are working currently. This is the ‘untracked’ area of git and any changes made to files here will be lost until specifically saved.
    The saving and tracking of these changes occurs in the ‘staging area’ of git.

4. `git add`

    This command moves files from your working tree to the staging area.
    `git add README.md` will add only the README, whereas `git add .` or `git add -a` will add all the files.

5. `git commit`

    This is what saves all the changes you have made in the local repo. This follows the `git add` command.
    `git commit -m <message>` will add a commit message.
    `git commit -m <message> -m <description>` can be used to add an extended description with the commit message.
    If the flag ‘-m’ is not specified, git will automatically open the default text editor and ask you to add the message.
    `git show HEAD` shows the latest commit. Each commit has a unique alphanumeric commit ID.

6. `git log`

    This displays a list of commits with their commit IDs, authors, timestamps,messages, etc. 
    
    `git show <commit ID>` using the commit ID for a specific commit will also display commit details and changes.
    
    As you probably know, git is a distributed version control system. Most operations are done locally. To communicate with the outside world, git uses what are called remotes.  
     These are repositories other than the one on your local disk which you can push your changes into (so that other people can see them) or pull from (so that you can get others changes). 

7. `git remote add origin <URL>`

    This adds a default remote, origin, with the specified URL.
    Origin refers to the default repository the local repo was cloned from. It is henceforth referred to as `origin` instead of the complete URL.

8. Either `git remote -v` or `git show remote` shows the list of remotes for a particular repo.

9. `git push`

    This command pushes the code from your local repository (In this case, the directory containing the files in your laptop) to the remote repository (In this case, your GitHub repo).
    The command `git push` by default, will not work because Git does not know which branch to push from, which remote to push to, etc.. 
    
    So, the required command is `git push <remote name> <local branch>:<remote branch>`(If the remote branch isn’t specified, a branch is created with the local branch name on the remote).
    But since it will be inconvenient to keep typing such a long command, Git has an easier alternative.
    
    `git push -u origin master`: The ‘-u’ flag is used to set the remote as an upstream for the master. You can start using ‘git push’ command after you run this command once because Git now knows where it should push your code to.

10. `git push -d <remote name> <branch name>`

    This command is used to delete a remote branch.

11. `git fetch`

    This command fetches the branches from one or more repositories, along with the objects necessary to complete their histories.

12. `git merge <branch name>`

    This command is used to merge the changes committed(since the time the branch was created) in the specified branch with another branch(Includes master branch).
    
    The below example shows the time the branch was created(At E) and the different commits made(B, C).
    
    ```
              A--B--C    branch
             /
    D---E---F---G        master
    ```
    
    After running the command `git merge branch` (In this case, <branch name> was branch), the changes committed in the branch have been merged with the master branch.
    
    ``` 
             A--B--C     branch
            /       \
    D---E---F---G---H    master
    ```

14. `git pull <remote name> <branch name>` or `git pull`

    This command helps get the changes made to the code from the remote repository into the current branch.
    It basically runs `git fetch` with the with the given parameters and then runs ‘git merge’ to merge the retrieved branch with the current branch.
    
    To create local copies of existing repos, we download the repo using the `git clone` command.

15. `git clone <URL>`

    URL => Eg. www.github.com/Username/RepoName.git
    This command will clone the repository in the URL into the specified directory on your computer.

### Difference between forking a repository and creating a branch

Each fork of the main repo corresponds to a contributor's work. A fork is really a Github (not git) construct to store a clone of the repo in your user account. As a clone, it will contain all the branches in the main repo at the time you made the fork.
Each branch within the fork and/or in the main repo can correspond to several kinds of things, depending on how you want to work. Each branch could refer to a version of the project but can also correspond to different channels of development, like hotfixes or experimental work. Hence, it is important to create branches and work on your code, and then merge it when you’re done so as to not affect anyone else’s work(others who are working with the same repository).
