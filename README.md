<!-- This document is based on a Windows terminal, probably I will add other terminal options in the future -->

# Git Notes

Git basically is Version Control System. Although I will also mention Github, they are not the same. 

In my own words I coul say that [Git](https://git-scm.com/) is a tool an software  that you can download and install in your own computer, it helps you organice your programs, keep track of changes, and also interact with public or private services to work in a collaborative way, suc as [Github](https://github.com/).
[Github](https://github.com/) is a public service, where you can open a account and have your own repositories; it is recommended to have one repository per project; and allows others to participate.
There are many companies that offer their code on this service. Another popular alternative to Gouhub is Gitlab.

*****

## Contents
- [Git verification](#git-verification)
- [Git configuration](#git-configuration)
- [Creating a repository](#creating-a-repository)
- [Adding gitignore file](#adding-gitignore-file)
- [Additional commands](#additional-commands)
- [Terminology](#terminology)
- [Additional references](#additional-references)

*****

## Git verification
Once you install Git on your local computer (in Windows is very easy, it is like any .exe application), open the _Git Bash_ terminal and verify with the single command:

```
$ git version
git version 2.28.0.windows.1
```

From the Git Bash terminal you still can use your traditional Windows commands, for example you can open the Windows explorer with:
```
$ explorer .
```
Open Visual Studio Code:
```
$ code .
```
Or listing the content of files and directories:
```
$ dir
```
But I will use more bash or linux type commands instead of the tradditional windows commands:
```
$ ls
```

*****

## Git configuration
We will explore some of the git config options, that allows to initiallice are Git configuration, and check configuration parameters if required.
```
$ git config --help
$ git config --global user.name username
$ git config --global user.email user@server.com
$ git config --local user.name username
$ git config --local user.email user@server.com
$ git config -l
...
user.name=username
user.email=user@server.com
...
$
$ git config -l --show-origin
...
file:C:/Users/user/.gitconfig  user.name=username
file:C:/Users/user/.gitconfig  user.email=user@server.com
...
$ git config remote.origin.url
https://github.com/<my_git_account>/git-notes.git
```


*****

## Creating a repository

The first I recommend is to create a directory to store all your repositories:
```
$ mkdir GitHubRepositories
$ cd GitHubRepositories/
```
Also to open your account on Github. You can create your repository on Github first and then clone it in your computer. This is the method I will show here (adding more pictures later). One you have 
```
$ git clone https://github.com/<my_git_account>/git-notes.git
$ cd git-notes/
(main *) git-notes
$ ls
README.md
(main *) git-notes
```
We can create our files on this directory, change the readme file, etc. For example we can create the garbage.txt file and play with it to show the use of git commands.
```
$ ls
README.md
$ touch garbage.txt
$ ls
garbage.txt  README.md
```
The _git status_ command can show actions to be executed and the git commands necessary to permoform thouse actions. 
```
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        garbage.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
First we need to add new or modified files to a _stagging area_. We can do it file per file using the file name or using * as a wild caracter for all files.
```
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md
        new file:   garbage.txt
```
Then we need to commit thouse files to our local repository. The -m option is to add a description of why we are performing the commit.
```
$ git commit -m "Just testing"
[main f27a3cc] Just testing
 2 files changed, 87 insertions(+), 2 deletions(-)
 rewrite README.md (100%)
 create mode 100644 garbage.txt
$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
Now the new files and changes to the files are in your local repository. But in order to push these changes to the remote repository, we need to push them. Also we could verify the destination of the remote repository first:
```
$ git config remote.origin.url
https://github.com/<my_git_account>/git-notes.git
$ git push [origin master]
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 1.81 KiB | 617.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/<my_git_account>/git-notes.git
   40408ca..f27a3cc  main -> main
```
Also if you need to update your local repository when someelse change files or added new files in the remote repository, you can pull thouse changes:text
<span >`git hub`</span>
```
$ git pull [origin master]
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 678 bytes | 32.00 KiB/s, done.
From https://github.com/<my_git_account>/git-notes
   f27a3cc..06c50df  main       -> origin/main
Merge made by the 'recursive' strategy.
 garbage.txt | 1 +
 1 file changed, 1 insertion(+)
$ cat garbage.txt
I added this line on Github.
```
*****

## Adding gitignore file
Adding _.gitignore_ files is easy and it is reccomended. Ussually there are files in the same directory of your repository that you do not want to upload to the server, or there are files you do not want to share.
just create a _.gitignorefile_ and add name files or extensions of the files you do not want to upload.
```
$ touch mypythonfile.py
$ ls
garbage.txt  mypythonfile.py  README.md
$ git status
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        mypythonfile.py

nothing added to commit but untracked files present (use "git add" to track)
$ touch .gitignore
$ echo "*.py" >> .gitignore
$ git status
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
$ git commit -m "Adding .ignore file to my repo"
[main ee31f56] Adding .ignore file to my repo
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
$ git push
```
This option is for a sigle repository, but there is also an option to configure a file for all repositories in your local computer.

*****

## Additional commands
Here is a list of additional commands to explore:
- git diff
- git restore
*****

## Terminology
There are many words used here that may requiere further explanation:
- Repository: each project is realted to a repository, it is the group of files related to the project.
- Local repository: usually are the files stored in your own computer
- Remote repository: refers to the files stored in a server where all users accessing the repository can have access.
- Branch: by default there is alwys at lesta one branch for each repository. The first brach is ussually named Master, it is the original bracnch. You can make copies of this branch i orer to develop new features, make some enhancemenets, etc. At some point usually these additional branches can be merged again to the main branch. Branchas allows multiple persons to work on copies of the original branch without working directly on the main branch.
- Clone:
- Fork:
- Push: local to remote.
- Pull: remote to local.
- Pull request:

## Additional references

[Git on Wikipedia](https://en.wikipedia.org/wiki/Git).

[Github on Wikipedia](https://es.wikipedia.org/wiki/GitHub).

[Pro-Git Book](https://git-scm.com/book/en/v2) by Scott Chacon and Ben Straub.

Learn Git in 15 Minutes by [Colt Steel](https://www.youtube.com/c/ColtSteeleCode).

[![Learn Git in 15 Minutes](https://img.youtube.com/vi/USjZcfj8yxE/default.jpg)](https://youtu.be/USjZcfj8yxE)

Learn Github in 20 Minutes by [Colt Steel](https://www.youtube.com/c/ColtSteeleCode).

[![Learn Github in 20 Minutes](https://img.youtube.com/vi/nhNq2kIvi9s/default.jpg)](https://youtu.be/nhNq2kIvi9s)

Git & GitHub Crash Course For Beginners by [Traversy Media](https://www.traversymedia.com/).

[![Git & GitHub Crash Course](https://img.youtube.com/vi/SWYqp7iY_Tc/default.jpg)](https://youtu.be/SWYqp7iY_Tc)

Git and GitHub for Beginners - Crash Course [freeCodeCamp](https://www.freecodecamp.org/).

[![Git and GitHub for Beginners](https://img.youtube.com/vi/RGOj5yH7evk/default.jpg)](https://youtu.be/RGOj5yH7evk)

What is Git | What is GitHub by [Edureka](https://www.edureka.co/).

[![What is Git | What is GitHub](https://img.youtube.com/vi/xuB1Id2Wxak/default.jpg)](https://youtu.be/xuB1Id2Wxak)

SSH Crash Course | With Some DevOps by [Traversy Media](https://www.traversymedia.com/).

[![SSH Crash Course](https://img.youtube.com/vi/hQWRp-FdTpc/default.jpg)](https://youtu.be/hQWRp-FdTpc)
