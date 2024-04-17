# Powershell File Operations

Now that we know how to move in the file system, let's check how to manipulate files and folders. In this challenge, you will discover and use the commands `Get-Content`, `echo`, `New-Item`, `Move-Item`, `Copy-Item`, and `Remove-Item`.

- Create a file named story1.txt
- Type `echo "Hello World" > story1.txt`
- Print the content of the file
- Create a folder named `story`
- Move `story1.txt` inside `story`
- Copy `story1.txt` as `story2.txt`
- Print both files
- Rename `story2.txt` as `me.txt`
- Append `me.txt` and add "I am a junior at Becode"
- Remove the folder story with it's content

## Solution:

```powershell
# Create a file named story1.txt
New-Item -Path .\story1.txt -ItemType File

# Type `echo "Hello World" > story1.txt`
echo "Hello World" > story1.txt

# Print the content of the file
Get-Content .\story1.txt

# Create a folder named `story`
New-Item -Path .\story -ItemType Directory

# Move `story1.txt` inside `story`
Move-Item -Path .\story1.txt -Destination .\story

# Copy `story1.txt` as `story2.txt`
Copy-Item -Path .\story1.txt -Destination .\story2.txt

# Print both files
Get-Content .\story\story1.txt
Get-Content .\story2.txt

# Rename `story2.txt` as `me.txt`
Rename-Item -Path .\story2.txt -NewName .\me.txt

# Append `me.txt` and add "I am a junior at Becode"
Add-Content -Path .\me.txt -Value "I am a junior at Becode"

# Remove the folder story with it's content
Remove-Item -Path .\story -Recurse
```

- `New-Item` command is used to create a new file or folder. The `-ItemType` parameter specifies the type of item to create, which can be either `File` or `Directory`.

- `echo` command is used to write text to a file. The `>` operator is used to redirect the output of the `echo` command to a file.

- `Get-Content` command is used to read the content of a file.

- `Move-Item` command is used to move a file or folder from one location to another.

- `Copy-Item` command is used to copy a file or folder from one location to another.

- `Rename-Item` command is used to rename a file or folder.

- `Add-Content` command is used to append text to a file.
  
- `-Recurse` parameter is used to delete a folder and all its contents.

We can also do this using the shorthand aliases:

```powershell
ni .\story1.txt -it f
echo "Hello World" > story1.txt
gc .\story1.txt
ni .\story -it d
mv .\story1.txt .\story
cp .\story1.txt .\story2.txt
gc .\story\story1.txt
gc .\story2.txt
ren .\story2.txt .\me.txt
ac .\me.txt "I am a junior at Becode"
ri .\story -Recurse
```

