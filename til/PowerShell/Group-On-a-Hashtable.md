# Running a group on a hashtable

Take your hashtable and convert it to a psobject

```powershell
$psobjects = @()

$hash = @{"key"="value"}
$psobjects += New-Object -TypeName PSObject -Prop $hash

$hash = @{"key"="value2"}
$psobjects += New-Object -TypeName PSObject -Prop $hash

$hash = @{"key"="value"}
$psobjects += New-Object -TypeName PSObject -Prop $hash

$psobjects | Group "key"
```

Oddy there is the ability to generate the output as a hashtable. so it does feel a bit odd that you cannot use one.
