# Export-Clixml

works against Import-Clixml


## CovertTo-Xml

For non PS outputs.

cannot be used with Clixml

```powershell
$xml = $things | CovertTo-Xml

$xml.Save($FullfileName)

```

```powershell
[xml]$xml = Get-Content $xmlFile
```

## Examples

```powershell

# output first 100 eventlogs to PS xml
$file = "C:\temp\test.xml"

Get-EventLog -LogName Application | Select -First 100 | Export-Clixml $file

#view file
psedit $file

# import file and group by source
Import-Clixml $file | Group Source

# export event logs to no ps xml
$file = "C:\temp\test2.xml"

[xml]$xml = Get-EventLog -LogName Application | Select -First 100 | ConvertTo-Xml

$xml.save($file)

psedit $file
```

I wanted to see what would happen with hashtables

```powershell
$stuff = @{
    things = @{
        Name = 1
        Other = 1
    }
    things2 = @{
        Name = 2
        Other = 2
    }
}

$stuff

$file = "C:\temp\test4.xml"

$stuff | Export-Clixml $file

psedit $file

$file = "C:\temp\test3.xml"

[xml]$xml = $stuff | ConvertTo-Xml

$xml.Save($file)

psedit $file
```

The clixml was more readable.