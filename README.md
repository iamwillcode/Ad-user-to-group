# Ad-user-to-group
script to add user to group

$group=read-host 'Enter Group name'
$user=read-host 'Enter user name'
$grp=Get-ADGroup -Filter {name -eq "$group"} |select -exp samaccountname |Out-GridView -Title  'choose a group' -PassThru
$usr=Get-ADuser -Filter {name -eq "$user"} |select -exp samaccountname |Out-GridView -Title  'choose a user' -PassThru
Try{
$ErrorActionPreference="stop"
 Add-ADGroupMember -Identity $grp -Members $usr -verbose
 }
 Catch
 {
 Write-host $_ $Error[0] -ForegroundColor REd
 }
