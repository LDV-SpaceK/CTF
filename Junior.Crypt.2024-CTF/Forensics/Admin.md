## Admin

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/676973e2-b00b-4dd5-9deb-8df5ac3e27a0)

## File forensics

file: Disk_G

## Tool

* binwalk
* DB Browser

## Solution

* check metadata file

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/ea576946-a8bb-4827-906e-438d2ec83caf)

* error: First 553 kB of file is binary zeros
* check hex of file

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/e974d475-f01f-4be0-8dc9-de9cda5a0d56)

* there was a sqlite file inside
* extract use binwalk

`binwalk -D='.*' Disk_G`

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/3cc2cddb-9abb-4617-b3b4-0cc85c2e5eb8)

* open by DB Browser

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/7aafad88-aaf9-44a8-b49d-29f29a152318)

* key's value in table person from 1-12 is DataBase_key

`grodno{DataBase_key}`




