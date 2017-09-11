# submodules

Can share.

to link is simple:

```powershell
git submodule add _insert location here_

#Then commit to git
git commit -, "Added Submodule"
git push
```

this creates a .gitmodules file to help references. you can edit submodules from the parent project.

```powershell
git submodule init

git submodule update
```

git submodule update checks out submodules in a headless state

when you make changes to submodules you must remember to make 2 separate commits, 1 is to the submodule the second is to the parent project with the reference.

push submodule then parent

git push --recurse-submodules=check

git push --recurse-submodules=on-demand