![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/46361d2e-90b3-41dd-b1c1-094ab7cdb1a3)
 
* Trong server discord có đoạn ascii

`49 66 20 61 6E 79 6F 6E 65 20 72 65 61 64 73 20 69 74 2C 20 49 20 61 6D 20 4A 6F 6A 6F 2E 20 49 20 68 61 76 65 20 62 65 65 6E 20 63 61 70 74 75 72 65 64 20 62 79 20 61 20 67 72 6F 75 70 20 63 61 6C 6C 65 64 20 4A 33 4A 75 4A 34 2E 20 50 6C 65 61 73 65 20 63 6F 6D 65 20 61 6E 64 20 73 61 76 65 20 6D 65 21 0A 4E 30 50 53 7B 4A 30 4A 30 5F 31 73 5F 6D 31 53 35 31 6E 47 21 7D`

* Mình sử dụng CyberChef để decode

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/ff187be8-ca76-4f2d-83a4-b5673ac4274a)

`N0PS{J0J0_1s_m1S51nG!}`

## OSINT
 
![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/04465a3d-3e86-43e1-9148-a0f853cb97dd)

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/0f7b183e-4abf-4798-a666-af75006bf3e8)

* Mình sử dụng google lens và tìm được nơi bức ảnh này được đăng tải

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/e233e657-13d7-4db4-88ed-b20418b4e2cc)

* Tiêu đề là praca do comercio

`NOPS{praca-do-comercio}`

## MISC

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/d1a3b169-72f1-4ed6-813c-b2bbb848480e)

* ciphertext là một đoạn mã morse

`....- ...-- -.... ..-. -.... . -.... --... --... ..--- -.... .---- --... ....- --... .- ..--- .---- ..--- ----- ..... ....- -.... ---.. -.... ..... ..--- ----- -.... -.... -.... -.-. -.... .---- -.... --... ..--- ----- -.... ----. --... ...-- ...-- .- ..--- ----- ....- . ...-- ----- ..... ----- ..... ...-- --... -... ....- -.. ...-- ----- --... ..--- ..... ...-- ...-- ...-- ..... ..-. ....- ....- ...-- ...-- -.... ...-- ...-- ----- -.... ....- ...-- ...-- ..... ..--- ..... ..-. ..... ----- --... ..--- ...-- ----- --... -..`

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/d3d4887d-eabc-439e-87d2-5018d594dcc2)

`N0PS{M0rS3_D3c0d3R_Pr0}`

## REVERSE

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/0f008ba8-ce47-4614-a37c-096582b34599)

* kiểm tra metadata của file main

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/e0deff1c-e3f8-4296-a03d-bf6534b4c0e0)

* Đây là file elf nên mình mở bằng ida để đọc

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/32e90e43-2fe3-4fdc-9805-3cf66e1f742f)

* Trong hàm main, các thành phần của mảng s được khai báo từ 0 đến 22 là những mã ascii tương ứng, vì nó ngắn nên mình đã decode bằng tay

`N0PS{cH4r_1s_8bits_1Nt}`

## CRYPTOGRAPHY

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/f7dcd29c-1575-4634-80be-9b8dbeedc5ab)

* Mình sử dụng cipher identifier để xác định đây là loại cipher gì

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/b4d21470-45da-4ab6-963b-076a4f80acec)

* Kết quả cho thấy đây có thể là Railfence Cipher
* Mình sử dụng dcode.fr để decode với depth là 3

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/f2c000f4-4d9e-43ec-a2c3-6b58835eb232)

`NOPS{SOMETIMESAFLAGISBETTERTHANACOOKIE}`

## WEB

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/3db80ec3-242b-4f08-ab0b-01ed3e15b6a9)

* Theo đề thì có thể bài này sẽ liên quan đến cookie nên mình đã thử xem cookie của web này
* Giao diện web 

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/bca3e1cd-25ad-4a89-b883-24273a059f7a)
 
* Instruction có vẻ đang hướng dẫn thao tác đổi cookie
* Thử input username: admin

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/90792f32-78e1-4cad-bd19-10afa097ed6c)

* Decode cookie

![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/4fd84b04-04e6-4d24-8dbe-a1857a5e1d4e)

* key isAdmin đang có value là 0, đổi thành 1 và encode, đổi cookie
* Sau khi đổi cookie và refresh lại thì mình đã lấy được flag
 
![ảnh](https://github.com/LDV-SpaceK/nopsctf2024/assets/151914246/41730913-69d9-4b65-911f-8e638d3f474d)

`N0PS{y0u_Kn0W_H0w_t0_c00K_n0W}`


