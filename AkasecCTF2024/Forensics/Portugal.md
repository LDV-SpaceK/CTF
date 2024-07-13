# Portugal

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/2add226e-a30a-4a29-9f61-0469ce1dd51e)

## Memory Forensics

* file: memdump1.mem

## Tools

* Volatility3

## Overview

* Kẻ tấn công lợi dụng lúc nạn nhân rời khỏi máy mà không khóa đã thực hiện những hành vi tìm kiếm thông tin tại máy nạn nhân

## Analysis

* Sử dụng volatility3 để phân tích những thông tin cơ bản

`vol -f .\memdump1.mem windows.info`

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/7d07b21b-2b0c-41b2-9057-f0f43e13fba0)

* phân tích các process

`vol -f .\memdump1.mem windows.pslist`

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/87d4d5e4-6825-4b29-9339-44c1e34e9af1)

* tại đây có 8 process chrome.exe, chrome là công cụ tìm kiếm nên có thể đây là nơi kẻ tấn công hành động
* mỗi trình duyệt đều lưu lại những gì người dùng tìm kiếm, truy cập, tải xuống trong file History
* tìm kiếm file History trong mem

`vol -f .\memdump1.mem windows.filescan.FileScan | findstr /I 'History'`

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/063a765a-f590-40be-9225-94c681b5b68b)

* file History của trình duyệt Chrome đã được tìm thấy ở offset `0x81595680`
* dump file ra để phân tích

`vol -f .\memdump1.mem -o C:\Users\XIII\Downloads windows.dumpfiles --virtaddr 0x81595680`

* sau khi dump tại địa chỉ đó, mình có hai file 

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/37cd5194-3581-4db4-a1c3-dff259b2e73e)

* đọc nội dung file

`strings file.0x81595680.0x98570f60.DataSectionObject.History.dat`

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/4ea14b32-90d6-455e-bd9c-8a226b87ab3c)

* mình đã thấy đoạn flag bị phân tách
* đó là những gì kẻ tấn công đã search bằng google, bằng chứng là có rất nhiều url

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/8cf9771d-5c2b-468c-adc8-26af40a5a5fc)

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/926e5fba-e9e1-4496-b459-911ed5503116)

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/0d7d1981-7196-4cae-a773-4bbff36abc07)

`AKASEC{V0L4T1L1TY_f0r_chr0m3_s34rch_h1st0ry}`






















