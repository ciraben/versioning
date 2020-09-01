# Learning How Git Versioning Works

Use `git tag` to check existing tags on a project.

Lightweight tags (`git tag TAGNAME`) just label a specific commit. They are 
>"basically the commit checksum stored in a file — no other information is kept."

Annotated tags sound like they're the most useful for versioning with github.
```bash
$ git tag -a v1.4 -m "version 1.4"
```
This adds the tag to the most recent commit (of the branch you're working on). If you want to declare something a few commits ago to be a version, use:
```bash
$ git log --oneline
f6face4 (HEAD -> main, tag: v0.0.1, origin/main) Commit license.
$ git tag -a v1.4 f6face4
```

## Releasing a Version to Github

To push a new release, normally we'll push our commits to main as well, to advertise our new release on our project's main page:
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
(This will update any and all tags you've fiddled with though, including lightweight tags. To update annotated tags only, use `git push origin --follow-tags`.)

Finally, to display your version as a release:
* Go to the repository's main page on Github.
* In the righthand panel under Releases, a text link "+ X release(s)" is displayed - click it!
* From the Releases page, on the righthand side, click "Draft new release".
* Begin typing your version's tag in the "Tag version" field, and select it from the dropdown menu. (Handily, if all your versions start with v, you can type `v` and see them all!)
* Optionally enter a title & description for this version.
* Scroll down & click "Publish release", and voilà!

Your new version will be displayed on your repository's main page in the righthand panel under Releases, and at the bottom of the main page, after the README. Github auto-generates .zip/.tar.gz distributions of each release version, downloadable from the releases page.
