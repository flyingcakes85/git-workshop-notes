# Working with Branches

Git provides the ability to create branches to let developers work on new features or bug fix without disturbing the main code. Changes you make to a branch are stored separately from the other branches. You can switch between branches anytime. When you think you have made enough changes to a branch and the changes are working, you can merge the branch into your `main` branch.

## Listing branches

`git branch` will show you your local branches, and adding the `-a` flag will also list remote branches.

```sh
[snehit@wired my-project]$ git branch
* main
[snehit@wired my-project]$ git branch -a
* main
  remotes/origin/main
```

The branch marked with an asterisk denotes the currently active branch. Any changes or commits you make are added on the currently active branch.

## Creating and switching branches

`git branch <name>` creates a new branch. `git checkout <name>` will switch to the new branch so that further changes are make to the new branch.

```sh
git branch add-emotes
git checkout add-emotes
```

You can also use the shorthand to create and switch branch in one command. Just use the `checkout` command with a `-b` flag.

```sh
[snehit@wired my-project]$ git checkout -b add-emotes
Switched to a new branch 'add-emotes'
```

You can also _checkout_ an older commit. This will replace the project files with the content that existed at that commit. Run `git log --oneline` to see the commit hashes.

```sh
[snehit@wired my-project]$ git log --oneline
f15f7dc (HEAD -> bugfix, origin/main, main, add-emotes) Update test.py
7e8fc14 Update test.py
9c804c0 Update test.py and add new code
5de911e Add test.py with basic code
```

Note the hash of whichever commit you want to checkout. Say, we want to go to the first commit. Its hash is `5de911e`.

```sh
git checkout 5de911e
```

This will land you to the first commit. If you see the project now, you will find only one file. Don't worry, our changes aren't lost. We can just switch to `main` branch to get our changes back.

```sh
git checkout main
```

## Working on branches - merging and stash

You usually create a branch to work on bug or feature without disturbing the actual code. The benefit here is that if there are any urgent changes required to the main code, you can make commits on main without needing to halt working on bug or feature.

There are usually three situations.

### Fast-forward merge

First checkout the newly created `add-emotes` branch.

```sh
git checkout add-emotes
```

Let's make some changes now.

```sh
echo "print(':-)')" >> emotes.py
git add emotes.py
git commit -m "Add emotes"
```

You test the code. It works and you are satisfied. So you decide to merge it into main. First checkout `main` branch then merge the other branch into it.

```sh
[snehit@wired my-project]$ git checkout main
Switched to branch 'main'
[snehit@wired my-project]$ git merge add-emotes
Updating f15f7dc..e74906b
Fast-forward
 emotes.py | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 emotes.py
```

Notice the phrase `Fast-forward`. It signifies that no commits were made on main from the time of creating branch `add-emotes` and the time when we merged it. Git could just "fast-forward" the `main` branch with commits from `add-emotes`. You ran use `git log --oneline` to verify that the commit was indeed applied on `main` branch too.

### Recursive merge

Let's do this process again, but we will make a commit on `main` before merging. Again, checkout `add-emotes` and make some changes.

```sh
git checkout add-emotes
echo "print(':/')" >> emotes.py
```

Let's say, you don't want to commit now, as you want to make more changes. But there's an important fix to make on the `main` branch. You can go forward and switch branch, but it can become messy, because the changes will also show up on main (they are uncommitted) and it will get confusing for you. So, you store the changes to a temporary directory and then make changes on main.

```sh
git stash
```

Upon running this, you will notice that the line we added to `emotes.py` is no longer there. Now make changes on main and commit.

```sh
git checkout main
echo "print('important bugfix')" >> test.py
git add test.py
git commit -m "Important Bugfix"
```

Now, let's switch back to `add-emotes` branch and complete our code. We use the `git stash pop` command to bring back the changes we had made earlier.

```sh
git checkout add-emotes
git stash pop
echo "print('B-)')" >> emotes.py
git add emotes.py
git commit -S -m "Add more emotes"
```

Now, let's switch back to `main` branch and try merging `add-emotes`.

```sh
git checkout main
git merge add-emotes
```

This will land you in your text editor, with the following text.

```
Merge branch 'add-emotes'
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
```

This is very much like making a commit. There was already a commit made on to `main` before we merged the branch. So, git cannot simply fast-forward. Save this file and exit. You should get this message.

```
Merge made by the 'recursive' strategy.
 emotes.py | 2 ++
 1 file changed, 2 insertions(+)
```

This time, it was not fast forwarded. Git used a different strategy called recursive.

### Merge conflict

Finally, if you change the same line of the same file in both branch then try to merge them, you run into a merge conflict. Let's quickly add different text to the same file on both `main` branch and `add-emotes` branch.

```sh
git checkout main
echo "print('added via main')" >> test.py
git add test.py
git commit -m "Make program better"
git checkout add-emotes
echo "print('added via add-emotes')" >> test.py
git add test.py
git commit -m "Make program fancy"
```

If you see the contents of `test.py`, you won't see the line `print('added via main')`. If you checkout `main`, then you won't see `print('added via add-emotes')`. So, what we have got is different content at same location in two branches. This will lead to a conflict.

First checkout `main` branch.

```sh
git checkout main
```

Let's now merge it and see what happens.

```sh
[snehit@wired my-project]$ git merge add-emotes
Auto-merging test.py
CONFLICT (content): Merge conflict in test.py
Automatic merge failed; fix conflicts and then commit the result.
```

Git bailed out saying it cannot merge - as we expected.

When you get a merge conflict, you shouldn't need to panic. It's not an "error". It only indicates that git is unable to decide which copy of the code to keep, because the two branches have different changes for the same file location.

Git is telling us that there is a conflict in `test.py`. Let's open that file and see what's there.

```
print('Hello World')
print('Another line')

print('Added via GitHub web')
<<<<<<< HEAD
print('important bugfix')
print('added via main')
=======
print('added via add-emotes')
>>>>>>> add-emotes
```

Here, you can see the conflicting part between angled brackets. From `<<<<<<< HEAD` to `=======` are the contents that are in `main`. From `=======` to `>>>>>>> add-emotes` are the contents that are in `add-emotes`. You can freely remove one of them, along with the angled brackets and equal signs. You may also just remove the brackets and equal signs in case you want to keep changes from both branches. Finally, you may remove it to add some other code altogether. It's all up to you.

Let's say, I remove the code from `main`. So my file should now look like this.

```
print('Hello World')
print('Another line')

print('Added via GitHub web')

print('added via add-emotes')
```

Now we can continue on to adding file and committing it.

```sh
git add test.py
git commit -m "Merge add-emotes into main"
```

This will create the merge commit.

## Deleting branches

You may want to delete a branch if you have merged it into `main`, and it is no longer needed. Or maybe you decided against incorporating the changes from that branch. In these cases, you can delete the branch.

```sh
git branch -d <name>
```

If you had published a branch you now want to delete, run this command

```sh
git push origin --delete <branch name>
```

Run these commands with care, as you may accidentally delete one of the important branches.
