# Prune by default on Fetch

a nice simple one and a couple of options.

basically when you type git fetch do you want it to prune any records you might have? yes, of course you do.

to set this against you global git config 

perform the following on commandline:

```
git config --global --add fetch.prune true
```

or  modify the file direct:

```
[fetch]
	prune = true
```

Both will perform the same thing, infact the commandline will generate the content I said to copy into your config.