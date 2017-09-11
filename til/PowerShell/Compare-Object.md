# Compare-Object  

Compare-Object allows you to ask and answer the simple question of, does this exist over there?

The other great part is, rather than having to do this for one file at a time, you can submit an array of Files (for example) and it will tell you if any are missing from each list?

## example  
````powershell
$from = "D:\From\"
$to = "D:\To\"

$items = Get-ChildItem $from -Recurse
$existingItems = Get-ChildItem $to -Recurse
$compared = Compare-Object -ReferenceObject $items -DifferenceObject $existingItems -PassThru | Where-Object {$_.SideIndicator -eq "<="}
````
the value of `-PassThru` is useful as it will then output the file.

from this you can then do the following and copy any missing files.

````powershell
foreach($compare in $compared)
{
    $current = $to + $compare.Fullname.Substring($from.Length, $compare.FullName.Length - $from.Length)
    Copy-Item $compare.FullName -Destination $current
}
````