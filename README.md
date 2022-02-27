# Powershell-Commands


### The PowerShell CLI
- PowerShell executable directory:
```sql
C:\Windows\System32\WindowsPowerShell\v1.0
```
- 64-bit PowerShell executable:
```sql
C:\windows\system32\WindowsPowerShell
```
- 32-bit Powershell executable:
```sql
C:\windows\SysWOW64\WindowsPowerShell
```
- Determine whether we’re running in a 32-bit or 64-bit PowerShell environment
```sql
PS C:\> [Environment]::Is64BitProcess
```
- View options : `powershell /?` `-Help` `-?`

- `ExecutionPolicy` -> The PowerShell execution policy determines which scripts if any, we can run and can easily be disabled with the "Bypass" or "Unrestricted" arguments:
```sql
C:\> powershell.exe -ExecutionPolicy Bypass .\script.ps1

C:\> powershell.exe -ExecutionPolicy Unrestricted .\script.ps1
```
- `-WindowStyle` parameter hides the Powershell window when used with the “hidden” argument.
```sql
C:\> powershell.exe -WindowStyle Hidden .\script.ps1
```
- `Command` used to specify a 'command' or a 'Script Block' to execute:
```sql
C:\> powershell.exe -Command Get-Process

C:\> powershell.exe -Command "& { Get-EventLog –LogName security }"
```
- `EncodedCommand` used to execute base64 encode scripts:
```
C:\> powershell.exe -EncodedCommand $encodedCommand
```
- `Get-Help` -> similar to `man pages on linux`:
```sql
PS C:\> Get-Help Get-Process
PS C:\> Get-Help Get-Process -Full
PS C:\> Get-Help Get-Process -Examples
```
- `Get-Command` shows all cmdlets, aliases, functions, workflows, filters, scripts and any applications that are available for us to use in PowerShell.
```
PS C:\> Get-Command –Name *Firewall*

-Name -> to liost a filter
```
### CMDLETS

```
PS C:\> Get-ChildItem

PS C:\> Get-ChildItem | Format-List *
-> This returns all 'named' properties with its 'objects'
-> The 'names' use to filter the output

PS C:\> Get-Process | Sort-Object -Unique | Select-Object ProcessName
PS C:\> Get-Process | Sort-Object -Unique | Select-Object ProcessName > uniq_procs.txt
-> list of processes
-> sorts the list with (-Unique) parameter
-> selects the "ProcessName" objects
-> returns a unique list of process names
```
- `Get-Process`
```sql
PS C:\> Get-Process
-> shows columns 'names'(properties)

PS C:\> Get-Process | Format-List *
-> shows all info(Properties)
-> we can now to filter the data fot specific properties

PS C:\> Get-Process chrome, firefox | Sort-Object -Unique | Format-List Path
-> info about specific 'processes' and 'path'(properties)

PS C:\> Get-Process chrome, firefox | Sort-Object -Unique | Format-List Path,Id
-> multipy 'properties' to cmdlet Format-List
```
- `Get-ChildItem` == `ls`
```sql
PS C:\Users> Get-Alias -Definition Get-ChildItem
-> to find alias for a specific cmdlet
```
- `Get-WmiObject`
```sql
PS C:\> Get-WmiObject -class win32_operatingsystem | select -Property *
-> 'select' alias 'Select-Object'
-> Info about the current operating system

OR

PS C:\> Get-WmiObject -class win32_operatingsystem | fl *
-> same information
-> 'fl' alias 'Format-List'

PS C:\> Get-WmiObject -class win32_service | Format-List *
-> list of properties for all services

PS C:\> Get-WmiObject -class win32_service |Sort-Object -Unique PathName | fl Pathname
-> gives command line arguments nad paths to all service executables`
```
- `Export-Csv`: saves the result in CSV format
```sql
PS C:\> Get-WmiObject -class win32_operatingsystem | fl * | Export-Csv C:\host_info.csv
```
- Exploring the Registry
```sql
PS C:\> cd HKLM:\
-> Access to Windows Registry

PS HKLM:\> cd .\SOFTWARE\Microsoft\Windows\CurrentVersion\
-> cd alias Set-Location
```
- `Select-String`
```sql
PS C:\> Select-String -Path C:\users\user\Documents\*.txt -Pattern pass*
-> contains the string 'pass' in their contents
```
- `Get-Content`
```sql
PS C:\> Get-Content C:\Users\user\Documents\passwords.txt
-> show full content

PS C:\> ls -r C:\users\user\Documents -File *.txt | % {sls -Path $_ -Pattern pass* }
-> '-r' recursive
-> '-File' searchs for files %.txt
-> '%' alias 'ForEach-Object'
-> 'sls' alias 'Select-String' for '-Path' in this case
-> '$_' variable for current value in the pipeline
-> '-Pattern' search for string 'pass'
```
- `Get-Service` : info about installed `services` and identify which is vulnerable
```sql
PS C:\> Get-Service

PS C:\> Get-Service “s*” | Sort-Object Status -Descending
-> services statinf with "s"
-> descending order and sorted by 'status' property
```






















