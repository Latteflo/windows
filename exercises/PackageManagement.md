# Powershell Package Management

It's time to start installing softwares and keep them updated. We will see how to use Chocolatey and how to use Windows Updates.

* Instructions

- Get Windows updates
    - Install the `PSWindowsUpdate` module
    - Type `Get-WindowsUpdate` to check for updates
    - Type `Install-WindowsUpdate` to install updates
- Manage Packages
    - Install `Chocolatey`
    - Install `VLC` from `Chocolatey`
    - Upgrade `VLC` to the latest version (it should already be but it's your first use)
    - Remove the `VLC` package using `Chocolatey`
    - Could you use `Chocolatey` on already installed software? How?
- Manage Windows Features
    - Get installed windows features with the command `Get-WindowsFeature`
    - Install a new feature such as hyper-v with `Install-WindowsFeature`

> **WARGNING**: This exercise **will only work on Windows** since it's specific to the way windows manages packages.


## Solution:

```powershell
# Get Windows updates
# Install the PSWindowsUpdate module
Install-Module -Name PSWindowsUpdate

# Check for updates
Get-WindowsUpdate

# Install updates
Install-WindowsUpdate -AcceptAll

# Manage Packages
# Install Chocolatey
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Install VLC
choco install vlc

# Upgrade VLC
choco upgrade vlc

# Remove VLC
choco uninstall vlc

# Manage Windows Features
# Get installed windows features
Get-WindowsFeature

# Install Hyper-V
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

- `Install-Module` command is used to install a module from the PowerShell Gallery.
- `Get-WindowsUpdate` command is used to check for available Windows updates.
- `Install-WindowsUpdate` command is used to install Windows updates.
- `Set-ExecutionPolicy` command is used to set the execution policy for the current session.
- `System.Net.ServicePointManager` class is used to manage the security protocols for network connections.
- `SecurityProtocol` property is used to specify the security protocols to be used for network connections.
- `Bypass` value is used to bypass the execution policy.
- `Force` parameter is used to force the execution of the command.
- `iex` command is used to invoke the expression.
- `New-Object` command is used to create an instance of a .NET Framework class.
- `System.Net.WebClient` class is used to download data from the internet.
- `DownloadString` method is used to download the content of a URI as a string.
- `choco` command is used to interact with Chocolatey package manager.
- `Get-WindowsFeature` command is used to get the list of installed Windows features.
- `Install-WindowsFeature` command is used to install Windows features.
- `Hyper-V` is a Windows feature that allows you to create and manage virtual machines.
- `IncludeManagementTools` parameter is used to install the management tools for the specified feature.
