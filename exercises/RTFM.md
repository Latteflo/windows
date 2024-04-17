# Powershell RTFM

Everybody needs a little help at one time or another. In this exercise we will check how you can get help on powershell and how you can find interesting commands following your needs.

- Open a PowerShell session in your terminal
- type `Get-Help`
- Find out what a command such as `Get-Process` does without looking on google
- Now try with the `-online` parameter
- What does `Get-command`? 

Optionally:

- Try to get help on common commands such as `ls`, `cp`, `mv`, ...


## Solution

```powershell
# Get help on Get-Process
Get-Help Get-Process

# Get help on Get-Process online
Get-Help Get-Process -Online

# Get help on Get-Command
Get-Help Get-Command
```

The `Get-Help` cmdlet is used to display detailed information about PowerShell commands and syntax. You can use it to get help on specific commands, parameters, or topics. The `-Online` parameter opens the online version of the help documentation in your default web browser.

The `Get-Process` cmdlet retrieves information about processes running on the local computer. It displays a list of processes, including their names, IDs, and memory usage.

The `Get-Command` cmdlet lists all commands available in PowerShell. It can be useful for finding specific commands or exploring available options.

You can also try getting help on common Unix-like commands such as `ls`, `cp`, `mv`, etc., to see if PowerShell provides similar functionality or alternatives.

- `Get-Help ls`
   - `ls` is an alias for the `Get-ChildItem` cmdlet, which lists items in the current directory.
- `Get-Help cp`
   - `cp` is an alias for the `Copy-Item` cmdlet, which copies an item from one location to another.
- `Get-Help mv`
   - `mv` is an alias for the `Move-Item` cmdlet, which moves an item from one location to another.