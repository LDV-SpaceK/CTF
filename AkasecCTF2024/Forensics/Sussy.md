# Sussy

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/1e4aa980-38f3-4f06-afbf-6b020eec078e)

## Network Forensics

* file: packet.pcapng

## Tool

* Wireshark

## Overview

* phising network dns

## Analysis

* Mở file pcapng và phân tích những bước đầu tiên:
    * Conversation
    
    ![ảnh](https://hackmd.io/_uploads/Sy5GOHNrC.png)
    
    * Protocol
    
    ![ảnh](https://hackmd.io/_uploads/ryQ8OrNH0.png)
    
* Nhìn chung thì không có quá nhiều thông tin đặc biệt, tuy nhiên khi mình nhìn vào DNS Query Name

![ảnh](https://hackmd.io/_uploads/rk84KB4S0.png)

* có rất nhiều dns query name là ở dạng hex
```
377abcaf271c000428d5bea6f0320000000000006200000000.akasec.ma
000000afc0b3fdf3a28da5f0a6ecb43084ad4350bc3b867658.akasec.ma
70b38e2640f0c586065f13ca54f177fbd45f4191f198d93d67.akasec.ma
3855d5eb988ad41fdf98e8a08490079d964add15a7b5c70510.akasec.ma
...
```
* có thể đây chính là những domain giả mạo
* mình extract tất cả các dns queries name

`tshark -T fields -e dns.qry.name -r packet.pcapng | grep akasec`

![ảnh](https://hackmd.io/_uploads/HyBlx8ESA.png)

* tuy nhiên hiện tại có rất nhiều dòng đang bị lặp lại

`tshark -T fields -e dns.qry.name -r packet.pcapng | grep akasec | uniq`

![ảnh](https://hackmd.io/_uploads/rk2UeUNrC.png)

* nếu để ý thì từ dòng đầu tiên, đây là những hex header của file 7zip

![ảnh](https://hackmd.io/_uploads/ryrZMUVS0.png)

* ghép những đoạn hex này thành 1 file

![ảnh](https://hackmd.io/_uploads/B1eX0GU4rR.png)

* mình được 1 file `new7z.7z`, tuy nhiên file này có password bảo vệ
* sử dụng hashcat crack file 7z
* lấy hash của file bằng tool
[7z2hashcat](https://github.com/philsmd/7z2hashcat.git)

`hashcat -m 11600 -a 0 7zhash.txt rockyou.txt`

* -m 11600: mode 7z
* -a 0: mode dictionary
* rockyou.txt: từ điển rockyou
* 7zhash.txt: file hash của new7z.7z

![ảnh](https://hackmd.io/_uploads/ByxZILVHR.png)

* password: `hellokitty`

* sau khi extract file này mình được một file flag.pdf, tuy nhiên file này cũng bị password protect
* mình sử dụng [web](https://www.ilovepdf.com/unlock_pdf) này để crack password
* sau khi crack

![ảnh](https://hackmd.io/_uploads/HkE9LUEHC.png)

`AKASEC{PC4P_DNS_3xf1ltr4t10n_D0n3!!}`















