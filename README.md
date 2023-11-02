# git-cheat-sheet

Comprehensive guide intended to serve as a quick reference tool for Git commands and processes. It encapsulates key Git concepts, common commands, and best practices. With this cheat sheet, both Git beginners and experts can navigate Git workflows with ease.

In this cheat sheet, you'll find everything from basic commands like `git clone`, `git commit`, `git pull` and `git push`, to more advanced operations like branch management (`git checkout`, `git branch`, `git merge`) and conflict resolution. It also covers the use of `.gitignore` files for managing untracked files, and advanced commands for manipulating the commit history like `git rebase` and `git reset`.

### Git WorkFlow

```
LOCAL SYSTEM                              REMOTE REPOSITORY (GitHub)

+-------------+      +-------------+      +------------------+      +------------+
| Working Dir | ---> | Staging Area| ---> |  Local Repository| ---> | Remote Repo|
|  (Edit)     |      |   (Stage)   |      |    (Commit)      |      |  (Push)    |
+-------------+      +-------------+      +------------------+      +------------+
       |                   |                      |                       |
       |                   |                      |                       |
       |<---- git checkout |<----- git reset HEAD |<---- git reset --soft |
       |                   |                      |                       |
       |<------------------ git reset             |<---- git reset --hard |
       |<-----------------------------------------  git clone / git pull  |
```

In this diagram:

1. **Working Directory (Edit)**: This is your workspace where you make changes to your files.
2. **Staging Area (Stage)**: You add your changes here when they're ready to be committed. The command `git reset HEAD` unstages files.
3. **Local Repository (Commit)**: When you're satisfied with your changes in the staging area, you commit them to your local repository. The `git reset` command undoes commits and `git reset --soft` undoes a commit but keeps changes staged.
4. **Remote Repository (Push)**: You can push your commits from your local repository to the remote repository. The `git reset --hard` command discards all local changes and makes the local repository identical to the remote repository. The `git clone` and `git pull` commands fetch changes from the remote repository to your local system.

### Install Git: Installation in Windows/Linux/Mac OS X

**Install Git on Windows**

Download the latest version of Git from [here](https://git-scm.com/download/win).

Open Command Prompt and run the following command to configure Git on your PC using your username and email.

```
$ git config --global user.name "user_name" 
$ git config --global user.email "user_email@template.test"
```

**Install Git on Linux**

You can install Git on Linux using the command apt-get:

```
$ sudo apt-get update
$ sudo apt-get install git
```

Configure your username and email using the following command:

```
$ git config --global user.name "user_name"
$ git config --global user.email "user_email@template.test"
```

**Install Git on Mac OS**

You can install Git on Mac OS using the following [homebrew](https://brew.sh/) command:

```
$ brew install git
```

Configure your username and email using the following command:

```
$ git config --global user.name "user_name"
$ git config --global user.email "user_email@template.test"
```

### Git Clone

`git clone` is a command which is used to clone or copy a target repository.

```
+----------------+                               +----------------+
|   Remote Repo  |                               |   Local Repo   |
|   (Github)     |  --- git clone command --->   |   (Your PC)    |
|                |                               |                |
+----------------+                               +----------------+
```

This diagram indicates that when you run the `git clone` command on your local machine (Your PC), it copies the entire contents of the remote repository (the original repository on GitHub) to a new directory on your local machine (Local Repo).

**The process includes:**

1. Creating a new directory.
2. Initializing a Git repository in the new directory.
3. Adding a remote (`origin`) pointing to the URL you cloned from.
4. Fetching all references from the remote repository (including commits, tags, branches, etc.).
5. Checking out the default branch (usually `master` or `main`).

As a result, you have a complete, working copy of the original repository on your local machine, allowing you to work on the project freely without affecting the original code.

**How to clone a repository?**

1. Find the repository you want to clone on a platform like GitHub.
2. Click the "Clone or Download" button to get the repository's URL.
3. Copy this URL.
4. Open your terminal or command line.
5. Use the command `git clone` followed by the URL you copied.
6. Wait for the process to complete. You now have a copy of the repository on your local machine!

**Clone a specific branch from the repository.**

1. Identify the repository and the specific branch you want to clone.
2. Copy the URL of the repository from the "Clone or Download" button.
3. Open your terminal or command line.
4. Use the command:

    ```
    git clone -b <Branch_name> <Repo_URL>
    ```

    Remember to replace `<Branch_name>` and `<Repo_URL>` with the actual branch name and the repository URL respectively.

5. Once the process finishes, you'll have the specified branch from the repository on your local machine!

### Git Branch

A branch in Git is like a new "version" of your project. It allows you to make changes without messing up the main project (usually called the 'main' or 'master' branch). It's like having a clean slate to draw on while keeping your original drawing safe.

If you want to make a new branch to work on, you can do so with a command like this:

```
git branch <name_of_your_new_branch>
```

Just replace `<name_of_your_new_branch>` with the name you want for your new branch, and you're ready to go!

```
          +-----+
          |     |  (3) Create branch "new_feature"
          |  O  <-----------------+
          |     |                 |
          +-----+                 |
            ^                     |
            |                     |
          +-----+                 |
          |     |  (2) Make changes 
          |  O  |                 
          |     |                 |
          +-----+                 |
            ^                     |
            |                     |
          +-----+                 |
          |     |  (1) Start      |
          |  O  |   "main" branch |
          |     |                 |
          +-----+                 |
```

In this diagram:

1. Start with the main branch. This is usually where your stable code lives.
2. Make some changes to your code. At this point, your changes exist only in the main branch.
3. Create a new branch named "new_feature" using `git branch new_feature`. Now, your changes are in the new "new_feature" branch, and the main branch remains as it was before the changes.

### Git Switch Branch

Using the `git checkout` command, we can switch from one branch to another.

```
git checkout <branch_name>
```

### Create Remote Branches

Git doesn't support directly creating a separate branch on a remote repository. However, it allows you to make a local branch remote by pushing it.

**To create a remote branch, follow these steps:**

First, create a local branch and switch to it:

```
git checkout -b <branch_name>
```

Next, push the local branch to the remote repository:

```
git push -u origin <branch_name>
```

> (Note: 'origin' is the standard name for the remote repository.)

Once the branch is pushed, anyone can retrieve updates by running:

```
git fetch
git checkout <branch_name>
```

Just replace `<branch_name>` with the name you've chosen for your branch.

### Delete Branches

After completing work on a branch and merging it with the main branch, it may be necessary to remove the branch.

You can accomplish this by using the command below:

```
git delete -d <branch_name>
```

> (Note: This command removes a local copy of the branch. The original branch could potentially remain in remote repositories.)

If you need to remove remote branches, utilize this command:

```
git push origin --delete <branch_name>
```

Please ensure to replace `<branch_name>` with the name of the branch you wish to delete.

### Git Checkout

The `git checkout` command is like a remote control for Git. It tells Git where you want to make changes in your project. Mostly, you use it to move between different branches of your project. It's also handy for getting back an old version of a file you've changed.

```
main:       A--B--C--D
                   \
new_feature:        E--F
```

In this diagram:

1. `A`, `B`, `C`, `D` are commits made on the `main` branch.
2. You decided to create a new branch at commit `B` (using `git checkout -b new_feature`).
3. On this `new_feature` branch, you've made three commits `E`, `F`, and `G`.
4. The `main` branch remained unchanged when you switched to `new_feature`.
5. You can use `git checkout main` to switch back to the `main` branch and `git checkout new_feature` to switch to your `new_feature` branch.

This graph visualizes how branches work in Git, representing each commit as a node (`A` through `G`) and branches as paths through those nodes. Each branch can be thought of as a unique pathway through a shared history of commits.

**Switching to a Different Branch**

If you want to switch to another branch or create a new one, use this command:

```
git checkout -b <branch_name>
```

This will move you over to the new branch you've named `<branch_name>`.

**Using a Tag to Remember a Point in Time**

When you're working on a big project, it can be handy to mark certain points in your work. That's what tags are for.

You can use the command below to go to a specific tag and branch:

```
git checkout <tag> <branch_name>
```

Just replace `<tag>` with the name of the tag you're looking for, and `<branch_name>` with the name of the branch you want to go to.

### Git Status

`git status` is like a progress report for your project. It shows you what's going on in your project and helps you keep track of changes you've made, including files you haven't told Git about yet.

**Here's how you use it:**

Just type:

```
git status
```

**Here's how to see the status after adding a file:**

First, add a file to your project. You can make a new one like this:

```
touch file.txt
```

Then, type `git status`. You'll get a message showing you what changes you've made in your project.

```
$ touch file.txt
$ git status

On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    file.txt

nothing added to commit but untracked files present (use "git add" to track)
```

**Here's how to see the status after deleting a file:**

First, remove a file from your project like this:

```
git rm file.txt
```

Then, type `git status` again. You'll get a message showing you that the file has been deleted.

```
$ git rm file.txt
$ git status

On branch main
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    deleted:    file.txt
```

### Git Commit

`git commit` is like saving your game. It takes a snapshot of your changes, so you can come back to them later if needed. Each commit gets a special ID for easy reference.

```
                           ┌──────────────────────┐
                           │                      │
    Working directory      │    Staging area      │            Git repository
 ┌────────────┐            │ ┌────────────────┐   │           ┌────────────┐
 │  Changes   │  git add   │ │  Changes       │   │  git      │            │
 │  made      ├───────────►│ │  staged        │   │  commit   │ Commit     │
 │            │            │ │                │   ├─────────► │ with       │
 └────────────┘            │ └────────────────┘   │           │ commit ID  │
                           │                      │           └────────────┘
                           └──────────────────────┘
```

In this flow:

1. You make changes to your files in the working directory.
2. You add these changes to the staging area using the `git add` command.
3. Then, you commit these changes to the Git repository using the `git commit` command.
4. The `git commit` command generates a unique commit ID for this set of changes.

This way, every commit (set of changes) has its own unique ID, allowing you to track or revert changes as needed.

**Here's how you use it:**

Just type `git commit`.

Want to leave a note for yourself about this commit? Use `-m` to add a message like this: `git commit -m "Your message here"`

If you only want to commit changes to files you've already staged, use `-am` like this: `git commit -am "Your message here"`

Made a mistake in your last commit message? No worries. Use `git commit --amend` to change it.

`git rm` is the delete button. Use it to remove files from your project.

Type `git rm file_name` to remove a specific file.

When you use `git status` afterward, it'll show you that the file has been deleted.

Now, here's a simple text-based flow showing the sequence of operations:

```
1. Make changes in your files
2. Use `git commit` to save your changes
3. If you want, add a note with `git commit -m "Your message"`
4. To change your last note, use `git commit --amend`
5. To delete a file, use `git rm file_name`
6. To check your changes, use `git status`
```

This "diagram" is essentially a step-by-step guide of using the mentioned Git commands. It lists the commands in a typical order of usage, starting from making changes to your files to checking the status of your changes.

### Git Rebase

Think of `git rebase` as a way of tidying up your project's history.

In simple words, it takes a series of changes you made on a side branch and replants them onto another branch, usually the main one.

So, why would you do this? To keep your project history in a straight line. That way, it's easier to understand what changes were made and when.

Here's an easy way to picture it:

You're working on a project. You've got your main branch, and then you've got a side branch where you've been experimenting with some new features.

When you're happy with those new features, you don't want them stuck out on a limb. You want to bring them back into the main flow of your project. That's where `git rebase` comes in. It allows you to neatly bring your work back to the main branch.

```
git rebase <branch_name>
```

### Git Fetch

Think of `git fetch` as a way to get a sneak peek at the latest updates from other people on your project. It brings in the newest changes from the remote repository to your local one, but it doesn't change anything in your current workspace.

This is great because you get to see what others have been working on, but it doesn't mess with the stuff you're currently working on. You can then take your time to look over these new updates and decide when and what you want to merge with your work using `git merge`.

So, in short, `git fetch` is like a polite neighbor - it brings you the latest news, but it doesn't barge into your house and rearrange your furniture!

```
┌──────────────────────┐          git fetch       ┌──────────────────────┐
│                      │ ───────────────────────► │                      │
│  Remote Repository   │                          │  Local Repository    │
│                      │  new changes             │                      │
│  (on GitHub)         │  ──────────────────────► │  (on your PC)        │
│                      │                          │                      │
└──────────────────────┘                          └──────────────────────┘
```

In this flow:

1. Changes are made to the remote repository (on GitHub for example).
2. You run the `git fetch` command on your local repository (on your PC).
3. The `git fetch` command brings the new changes from the remote repository into your local repository. But it doesn't merge them or change your current workspace.
4. You can review these changes and decide when to merge them into your project.

This way, you can see the latest updates and changes made by others, without disrupting your own work.

Just type:

```
git fetch <branch_name>
```

### Git Pull Remote Branch

The `git pull` command is like a magnet that draws in all the updates from your remote repository (the one you've copied or "forked") to your local repository (the one on your computer).

Imagine it like this: with `git pull, you're catching all the new stuff from your remote repository and instantly updating your local repository to match it.

So, in short, `git pull` keeps your local work in sync with the remote one.

```
┌──────────────────────┐          git pull        ┌──────────────────────┐
│                      │ ───────────────────────► │                      │
│  Remote Repository   │                          │  Local Repository    │
│                      │  new changes             │                      │
│  (on GitHub)         │  ──────────────────────► │  (on your PC)        │
│                      │                          │                      │
└──────────────────────┘                          └──────────────────────┘
```

In this flow:

1. Changes are made to the remote repository (on GitHub for example).
2. You run the `git pull` command on your local repository (on your PC).
3. The `git pull` command brings the new changes from the remote repository and directly updates your current workspace with these changes.
4. This way, your local repository is always in sync with the remote repository.

The `git pull` command is like a magic word that brings over the updates from a remote repository. Here's how you use it:

Just type:

```
git pull
```

It's as simple as that! This command is just like typing `git fetch origin head`.

Want to see if there's anything new? Use this command: 

```
git pull <NameOfTheRemote> <NameOfTheBranch>
```

If everything is already up-to-date, it'll say "Already up to date". But if there are any new updates, it'll bring them into your local repository and merge them in.

### Git-Ignore

Sometimes, we don't want Git to track every file. Let's say you have files with sensitive info like passwords, API keys, or just personal stuff. We can tell Git to ignore these using a magic file called `.gitignore`.

This `.gitignore` file lives right inside your project folder, and it tells Git what files to stay away from when making commits.

So how do you set up a `.gitignore`? It's super easy:

1. Open up your project folder on your computer.
2. Make a new file in there and name it `.gitignore`.
3. Inside this file, write down all the files or folders you want Git to ignore.
4. Add the `.gitignore` file to your repository.

And that's it! If you now check your repository status, all the stuff you listed in the `.gitignore` won't show up. Git knows to keep its hands off them.