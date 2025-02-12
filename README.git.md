# A Quick Guide to Using Git and GitHub For Your Project

Big thanks to [@NetNinja](https://www.youtube.com/@NetNinja) and his YouTube playlist on [how to use Git and GitHub](https://youtube.com/playlist?list=PL4cUxeGkcC9goXbgTDQ0n_4TBzOO0ocPR&si=GUFSiFppn8n_o8VA) for getting me started with Git and GitHub.

**I would highly suggest watching those videos first** if you are completely new to the concepts of Git and GitHub.

This guide is intended to get you quickly setup with Git and GitHub and won't cover many useful and essential functions.

##

Now there are a few ways of using Git and GitHub:

-   completely within an IDE (IntelliJ IDEA)
-   the GitHub Desktop App
-   manually through the command-line

I believe using the command-line is the best way to learn Git because it is universal. If you know how to use it in the command-line, you know how to use it no matter the IDE or operating system.

Once you have a fundamental understanding on how Git works, you'll be able to use the Git implementaions in IDEs and other helpers as a convenience and not as a crutch.

##  Install Git

Firstly, to install Git onto your system, you can go to the Git download page at: https://git-scm.com/downloads and follow the installation instructions for your operating system.

To test if you have Git installed, type `git --version` into your terminal. It should return the version of Git you are running.

### Big Tip

Type `git -h` to list common Git commands if you forget them!

##  Initialize the Git Repository

You can create/initialize a new Git repository in a directory that is clean, or one that already has files inside.

>   Make sure you are running this within your project directory!

```
git init
```

Once your repository has been initialized, you should see a folder called `.git`. To check for this file:

>   For Windows (Powershell)

```
Get-ChildItem -h
```

>   For Linux/MacOS

```
ls -A
```

##  Adding to the Staging Area

Once you modify and create new files within the repository directory, you need to add those files to the staging area to tell git to track the changes made to these files in the next commit.

To view the status of files within your repository, use:

```
git status
```

It will show the files that are and aren't being tracked.

To add files to the staging area, use `git add` followed by the names of the files separated by spaces:

```
git add file1.txt file2.java file3.json
```

Alternatively, you can simply add a wildcard to add all the new and modified files to the staging area:

```
git add *
```

After that, you can use `git status` to confirm.

To remove from the staging area, use `git remove`.

### The `.gitignore` File

Sometimes, there will be certain files/folders that you don't want to track within your repository. You can tell Git to ignore these files/folders by including them in a `.gitignore` file.

Create a file named `.gitignore` and open it with a text editor. Then, you can add the names of files, folders, or specific file types that you do not want Git to track.

For example:

```
bin
out
*.class
src/TESTING
.vscode
.idea
*.iml
.DS_Store
```

##  Commit Your Changes

Commits are basically save points for your repository/branch. These allow you to rollback to specific commits and merge with others on other branches of your repository.

To make a commit with the files in your staging area:

```
git commit -m "This is a commit!"
```

>   You need to add a message to your commit with `-m`. If you forget to do so, Git will use the default text editor used by your operating system.

Use `git log` to view recent commits.

##  Setting Up a Remote Git Repository on GitHub

What you have right now is only a local repository, meaning that it is only stored on your local machine.

To make your repository accesible online, you can host a remote repository on GitHub to store your local repository.

Login/signup to https://github.com and [create a new repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository).

>   I wouldn't recommend initializing the repository with READMEs .gitignores and licenses. This is because it would create a separate commit and may cause an issue when pushing to the repository if you already have commits made in your local repository.

Once you have created the repository on GitHub, run the commands under "... or push an existing repository from the command line"

```
git remote add origin https://github.com/username/repo-name.git
git branch -M master
git push -u origin master
```

>   Git may ask you to authorize Git to have access to your account.

Now, your GitHub remote repository is up-to-date with your local repository.

##

### Issue: I'm getting an "authorization denied" or I need to type in my username and password each time I push or pull!

GitHub has made using a personal access token a requirement in place of passwords to access your repos through the command-line (using HTTPS). See [here](https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls).

This is mainly a Linux (and MacOS?) "issue" as I did not experience this problem on Windows.

<ins>A quick fix</ins> to this is to run Git through the terminal in an IDE such as VS Code/Codium. Then, your IDE should create a request to GitHub to authorize your IDE access to your account. The downside to this is that you can only clone, fetch, pull, and push within the terminal in your IDE.

##  Branches

When working with others, each member may be in charge of different features of the project. It is probably best to have each member work on their own branch separate from the master branch to avoid conflicts with other members and make sure the master branch only recieves complete and stable versions of features.

Create a new branch off of the master branch

```
git branch <name of new branch>
```

You should see your new branch listed when you use `git branch -l` to list all of your local repository's branches.

You may have noticed that you are still on the master branch so to start working on the new branch, use `git checkout`

```
git checkout <name of new branch>
```

Now, any commits made will be towards the branch you have currently checked out.

##  Pushing to GitHub

Once you've made some commits that you are happy with, it's time to sync them with the remote repository on GitHub.

Use `git branch` to confirm which branch you are on.

Use `git push` to push your changes to GitHub.

```
git push origin <name of branch you want to push to>
```

### Note 

When working on a project, avoid pushing to the master/main branch of the repository if you are pushing changes from a different branch. This is to reduce conflicts and keep your repository maintainers happy.

##  Pulling Changes Made on a Different Branch Into Another.

Now, there may be a branch with code that doesn't exist on another. What `git pull` does is that it takes code (and commits) from a specified branch, and integrates that code into which branch you specify.

<ins>For example:</ins> Let's say someone has updated the master branch on GitHub with new code and you want that new code and commits copied/integrated into your own separate branch.

In this case you can run:

```
git pull origin master
```

When you run this command, Git will fetch for new commits made on the master branch on GitHub and copies/integrates all those commits into the branch that you are currently on.

### Updating the Master Branch

When you want to update the master branch, it is recommended to use GitHub's pull request feature instead of using `git pull`.

>   Pull requests are a GitHub feature and not a part of Git.

Doing so allows everyone to be notified that you want to update the master branch and review the code before agreeing to do so.

To create a pull request on GitHub, go to the main page of the repository on GitHub and click on the `Pull requests` tab on the top toolbar.

Then, you can create a `New pull request` and specify what branch you want to pull into the master branch.

##

That is it for this guide. The purpose of this was to help people start learning how to use Git and GitHub quickly when starting a new project with a team.

There is a lot more you can do with Git and GitHub than what is mentioned in this guide, so I highly recommend watching the playlist linked at the top of this guide and continuing your journey from there.

I hope this guide helped :)
