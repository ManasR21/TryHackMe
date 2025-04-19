Velociraptor Tasks Summary

Task 2: Deployment

Launch Instant Velociraptor on Windows: Velociraptor.exe gui

Task 3: Interacting with Client Machines

Client Hostname: thm-velociraptor.eu-west-1.compute.internal
Agent Version: 2021–04–11T22:11:10Z
VQL Command for Client User Accounts: LET Generic_Client_Info_Users_0_0=SELECT Name, Description, Mtime AS LastLogin FROM Artifact.Windows.Sys.Users()


Column Header for PowerShell whoami Output: stdout
VQL Command for PowerShell Get-Date: powershell -ExecutionPolicy Unrestricted -encodedCommand RwBlAHQALQBEAGEAdABlAA==



Task 4: Creating a New Collection

Parameter Description for Ubuntu Artifacts: Ubuntu on Windows Subsystem for Linux
Number of Files Uploaded: 20

Task 5: VFS (Virtual File System)

Accessor for Hidden NTFS Files and Alternate Data Streams: NTFS Accessor
Accessor for File-like Registry Access: Registry Accessor
File in $Recycle.Bin: desktop.ini
Hidden Flag in Admin’s Documents Folder: THM{VkVMT0NJUkFQVE9S}

Task 6: VQL (Velociraptor Query Language)

Follows SELECT Keyword: Column Selectors
Follows FROM Keyword: VQL Plugin
Follows WHERE Keyword: Filter expression
View Completions in Notepad Interface: ?
Plugin to Run PowerShell Code: execve()

Task 7: Forensic Analysis VQL Plugins

Arguments for parse_mft(): parse_mft(filename="C:/$MFT", accessor="ntfs")
Filter Expression to Exclude Directories: IsDir

Task 8: Hunt for a Nightmare

Artifact Exchange Name for PrintNightmare Detection: Windows.Detection.PrintNightmare
Select Clause: SELECT "C:/" + FullPath AS Full_Path,FileName AS File_Name,parse_pe(file="C:/" + FullPath) AS PE


DLL Placed by Attacker: nightmare.dll
PDB Entry: C:\Users\caleb\source\repos\nightmare\x64\Release\nightmare.pdb

