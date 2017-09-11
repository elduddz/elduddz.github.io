# Things I should know but keep forgetting about

## Get-Member

basically doing `Get-Service | Get-Member #gm is alias` returns a list of all the properties on the function

## Aliases

Thinks have Aliases, you dont need to call `Where-Object` when `where` covers it. sames with `sort` using `Get-Alias -Definition Where-Object` (for example) will expose if there is an alias.

```powershell
# was getting confused why it was saying out was not a string! this make sense.
Tee -OutVariable "thing"
```