## Linking to patchset
```
gitdir=$(git rev-parse --git-dir); scp -p -P 29418 duddridgel@gerrit-infra.mint.ukho.gov.uk:hooks/commit-msg ${gitdir}/hooks/

git commit --amend

# then just
:wq

git push origin head:refs/for/[name]
```