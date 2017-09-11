# Redirecting Outputs

## Rules

Out should be the last thing you do on a pipeline

## Out-File (with -append)

Outputs pipeline to file `-append` appends the information

## Out-Printer

Sends to default printer

## Tee-Object (tee)

Allows output to be sent to both pipeline and a file or pipeline and a variable

## Out-GridView

**TBC**

## Out-Null

**TBC**

Not sure why I havent go this, basically, pipelines are run out of PowerShell

1 is standard
2 is error

to append the error output to the standard out (effectively merging the two, you can do the following: `2>&1`