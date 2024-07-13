## Confusion

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/bbf80f0f-937e-48a0-b4d0-2a8c29dda320)

## File forensics

* file: Doc1.docx

## Tool

* binwalk
* hashcat
* rar2john

## Overview

* A doc file contain another files

## Solution

* first,  check metadata of file

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/ee22eb93-3d06-4b27-8ff5-f2db049c763e)

* the base64 in the Description tag:

`UmFyIRoHAQC+bUHzCgEFBhAFAQHWgQA1WCtCEwMCngAEngAAeer5TYAAAANDTVTQk9GA0JPQow0KaHR0cHM6Ly93d3cuZ3JzdS5ieS/RywybbAIDVKAAAIsAIIAFAAtjdGZfa2V5LnR4dDABAAMPNei7keFMKF9ZEAP+GGyYoTmHBZLgMEldLHZvlF0UzLghX4N7U+PQ/fc0c/siAgCKwl+1/iVpBnE2sKJlR+BXdJjxcVxfGy9b+tsqQm8xLXA1VHLzKmeWpBqd0r9+mONHKJxYwA5DGMH/t6TFr8jVR16xEw4DBvoAAPoAAIAAAAJRTwVkCJh1AJEBcdHLDJtsAgNUoAAAiwAggAUAC2N0Zl9rZXkudHh0MAEAAw816LuR4UwoX1kQA/4YbJihOYcFkuAwSV0sdm+UXRTMuCFfg3tT49D99zRz+yICAIrCX7X+JWkGcTawomVH4Fd0mPFxXF8bL1v62ypCbzEtHXdWUQMFBAA=`

* after decoding

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/5669de3e-dbda-4450-8a4e-114aaa759fea)

* there is content of RAR file
* save into rar file

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/353a083b-a277-4313-8c43-5788e20275d8)

* file `ctf_key.txt` is protected, so I have to crack password
* use rar2john to extract hash from rar file

`$rar5$16$35e8bb91e14c285f591003fe186c98a1$15$39870592e030495d2c766f945d14ccb8$8$215f837b53e3d0fd`

* hashcat crack password

`hashcat -m 13000 -a 0 hash.txt rockyou.txt/rockyou.txt`

* password is `0112`

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/f1bdb1b2-0ae3-46ad-b9fd-72170519f4e6)

`grodno{ctf_zip_key}`
