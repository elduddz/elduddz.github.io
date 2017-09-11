# Export-Csv

```powershell
$file = "C:\temp\test.csv"

Get-Service u* | Export-Csv $file
```

you can use `-NoTypeInformation` to bypass type including.

`-Append` can be used to append to an existing file


## Import-Csv

may need to add filtering to ignore blank lines

file may have the flowing for example

Header,Header2

1,1

2,2

\<blank line\>

```powershell
Import-Csv $file
```

This would include blank lines so...

```powershell
Import-Csv $file | where {$_.Header}
```

## ConvertFrom-Csv

## ConvertTo-Csv
