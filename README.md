Squash-merging can be annoying. In particular, I like to use

```sh
git branch --merged
```

to check which local branches have been merged into the main branch, but
with squash-merging, that doesn't work correctly.

This Bash script solves my need and checks if a given branch has been
squash-merged into the main branch of the repository.  Run it like so:

```sh
git-was-branch-squash-merged <branch_name>
```

To determine if the branch was squash-merged, this checks out the branch
as a detached head, creates a squashed merge commit with the merge-base,
and then checks if that commit exists in the main branch.  That's a bit
of a mess and will end up creating a new commit if the squashed branch
doesn't exist.

This tries hard to be safe, in terms of preventing anything from running
if there are any uncommitted local changes or if it can't figure out
anything about the current Git repo, but I can't promise that it's perfect
in that regard.  It also has a bit of a hacky check for what the name of
the actual main branch is, but it meets my needs.
