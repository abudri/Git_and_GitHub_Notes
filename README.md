# Git and GitHub Notes


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

#### Commands

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

1. Recall from the above, at this point your PR is ready to be merged with `main`.  At this point, locally, tag your latest commit, such as `git tag -a v1.0 -m "first version"`:
```bash
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
v0.1
v1.3
v1.4
```
2. You can then push your tags to the remote repo, and this will push anything that is tagged locally
```bash
git push origin --tags
```
3. When you visit the repository you should now see your tag and a release automatically generated from that tag.  Simple as that.

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

### Resources

https://semver.org/

https://git-scm.com/book/en/v2/Git-Basics-Tagging
