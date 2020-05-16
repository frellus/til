# Revert A File From Previous Commit

From Git 2.23+ (August 2019) you can revert a file with the `git restore` command:

```bash
git restore -s <SHA1>     -- afile
git restore -s somebranch -- afile
```

That would restore on the working tree only the file as present in the "source"
(-s) commit SHA1 or branch 'somebranch'.
