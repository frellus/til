# Squashing Commits

1. Make sure your commit is up to date from Master

2. Run `git rebase -i master`

3. Make sure the first commit says "pick" and change the rest from "pick" to
   "squash". -- This will squash each commit into the previous commit, which
   will continue until every commit is squashed into the first commit.

4. Save and close editor

5. You have chance now to change the commit message or not, save and close
   editor

6. Force push the final, squashed commit: `git push --force-with-lease origin`