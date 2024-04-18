# Powershell Permissions

Now that we can navigate and create files, we should be able to change permissions on these. We will use the commands `Get-Acl`, `Set-Acl`, `RunAs`

- Create a file
- Check the owner and the groups
- Change the file owner to the built-in administrator (administrator account is disabled by default, check how to enable it. Don't forget to set a strong password!)
- Check the file's permission
- Try to print the content of the file as your normal user
- Print the content of the file using administrator account

> **WARNING**: This exercise **will only work on Windows** system since file system permissions are not managed the same way on Windows and Linux.

## Solution:

```powershell
# Create a file
New-Item -Path .\file.txt 

# Check the owner and the groups
Get-Acl .\file.txt

# Change the file owner to the built-in administrator
$admin = New-Object System.Security.Principal.NTAccount("BUILTIN\Administrators")
$acl = Get-Acl .\file.txt
$acl.SetOwner($admin)
Set-Acl .\file.txt $acl

# Check the file's permission
Get-Acl .\file.txt

# Try to print the content of the file as your normal user
Get-Content .\file.txt

# Print the content of the file using administrator account
RunAs /user:Administrator "Get-Content .\file.txt"

```

- `Get-Acl` command is used to get the access control list (ACL) of a file or folder.
- `Set-Acl` command is used to set the access control list (ACL) of a file or folder.
- `RunAs` command is used to run a program as a different user.
- `New-Object` command is used to create an instance of a .NET Framework class.
- `System.Security.Principal.NTAccount` class is used to represent a user or group account in Windows.
- `SetOwner` method is used to set the owner of a file or folder.
- `BUILTIN\Administrators` is the built-in administrator group in Windows.
- `Administrator` is the default administrator account in Windows.
- `Get-Content` command is used to read the content of a file.
- `RunAs /user:Administrator` command is used to run a program as the Administrator user.
  
We can also use the shorthand `icacls` command to change file permissions:

```powershell
# Grant read permission to the Users group
icacls .\file.txt /grant Users:R

# Revoke read permission from the Users group
icacls .\file.txt /remove Users

# Remove all inherited permissions
icacls .\file.txt /inheritance:r

# Apply the operation to all subfolders and files
icacls .\file.txt /T

```

- `icacls` command is used to display or modify access control lists (ACLs) for files and folders.
- `/grant` parameter is used to grant access to a user or group.
- `/remove` parameter is used to remove access from a user or group.
- `Users:R` grants read permission to the Users group.
- `Users` is the built-in group that includes all user accounts on the system.
- `/R` parameter is used to remove all inherited permissions from the file or folder.
- `/T` parameter is used to apply the operation to all subfolders and files.
- `/inheritance:r` parameter is used to remove all inherited permissions from the file or folder.

Let's create a file named Permissions in a text format and check the permissions:

1. **Create a File:**
   Creating a file named `Permissions.txt` in the current directory is the first step, serving as the target for permission changes.

   ```powershell
   New-Item -Path .\Permissions.txt -ItemType File
   ```

2. **Check the Owner and Groups:**
   Using `Get-Acl`, you retrieve the Access Control List (ACL) of the file, which includes details about the file's permissions, owner, and associated security principals (groups/users).

   ```powershell
   Get-Acl .\Permissions.txt | Format-List
   ```

3. **Enable and Set Password for the Administrator Account:**
   You're ensuring the built-in Administrator account is enabled and setting a strong password for it. This step is crucial for security purposes and to prevent unauthorized access.

   ```powershell
   Enable-LocalUser -Name "Administrator"
   $adminPassword = ConvertTo-SecureString "YourStrongPasswordHere" -AsPlainText -Force
   Set-LocalUser -Name "Administrator" -Password $adminPassword
   ```

4. **Change the File Owner to the Built-in Administrator:**
   By creating an `NTAccount` object for the "BUILTIN\Administrators" group and using it to set a new owner on the file's ACL, you're transferring ownership to the Administrator. This step demonstrates the process of modifying ownership at a low level within Windows' security model.

   ```powershell
   $admin = New-Object System.Security.Principal.NTAccount("BUILTIN\Administrators")
   $acl = Get-Acl .\Permissions.txt
   $acl.SetOwner($admin)
   Set-Acl .\Permissions.txt $acl
   ```

5. **Try to Print the Content of the File as Your Normal User:**
   Attempting to read the file with `Get-Content` as a normal user can help illustrate the impact of permissions on file accessibility.

   ```powershell
   Get-Content .\Permissions.txt
   ```

6. **Print the Content of the File Using the Administrator Account:**
   The use of `RunAs` in the script snippet is intended to demonstrate running a command as the Administrator. However, it's important to note that `RunAs` with PowerShell commands in this manner might not directly execute as intended because `RunAs` is a CMD utility. Instead, you might use the PowerShell `Start-Process` cmdlet with `-Credential` parameter or log in as Administrator to execute PowerShell commands.

