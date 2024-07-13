![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/2e877330-c5b5-42f2-958b-83f2edffa80f)

* sử dụng gg lens để kiểm tra xem bức ảnh này có ở ở đâu không

![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/d172c1cc-5847-434c-941d-c5bf0ffb2403)

![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/d65f239c-f1a5-4ea4-be2c-d34ae7451cc3)

* tuy nhiên mình không tìm thấy bất kì thông tin nào từ gg nên mình đã chuyển hướng sang kiểm tra metadata của bức ảnh

![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/724fe1f6-0383-4fca-8515-48bcec345e49)

* không có thông tin nào đặc biệt
* mình kiểm tra xem có file nào bị ẩn trong bức ảnh không `binwalk`

![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/26d8e528-eab7-4a2b-9663-00d13d4778b8)

* kiểm tra hex của bức ảnh

![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/8c878410-6513-44f6-bf56-bcf054e8a5c0)

* mình thử sử dụng tool steganography decoder: https://futureboy.us/stegano/decinput.html

![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/19cd5be9-c5a0-44ef-ad9a-55f65b571811)

* mình được một chuỗi base58

![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/95ec4bdc-cbaf-4dda-b765-df15a9ddb12b)

`actf{crazy?_i_was_crazy_once}`
