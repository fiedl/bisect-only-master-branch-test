# bisect-only-master-branch-test

This is an experiment for https://github.com/fiedl/icecube-git-migration/issues/11

![image](https://user-images.githubusercontent.com/1679688/76907340-43d34300-68a6-11ea-9ef1-b65561863e36.png)

### List all commits of the master branch

```
[2020-03-18 00:36:28] fiedl@fiedl-mbp ~/icecube/bisect-only-master-branch-test master
▶ git log --first-parent --oneline
2bdb043 commit H
cb392e6 commit G
3f609d1 commit F
1dd0aaf commit E
2c7c215 commit D
076b337 commit C
ba453a6 commit B
90025a8 commit A
```

### List all commits of the feature branches

```
[2020-03-18 00:02:35] fiedl@fiedl-mbp ~/icecube/bisect-only-master-branch-test master
▶ for rev in $(git rev-list 90025a82512894c8d0638436380b14e41a1fa3bb..master --merges --first-parent); do git rev-list $rev^2 --not $rev^ --format=%b --oneline; done
1e19d15 commit L
707fb86 commit K
27a5aa9 commit J
390e46a commit I
c8e2568 commit P
d1e2fe0 commit O
c18703d commit N
ccdba6f commit M
```

which can be passed to `git bisect skip`.

## Caveats

- We might need to prevent fast-forward commits (https://github.com/fiedl/bisect-only-master-branch-test/issues/2#issuecomment-600353757)

## Resources

- [How to create this graph](https://github.com/fiedl/bisect-only-master-branch-test/issues/1)
- [How to get only the commits of the master branch for bisection](https://github.com/fiedl/bisect-only-master-branch-test/issues/2)
- [Look at the git graph in the github ui](https://github.com/fiedl/bisect-only-master-branch-test/network)
- https://blog.quantic.mba/2015/02/03/git-bisect-debugging-with-feature-branches/
- https://redfin.engineering/visualize-merge-history-with-git-log-graph-first-parent-and-no-merges-c6a9b5ff109c
- https://git-scm.com/docs/git-rev-list
