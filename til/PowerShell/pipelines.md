```powershell
 Function Test-Demo
 {
  Param ($Param1)
  Begin{ write-host "Starting"}
  Process{ write-host "processing $_ for $Param1"}
  End{write-host "Ending"}
 }

Echo Testing1, Testing2 | Test-Demo Sample
```

The above is not a cmdlet, if you were to add [[cmdletBinding]] it will error.

I found an example that was talking about the pipeline variable, and was still mention the foreach at some point, it made me wonder if the same $_ was available.

```powershell
function Test-Pipe {
[CmdLetBinding()]
param(
[parameter(ValueFromPipeline=$true)]
$Data
)
begin {}
process {
write-host "booya $_"
}
end {}
}

1..5 | Test-Pipe
```