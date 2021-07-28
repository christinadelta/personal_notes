# Quick tutorial on Git and Github (for Macos systems) 

## What is Git?
Git is a Version Control System (VCS). What does this mean?

![Imgur](https://i.imgur.com/xcc9itq.png) 

Let’s say you have a file, and you want to keep all the changes of that file. The version control system does exactly that. It checks all the changes in your file and maintains the version history. 

### So why do we use VCS?
* to track changes in files/folders
* collaborate in teams

![Imgur](https://i.imgur.com/lts7T9t.png)

Now, things between members of teams become very easy. Person A can add new changes to the file, and person B will be able to check those changes and vice versa.

### Centralized Version Control:
![Imgur](https://i.imgur.com/4j08i3M.png)

### Distributed Version Control:
![Imgur](https://i.imgur.com/7YM4LK5.png)

Git is a distributed version control system.

## What is GitHub?
Github is a website that you can upload your repositories online.

* It provides backup
* It provides visual interface to your repositories
* Makes collaboration easier

### Is Git related to Github?
NO! Git is a VCS whereas GitHub is just a website where you can upload your repositories.

## Getting started with Git and GitHub
### Install Git (Mac)
First check if git is already installed. Open a terminal and type:

```git --version```

 If it is not installed, it will prompt you to install it. Once installed, try again the previous command.
 
### Add files and folders to git (and track)
Create a new folder, call it: **myFolder**. In the terminal, go to the location of the folder:

``` mkdir myFolder```

### Initialize an empty Git repository (hidden folder)
``` git init ```

To see it, the command is:

``` defaults write com.apple.finder AppleShowAllFiles YES ```

One you type the command and hit enter, press **option + command** keys and right click on finder → relaunch

You can then check your git status by typing:

``` git status ```

if we have not added anything, the output is *“nothing to commit”*. So, add file:

``` touch test1.txt ```

and check the status again:

``` git status ``` 

This will show you the file name and type in red. Type:

``` git add test1.txt ```

if you type git status again you will see the file (test1.txt) is now green. It means that the file is checked but still not committed. So, now it's time to commit the file:

``` git commit -m “write a message in here….” ```

Type ``` git status``` again. You should get a message *“nothing to commit”*. 

You can also add changes to the file (any change) and create a new file:

 ```touch index.html```
 
Type ```git status``` again. Both files should now be red (the txt file appears as modified and the new file as untracked). 

### There are a few more things you can do here (because you have 2 files):

For example, try these:

* ```git add *.txt``` will add only txt files 
* ``` git add *.*```  will add everything
* ```git add .``` will add everything within that particular folder/project. 

So, in your case, you will use the 3rd option. Type:

```git add .```, then ``` git commit -m”msg…...”```, and lastly ```git status```.

### Add files on Github
Now that you have two files, let's add these on Github. First create a repository (github website → your profile). Note that if you don't yet have an acount on GitHub, you need to create one [here](https://github.com) by choosing **sign up**. 

Then you can add your local repository on GitHub by typing
``` git remote add origin https://github.com/location/of/the/repository.git ```  

You can now push the changes from the local (your computer) to the server:

``` git push ``` or ```git push -u origin master```

### Enable git commands, autocomplete and colours
#### Add colour
First check if colouring is already enabled:

``` git config color.ui```. If color.ui  doesn't exist, type:

```git config --global color.ui true```. This command enables colouring 

### Branching and merging 
#### What are branches 

When you are making changes to your code, it is not recommended that you do them on the main branch or the master branch but rather create a branch for yourself, and once changes are ready, merge these changes with the master. 

Create branch:

```git branch “branch name”```

Checkout branch:

```git checkout “branch name”```

![Imgur](https://i.imgur.com/zSQvh5C.png)

#### Now let’s do some changes:

``` touch test2.txt```

```git status```

``` git add .```

```git commit -m “added test2.txt”```

```git push```

#### You can switch between you master and your branches using the commands:

```git checkout master```

```git checkout “branch name”```

Now you need to merge the new branch in master:

```git merge “branch name”```. 

Remember that to merge, you have to make sure that you are on master. But to see the merge changes in your repository you need to push:

```git push -u origin master```

after that, branch and master should be in synch.

You can also delete a branch. To delete a branch from your local type ```git branch -d “branch name"```. To delete from remote type ```git push origin --delete “branch name”```.

### Copy a GitHub repository to your (local) computer
To get a copy of a github repository in your local machine you need to copy the URL of that repository on github, which looks something like that: ``` https://github.com/username/repository_name.git```. So, the command to simply copy a repository is:

```git clone https://github.com/username/repository_name.git```

Now, you’ll notice that you are running as master. Type:

```git remote -v```. The output is the origin url of the repo (as fetch and push). If you don’t get origin, type:

```git remote add origin https://github.com/username/repository_name.git```

#### Pull changes from a branch to your local
If you want to pull a branch version of a repository type:

```git pull <remote name> <branch name>```
 
#### Push to a branch (not master) from local
First checkout/switch to the branch:

```git checkout -b <branch name>``` and then ```git push -u <remote name> <branch name>```

#### Check your current branch from terminal
If you want to check your current branch, just type:

```git branch```

 this will give you all the branch names and your current branch with an asterisk. 























 












