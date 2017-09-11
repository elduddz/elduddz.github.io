# DSC Resource

## What is it

is a thing / element we want to define on a server, this can be software or OS.

3 functions within in each provider

- Get-TargetResource
- Set-TargetResource
- Test-TargetResource

`Find-Module -Tag DSCResourceKit`

`Find-DscResource`

look for PSDesiredStateConfiguration on PSModulePath.

Others can be added via DSC resource hub from PS commiunity.

expermimental resources are prefixed with an x.

Remember **Do this with ISE** for some reason... why did I make this note? who knows may just delete it.

Things like `File` and `Service` are valid template words, anything else you might need to install using `Import-DSCResource` (this is a missing KB, currently looking for one that will work on Windows 7).

All this allows is that if any custom configurations are used then let the ISE and the script run to understand what is going on.

They must be installed on Target nodes

```powershell
Configuration xyCore {
    Import-DscResource -ModuleName PSDesiredStateConfiguration,xSMBShare
    Node yy {
        File Data {
            DestinationPath = "C:\Data"
            Ensure = "Present"
            Type = "Directory"
        }
        xSmbShare Data {
            DependsOn = "[File]Data"
            Name = "Data"
            Path = "C:\Data"
        }
    }
}
```

There is an option to make the Configuration Data more dynamic

## Dynamic Configuration Data

```powershell

$ConfigurationData = @{
    AllNodes = @(
        @{NodeName = "01";Role="FilePrint"},
        @{NodeName "02";Role="Webserver"},
        @{NodeName ="*" #For wildcard match
        Features = "Windows-Server-Backup","PowerShell-V2"}
        NonNodeData = @{Something special #Doesnt have to be NonNodeData, but so long as it does not match the standard naming convention it will be ignored.
        }
    )}

$AllNodes
$Node
$ConfigurationData

Node $AllNodes.NodeName {
    $Node.features.foreach({
        WindowsFeature $_ {
            Name = $_
            Ensure = "Present"
        }
    })
}
```

It is important to note that you cannot Undo.

Can restore using `Restore-DSCConfiguration -Verbose`

Can't  test last applied config using `Test-DSCConfiguration -Verbose`

## working with config

```powershell
. .\Config.ps1
#Call configuration
xyCore

#Start config
Start-DscConfiguration -Path .\xyCore -OutVariable "j"

#you can also append -wait -verbose to the start which will display to screen as it goes.

#or wait for complete
wait-job $j

#and review job
$j | restore-job -keep -verbose


```

DscConfiguration will return a boolean response by default

DscConfiguration has a set pattern of functions.

```powershell
function Get-TargetResource
{
}

function Set-TargetResource
{
}

function Test-TargetResource
{
}
```

Deploying is easy, creating and restoring is harder.

push model is easiest for testing.

**Q -** if dsc runs as system how can this be performed on each machine without a session? (maybe I am about to learn this?)

Resources must exist on target nodes, (xSmbShare for example). Safest place to add these are C:\Program Files\WindowsPowerShell\Modules as this is available on all PSModulePaths.

One Config per server

Rollback using Restore- you cannot undo if there has never been a run before

use `Test-DscConfiguration` to verify and use `-Verbose` as well to see all messages.

## Local Configuration Manager

### What is LCM

- The "Engine"
- Responsible for applying configurations
- Default behaviour can be modified by configuration meta information
- Can be modified per server

uses same setup as resouces so you can use `$AllNodes` etc.

```powershell
Get-DSCLocalConfigurationManager to check node settings

Set-DSCLocalConfigurationManager to apply
```

`Get-DSCLocalConfigurationManager` Can specify a cim or computer name.

LocalConfigurationManager is a "Service".

```powershell
Configuration Configs {
    Node @($nodes) {
        LocalConfigurationManager {
            ConfigurationMode = "ApplyAndAutoCorrect"
            ConfigurationModeFrequencyMins = 120
            RefreshMode = "Push"
            RebootBodeIfNeeded = $true
        }
    }
}
```

Some LCM settings only apply to PULL configurations

`<computername>.meta.mof` created from configuration command for each node

`Set-DscConfiguration` does not set LCM

`Set-DscLocalConfigurationManager -ComputerName (has to match mof and configuration) -Path .\Configs

## Troubleshooting

- Be Verbose
- Log at the event log
- Add logging to config
- Use xDSCDiagnostics

### Verbose

Turn on `-Verbose` and `-Wait` Test will only tell you True or False without Verbose

### Event Logs

use Get-WinEvent and look at:

- Microsoft-Windows_DSC/Operational
- Microsoft-Windows-PowerShell-DesiredStateConfiguration-FileDownloadManager/Operational
- Microsoft-Windows-Powershell-DesiredstateConfiguration-PullServer/Operational

`Get-WinEvent -LogName Microsoft-Windows-DSC/Operational -ComputerName "Serverx" | Select -First 40`

Because these are new log style, you need to use `Get-WinEvent` `-FilterHashTable`

Enable Analytic and Debug Logs, enable before troubleshooting, hidden by default, found under Desired State Configration (Right-click view > Show...)

ONLY TURN ON WHEN NEEDED

### Add Logging

```powershell
Configuration y {
    Node x {
        Log NetworkConfig {
            Message = "Network Config Complete."
            DependsOn = "[File]LocalData"
        }
    }
}
```

## xDSCDiagnostics

`Get-xDSCOperation -Newest 1 -ov op` Newest defaults to 10 (`-ov` = OutVariable).

`Trace-xDSCOperation`

You can outvar the get command above and then perform a trace action.

```powershell
Trace-xDSCOperation -JobId $op[0].JobID -ComputerName $op[0].ComputerName | `
Out-GridView -Title "Job $($op.JobId)"
```

`Update-xDSCEventLogStatus`

## The basics of setting up a DSC Module

```powershell
$Website = New-xDscResourceProperty –Name Name -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$AppPool = New-xDscResourceProperty –Name AppPool -Type String -Attribute Write
$Source = New-xDscResourceProperty –Name Source -Type String -Attribute Write
$Destination = New-xDscResourceProperty –Name Destination -Type String -Attribute Write

New-xDscResource -Name "UKHO_xWebsiteDeploy" -ModuleName "UKHO.xWebAdministration" -Property $Website, $Ensure, $AppPool, $Source, $Destination
```

good list of dsc windows features:
http://geekswithblogs.net/Wchrabaszcz/archive/2015/07/01/server-2016--how-to-add-or-remove-windows-features.aspx

good example of an uninstaller:
http://blogsprajeesh.blogspot.co.uk/2015/09/silent-installation-of-visual-studio.html
