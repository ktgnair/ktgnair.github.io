 **[Assignment 1](https://ktgnair.github.io/) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Rules For Code](https://ktgnair.github.io/Rules For Code)**  

 **Git Tutorials (_A basic tutorial for people who are new to 'git'_)**  

### Something about git before starting to implement it.    

Git is great opensource platform to share the code and to make sure that your code is not lost.  

The main purpose of using git for programmers like us is to sync the local repository with the git server repository.  
Another way of understanding git is, lets say you are doing a project and you need to share the code with someone else who can work on their machine and make the updates, so for that you could just share your url with that person and that person will be able to download it or clone it and get started.  

So now that you know something about git _let's begin....._  

I am going to mention the steps so that you can be familiar with 'how to use git'.  
You can also do it simultaneously while reading as it doesn't take much time to learn the basics. Afterwards you can explore more if you find this interesting.  
After this tutorial i am sure you will be able to do git nicely.  

Step 1: 

Create an account by clicking on this link [Github Account creation page](http://github.com)  

Step 2:  

To install git in your machine (I am using Linux Ubuntu, other operating systems might be little different)    
Just type in this command in your terminal.  
```
sudo apt-get install git-all
```   
If you are using Linux Fedora then go for this command.    
```
sudo dnf install git-all
```  

Step 3:  

After doing step 2 do this to check whether our git has been porperly installed and to know the version.  
The command is   
```
git --version
```  
The output will show the installed version of git.  
```
git version 2.11.0
```  

Step 4:  

Create your own local clone of a repository.   
- Go to your directory where you want to clone.  
For me it was this  
```
cd Documents/Demo/
```  

- After going in the directory type this to clone  
```
git clone https://github.com/<your github account>/<your new directory name>.git
```  
Eg: git clone https://github.com/myacccountname/TestingGit.git  

This is what happens after cloning  
```
Cloning into 'TestGit'...
warning: You appear to have cloned an empty repository.
```  

Step 5:  

- Switch to your newly created directory i.e ~/Documents/Demo/TestingGit  

- Create an empty file for testing purpose.  
```
gedit gitDemo.txt
```  

- Write some content into the text file and save it.  

- Type this command  
```
ls
```  
and you will be able to see all the files in your directory.  

Step 6:  

To know the status of the branch you are working on.  

```
git status
```  
The output will be  
```
On branch master
Initial commit
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	gitDemo.txt
nothing added to commit but untracked files present (use "git add" to track)
```  

As you can see that the status tells you to add the file.  

- So the 3 basic things in git is to:    
  - First add files,  
  - Second commit the added files and   
  - Third is to push the files.  
  
 **_Commit_** means the files are saved in your local directory but not on your git account.  
 **_Push_** means to save in the server(your git account).  

Step 7:   

Add your file using this command  
```
git add gitDemo.txt
```  

- Now again check the status and see the difference  
```
git status
```  
The difference:  
```
On branch master
Initial commit
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   gitDemo.txt
```  

Step 8:  

- Commiting the files which are added.  
```
git commit
```   
Write commit message Testing Git in vi editor then press Ctrl + x, then y for save and press Enter on your keyboard.  
```
Testing Git
 1 file changed, 4 insertions(+)
 create mode 100644 gitDemo.txt
```  

- You need to cultivate a habit of checking the status everytime you do some operation in git.  
```
git status
```  

- Now type  
```
git log
```  
It shows you all the commits you have made so far  
```
commit 7c9371114c1e86503ad5b5ad975f255ccd60034b
Author: <your github account> <emailid@gmail.com>
Date:   Fri Mar 18 14:39:52 2018 +0530
    Testing Git
```  
Step 9:  

- Push the files into your git account.  

```
git push
```  

- It will ask for your github username and password(it is what you created at step 1).  

```
Username for 'https://github.com': <your user name>
Password for 'https://abc@github.com': 
Counting objects: 1, done.
Writing objects: 100% (1/1), 220 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To https://github.com/<your account name>/TestingGit.git
 * [new branch]      master -> master
 ```  
 
Step 10:  

- Now create more 2 files and perform the last three steps again to practice.  
- And type  
```
ls
```  

The total three files in your directory is listed here  

```
gitDemo.txt  SecondFile.txt  ThirdFile.txt
```   
- After creating open one of the created files, make changes into that and save it.  
```
gedit gitDemo.txt
```  
- See the status.  
```
git status
```  

```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
	modified:   gitDemo.txt
no changes added to commit (use "git add" and/or "git commit -a")
```  

- Now type this command and see the result.  
```
git diff
```  
Result  

```
diff --git a/gitDemo.txt b/gitDemo.txt
index df72b36..0eef335 100645
--- a/gitDemo.txt
+++ b/gitDemo.txt
@@ -1,4 +1,5 @@
 This is older file
 This is older content
-
+
+This is the latest added content  
```  
The command you typed just now tells you the changes you made in your files, isn't that just great.  

- Now lets say you want to delete a file.  
```
git rm SecondFile.txt
```  
```
rm 'SecondFile.txt'
```  
```
git status
```   

```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
	deleted:    SecondFile.txt
```  
```
git commit
```  
Write commit message Deleted in vi editor then press Ctrl + x, then y for save and press Enter on your keyboard.  

```
[master f1b0591] Deleted
 1 file changed, 2 deletions(-)
 delete mode 100644 SecondFile.txt
```  
```
git push
```  

```
Username for 'https://github.com': <your user name>
Password for 'https://abc@github.com': 
Counting objects: 2, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 261 bytes | 0 bytes/s, done.
Total 2 (delta 0), reused 0 (delta 0)
To https://github.com/<your account name>/TestingGit.git
   27f1813..f1b0592  master -> master
```  

Step 11:  

- Now go to your github account in the browser.  
- Select the repository you are working on ie.TestingGit.  
- Click on create new file and name the file with .txt extention.(I am naming it as ForPullDemo.txt)  
- Write something in it and click commit button which is at the end of the page.  

The new file is present in your github account but not in your local directory, to get that we need to pull the file.  
The command is  
```
git pull
```    

```
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/<your account name>/TestingGit
   f1b0591..6520792  master     -> origin/master
Updating f1b0591..6520793
Fast-forward
 ForPullDemo.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 ForPullDemo.txt
```  

- Now see the files in your directory by using 'ls', you will see something like this.  

```
ForPull.txt  gitDemo.txt  ThirdFile.txt
```  

Step 12:  

To Create a new branch in git.  
- Before creating a branch just type this in your terminal  

```
git branch
```  
You will see that something like this is displayed on your terminal  

```
* master
```  
This is because you are on master branch i.e main branch, there is no other branches available so whenever we create a file on git it is saved on master.  
Usually while doing a project the files are saved on different branches and after everything is finalized those files are merged on the master, so in-short the master branch has files without any garbage.  
- Now that you all are aware of what master is and what is the use of creating a new branch, we will create one.  

```
git checkout -b New_Branch
```  

```
Switched to a new branch 'New_Branch'
```  
Now we are in the New_Branch.  

```
git branch
```  
```
* New_Branch
  master
```  
- Checkout if there are any files in your this branch.  

```
ls
```  

```
ForPull.txt  gitDemo.txt  ThirdFile.txt
```  

What how did i get these files here when i had pushed it in master?  
**ANSWER:** Since the branch is created from master so all the files in master is automatically here in this branch.  

- Now create a file in this branch, add some content and save it.  

```
gedit BranchDemo.txt
```  
- Check the contents in the directory by using 'ls'.  

```  
BranchDemo.txt  ForPullDemo.txt  gitDemo.txt  ThirdFile.txt
```  
- Add your file.  
```
git add BranchDemo.txt
```  
- Commit your file.  
```
git commit -m "Branch commit"
```  
You will notice that i used -m "Branch commit". This is to write the commit messages directly without going to vi editor which we were doing till now.  

```
[New_Branch 9045454] Branch commit
 1 file changed, 1 insertion(+)
 create mode 100645 BranchDemo.txt
```  
```
git status
```  
```
On branch New_Branch
nothing to commit, working tree clean
```  
- To push the new branch files use this coomand which is different from the usual one.  

```
git push origin New_Branch
```  

```
Username for 'https://github.com': <your user name>
Password for 'https://abc@github.com': 
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 362 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/<your account name>/TestingGit.git
 * [new branch]      New_Branch -> New_Branch
```   

Step 13:  

To merge to master.  

- Switching to different branch is performed by this command.  
```
git checkout master
```  

```
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
```   

- Check whether you have switched to master.  
```
git branch
```  

```
New_Branch
* master
```  
The * tells you which branch you are in currently.  

- Since you have switched to master type 'ls' and see the files, you will notice that your recent created file BranchDemo.txt is not there.  
That's because you have not merged the file with master.  
- Type this to merge.  
```
git merge New_Branch
```  
```
Updating 6520792..9045454
Fast-forward
 BranchDemo.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 BranchDemo.txt
```  
- Check the logs you will see all the commits you have made so far.  
```
git log
```  

- Now that you have merged with master type 'ls' and see the changes from the earlier one.  
```
BranchDemo.txt  ForPull.txt  readme.txt  ThirdFile.txt
```  
```
git push
```  

```
Username for 'https://github.com': <your user name>
Password for 'https://abc@github.com': 
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/<your account mane>/TestingGit.git
   6520792..9045454  master -> master
```  

Step 14:  

- To delete a branch from local directory.  
```
git branch -D New_Branch
```  
```
Deleted branch New_Branch (was 9045454).
```  
```
git branch
```  
```
* master
```  

- Now to delete a branch from the github account.  
```
git push  origin --delete New_Branch
```  

```  
Username for 'https://github.com': <your user name>
Password for 'https://abc@github.com': 
To https://github.com/<your account name>/TestingGit.git
 - [deleted]         New_Branch
```  

Step 15:  

- Multiple commits into single commit  
All the commit messages you have made so far in a new branch will be attached in the master while performing merge, so to remove those unnecessary commit messages and just putting one message we use this.  
```
git merge --squash branchname --Your message
```  

As promised you will be able to perform basic git operations nicely after this blog.      
If you liked my blog then make sure you follow me so that you get notifications for some more good contents which i will be writing in future.  
