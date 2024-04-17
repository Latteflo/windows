# Powershell Navigation

Now we will learn how to move around in the filesystem with `Set-Location`, `Get-Location`, `Get-ChildItem` ...

- Print your current location on the screen
- Print the content of your current directory
- Print the content of your root (`C:` _if you're running windows_, `/` _for linux_)
- Go into your home folder (_C:\Users\Username or /home/Username_)
- Print the content of your home
- Those commands are pretty long to type, do you know any shorter way to do it?


# Solution

```powershell
# Print your current location
Get-Location 
#or
pwd
#or
gl 

# Print the content of your current directory
Get-ChildItem
#or
ls
#or
dir

# Print the content of your root
Get-ChildItem C:\
# or
Get-ChildItem /
# or
ls C:\
# or
ls /


# Go into your home folder
Set-Location ~
# or
cd ~
#or 
cd $home

# Print the content of your home
Get-ChildItem
# or
ls
# or
dir

```

The `pwd` command is a shorthand for `Get-Location`, and `ls` is a shorthand for `Get-ChildItem`. 

Other useful aliases include:

- `cd` for `Set-Location`
- `dir` for `Get-ChildItem`
- `cls` for `Clear-Host`
- `rm` for `Remove-Item`
- `cp` for `Copy-Item`
- `mv` for `Move-Item`
- `echo` for `Write-Output`
- `cat` for `Get-Content`
- `man` for `Get-Help`
- `history` for `Get-History`
- `ps` for `Get-Process`
- `kill` for `Stop-Process`
- `clear` for `Clear-Host`
- `pushd` for `Push-Location`
- `popd` for `Pop-Location`
- `mkdir` for `New-Item -ItemType Directory`
- `rmdir` for `Remove-Item -Recurse`
- `type` for `Get-Content`
- `where` for `Get-Command`
- `help` for `Get-Help`
- `?` for `Where-Object`
- `foreach` for `ForEach-Object`