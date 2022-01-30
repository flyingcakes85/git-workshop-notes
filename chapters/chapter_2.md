# Starting with Git

We already know that Git tracks your project. So, every time you change a file and commit it to the project (basically asking Git to mark a milestone you can return to later, if needed), Git is recording the **changes** you made to each file. Note that complete files are not duplicated. Only the changes you made to each file are stored by Git. It is intelligent enough to create the complete file by knowing the changes you made all through.

## Installing

Downloads are offered at git-scm website. Windows users should download installer from the website. Users on \*nix systems can use their package manager for the same.

[https://git-scm.com/downloads](https://git-scm.com/downloads)

To check if git is working, open a terminal, and run

```sh
git --version
```

This should output the version name. An example output, on my system:

```
git version 2.33.0
```

I'm starting with shell commands now. Git commands should work on all systems, but other commands like `echo` will probably work only on \*nix based systems. May also in Git Bash on Windows.

## Setting up Git

Git needs some info to create commits. At the very least, it needs to know your name and email. Run the following commands to set them up.

```sh
git config --global user.name "Your Name"
git config --global user.email "email@domain.com"
```

You can verify them too. I have shown the commands with their outputs.

```sh
[snehit@wired ~]$ git config --global user.name
Snehit Sah
[snehit@wired ~]$ git config --global user.email
snehitsah@protonmail.com
```

You may also change the default init branch to something other than `master`.

```sh
git config --global init.defaultBranch main
```

You can replace `main` with any other name you like. This step is not necessary. Do this only if you don't want your default branches in new repositories to be named `master`.

## Initializing a repository

Create a new folder. Change working directory to this new folder. And then initialize a new repository.

```sh
mkdir my-project
cd my-project
git init
```

Now, you can open your code editor in this folder. Any files you add here will automatically be noticed by git. I run the following command to launch VS Code in my repo.

```sh
code .
```

## Adding files

You can either create files via a text editor like VS Code, or even the classic notepad, or you can use a terminal utility to create files. I'll use `echo` to create a simple python script.

```sh
echo "print('Hello World')" > test.py
```

It creates a file `test.py` with the code `print('Hello World')`.

Now, lets check if git notices this file or not. Run `git status` in the same folder, and you should get such an output.

```sh
[snehit@wired my-project]$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	test.py

nothing added to commit but untracked files present
(use "git add" to track)
```

There is quite some information here. The first line tells we are on this branch called `main`. Don't worry if you don't know what branches are. I'll discuss it soon.

Next is a section called `Untracked files`. This lists the file that are there in folder, but git isn't yet tracking them for changes. Our file, `test.py` is listed there. Git is also telling us a command to start tracking them... So lets move on to that.

## Adding files to staging

Run this command to start tracking `test.py`.

```sh
git add test.py
```

`git add` serves two purposes. If a file is untracked, then it will start tracking it and add to staging area. If a file is already being tracked, but has some changes, then git will simply just add the file to staging area.

What is the staging area, you ask? It's the files whose change will be recorded and stored when you run git commit the next time.

Before we move on to the next command, let's see the output of `git status` after running the above `git add` command.

```sh
[snehit@wired my-project]$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   test.py
```

Our file `test.py` is now listed under a different section - `Changes to be committed`.

If you have multiple files in a project, you can simply use the following command to add all changed and untracked files.

```sh
git add -A
```

Be careful while running this. It may add any extra files you created in the repository which you actually don't want in commits.

## Committing changes

Once you have files in the staging area, you `commit`. This is an important step. Note that commits are the mechanism by which git is able to preserve history. You can see commits as milestones, which anyone can check out.

Commits are accompanied by at least a title, and an optional message. Try to keep the message/title short, yet informative. For larger projects, it becomes necessary to have informative commit messages so that reviewers know what the commit does.

Run this in the terminal

```sh
git commit
```

This should land you in a text editor, usually vi(m), where you add commit title and message. This is what you should see.

```

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch main
#
# Initial commit
#
# Changes to be committed:
#	new file:   test.py
#
```

You get the output you saw with `git status` one more time, so that you can be sure that you are committing all the files you want. On the first line, give a commit title. Leave a blank line, and from the third line, you can write the description.

Here is an example. Note that I did not remove the lines that were already there. They are starting with a '#' and git will ignore them.

```
Add test.py with basic code

New beginnings - This file prints
Hello World. Tested with Python3.7
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch main
#
# Initial commit
#
# Changes to be committed:
#	new file:   test.py
#
```

Save and close the file. Git should create a commit now, and print some message in the terminal.

```sh
[snehit@wired my-project]$ git commit
[main (root-commit) 5de911e] Add test.py with basic code
 1 file changed, 1 insertion(+)
 create mode 100644 test.py
```

It's called `root-commit` because it's the first commit in this repo. There is a fancy alphanumeric string following it. `5de911e` - these are the first few characters of the commit hash. Commit hash is a 20 character alphanumeric SHA1 hash that is generated using data from past commit, changes in current commit, timestamp, author info etc. These hashes are git's primary mechanism to detect any changes to past code.

If you don't want to add a description to your commit - maybe because the change is very minor and self-explanatory - you can use the shorthand to just add a commit title.

```sh
git commit -m "Fix typo in code"
```

## Checking logs

Since we have made a commit, it's a permanent part of the repository now. You can see logs to verify the commit is there.

```sh
[snehit@wired my-project]$ git log
commit 5de911e18db087d3c3a57031dab49637e316608f (HEAD -> main)
Author: Snehit Sah <snehitsah@protonmail.com>
Date:   Thu Sep 9 12:12:00 2021 +0530

    Add test.py with basic code

    New beginnings - This file prints
    Hello World. Tested with Python3.7
```

This gives us information about the commit we just made. As we make more commits, the log will grow lager. In the first line, you have the complete commit hash. (in the last section, we only saw first 7 characters). We also have information about the author, commit date/time and message. If you are not interested in author info, and just want to see commit messages, we can use the shorter format with `git log --oneline`

```sh
[snehit@wired my-project]$ git log --oneline
5de911e (HEAD -> main) Add test.py with basic code
```

This is more useful to know how the project grew, since it omits author info, dates and commit description.

## Amending last commit

Sometimes it happens that you forgot to add a file to staging before commit, or there's a tiny change you need to make, which should have been a part of the last commit. In such situations, git provides an easy way to amend last commit. Assuming you made a commit, do some edits to code. Then do `git add` as usual. While committing, include the `--amend` flag to instruct git to update the last commit instead of creating a new one.

```sh
git commit --amend
```

If you look at the log, you will see the commit hash changes. This signifies that _some_ changes were made. Later on when you upload your code on the internet, these hashes will allow other collaborators ensure they have the same code as you. If you edit a past comment and upload it, then other collaborators will get to know about it. In general, it's not a good idea to amend/edit commits if you have published them onto the web. Do this only if the commits to be edited are only on your local machine. One exception is that when you accidentally commit and publish sensitive info, like access keys, password etc.

PS. In case you are wondering if other collaborators will match commit hash letter by letter to verify integrity - the answer is an obvious "no!". Git does that automatically.

## Recap

Try creating another file, and make some changes to `test.py`. Check status. Add both files to staging, and then make a commit. Check log to verify the commit was made.

You can use any text editor for the task. I'll quickly give the relevant shell commands for those who want to follow along in the shell.

```sh
echo "print('New file')" > new_file.py
echo "print('Another line')" >> test.py
```

Output of `git status` at this stage.

```sh
[snehit@wired my-project]$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   test.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	new_file.py

no changes added to commit (use "git add" and/or "git commit -a")
```

Continuing on to add files and commit them.

```sh
git add new_file.py
git add test.py
git commit -m "Update test.py and add new code"
```

Output of `git log`

```sh
[snehit@wired my-project]$ git log
commit 9c804c05610ca86f720abda62b297e9d2e6a725f (HEAD -> main)
Author: Snehit Sah <snehitsah@protonmail.com>
Date:   Thu Sep 9 12:34:49 2021 +0530

    Update test.py and add new code

commit 5de911e18db087d3c3a57031dab49637e316608f
Author: Snehit Sah <snehitsah@protonmail.com>
Date:   Thu Sep 9 12:12:00 2021 +0530

    Add test.py with basic code

    New beginnings - This file prints
    Hello World. Tested with Python3.7
```

## Using gitignore file

You may have some files in your project directory which you don't want git to track. For example, upon testing C/C++ apps, you have a binary that shouldn't be there with the code. To prevent them from accidentally being committed, you can add them to gitignore file. You'll first have to create a file named `.gitignore` in the root of your repo folder. Then you list the file paths that should not be tracked.

```sh
echo "*/a.out" >> .gitignore
```

This will prevent git from tracking any file with name `a.out`. The asterisk at beginning is a wildcard that will select any path where `a.out` exists. To add folders, append a forward slash after path.

```sh
echo "build/" >> .gitignore
```
