# Things I should know but keep forgetting about

## Get-Member

basically doing `Get-Service | Get-Member #gm is alias` returns a list of all the properties on the function

## Aliases

Thinks have Aliases, you dont need to call `Where-Object` when `where` covers it. sames with `sort` using `Get-Alias -Definition Where-Object` (for example) will expose if there is an alias.

```powershell
# was getting confused why it was saying out was not a string! this make sense.
Tee -OutVariable "thing"
```

## Find edition of of VS2017 (15) installed

$vs = Get-ItemProperty "HKLM:\SOFTWARE\WOW6432Node\Microsoft\VisualStudio\SxS\VS7" #| Select -ExpandProperty Property

$vs.'15.0'