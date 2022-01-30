# Introduction to Git

## Basics

Git is an open source distributed version control system.

VCS (version control system) refers to a system which can keep track of all the code that is added to a project. Often, you want the history of the project to be preserved for various reasons. Say, the latest version of your software has major bugs, and as a result, you want to roll back some changes to an earlier date. This will only be possible if your code base is version controlled.

Git is also called _distributed_ because the code base isn't stored on one server. Instead, each of the developers working on the project can have their own copies of the project. They can make changes independently on their machines, and then request for their changes to be merged back into the original software.

## Why Git?

Git is one of the topics covered in MIT's Missing Semester. This course covers multiple useful topics that are often not formally taught, but they can be very useful to students.

Git is a vast and powerful software, but **you don't need to be an expert at Git.** You just need to know enough commands to maintain your repository and contribute to other repositories. Rest of the stuff, you can learn as you go.

There are two things that I believe are important for open source software programs, and Git helps you realize them.

1. Integrity of history : The project history is an important data that lets users trust the software. Anyone can see how the software developed or when the different components were added. It also lets people track new changes, so that external contributors can focus more on testing new code and also restrict themselves to auditing new code.
2. Long term maintainability : With git, you can associate commits with a descriptive commit message. This lets future maintainers know more about the code. Commits also carry author email - which can be useful in case a maintainer needs to contact a past maintainer to discuss some legacy code.

## My approach to Git

I believe many Git workshops get the direction wrong. Their focus is on GitHub; and git is shown as a side utility. I call that the "easy way". Instructor will create a repository. They'll ask viewers to fork the repo, make some minor change via GitHub web interface, and create pull request. Such workshops end with a "grand message" that the viewer made their first PR. Its cool and all, but it's severely lacking in some important concepts.

I instead prefer bringing Git to the center stage. Git is very powerful, and knowing how to work with the command line utility is going to serve you quite far on your journey. GitHub has a cool self-explanatory UI - do you really need to focus more over learning that as compared to a powerful command line utility?

Another minor complaint with having all focus on GitHub is that new students fail to appreciate the existence of other git repository hosting services. Truth is that once you learn Git, you can work with any hosting service.

## A note about Git GUI programs

I'm not against GUI programs altogether. Once in a blue moon, even I fall back to using GUI. However, while learning it's better to use command line client only. That way you know what is happening, and it strengthens your understanding.

PS. Recorded lectures from The Missing Semester are free to view. You can check out their website here : [https://missing.csail.mit.edu/](https://missing.csail.mit.edu/).
