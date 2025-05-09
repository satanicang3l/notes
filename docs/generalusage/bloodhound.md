---
title: Bloodhound
parent: General Usage
layout: default
nav_order: 1
---

1. Kali starts neo4j: `sudo neo4j console`
2. Kali starts bloodhound: `bloodhound`
3. Login as domain member from victim (optional):
   `runas /user:spotless@offense powershell` (if machine is domain machine)
   `runas /netonly /user:spotless@offense powershell` (if machine is non domain member)
4. Victim dot script: `. .\SharpHound.ps1`
5. Victim collect script: `Invoke-BloodHound -CollectionMethod All`
6. Drag the generated zip to the open bloodhound interface