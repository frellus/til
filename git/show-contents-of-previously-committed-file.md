# Show Contents Of Previous Committed File 

Examples:
```bash
# show contents of file by previous commit sha
git show 1a4af8fb5af28f77e1e8ccf4b3f09978d72d72a4:file.txt

# show by branch name
git show somebranch:file.txt

# show by HEAD + x number of ^ characters
git show HEAD^^^:test/test.py

# show current diff of file to previous commit (same as git diff)
git show file.txt
```

The command takes the usual style of revision, meaning you can use any of the following:
- full commit sha
- first 5 characters of commit sha
- branch name
- HEAD - 3 

> *NOTE:* Always specify a path to the file from the root of the repository,
> _not_ your current directory position.