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




















