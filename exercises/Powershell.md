# PowerShell Notes

## Introduction to PowerShell
- PowerShell is a task automation and configuration management framework from Microsoft.
- It's built on the .NET framework and includes a command-line shell and a scripting language.

## Basic Commands

### Getting Help
- `Get-Help <cmd>`: Displays detailed information about PowerShell commands and syntax.
- `Get-Command`: Lists all commands available in PowerShell.

### File System Navigation
- `Set-Location <path>`: Changes the current directory to the specified path.
- `Get-ChildItem`: Lists items in the current directory (similar to `ls` in Bash).
- `Push-Location`/`Pop-Location`: Save and restore the current location, respectively.

### File Operations
- `New-Item <path>`: Creates a new item (e.g., file or directory).
- `Copy-Item <source> <destination>`: Copies an item from one location to another.
- `Move-Item <source> <destination>`: Moves an item from one location to another.
- `Remove-Item <path>`: Deletes an item.

## Advanced Operations

### Permissions Management
- `Get-Acl <path>`: Gets access control list (ACL) for a file or directory.
- `Set-Acl <path>`: Sets the ACL for a file or directory.

### Package Management
- `Find-Package <name>`: Searches for a package by name.
- `Install-Package <name>`: Installs a package.

### Environment Variables
- `Get-ChildItem env:`: Lists all environment variables.
- `Get-Item env:<name>`: Retrieves the value of a specific environment variable.
- `$env:<name>`: Accesses an environment variable directly.

## Scripting
- PowerShell scripts use the `.ps1` file extension.
- `Write-Output`: Writes output to the console.
- `Write-Host`: Writes output to the console with optional colors.

## PowerShell Remoting
- PowerShell Remoting lets you run PowerShell commands on remote computers.
- `Invoke-Command -ComputerName <name> -ScriptBlock {<commands>}`: Executes commands on a remote computer.

## Security
- By default, PowerShell restricts execution of scripts. Use `Set-ExecutionPolicy` to change this behavior.


## Resources
* ["VBScript" - CVE](https://www.cvedetails.com/vulnerability-list/vendor_id-26/product_id-20672/Microsoft-Vbscript.html)
* ["New Windows Terminal" - Windows Store](https://github.com/microsoft/terminal)
* ["Powershell Documentation" - Microsoft](https://docs.microsoft.com/en-us/powershell/)
* ["WMI" - Wikipedia](https://en.wikipedia.org/wiki/Windows_Management_Instrumentation)
* ["CIM" - Microsoft Documentation](https://docs.microsoft.com/en-us/windows/win32/wmisdk/common-information-model)
* ["WMI" - Microsoft Documentation](https://docs.microsoft.com/en-us/windows/win32/wmisdk/wmi-start-page)
* ["Powershell videos" - Powershell.org](https://www.youtube.com/powershellorg)
* ["ACL" - Wikipedia](https://en.wikipedia.org/wiki/Access-control_list)

