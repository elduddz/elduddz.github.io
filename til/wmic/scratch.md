Use wmic to find the exact name of the software:
wmic product get name

Once you know the name of the software, you can remove it with wmic as well:
wmic product where name="application name" call uninstall