rdate -n \<dc-ip\> ***Sync localtime with DC***
  
xfreerdp /v:IP /u:USERNAME /p:PASSWORD +clipboard /dynamic-resolution /drive:/usr/share/windows-resources,share ***RDP***

$ErrorActionPreference= 'silentlycontinue' ***Hide Error in PowerShell***

Get-UserProperty -Properties logoncount | Where logoncount -ne 0 ***Filtering Powershell objects***

Get-ObjectAcl -SamAccountName Control174User –ResolveGUIDs | Where-Object {$_.IdentityReference -match "RDP"} ***Filtering Powershell objects***

ls function: ***powershell function store***

Copy-Item -ToSession $appsrv1 -Path C:\AD\Tools\Rubeus.exe -Destination C:\Users\appadmin\Downloads ***Copying to Session***
