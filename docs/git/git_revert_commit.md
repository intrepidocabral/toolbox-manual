# Case 1: Delete the last commit
Deleting the last commit is the easiest case. Let's say we have a remote mathnet with branch master that currently points to commit dd61ab32. We want to remove the top commit. Translated to git terminology, we want to force the master branch of the mathnet remote repository to the parent of dd61ab32:

``` 
$ git push mathnet +dd61ab32^:master
```

Where git interprets x^ as the parent of x and + as a forced non-fastforward push. If you have the master branch checked out locally, you can also do it in two simpler steps: First reset the branch to the parent of the current commit, then force-push it to the remote.

```
$ git reset HEAD^ --hard
$ git push mathnet -f
```

# Case 2: Delete the second last commit
Let's say the bad commit dd61ab32 is not the top commit, but a slightly older one, e.g. the second last one. We want to remove it, but keep all commits that followed it. In other words, we want to rewrite the history and force the result back to mathnet/master. The easiest way to rewrite history is to do an interactive rebase down to the parent of the offending commit:

```
$ git rebase -i dd61ab32^
```

This will open an editor and show a list of all commits since the commit we want to get rid of:

```
pick dd61ab32
pick dsadhj278
```

Simply remove the line with the offending commit, likely that will be the first line (vi: delete current line = dd). Save and close the editor (vi: press :wq and return). Resolve any conflicts if there are any, and your local branch should be fixed. Force it to the remote and you're done:

```
$ git push mathnet -f
```

# Case 3: Fix a typo in one of the commits

This works almost exactly the same way as case 2, but instead of removing the line with the bad commit, simply replace its pick with edit and save/exit. Rebase will then stop at that commit, put the changes into the index and then let you change it as you like. Commit the change and continue the rebase (git will tell you how to keep the commit message and author if you want). Then push the changes as described above. The same way you can even split commits into smaller ones, or merge commits together.

