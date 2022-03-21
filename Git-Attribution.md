Everyone likes to be credited for their work. Nobody likes to have someone else claim the credit for their work (knowingly or not). For this reason, we think you should be actively trying to attribute commits to other people where relevant.

Projects come and go, patch notes will be lost over time, but the git history is forever!

You can attribute in multiple ways:

## Full Author

If you are fully taking someone else's work, and modifying it to fit your needs, you should do this as two commits:

1: Take the work as-is

2: Modify it to your needs

For commit number 1, you should commit it with: `git commit -m "Commit message" --author "Author Name <authoremail@gmail.com>"`

In this case, you will be the committer, and they will be the author.

## Co-Author

If you have been working closely with someone, and need to credit them (or you're referencing their work), you can add their information as a co-author in your commit message:

```
Commit title

Commit body

Co-authored-by: name <additional-dev-1@example.com>
Co-authored-by: name <additional-dev-2@example.com>
```

### Reference

https://stackoverflow.com/questions/7442112/how-to-attribute-a-single-commit-to-multiple-developers