## Series SAM

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/1a3bcc37-86db-4582-bc21-b0e84f5a0f02)

## Windows forensics

* file:
  * ntds.dit
  * SYSTEM 

## Tool

* [secretsdump.py](https://github.com/fortra/impacket/blob/master/examples/secretsdump.py)
* DSInternals

## Overview 

* After dumping 2 file SYSTEM and ntds.dit, the next task is dump user's password from them

## Solution

* The Ntds.dit file is a database that stores Active Directory data, including information about user objects, groups and group membership.
* Importantly, the file also stores the password hashes for all users in the domain
* In this case, I use tool [secretdump.py](https://github.com/fortra/impacket/blob/master/examples/secretsdump.py)

`python .\secretsdump.py -system .\SYSTEM -ntds .\ntds.dit local`

* there was a notification `NTDSHashes.__init__() got an unexpected keyword argument 'skipUser'`

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/c0dfdd45-b96f-44f7-ab64-6c32ee831af3)

* However, I still got the BootKey `0be7a2afe1713642182e9b96f73a75da`
* Base on this [blog](https://blog.netwrix.com/2021/11/30/extracting-password-hashes-from-the-ntds-dit-file/), there are another tool is DSInternals
* Its module Get-ADDBAccount can dump all user hashed password

`Get-ADDBAccount -All -DBPath .\ntds.dit -BootKey 0be7a2afe1713642182e9b96f73a75da > hash.txt`

* I found user Tilen2000 hash password
  
![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/2e820250-35bc-48d7-b3ff-e404efffdebd)

* NTHash: `c0720d115b8b326aca0d9b95f0eca86e`
* after crack, the password is `Hello123`

`grodno{Hello123}`




