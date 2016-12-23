# **Git & GitFlow Standards**
# Intro
Git is a distributed version control system that allows developers, designers, and other power users to view, edit or approve versioned code changes without weighing down their systems with multiple copies of the codebase. Read more at <https://git-scm.com>

For the new Connect Platform, git on Visual Studio Team Services is used, rather than the Team Foundation Version Control that was used in the past. Furthermore,  the new platform uses the git flow branching strategy to maintain a readable and easily adopted way to version code.

Below is a quick reference for developers to use.    

# Git Dictionary

Although most version control systems share a lot of terminology, each has its own variations.  Git has a very consumable naming convention to its terminology, allowing users to pick up quickly.

Below are some of the most common terms used within git.

* **.gitignore** - This is a file within a repository that git references to ignore certain file types when a developer commits changes.  Generally each development framework has a standard .gitignore that you can use as a guide. When creating a repo in Visual Studio Team Services, VSTS allows you to choose a standard .gitignore file from a list of tech stacks. 
 	
* **commit** - Committing is the action taken to save a version of your changes to a repository.  Commits are notated and recorded as a history of the changes made for later reference.

* **checkout** - Checkout is the term used to switch branches within a repository.  If the branch doesn't already exist on the developers machine, it will pull the changes from the origin/remote and switch to that branch.

* **repository** - Similar to most version control systems, a repository is a collection of code, generally for one project.  Within the repository are branches or versions of the code.

* **branch** - A branch is just another version of the repository, unlike some VCS's, branches in git are not an entirely new copy of the code, but just a diff from the other versions.  This prevents large projects from taking up covetted hard drive space.

* **pull request** - A pull request takes a feature branch that a developer has finished and applies it to the develop or master branch by merging and testing the code. When a PR is submitted, VSTS will attempt to merge the branches into a temporary branch, and if successful, the build system will kick off a build to validate that it builds correctly.  If both merge and build are successful, the PR will have to be approved by other developers that review the code changes.  Once reviewd and approved, the PR can be completed which merges the source and destination branches permanently, committing all changes in the branch to the destination branch.

* **origin/remotes** - A remote is a copy of the repository that is stored on a server.  While developing, all changes are made locally then pushed to a remote repo for others to consume.  There may be multiple "remotes" for a repository, but generally and in this context, VSTS will be the remote for all Connect Platform repositories. 

* **stash** - A stash is a copy of uncommitted work, stored locally to allow developers to save changes that might not be ready for a commit.  If desired, developers can reapply changes by "popping" the stash, which applies the changes to whichever branch is currently checked out.  The most common use for a stash is to swap the changes a developer has made from one branch to another.

* **push** - A push copies all changes on the current local branch to the origin/remote.  Generally in the case of the Connect Platform, only feature and hotfix branches will be permitted and a PR will be required to make changes to the develop and master branches.
 
* **pull** - A pull is push in reverse.  If changes have been made by another developer and pushed or merged via PR, a develop will pull those changes locally to their branches.  Pulls are branch specific, so only the branch that is currently checked out will pull.

* **fetch** - A fetch checks the origin/remote for any changes made, but does not pull them locally.  This allows a developer to check the diff of their branch to the remote without overwriting their work.

* **merge** - A merge is the action of merging changes between branches.  If the code cannot be merged automatically, git will warn of conflicted code.  To resolve merge conflicts, use a diff tool like BeyondCompare or Visual Studio to choose or ignore certain changes.

* **rebase** - Like a merge, a rebase is a way of integrating changes to a branch, however, a rebase will apply commits of both branches in a linear fashion as if they happened in succession rather than in parallel.  Rebasing gives the commit history a cleaner look but is not always recommended.

* **cherrypick** - Cherrypicking allows a developer to apply changes of a particular commit in a branch rather than the latest commit.  This is used generally if you are developing multiple proof of concepts with similar but different sets of code. 

These are just a few of the many terms used in git.  More can be found at <https://git-scm.com> or <https://github.com>

# Git Commands and Aliases 

There are many ways to use/access git.  There are multiple apps that allow you to do all of your SCM via a GUI and multiple console-based apps that give you the same options.  Here are a few prominent apps:

[SourceTree] ('https://www.sourcetreeapp.com/' "SourceTree") - Atlassian's git GUI, with great integration for other Atlassian apps, but still usable for other environments (Requires git be installed locally)

[GitKraken]('https://www.gitkraken.com/' "GitKraken") - Another git GUI, visually clean and provides functionality of most command like utilities (Does not require git installed locally)

[TortoiseGit]('http://tortoisegit.org'"TortoiseGit") - Another git GUI, much like its SVN counterpart. (Requires git installed locally)

[Git for Visual Studio]('http://visualstudio.com'"Visual-Studio") - Visual Studio provides a plugin that integrates directly into the IDE, however, terminology varies and functionality is limited.

[Git for Windows]('https://git-scm.com/download/win' "Git-for-Windows") - The most basic GUI for git on Windows.  This installation is required for most other GUI apps, minus GitKraken.

[git bash/cmd]('https://git-scm.com/download/win' "Git-Bash") - The most functional and most supported way to use git.  Given the option of bash or cmd, the developer has all of the functionality of the version control system.  This is included in the Git for Windows installation.

[PoSH-git]('https://github.com/dahlbyk/posh-git' "PoSH-git") - A Powershell plugin that allows git commands in the console.

Whichever tool suits the need, each will use quite a few common commands:

**COMMAND**

* git init - (Initialize a folder as a repository)

**SYNTAX** 
>`git init [-q | --quiet] [--bare] [--template=<template_directory>]
	  [--separate-git-dir <git dir>]
>	  [--shared[=<permissions>]] [directory]`

**USAGE**
>See the git [documentation]('https://git-scm.com/docs/git-init#git-init--q').

--
**COMMAND**

* git commit - (Save the state of your repository and give notation)

**SYNTAX**
>`git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
	   [--dry-run] [(-c | -C | --fixup | --squash) <commit>]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
	   [--date=<date>] [--cleanup=<mode>] [--[no-]status]
	   [-i | -o] [-S[<keyid>]] [--] [<file>…​]`
	   
**USAGE**
> See the git [documentation]('https://git-scm.com/docs/git-commit').

--
**COMMAND**
	   
* git push - (Push your changes and commits to the origin/remote repository)

**SYNTAX**
>`git push [--all | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
	   [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-v | --verbose]
	   [-u | --set-upstream] [--push-option=<string>]
	   [--[no-]signed|--sign=(true|false|if-asked)]
	   [--force-with-lease[=<refname>[:<expect>]]]
	   [--no-verify] [<repository> [<refspec>…​]]`

**USAGE**

>See the git [documentation]('https://git-scm.com/docs/git-push').

--
**COMMAND**

* git pull - (Get the latest changes from the origin/remote repository)

**SYNTAX**

>`git pull [options] [<repository> [<refspec>…​]]`

**USAGE**
> See the git [documentation]('https://git-scm.com/docs/git-pull').

--
**COMMAND**

* git merge - (Merge your branch changes into another branch)

**SYNTAX**

>`git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit]
	[-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
	[--[no-]allow-unrelated-histories]
	[--[no-]rerere-autoupdate] [-m <msg>] [<commit>…​]
git merge <msg> HEAD <commit>…​
git merge --abort
`

**USAGE**
> See the git [documentation]('https://git-scm.com/docs/git-merge').

--
**COMMAND**

* git status - (Get a list of changes you've made since your last commit)

**SYNTAX**

>`git status [<options>…​] [--] [<pathspec>…​]`

**USAGE**

> See the git [documentation]('https://git-scm.com/docs/git-status').

--
**COMMAND**

* git diff - (Show a list of differences between your current branch and another)

**SYNTAX**

>`git diff [options] [<commit>] [--] [<path>…​]
git diff [options] --cached [<commit>] [--] [<path>…​]
git diff [options] <commit> <commit> [--] [<path>…​]
git diff [options] <blob> <blob>
git diff [options] [--no-index] [--] <path> <path>`

**USAGE**

> See the git [documentation]('https://git-scm.com/docs/git-diff').

--
**COMMAND**

* git stash - (Save all uncommited changes to a store with the ability to reapply them later, resetting your branch to the last commit.)

**SYNTAX**
>`git stash list [<options>]
git stash show [<stash>]
git stash drop [-q|--quiet] [<stash>]
git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]
git stash branch <branchname> [<stash>]
git stash [save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
	     [-u|--include-untracked] [-a|--all] [<message>]]
git stash clear
git stash create [<message>]
git stash store [-m|--message <message>] [-q|--quiet] <commit>`

**USAGE**
> See the git [documentation]('https://git-scm.com/docs/git-stash').

--
**COMMAND**

* git checkout - (Change branches)

**SYNTAX**

>`git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] [--] <paths>…​
git checkout [-p|--patch] [<tree-ish>] [--] [<paths>…​]`

**USAGE**

> See the git [documentation]('https://git-scm.com/docs/git-checkout').

--

# Naming Convention
All git repositories, as well as their branches, should follow a strict naming convention.

All repositories should be named as follows:

>**psg-[TeamName]-[Function]-[Project]**

For example, an API called *Clinic* written by the Connect Platform team would be named:

>**psg-cp-api-clinic**

**This is subject to change**

# Branching Strategy

Following the gitflow branching strategy makes branching simple, readable and business consumable.



# Creating a Pull Request

Although while using Visual Studio Team Services does not allow creating PR from the command line or any other git tool, they do provide a solid solution for creating one.

# Keep a Clean Repo!

When your PR is complete, you will be given the option to DELETE the source branch of the PR and to SQUASH the commits.  Do not worry, your branch is safe, and your commit history is too.

By deleting the source branch on the origin, you keep the repository clean from clutter and prevent potentially confusing another developer.  However, deleting the branch on the remote leaves your local branch intact.  This allows you to make changes or revert back to a state that you know is functional.

By squashing your commits, this allows a clean visual of the state and changes for each feature you've merged.  Depending on the habits of the developer, the amount of commits can range from just 1 to 20 commits in the life of the feature development.  Without squashing the commits, it is hard to determine what commits were applied when merging your PR.  By squashing, all commits are appended to one, maintaining your notation, but keeping the commit history clean and readable.

## Resources

 

