# Powershell for managing Azure Resource Managed (Rm) VMs
```powershell
Get-AzureRmContext

Login-AzureRmAccount

Get-AzureRmVm -Name [Name] -ResourceGroupName [ResourceGroupName] | Start-AzureRmVM

$vm = Get-AzureRmPublicIpAddress
$vm.IpAddress

Get-AzureRmVm -Name [Name] -ResourceGroupName [ResourceGroupName] | Stop-AzureRmVM -Force
```