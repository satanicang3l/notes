---
title: PowerView
parent: Active Directory Recon
layout: default
nav_order: 1
---

Get from https://github.com/PowerShellMafia/PowerSploit.\
Then import it using\
`powershell-import .\PowerView.ps1`

`Get-Domain`\
or add `-Domain` for other domain.

`Get-DomainController`\
Get the DC information.

`Get-ForestDomain`\
Returns all domain for the forest or specify a forest with `-Forest`.

`Get-DomainUser`\
Can use `-Properties MemberOf` to filter properties or `-Identity anyuser` to filter users.

`Get-DomainComputer`\
Same can use `-Properties DnsHostName`

`Get-DomainGroup`\
Return the domain group. Can use things like `| where Name -like "*Admins*" | select SamAccountName` to further filter the results.

`Get-DomainGroupMember -Identity "Domain Admins" | select MemberDistinguishedName`\
Returns which members are in Domain Admins.

`Get-DomainTrust`\
Get domain trust information.