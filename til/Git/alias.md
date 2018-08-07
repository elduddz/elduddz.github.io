# git aliases

This is quite straight forward.

aliases exist in the config, so you can create local or global aliases.

```powershell
git config --global alias.subpush 'push --recurse-submodules=on-demand'
```

so a nice one would be

```powershell
git config --global alias.masterfresh 'reset --hard origin/master'
```

Or

```powershell
git config alias.refresh 'reset --hard'
```

so you can then provide the path.

`git refresh origin/master`

this is saved in the .gitconfig, so if you locate the file in your profile, then it can be easily modified.

You can also string several arguments together under 1 alias, so the following will fetch with a prune argument then reset the current branch to a reflective point against the origin. `git rev-parse --abbrev-ref HEAD` gets the name of the current branch. the clean with -dfx and -dfX do different things, but it is often a good idea to do both.
```
[alias]
refresh = !git fetch --prune && git reset --hard origin/$(git rev-parse --abbrev-ref HEAD) && git clean -dfx -e '.vs/'
```

some of my favourites:
>refresh = !git fetch --prune && git reset --hard origin/$(git rev-parse --abbrev-ref HEAD) && git clean -dfx -e '.vs/'  
flat = !git log --first-parent $(git rev-parse --abbrev-ref HEAD) --graph  
st = status  
aa = add .  
ci = commit  
cim = commit -m  
co = checkout  
br = branch  
unstage = reset HEAD --
last = log -1 HEAD  
pushit = !git push origin $(git rev-parse --abbrev-ref HEAD)  
pom = !git push origin head:master  
poh = "!f() { git push origin head:$1;}; f"  
doh = "!f() { git push origin :$1;}; f"  
uplink = !git branch --set-upstream-to origin/$(git rev-parse --abbrev-ref HEAD)  
unlink = branch --unset-upstream
pfd = push origin HEAD:refs/for/develop  
pfm = push origin HEAD:refs/for/master  
pfb = !git push origin HEAD:refs/for/$(git rev-parse --abbrev-ref HEAD)  