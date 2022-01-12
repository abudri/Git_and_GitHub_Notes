# Git and GitHub Notes

[**Tags and Releases**](https://github.com/abudri/Git_and_GitHub_Notes#tags-and-releases)
- [Tags vs Releases](https://github.com/abudri/Git_and_GitHub_Notes#tags-vs-releases)
- [Commands](https://github.com/abudri/Git_and_GitHub_Notes#commands)
- [Tag and Release Walk-Through, with a Pull Request](https://github.com/abudri/Git_and_GitHub_Notes#tag-and-release-walk-through-with-a-pull-request)
- [Create a Feature Branch in a Repo Based on a Prior Version/Realease: Checking out a Tag/Version Locally and Pushing a feature Branch to the Remote Repo from There](https://github.com/abudri/Git_and_GitHub_Notes#create-a-feature-branch-in-a-repo-based-on-a-prior-versionrealease-checking-out-a-tagversion-locally-and-pushing-a-feature-branch-to-the-remote-repo-from-there)

[**Repo Setup**](https://github.com/abudri/Git_and_GitHub_Notes#repo-setup)
- [Connecting Local Repo with Commits to a New Remote Repo that has a File/s Already]

[**Pull Requests**](https://github.com/abudri/Git_and_GitHub_Notes#pull-requests)
- [How to Do a Pull Request](https://github.com/abudri/Git_and_GitHub_Notes#how-to-do-a-pull-request)
- [How to Make and Push Changes to _Someone Else's_ Pull Request](https://github.com/abudri/Git_and_GitHub_Notes#how-to-make-and-push-changes-to-someone-elses-pull-request)
- [Resolving Merge Conflicts](https://github.com/abudri/Git_and_GitHub_Notes#resolving-merge-conflicts)

[**Other Issues**](https://github.com/abudri/Git_and_GitHub_Notes#other-issues)
- [How to make a folder a non Git directory?](https://github.com/abudri/Git_and_GitHub_Notes#how-to-make-a-folder-a-non-git-directory)
- [How to Remove Sensitive Commits From a Repository](https://github.com/abudri/Git_and_GitHub_Notes#how-to-remove-sensitive-commits-from-a-repository)
- [Pulling Down a Remote Branch from Github and all it's feature branches](https://github.com/abudri/Git_and_GitHub_Notes#pulling-down-a-remote-branch-from-github-and-all-its-feature-branches)

___

## Tags and Releases

### Tags vs Releases

A `tag` is a pointer to a specific commit. This pointer can be super charged with some additional information (identity of the creator of the tag, a description, a GPG signature, ...).

A `tag` is a git concept whereas a `Release` is GitHub higher level concept.

As stated in the **[official announcement](https://github.blog/2013-07-02-release-your-software/)** post from the GitHub blog: *"Releases are first-class objects with changelogs and binary assets that present a full project history beyond Git artifacts."*

A `Release` is created from an existing `tag` and exposes release notes and links to download the software or source code from GitHub.

[Reference](https://stackoverflow.com/questions/18506508/whats-the-difference-between-tag-and-release) 

### [Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

Like most VCSs, Git has the ability to tag specific points in a repository’s history as being important. Typically, people use this functionality to mark release points (v1.0, v2.0 and so on). In this section, you’ll learn how to list existing tags, how to create and delete tags, and what the different types of tags are.

A tag is a pointer to a specific commit. This pointer can be super charged with some additional information (identity of the creator of the tag, a description, a GPG signature, ...).

### Commands

**Listing Your Tags**
Listing the existing tags in Git is straightforward. Just type git tag (with optional -l or --list):

```bash
$ git tag
v1.0
v2.0
```

This command lists the tags in alphabetical order; the order in which they are displayed has no real importance.

**Annotated Tags**

Creating an annotated tag in Git is simple. The easiest way is to specify `-a` when you run the `tag` command:

```bash
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
v0.1
v1.3
v1.4
```

The `-m` specifies a tagging message, which is stored with the tag. If you don’t specify a message for an annotated tag, Git launches your editor so you can type it in.

You can see the tag data along with the commit that was tagged by using the `git show` command:

```bash
$ git show v1.4
tag v1.4
Tagger: Ben Straub <ben@straub.cc>
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number
```

That shows the tagger information, the date the commit was tagged, and the annotation message before showing the commit information.

### Tag and Release Walk-Through, with a Pull Request

You will want to make your PR first.  Once you have finished any changes/commits in the PR, and you are ready to merge, then locally you can create the tags (or even in the GitHub UI) and _then_ you can **merge** the branch into `main`.  Also, if your change is so significant that it is breaking, then bump the version to the next version, meaning from say `1.2` to `2.0`. Also, as of now, when you push your tags from local to the remote repo, **the release is automatically created from the tag**, so no work needed from you there.

Also, please note that a pull request does not _include_ tags. You work with them separately. [Reference](https://stackoverflow.com/questions/12278660/adding-tags-to-a-pull-request)

1. Recall from the above, at this point your PR is ready to be merged with `main`, but don't merge the PR yet.  At this point, locally, tag your latest commit, such as `git tag -a v1.0 -m "first version"`:
```bash
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
v0.1
v1.3
v1.4
```
This will tag your latest commit - ie, what you just committed and pushed as a PR to the remote repo.  Meaning, once you push your new tag to the remote repo - step 3 below - that tag will be associated with your current PR.

2. You can then push your tags to the remote repo, and this will push anything that is tagged locally
```bash
git push origin --tags
```

3. When you visit the repository you should now see your tag and a release automatically generated from that tag.  Simple as that.  Now you can merge your PR if approved.

### Creating a Tag and Release Through the UI

Hit Create New Release Below:

<img src="https://user-images.githubusercontent.com/17362519/115073339-2f58e400-9ec6-11eb-9dd6-bca395522211.png" width="350;" />

You can from here create a New Release:

<img src="https://user-images.githubusercontent.com/17362519/115073372-3d0e6980-9ec6-11eb-8880-c3ecc6aac608.png" width="650;" />

From there you can create your release with tag:

<img src="https://user-images.githubusercontent.com/17362519/115073418-4ef00c80-9ec6-11eb-8624-198db63a2419.png" width="650;" />

And there you have it:

<img src="https://user-images.githubusercontent.com/17362519/115073448-59aaa180-9ec6-11eb-9353-4cc37eb0aede.png" width="650;" />

And on your repo's home page:

<img src="https://user-images.githubusercontent.com/17362519/115073481-63340980-9ec6-11eb-959f-6fb28b759d25.png" width="350;" />

### Create a Feature Branch in a Repo Based on a Prior Version/Realease: Checking out a Tag/Version Locally and Pushing a feature Branch to the Remote Repo from There

Doesn't appear to be a way to do this in the UI at this time. The easy way is to checkout to the older version locally, and then checkout to a new feature branch, make your changes in that older version code, and then push the feature branch out to the code repo.  So,

```bash
git checkout v1.1   # whatever the tag/commit is
git checkout -b my-test-feature-branch
```
From there, make changes, commit them, and then push your `my-test-feature-branch` out to the remote repo as is normally done and it should appear in GitHub.

### Resources

https://semver.org/

https://git-scm.com/book/en/v2/Git-Basics-Tagging

[Git and GitHub Beginner Tutorial 7 - Git Tags - what, why, when and how - Raghav Pal](https://www.youtube.com/watch?v=govmXpDGLpo&t=464s)

## Repo Setup

### Connecting Local Repo with Commits to a New Remote Repo that has a File/s Already

I had a repo locally that I had already setup, with files committed and all.  I created a remote repo to connect the remote to, but also happened to create a README.md upon creating the remote repo. They thus had two unrelated histories and threw errors originally.

In any case, in the lines below, I added the GitHub remote repo as a `origin` (remote) to my local repo below, and also checked with a `git remote -v`, and then also changed my local brain name to `main` instead of `master`, which would match my newly created remote repo as well:

```bash
z@Mac-Users-Apple-Computer abdullahs-microservice % git remote add origin https://github.com/abudri/abdullahs-microservice
z@Mac-Users-Apple-Computer abdullahs-microservice % git remote -v
origin	https://github.com/abudri/abdullahs-microservice (fetch)
origin	https://github.com/abudri/abdullahs-microservice (push)
z@Mac-Users-Apple-Computer abdullahs-microservice % git branch        
* master
z@Mac-Users-Apple-Computer abdullahs-microservice % git branch -m master main
z@Mac-Users-Apple-Computer abdullahs-microservice % git branch
* main
```

To push your changes to the remote repo, you first need to connect by creating a personal access token, and then when trying to push locally to the remote, you will be asked for your username and password.  Your personal access token will serve as your password. See more on creating a personal access token and using it, [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). 

Then I had to set the local `main` branch to track the `origin`'s (the remote repo on GitHub's) `main` branch

```bash
git branch --set-upstream-to=origin/main main
```

But a `git pull` alone will not work:

```bash
z@Mac-Users-Apple-Computer abdullahs-microservice % git pull
fatal: refusing to merge unrelated histories
```

The fatal error message was received above. What is needed is the `--allow-unrelated-histories` flag on that, which essentially keeps your local `main`'s files and commits, and also will add the remote's `main` `README.md` file to your local `main` branch:

```bash
z@Mac-Users-Apple-Computer abdullahs-microservice % git pull --allow-unrelated-histories
Merge made by the 'recursive' strategy.
 README.md | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 README.md
z@Mac-Users-Apple-Computer abdullahs-microservice % git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

Finally, with all the local changes on my local `main` still not up in the remote repo at `main` there, I did a `git push` and all was fixed and fine:

```bash
z@Mac-Users-Apple-Computer abdullahs-microservice % git push 
Counting objects: 8, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (8/8), 842 bytes | 842.00 KiB/s, done.
Total 8 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/abudri/abdullahs-microservice
   35deb89..5b87546  main -> main
```

## Pull Requests

### How to Do a Pull Request

This presumes you have already set up your remote repo to link to your local repo - do `git remote -v` to check. Also this presupposes you are currently checked out onto your feature branch that you want to create a pull request for.  

1. `git add -A` - add all your changes as is normal.
2. `git commit -m "message about your changes"` - do your typically commit locally
3. `git push -u origin new-feature-branch` -  where `new-feature-branch` is your new branch you made locally. Do this command from your local feature branch - meaning, locally you should also be on `new-feature-branch`.
4. Then follow the steps in the article: **[How to create a pull request in GitHub](https://opensource.com/article/19/7/create-pull-request-github)**

Once you push the changes to your repo, the Compare & pull request button will appear in GitHub.

<img src="https://user-images.githubusercontent.com/17362519/115149964-5df4cd00-a034-11eb-83a9-96aa2367f4d6.png" width="550;" />

**Click it** and you'll be taken to this screen:

<img src="https://user-images.githubusercontent.com/17362519/115149988-7cf35f00-a034-11eb-8918-7e791170c8ce.png" width="550;" />

5. Open a pull request by clicking the **Create pull request** button. This allows the repo's maintainers to review your contribution. From here, they can merge it if it is good, or they may ask you to make some changes.

Note: you don't have to create the branch on the remote repo, if you do a push of your local branch to the remote repo, the remote repo on github will refresh with your new feature branch you just pushed from local, like `git push origin new-feature`, and github will automatically refresh with `new-feature` showing up on it's site.

### How to Make and Push Changes to _Someone Else's_ Pull Request

If you are on a team and a team member needs help, chances are you will need to help them along and make changes to a number of files and not just a simple single file change in the PR in the GitHub UI, and the features of your code editor such as VSCode may be more helpful, or perhaps you need to change a file your teammate has not touched yet in their PR.  In that case, the below steps help you fetch the remote branch, make changes to that branch, and push your changes which end up showing in your teammate's PR.

1. `git fetch` - to update your remote-tracking branches under `refs/remotes/<remote>/`. This operation never changes any of your own local branches under `refs/heads`, and is safe to do without changing your working copy.
2. `git checkout origin/branch_name` - check out to the remote branch that the PR is tracked in, ie, your teammate's branch in their PR.
3. Make your necessary code changes and updates.
4. `git add` - add all your changes to staging as is normal.
5. `git commit -m "message about your changes"` - do your typically commit locally
6. `git push` - This will take your local changes to your teammate's PR branch you are currently on, and push them to the remote repo into the PR of your teammate.

References:  [The difference between `git fetch` and `git pull`](https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch)

> In the simplest terms, `git pull` does a `git fetch` followed by a `git merge`.

> You can do a `git fetch` at any time to update your remote-tracking branches under `refs/remotes/<remote>/`. This operation never changes any of your own local branches under `refs/heads`, and is safe to do without changing your working copy. I have even heard of people running `git fetch` periodically in a cron job in the background (although I wouldn't recommend doing this).

> A git pull is what you would do to bring a local branch up-to-date with its remote version, while also updating your other remote-tracking branches.

> From the Git documentation for git pull:

>> In its default mode, `git pull` is shorthand for `git fetch` followed by `git merge FETCH_HEAD`.

### Resolving Merge Conflicts

Say you have a feature branch that needs to get caught up with the `main` branch, if you try to merge master into your feature branch then you may run into merge conflicts that need to be resolved. To be more precise, what is a merge conflict:

> A merge conflict is an event that occurs when Git is unable to automatically resolve differences in code between two commits. When all the changes in the code occur on different lines or in different files, Git will successfully merge commits without your help. However, when there are conflicting changes on the same lines, a “merge conflict” occurs because Git doesn’t know which code to keep and which to discard. [Source](https://blog.axosoft.com/learn-git-merge-conflict/#:~:text=A%20merge%20conflict%20is%20an,merge%20commits%20without%20your%20help.)

Here is a general approach:

```bash
git pull origin your-feature-branch # this is in the case that you have already pushed your feature branch out to Github and changes have been made to the branch there remotely
git checkout main  # checkout to the `main` branch
git pull --rebase origin main  # get updates for `main` before the merge
git checkout your-feature-branch  # get back to your feature branch
git merge main  # merge `main` into your feature branch
```
From here you may or may not have merge conflicts.  If you do, you will need to resolve them from here. An easy way I've been getting accustomed to is using the VSCode interface. Carmelle Codes actually has a great and concise [video](How to resolve merge conflicts in Visual Studio Code | Fast tutorial 2020
) on this. 

Firstly, the green text below represents the local branch changes, and the blue text reflects the incoming changes. Since in this case Carmelle wants to be updated with master, she accepts the incoming changes:

<img src="https://user-images.githubusercontent.com/17362519/115415714-236e6a00-a1c5-11eb-90e8-70b389f2c5b1.png" width="400;" />

But in other cases maybe your code is ahead of `main` and you want to keep your local changes, so keep that in mind. So, Carmelle accepted incoming changes from the remote repo, and notes that merge conflict files have the purple **C** next to it:

<img src="https://user-images.githubusercontent.com/17362519/115416090-721c0400-a1c5-11eb-9b86-e9ee7870d811.png" width="400;" />

At this point she has saved the file and then she hits the **+** symbol to stage the changes:

<img src="https://user-images.githubusercontent.com/17362519/115416214-92e45980-a1c5-11eb-9d0a-e9bd4e392ce3.png" width="400;" />

Then she uses `command + enter` on Mac to commit the changes locally:

<img src="https://user-images.githubusercontent.com/17362519/115416312-a8f21a00-a1c5-11eb-95b6-7bc483a9fb79.png" width="400;" />

After that she can `push` all those changes by going to the bottom of the VSCode interface and clicking that circular icon:

<img src="https://user-images.githubusercontent.com/17362519/115416407-c32bf800-a1c5-11eb-8c34-a18af4db0271.png" width="400;" />

And there you go, you resolved the merge conflicts and pushed that update of your feature branch out to the remote repo. Now, your feature branch is up to date with `main` both locally and remotely

If you wanted to do the above via the CLI, then you can simply do the below after keeping your local changes or accepting incoming changes or whatever changes you want to keep, saving the file/s, and then you can do the below via the CLI for the same effect:

```bash
git add -A
git commit -m "pull updates from origin main"
git status  # things are commited locally now after merging `main` into your feature branch
git push   # push the changes in your feature branch out to the remote
```
You should be good from there. 

## Other Issues

### How to make a folder a non Git directory?

It's super simple:

```
rm -rf .git
```

Removing this folder will make it a non git directory. Maybe accidentally someone previously by doing `git init` initialized a git repository in your folder of your concern..

[Resource](https://stackoverflow.com/questions/47273592/how-to-make-a-folder-a-non-git-directory)

### How to Remove Sensitive Commits From a Repository

One issue that may come up is committing secrets or senstive data locally and/or remotely - such as on GitHub.  There are a number of ways to go about them.  Here are two.

1. GitHub's own documentation on [Removing sensitive data from a repository](https://docs.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository). From that doc, here is one method:

#### **[Purging a file from your repository's history](https://docs.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository#purging-a-file-from-your-repositorys-history)**

#####  **[Using the BFG](https://docs.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository#using-the-bfg)**

The [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) is a tool that's built and maintained by the open source community. It provides a faster, simpler alternative to `git filter-branch` for removing unwanted data. For example, to remove your file with sensitive data and leave your latest commit untouched, run:

```
$ bfg --delete-filesYOUR-FILE-WITH-SENSITIVE-DATA
```

To replace all text listed in `passwords.txt` wherever it can be found in your repository's history, run:

```
$ bfg --replace-text passwords.txt
```

After the sensitive data is removed, you must force push your changes to GitHub.

```
$ git push --force
```

See the [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/)'s documentation for full usage and download instructions.

2. Clear out the **entire** history and all commits from a repository. Chances are this isn't the ideal of what you want to do if option 1 is possible. Steps to clear out the history of a git/github repository

```
    -- Remove the history from 
    rm -rf .git

    -- recreate the repos from the current content only
    git init
    git add .
    git commit -m "Initial commit"

    -- push to the github remote repos ensuring you overwrite history
    git remote add origin git@github.com:<YOUR ACCOUNT>/<YOUR REPOS>.git
    git push -u --force origin master
```
[Source](https://gist.github.com/stephenhardy/5470814)

If you push a commit to a remote repository, the entire history of that commit is also pushed. If you have a commit with secrets in your history, another option is you could also rewrite your history to get rid of it using an interactive rebase before you push it. You could also use git rebase -i and squash all your commits.

## Un-doing Your Last Commit

Sometimes you make a mistake and commit to `main` branch.  Ok, maybe it's just me.  Normally, with the team I make a feature branch locally, commit my changes, make the Pull Request, and then wait for teammates to approve, and then finally merge into `main`.  In any case, it's pretty easy to resolve if you've mistakenly committed your changes to `main` before making a PR.  

If you want to move `main` back one commit - prior to your mistaken commmit on `main` - and in addition keep the changes in that make mistake unstaged, just do the below:

```
$ git reset --soft HEAD~1
```

You'll see you are back to the last/original state of `main`, and your changes are available now, just uncommitted. Pretty easy and there you go!

[Reference](https://www.git-tower.com/learn/git/faq/undo-last-commit/)

### Pulling Down a Remote Branch from Github and *all it's feature branches*

[https://stackoverflow.com/questions/67699/how-to-clone-all-remote-branches-in-git](https://stackoverflow.com/questions/67699/how-to-clone-all-remote-branches-in-git)

First, clone a remote [Git](http://en.wikipedia.org/wiki/Git_%28software%29) repository and [cd](http://en.wikipedia.org/wiki/Cd_%28command%29) into it:

```
$ git clone git://example.com/myproject
$ cd myproject
```

Next, look at the local branches in your repository:

```
$ git branch
* master
```

But there are other branches hiding in your repository! You can see these using the `-a` flag:

```
$ git branch -a
* master
  remotes/origin/HEAD
  remotes/origin/master
  remotes/origin/v1.0-stable
  remotes/origin/experimental
```

If you just want to take a quick peek at an upstream branch, you can check it out directly:

```
$ git checkout origin/experimental
```

But if you want to work on that branch, you'll need to create a local tracking branch which is done automatically by:

```
$ git checkout experimental
```

and you will see

```
Branch experimental set up to track remote branch experimental from origin.
Switched to a new branch 'experimental'
```

Here, "new branch" simply means that the branch is taken from the index and created locally for you. As the *previous* line tells you, the branch is being set up to track the remote branch, which usually means the origin/branch_name branch.

Now, if you look at your local branches, this is what you'll see:

```
$ git branch
* experimental
  master
```

You can actually track more than one remote repository using `git remote`.

```
$ git remote add win32 git://example.com/users/joe/myproject-win32-port
$ git branch -a
* master
  remotes/origin/HEAD
  remotes/origin/master
  remotes/origin/v1.0-stable
  remotes/origin/experimental
  remotes/win32/master
  remotes/win32/new-widgets

```

At this point, things are getting pretty crazy, so run `gitk` to see what's going on:

```
$ gitk --all &
```


