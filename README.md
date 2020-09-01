# Learning How Git Versioning Works

In Git, we use tags to flag notable commits in a project. Use `git tag` to check existing tags on a project. There are two different kinds of tags.

**Lightweight tags** (`git tag TAGNAME`) just label a specific commit. From the [Git website](https://git-scm.com/book/en/v2/Git-Basics-Tagging),
>"[They are] basically the commit checksum stored in a file — no other information is kept."

**Annotated tags** store a bit more info. It sounds like they're the most useful for versioning with github. To declare a new version using a tag: 
```bash
$ git tag -a v1.4 -m "version 1.4"
```
This adds the tag to the most recent commit (of the branch you're working on locally). If you want to declare something a few commits ago to be a version, use:
```bash
$ git log --oneline
f6face4 (HEAD -> main, tag: v0.0.1, origin/main) Commit license.
$ git tag -a v1.4 f6face4
```

## Releasing a Version to Github

To push a new release, normally we'll push our commits to `main` as well, to advertise our new release on our project's main page:
```bash
$ git push
```
Either way, we push our commits to the new version's tag:
```bash
$ git push origin v1.4
```
or, if you like typing the same thing every time,
```bash
$ git push origin --tags
```
This will update any and all tags you've fiddled with though, including lightweight tags. To update annotated tags only, use `git push origin --follow-tags`.

Finally, to display your version as a release:
* Go to the repository's main page on Github.
* In the righthand panel under Releases, a text link "+ X release(s)" is displayed - click it!
* From the Releases page, on the righthand side, click "Draft new release".
* Begin typing your version's tag in the "Tag version" field, and select it from the dropdown menu. (Handily, if all your versions start with v, you can type `v` and see them all!)
* Optionally enter a title & description for this version.
* Scroll down & click "Publish release", and voilà!

Your new version will be displayed on your repository's main page in the righthand panel under Releases, and at the bottom of the main page, after the README. Github auto-generates `.zip`/`.tar.gz` distributions of each release version, downloadable from the releases page.

## More git tips

I sometimes lose track of Git tips I've learned in between projects. Here are some of my faves.

### The `master` branch

Tired of seeing `master` all over your projects? As [Scott Hanselman](https://www.hanselman.com/blog/EasilyRenameYourGitDefaultBranchFromMasterToMain.aspx) suggests, here's a one-time fix to change the term to `main` (or `latest`, or whatever): 
```bash
$ git config --global init.defaultBranch main
```
Check his article for details on amending projects in progress.

### Making a new repository

Here's the standard:
```bash
$ git init
$ touch .gitignore
$ git add .
$ git commit
```
Since I edit in vim, I'll also add `*.swp` to my .gitignore right off the bat. Then, make a new repository on github.com, grab the generated address and:
```bash
$ git add origin ADDRESS
$ git push -u origin main
```
If you're ready to start versioning, now's the time:
```bash
$ git tag -a v0.1.0
$ git push origin --tags
```
Then follow the earlier instructions for setting v0.1.0 as a Github release.

### Getting Around in Git

These commands help me observe my git "surroundings":

* `git tag` lists all the tag names on your project.
```bash
$ git tag
v0.0.1
v0.1.0
v0.1.1
```
* `git log --oneline` lists your commits with tags & origin labeled.
```bash
$ git log --oneline
237406c (HEAD -> main, origin/main) Rearrange README contents.
002cae5 Add info on releasing versions to Github.
36e18ad (tag: v0.1.1) Change faulty code block in README.
758c7ef (tag: v0.1.0) Update changelog.
2832746 Commit changelog.
fc718b4 Commit .gitignore.
1623d3c Commit a readme.
f6face4 (tag: v0.0.1) Commit license.
```
* `git describe` shows where you are with respect to most recent tag, in the form `V-N-H`, where `V` is the most recent version/tag name, `N` is the number of commits since then, and `H` is the last commit's hash ID. Like this:
```bash
$ git describe
v0.1.1-2-g237406c
```
* `git status` shows which files have been changed since last commit.
```bash
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md
```
* `git diff HEAD` shows line-by-line details of those changes.
```bash
$ git diff HEAD
diff --git a/README.md b/README.md
index 190ea13..a75d153 100644
--- a/README.md
+++ b/README.md
@@ -1,15 +1,15 @@
 # Learning How Git Versioning Works

-Use `git tag` to check existing tags on a project.
+In Git, we use tags to flag notable commits in a project. Use `git tag` to check existing tags on a project. There are two different kinds of tags.

-Lightweight tags (`git tag TAGNAME`) just label a specific commit. They are
->"basically the commit checksum stored in a file — no other information is kept."
+Lightweight tags (`git tag TAGNAME`) just label a specific commit. From the [Git website](https://git-scm.com/book/en/v2/Git-Basics-Tagging),
+>"[They are] basically the commit checksum stored in a file — no other information is kept."

-Annotated tags sound like they're the most useful for versioning with github.
+Annotated tags store a bit more info. It sounds like they're the most useful for versioning with github. To declare a new version using a tag, do:
```

### Odds and ends

Edit most recent commit message before pushing:
```bash
$ git commit --amend
```
(This adds current changes to the commit, however.)

Move a tag to most recent commit:
```bash
$ git push origin :refs/tags/TAGNAME
$ git tag --force -a TAGNAME
$ git push origin main --tags
```

# Thanks for reading!

## References

* [Git Basics - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
* [marco.marinangeli on Stack Overflow](https://stackoverflow.com/questions/37814286/how-to-manage-the-version-number-in-git#46434732)
* [The Stack Overflow community wiki](https://stackoverflow.com/questions/179123/how-to-modify-existing-unpushed-commit-messages)
* [Greg Hewgill on Stack Overflow](https://stackoverflow.com/questions/8044583/how-can-i-move-a-tag-on-a-git-branch-to-a-different-commit)
* [Scott Hanselman](https://www.hanselman.com/blog/EasilyRenameYourGitDefaultBranchFromMasterToMain.aspx)

## Contact

If you think this was helpful, or you want to suggest a change, give me a shout at tom.on.github@gmail.com — I'd love to hear it!

## License

**Learning How Git Versioning Works** is licensed under [The Hippocratic License 2.1](https://firstdonoharm.dev/).

