# GitHub Group Project: Quickstart Guide

**What does it mean to work as a team in GitHub?**

When you initialize a repo for a new project, there is only one branch -- the `main` branch. This is fine when you're the only one working in your repo, but when many people are working in the same codebase it's easy for code to get out of sync and for people's changes to get overwritten.

In order to work as a team and ensure that everyone is basing their work on the last accepted version of committed code, we fork from `main` and then create individual branches that can be worked on independently and don't affect `main` while they're in progress. 

When the code in your individual branch is in a place that is ready to be shared with the rest of your team, you will create a `pull request` that the team can review before your code gets merged and becomes part of the `main` branch. When a branch is merged to `main`, every developer will be able to `pull` an updated copy of the code that contains the latest changes.

*The most important thing about working in a group is communication. Check in with each other to make sure you're not working on the same feature and that you're not stepping on each other's code in shared files. It's worth it to take a small break to let a teammate finish their work so you can grab their latest code, rather than potentially creating conflicts by working in the same file.*

Let's go over some definitions before we get into the workflow:

**What is a branch?**

A branch is an exact copy of your GitHub `main` that you can work on independently without affecting anyone else's code. Your branch will contain the code from the last committed version of `main`.

Branches allow projects to be broken up into smaller tasks and worked on by separate developers without needing to worry that you will be writing code over top of each other. Typically, developers create a new branch when they start work on a new feature, and merge each branch when that feature is complete.

The work you do on your branch won't be shared with `main` until you say that it's ready (which you do by creating a `pull request`).

**What is main (or master)?**

`main` is the default name for the main branch in GitHub; in a workplace, it's often the *production* branch, and only holds code that is final and approved. In this project, `main` will be the main fork created by your team lead (the place where your branches come from). 

*Note: new GitHub repositories are using `main` instead of `master`, but because this is cloned from an old repo, the main branch is still called `master`. Feel free to update the name from `master` to `main` so you're using the latest!*

https://github.com/github/renaming

**What is origin?**

`origin` is a reference to the original remote repository that you cloned from -- the place from which files originate. In this case, your `origin` is your team lead's repo.

**What is upstream?**

`upstream` is the place that your pull requests will be merged into, and also the source of truth for all your group collaboration. As a team member, you will set your `upstream` as your team lead's repo (which is also your `origin`) the first time that you `push`! 

**This feels a little confusing**

Git takes a long time to master, so don't worry if you don't understand everything right away!  

The commands we're using here are the basic ones you need for collaboration, but if you want to explore a little bit more here are some good resources:

https://learngitbranching.js.org/

https://www.makeuseof.com/tag/git-version-control-youre-developer/

https://git-scm.com/book/en/v2


## Team Workflow

In this project, you will decide which team member will be the lead and will have the `main` repository. The lead will fork the repo from `cb-wd-7`, and *ALL team members (including the lead) will create branches* from this fork so that **NOBODY** is *ever* working directly on `main`. We do this to have one agreed-upon source of truth for the code. In a company, it's typically the lead of your dev team who will manage `main`, and they are the gatekeeper for the code that goes into the repo (which is the code that is live and ends up in the final product).

From the `main` branch, each team member will create a `feature` branch, which is a branch that they can use to work on a specific feature. When that feature is complete, the branch can be merged into `main` by the team lead. 

In GitHub-speak, your `upstream` is the source of truth and the birthplace of your code. All team collaboration happens `upstream`. We're also going to set your `origin` as your `upstream` so that when you open a `pull request` your code will be incorporated into the team code.

Here are the steps, with details specific to this group project:

- Team lead forks the repo from `cb-wd-7` and opens *settings* from the nav bar at the top
   - rename the branch to `main` (instead of `master`)
   - rename the repo to be called `group-project-ecomm`
   - in the *manage access* tab, add each group member and give them `write` access
    and gives team members `write` access
- Everyone (team lead *and* team members) `clone` to their desktop from the link on the team lead's repo and opens the new project in VSCode
- Everyone (team lead *and* team members) uses VSCode to create a new `branch` from the forked repo
   - click the *source control* icon on the left side of VSCode
   - click the 3 dots to open the menu and choose the *branch/create branch* option
   - give your branch a name that starts with your initials - for example, `jdg-branch`
   - look in the lower left corner of VSCode to make sure it shows your branch name - this confirms that you are on your new branch!
   - if you need to change to a new branch, type `git checkout <branchName>` in the terminal - I would type `git checkout jdg-branch` to switch to my branch
- Add, commit, and push your code in the same way that you always have, making sure you're *on your branch* when you are making changes
- The first time you `push`, you will probably get a message letting you know that your current branch has no upstream branch
   - if you pushed your code using the VSCode tool, you will get a modal with this message - click `ok`. You will see a dropdown asking you to set the `upstream`, and it is *VERY IMPORTANT* that you choose the `origin` as your `upstream`.
   - if you pushed your code using the terminal, you will get a message that says, `fatal: The current branch <branchname> has no upstream branch. To push the current branch and set the remote as upstream, use git push --set-upstream origin <branchname>`. Do this! 
- Open a `pull request` when your branch is ready to be merged (when your feature is complete).
  - if you pushed and set your origin using the VSCode tool, you'll be automatically asked if you want to create a `pull request`. If your feature is complete and you're ready, then go ahead!
- VSCode will show you a confirmation of where your changes are coming *from* and where they are going *to* - *PAY CLOSE ATTENTION HERE!*
  - your changes should be coming *from* your branch
  - your changes should be going *to* the `main` branch
- When you submit your PR, *message the group chat* 
  - this lets your team lead know that your code needs to be merged - *NEVER* merge your own PR!
  - team lead: reply to the message to let your team know that they need to pull the updated code from `main` into their own repo    
- To start working on your next feature, create a new `branch` and repeat!

For a version of this workflow with screenshots, take a look at this document:

https://docs.google.com/document/d/1JWv1x3mL4fSrn7fhQVexnKKAh2YOM7JkHX-Dv1PnpNY/edit

