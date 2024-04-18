# Powershell Environment Variables

In any programming language you can store data within variables. However they only exist as long as the program is executed, but what if you wanted to share information between two applications not running at the same time.

Then you could use environment variables, which are variables stored at the OS level. You can access them from anywhere.

- Open a Powershell Terminal
- Type `echo $env:computername`. It should show your computer name
- Create a variable by typing `$env:test = "hello powershell"`
- Check the variable you just created the same way you did with the computer name
- Now we will add something to this variable by typing `$env:test += " Becode"`
- Check the variable- There is one really important environment variable : `$env:path`. This variable store the location where windows looks for files that are not in your current folder. For example, if you call VSCode from the powershell terminal, it opens it even if the executable isn't present in the current folder. That's because the path to the vscode's executable is stored in `$env:path`. Now download ([rufus](https://github.com/pbatard/rufus/releases/download/v3.13/rufus-3.13p.exe)) If you try from a command line to launch it, it will fail with a command not found (if you are not in the same folder).
- Try to happen the $env:path to add the path to rufus' executable (It should be something like this if you copied it on your desktop : `C:\Users\Username\Desktop`)  
- Now try to launch Rufus from the command line. It should work now. We call it by typing `rufus-3.13p.exe`

> **WARNING**: This exercise will **only work on windows** since it's specific to the way windows manages environment variables.


## Solution : 

```powershell
# Get the computer specs
$computer = Get-WmiObject Win32_ComputerSystem
$os = Get-WmiObject Win32_OperatingSystem
$cpu = Get-WmiObject Win32_Processor
$ram = Get-WmiObject Win32_PhysicalMemory

# Calculate the total RAM capacity in GB
$totalRamCapacityInBytes = ($ram | Measure-Object -Property Capacity -Sum).Sum
$totalRamCapacityInGB = $totalRamCapacityInBytes / 1GB

# Create a CSV file content
$csv = "Computer Name,Manufacturer,Model,OS,Architecture,Processor,RAM`n"
$csv += "$($computer.Name),$($computer.Manufacturer),$($computer.Model),$($os.Caption),$($os.OSArchitecture),$($cpu.Name),$($totalRamCapacityInGB) GB`n"

# Save the CSV file
$csv | Out-File -FilePath "$env:USERPROFILE\computer_specs.csv"

# To run the script, you need to change the execution policy to allow running scripts
# Set-ExecutionPolicy RemoteSigned
```

To change the execution policy in a secure way, you can use the `Set-ExecutionPolicy` cmdlet with the `-Scope` parameter set to `CurrentUser`. This will only change the execution policy for the current user, making it more secure than changing it globally.

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

And sure enough, the script will create a CSV file with the computer's specs in the user's profile folder.

### **Rufus** 
- is a popular tool for creating bootable USB drives, and it's often used to install operating systems or run diagnostic tools.

In our requirements we need to call for Rufus - and we can do this by adding the path to the executable to the `$env:Path` variable using the following command:

```powershell
$env:Path += ";C:\Users\Username\Desktop"
```

Replace `Username` with your actual username and `Desktop` with the folder where you copied the Rufus executable. After adding the path, you should be able to run Rufus from anywhere in the PowerShell terminal.

```powershell
rufus-3.13p.exe
```

This will launch Rufus even if you're not in the same folder as the executable.