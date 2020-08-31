# Learning How Git Versioning Works

Use `git tag` to check existing tags.

Lightweight tags (`git tag TAGNAME`) just label a specific commit. They are 
>"basically the commit checksum stored in a file — no other information is kept."

Annotated tags sound like they're the most useful for versioning with github.
```
git tag -a v1.4 -m "version 1.4"
```
This adds the tag to the most recent commit (of the branch you're working on). If you want to declare something a few commits ago to be a version, use:
```bash
$ git log --oneline
f6face4 (HEAD -> main, tag: v0.0.1, origin/main) Commit license.
$ git tag -a v1.4 f6face4
```

