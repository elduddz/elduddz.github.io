# How to Desired State Configuration (DSC)

**Pluralsight course:** [DSC Fundamentals](https://app.pluralsight.com/library/courses/powershell-desired-state-configuration-fundamentals/table-of-contents)

## Intro

- course assuming PS 4 (will need this for demos on Client and Server)
- how to manage server manual
- install RSAT
- Domain Environment with Admin and Powershell Remoting

## What is DSC

- can use PS syntax to create configuration scripts
- use PS language and cmdlets to create and deploy configurations **on servers**
- "Set it and Forget it"

Simlar to Puppet and Chef, DSC can be integrated with this.

Based on industry standards using Managed Object Format(MOF) and COmmon Information Model(CIM)

This is the future of Windows Server management

## Benefits

- Prevents configuration "drift"
- Separate configuration from implementation
- Offers "continuous" deployment
- Works both on prem and in the cloud

- Each server has one MOF file using Local Configuration Manager(LCM), configured with DSC and can be managed with cmdlets

**"One MOF to rule them all"**

Has CIM DSC Namespace

## DSC Module

### Autoring phase

- imperative (do something) commands
- declarative (look like this) commands
- Create MOF Definitions

### Staging Phase

- Declarative MOFs
- Configuration calculated per node


### "Make It So"

- Declarative configurations implements through imperative providers

## Architecture

### Push

- Configuration deployed to servers from a staging point
- Start-DSCConfiguration

### Pull (TODO)

- Servers poll a cerntral server
    - HTTP(s)
    - SMB file share

### One Configuration per server

This is very important

## Basic Config

- defined using PS
- `Configuration` keywords
- Define a node
- Configure a resource

```powershell
# Create basic Core (projectCore.ps1)
Configuration ProjectCore {
    Node Server01 {
        File Work {
            Type = "Directory"
            Ensure = "Present"
            DestinationPath = "C:\Work"
        } #Create Directory
        Service RemoteRegistry {
            Name = "RemoteRegistry"
            StartupType = "Automatic"
            State = "Running"
        }
    } # What does each "Node" in Core
}
```

then you can load this into memory as normal practise

```powershell
# Load CoreConfig into memory
. .\ProjectCore.ps1
```

And  Invoke config to create MOFs

```powershell
ProjectCore # Remember this is the name of the "Configuration"
```
This creates a directory called ProjectCore, inside which is a MOF for each Node.

Then you can simply start the dsc configuration by calling Start-DscConfiguration and define the location of the MOFs.

```powershell
Start-DscConfiguration -Path .\ProjectCore
```

This should then start applying the configs

## Future

Microsoft is invested, and devoting a lot of manpower into this methodology.

Remember it can be managed by chef.

Again as this is a standard, this can be used against apache