![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/3030620f-c8c4-4848-8321-e978ee2f8f7e)

* Sau khi giải nén file 7z mình được một file

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/bc3acc26-1bf5-4014-ae00-fb6510e354b0)

* mình kiểm tra hex của file thì đó là file vhdx

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/b2057f82-f723-4834-a921-b11306f1bc40)

* mình đổi extension và mở xem bên trong có gì(đoạn này phải nhập password: videogames đề bài đã cho sẵn)

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/c525c203-d4fe-42a1-8292-4976baf5d164)

* mình thấy rất nhiều file jpg ở trong file ổ đĩa này, kiểm tra thử vài file(sử dụng Autospy 4.21.0)

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/1a938670-8d87-45af-8459-e3732637d446)

* có những file Zone.Identifier để lưu trữ ZoneId và Url được tải về ở đâu
* lướt một lúc thì có vẻ những file ảnh này đều được tải về từ một Url là `https://imgur.com/a/gaming-wallpapers-1080p-6EPQG`
* tuy nhiên tại một bức ảnh thì mình đã thấy sự khác lạ trong url

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/559ece86-9df6-44c3-9303-74f917fee2fe)

`https://www.gamewallpapers.com/wallpapers_slechte_compressie/01wallpapers/&#102;&%23108;&%2397;&%23103;&%23123;&%2356;&%2351;&%23102;&%2350;&%2398;&%2348;&%2397;&%2356;&%2399;&%23101;&%2351;&%2357;&%23102;&%2350;&%23101;&%2353;&%2398;&%2397;&%2349;&%23100;&%2354;&%2399;&%2355;&%2348;&%23101;&%2357;&%2355;&%23102;&%2350;&%2357;&%2349;&%23101;&%23125;`

* chuỗi này có vẻ giống html entity nên mình đã thử decode bằng CyberChef

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/cc0a07e1-34ea-4a67-aa73-2e235bec8ffd)

`flag{83f2b0a8ce39f2e5ba1d6c70e97f291e}`
