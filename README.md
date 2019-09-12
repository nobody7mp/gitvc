Scott Parker NO NAME name removed
# Version Control with Git and GitHub - Basics
This repository is meant to help guide you in using the basic Git commands while working with version control in a team environment. 

## Getting Started

Download the following:
- [Git](https://git-scm.com/downloads "Git Download")
- [Github Desktop](https://desktop.github.com/ "GitHub Destop Download")

If you haven't configured the author name and email address to be used with your commits, you can do so with the following comands.

Note Git strips some characters (for example trailing periods) from user.name.

`git config --global user.name "Sam Smith"`

`git config --global user.email sam@example.com`

------------
### Repositories

Create a new local repository

`git init`

### Check out a repository

Create a working copy of a local repository:

`git clone /path/to/repository`

For a remote server, use:

`git clone username@host:/path/to/repository`

### Add files
Add one or more files to staging (index):

`git add <filename>`

`git add *`

`git add .`

### Commit	
Commit changes to head (but not yet to the remote repository):

`git commit -m "Commit message"`

Commit any files you've added with git add, and also commit any files you've changed since then:

`git commit -a`

### Push
Send changes to the master branch of your remote repository:

`git push origin master`

### Status
List the files you've changed and those you still need to add or commit:

`git status`

### Connect to a remote repository
If you haven't connected your local repository to a remote server, add the server to be able to push to it:

`git remote add origin <remote_repo_url>`
`git push --all origin`

To set this as the default origin, you can do: 

`git push --all --set-upstream origin`

List all currently configured remote repositories:	

`git remote -v`

### Branches
Create a new branch and switch to it:

`git checkout -b <branchname>`

Switch from one branch to another:

`git checkout <branchname>`

List all the branches in your repo, and also tell you what branch you're currently in:

`git branch`

Delete the feature branch:

`git branch -d <branchname>`

Push the branch to your remote repository, so others can use it:

`git push origin <branchname>`

Push all branches to your remote repository:

`git push --all origin`

Delete a branch on your remote repository:

`git push origin :<branchname>`

### Update from the remote repository
Fetch and merge changes on the remote server to your working directory:

`git pull`

### Merging
To merge a different branch into your active branch:

`git merge <branchname>`

View all the merge conflicts:

`git diff`

View the conflicts against the base file:

`git diff --base <filename>`

Preview changes, before merging:

`git diff <sourcebranch> <targetbranch>`

After you have manually resolved any conflicts, you mark the changed file:

`git add <filename>`

### Tags 
You can use tagging to mark a significant changeset, such as a release:

`git tag 1.0.0 <commitID>`

Push all tags to remote repository:

`git push --tags origin`

### Logging
CommitId is the leading characters of the changeset ID, up to 10, but must be unique. Get the ID using:

`git log`

Get all commits rendered as individual lines

`git log --oneline`

Render a text-based graphical representation of the commit history.

`git log --graph`


### Undo local changes
This will checkout the file from HEAD, overwriting your change:

`git checkout -- <filename>`

To drop all your local changes and commits, fetch the latest history from the server and point your local master branch at it, do this:

`git fetch origin`
`git reset --hard origin/master`

### Stashing
Stashing takes the dirty state of your working directory — that is, your modified tracked files and staged changes — and saves it on a stack of unfinished changes that you can reapply at any time.

To stash changes

`git stash`

To see everything in stash

`git stash list`

To apply stashed changes

`git stash apply`

To show stashed item

`git stash show`

To apply an older stashed item

`git stash apply stash@{2}`

Remove a single stashed state from the stash list and apply it on top of the current working tree state

`git stash pop`

### Search

Search the working directory for foo():

`git grep "foo()"`

### Deleting Commits

Delete a commit locally

Example: 

`git log --pretty=oneline --abbrev-commit`

```
46cd867 Changed with mistake
d9f1cf5 Changed again
105fd3d Changed content
df33c8a First commit
```

Commit 46cd867 is the most recent commit and the one we want to delete, for doing that, we will use rebase.

`git rebase -i HEAD~2`

That command will open your default text editor with your two (Change the number 2 with the number of commits you want to get) latest commits:

```
pick d9f1cf5 Changed again
pick 46cd867 Changed with mistake
                                `
# Rebase 105fd3d..46cd867 onto 105fd3d

#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but sto...
```

We just need to delete the line that corresponds to the commit we want to delete and save the file.

Check to see that the change was applied correctly:

`$git log --pretty=oneline --abbrev-commit`

```
d9f1cf5 Changed again
105fd3d Changed content
df33c8a First commit
```

Delete a remote commit
To remove a commit you already pushed to your origin or to another remote repository you have to first delete it locally like in the previous step and then push your changes to the remote.

`git push origin +master`

Notice the + sign before the name of the branch you are pushing, this tells git to force the push. It is worth to mention that you should be very careful when deleting commits because once you do it they are gone forever. Also, if you are deleting something from a remote repository make sure you coordinate with your team to prevent issues.

### Useful Information

Basic Flow

![Basic Flow](https://raw.githubusercontent.com/inland-empire-software-development/gitvc/master/images/basic-flow.png)


Commit Referencing

![Commit Referencing](https://raw.githubusercontent.com/inland-empire-software-development/gitvc/master/images/commit-referencing.jpg)

------------

Credits:
[List of basic commands](https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html "List of basic commands") - Atlassian 
[Deleting a Commit](https://ncona.com/2011/07/how-to-delete-a-commit-in-git-local-and-remote/ "Deleting a Commit") - Ncona
