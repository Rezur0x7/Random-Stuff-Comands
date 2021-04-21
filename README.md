rdate -n \<dc-ip\> ## Sync localtime with DC
  
xfreerdp /v:IP /u:USERNAME /p:PASSWORD +clipboard /dynamic-resolution /drive:/usr/share/windows-resources,share ## RDP

$ErrorActionPreference= 'silentlycontinue' ## Hide Error in PowerShell

Get-UserProperty -Properties logoncount | Where logoncount -ne 0 ## Filtering Powershell objects

Get-ObjectAcl -SamAccountName Control174User –ResolveGUIDs | select ObjectDN,IdentityReference,ActiveDirectoryRights| Where-Object {$_.IdentityReference -match "RDP"} ## Filtering Powershell objects

ls function: ## powershell function store
