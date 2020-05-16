# Use Different SSH Keys for github.Com

By default when you run `git` your `~.ssh/id_rsa` key is used to communicate
with the git server. What if you want to use a different ssh key, maybe a
personal one instead of a work one for example?

1. Create the new ssh key, or copy your personal one into a directory (ex. maybe
   `~/private/.ssh`)

2. Create or edit your `~/.ssh/config` file and add the following:
```
host github.com
   Hostname github.com
   IdentityFile ~/private/.ssh/id_rsa
   IdentitiesOnly yes
```

3. cd into the repository clone you want to push for and run the following:
```bash
greg:til greg$ git config --list | grep email
user.name=Greg Gallagher
user.email=greg@gexample.com
```

4. This is a global setting. The local setting however can be made which will
   override the global setting. For example:
```bash
git config --local user.email greg.b.gallagher@gmail.com
```

Now the setting is overriden in both the `~/.ssh/config so the private key will
be used for github, and the metadata for the git operations will use your
personal e-mail (from git config --local) and not the global one i.e. maybe your
work e-mail) 
