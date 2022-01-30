# Beyond the book

## General development workflow

I'll briefly tell the workflow you follow when contributing to someone else's repo. You first fork the repository to your account. You clone your fork with `git clone <link>`. Likewise, you will then create a new branch which shall hold the commits you make. Furthermore, you can also directly make commits on `main`, but this is almost **never** recommended.

You make some changes then commit it. When you think you have made all the changes you wanted, you push the branch to remote on your repo, using `git push -u origin <branch name>`. On GitHub, you finally create a pull request from your branch to the `main` or `dev` branch of original repo.

Maintainers will often have a separate `dev` branch. This can be for various reasons - the simplest one being that they don't want everyone to be using the latest changes by default as it can be buggy and unstable. Those who want to test new features can manually switch to dev branch and use. Once features from dev branch are tested, it is finally merged into `main`.

If available, read the `CONTRIBUTING.md` file on the original repo.

## Referencing GitHub pull requests/issues

Say your pull request fixes a certain issue open on the original repository. You can add `Fixes #N` to your commit description. Here `N` is a number that shows just after the issue title. The numbers also show up on pull request titles. You can use the same `#N` format to reference a certain pull request or issue while adding commits on GitHub.
