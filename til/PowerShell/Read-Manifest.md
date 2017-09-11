#Reading manifests

This should work

```powershell
Import-LocalizedData -BaseDirectory .\path -FileName example.psd1 -BindingVariable Data
```

This works well

```powershell
$manifest = gc .\$psdFileName | Out-String | iex
```