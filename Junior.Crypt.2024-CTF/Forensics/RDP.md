## RDP

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/bb8d81b5-f490-4311-b3d6-12722775f07d)

## Windows forensics

* file: Windows logs

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/2f515dee-5e2f-4ec2-bc09-6fe255971ea5)

## Tool 

* Event viewer

## Overview

* An user connect via RDP(Remote Desktop Protocol), find his location

## Solution

* RDP connection info is stored in log `Microsoft-Windows-TerminalServices-RemoteConnectionManager/Operational`
* eventID 1149 - User Authentication Succeeded

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/650ee8e5-d5af-480d-975a-0dae9dc5b186)

* IP source: 103.109.92.4
* ip2location to view info of this IP address

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/c528dfa6-6d9d-40e2-8477-0ac644d26db7)

* Contry: Bangladesh

`grodno{Bangladesh}`
