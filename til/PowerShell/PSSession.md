# a couple of options

For a basic connection
$session = New-PSSession -computername $serverName -credential $testCred

For a more secure connection
$session = New-PSSession -computername $serverName -credential $testCred -Authentication CredSSP

once created you can use `Enter-PSSession $session`

`Remove-PSSession` closes it

# Things to check
Computer Configuration -> Administrative Templates -> System -> Credentials Delegation -> Allow Delegating Fresh Credentials