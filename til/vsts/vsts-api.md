```powershell
$repos = curl -Uri http://{UrlToProject}/_apis/git/repositories -UseDefaultCredentials

$json = $repos.Content

$hashtable = @{}

(ConvertFrom-Json $json).psobject.properties | Foreach { $hashtable[$_.Name] = $_.Value }

foreach($value in $hashtable.value)
{
    $prs = curl -Uri http://{UrlToProject}/_apis/git/repositories/$($value.id)/pullRequests -UseDefaultCredentials

    $prjson = $prs.Content

    $prhashtable = @{}

    (ConvertFrom-Json $prjson).psobject.properties | Foreach { $prhashtable[$_.Name] = $_.Value }

    if($prhashtable.value.count -gt 0)
    {
        $prhashtable.value
    }
}
```