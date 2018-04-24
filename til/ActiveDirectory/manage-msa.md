```powershell
install-windowsfeature rsat-ad-powershell

install-adserviceaccount -identity <serviceaccount>

Test-ADServiceAccount -identity <serviceaccount>
```