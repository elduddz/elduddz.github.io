# PowerShell: $array.ForEach({})

## In the beginning, there was a cmdlet...

Most times, when you think about writing something in PowerShell, you will usually find within the first lines a `Get-ChildItem`, you will then inevitably have a for each loop.

Normally I would write this as `foreach($item in $items)`, but on one occasion the autocomplete came up on the array variable with a `.ForEach` option, I didn't know the correct use of this so I tried the usual

```powershell
Get-Help ForEach -Examples

Get-Help ForEach -Online
```

As this didn't really show this option (to be honest I may have not gone to the right help from PS) so I **Googled** the same thing, which initially took me to a similar page on ss64.com, but they provided a link to other `ForEach` options, one of which contained how to use the [ForEach (Method)][ss64ForEach].

## How to use .ForEach

Lets see if I can explain it better in code:

```powershell
$items.ForEach({
# This exposes the $_ object, but I find that it doesn't know what each item is.
# So I often find myself setting that to a new variable.
$item = $_
#I guess as you learn more and more you become versed in the ways of the object and can free type out the properties you need.
})
```

This form of writing a ForEach still allows a full set of statements to be written, and exposes a `$_` object to represent each item in the loop. As long as you know what properties you are after, you never have to set the `$_` to a variable, but I know I will.

## Check your $PSVersionTable  

There is something to be aware of in PowerShell version 3. If the `$array` could be null, you need to put in a check for that before doing your actions.

```powershell
if($items -ne $null)
{
...
}
```

If you have used PowerShell 2, you may be aware of this problem with arrays already. 

PowerShell 3 and above the foreach loop handles null array objects automatically. With PowerShell 3, you will need the above when using the ForEach method. 

With PowerShell 5, the ForEach method handles null arrays.

## Do I like it?  

This is an alternative to `foreach($item in $items)`, but trying to provide a preference for one or the other is too close to call. I may flip every now and again without concern. Personally, I would say as a guideline to pick one way of representing this process stick to it.

[ss64ForEach]: http://ss64.com/ps/foreach-method.html