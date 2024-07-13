## Admin rights

![ảnh](https://github.com/LDV-SpaceK/CTF/Junior.Crypt.2024-CTF/assets/151914246/858b082a-c895-49f4-a9ee-27bd11b83efb)

## Windows forensics

* file: SAM

## Tool

* Registry explorer

## Overview

* find account has administrator rights

## Solution

* User account detail in this path `SAM\Domains\Account\Users`

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/27b7d4c5-30c9-45f5-8871-a7261af27f73)

* Groups Администраторы : Administrators
* user_7565 is in Administrators group

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/88296ec7-313b-4acd-b5e1-76c40b3f2cb5)

`grodno{user_7565}`
