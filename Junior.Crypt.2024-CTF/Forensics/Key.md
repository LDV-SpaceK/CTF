## Key

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/3fca20d9-8909-4685-9e8f-13ad7841bd83)

## File Forensics

* file: __ctf_key.exe

## Tool

* binwalk
* hashcat

## Solution

* When I use `strings __ctf_key.exe`, in the last of file, there are a xml code and content of a rar file

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/1acd7f07-4d91-462c-9e54-6110c382bbf9)

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/6fd401ef-697b-4740-9ad6-ebea10627581)

* So I binwalk extract rar file from exe file

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/5f350b52-d176-4b23-9629-b909a9644a10)

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/d9fa8535-941a-452e-b902-042065e99ece)

* inside file 6E600.rar is ctf_key.rar, but this file was password protected, so I decide to bruteforce this password using hashcat and rockyou.txt
* but somehow, I cant break the rar key, so I remember the last challenge, the password was 4-digit number
* bruteforce from 0-9999 and got the key: `0152`

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/f0fdbb2f-f9d8-47da-96d1-7cb7325ea5f5)

`grodno{ctf_not_zip_key}`
