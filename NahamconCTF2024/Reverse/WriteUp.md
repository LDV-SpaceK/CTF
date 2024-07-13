

# IPromise

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/3d5d1287-faaa-45fd-a5c9-c9bd0f1f4e72)

Kiểm tra file bằng ExeInfo để kiểm tra thông tin file.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/a98e3965-dfdb-4ff1-be95-09a6830ca53f)

Phân tích tĩnh file và ta thấy hitn của tác giả. Kiểm tra hàm main tôi chỉ thấy hàm này k gọi bất kỳ hàm nào.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/2b32c229-c785-4bd2-8805-ddd859ddc56c)

Ở đây tôi có thấy hàm  `decryptIPromise`. Khai báo một mảng ký tự v1 với kích thước 200. Khởi tạo ngữ cảnh AES bằng cách gọi hàm AES_init_ctx(). Giải mã ba khối dữ liệu riêng biệt sử dụng AES trong chế độ ECB. Đầu tiên, giải mã dữ liệu từ &encrypted và lưu kết quả vào v1. Tiếp theo, giải mã dữ liệu từ &unk_404050 và lưu kết quả vào v1. Cuối cùng, giải mã dữ liệu từ &unk_404060, lưu kết quả vào v1 và trả về kết quả này từ hàm.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/8e5125a7-ba39-4ffb-8f02-83f5a1554dc6)

Ở đâyb ta debug và ta có flag là `flag{d41d8cd98f00b204e9800998ecf8427e}`

# Taylor's First Swift

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/89459a43-f49c-4c95-9a51-76a3162b6bf4)

Kiểm tra file bằng ExeInfo để kiểm tra thông tin file.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/e35795d3-dd30-47a5-80d6-1779b02a709e)

Ở đây tôi thấy chương trình chức năng chính là kiểm tra giá trị bằng hàm `flagcheck`. Vì đây là ngôn ngữ IOS nên tôi k thể debug được.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/318e4087-c6d9-456e-a260-b56e93db796d)

Nhìn sơ qua hàm này thì tôi thấy nó đang xor 2 chuỗi là `FRsIAQ8PVBUVEREIVERbBkURFkUIBxVQVkAYFxJfV0FYVkIVQgo=` và `swifte!` với nhau và hiển thị bằng UTF8.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/98279372-3c90-496d-a59f-3bfc6f2c1803)

Sau khi xor thì ta có flag là.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/963b25ca-5150-4d51-8283-9821f02d5ed8)

`flag{f1f4bfa202c60e2aaa9339de61513141}`

# What's in the Box?

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/bfa2a6bd-04b1-449e-8f7e-0fc3d4562217)

Kiểm tra file bằng ExeInfo để kiểm tra thông tin file.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/74e0ff5f-3a74-42c3-966d-f604d6432c1a)

Đây là file shell scrip. Mở thử file a thì tôi thấy file này đã được `This script was generated using Makeself 2.5.0`. Vậy Makeself là gì?. Đây là  một công cụ dòng lệnh mã nguồn mở dùng để tạo các tập tin tự giải nén. Đây là các script shell tự chứa, khi được chạy, sẽ giải nén nội dung lưu trữ bên trong và có thể thực thi các lệnh kèm theo nếu cần thiết. vậy tôi sẽ chạy thử cái file này. Chạy thử file và chương trình hỏi mình mã code.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/52870049-182a-4670-8ddc-0ebcbd6c29be)

Ở đây tôi dùng chức năng `--target dir` của  `Makeself`. Nó sẽ dump ra chương trình gốc. Sau khi đọc và xác định được mã pin ở đây là `1234` và tôi có flag là

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/aa230cf3-31eb-45db-bb24-b07b3bbce2e4)
`flag{da0a0a25f5b35fbf99e3351997bfc4c8}`

# A Locked Box

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/431f13dc-91cc-4dfa-8e88-5c1a38b2f1c2)

Kiểm tra file bằng ExeInfo để kiểm tra thông tin file.

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/5dc1a722-ff71-4601-890e-dc11d9d83b5c)

Đây là file shell scrip. Mở thử file a thì tôi thấy file này đã được `This script was generated using Makeself 2.5.0`. và có 1 điểm khả nghi là hàm MD5 bị null 2 giá trị 

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/f09b1c62-4d58-40d9-bf72-357ee8c243e7)

Và khi mình thực thi cái file này nó cũng hiển thị y chang. 

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/4b5451c0-3a5c-4b6d-b350-a3a1099a14c2)

Tôi sẽ fix  lại file bằng `https://hexed.it/`

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/87bd9195-dfe8-45a5-ba37-04e453dd0c20)

Thực thi file sau khi fix và tôi có flag là: `flag{3a50c5e41a1c3eee6dcddca9e04992e0}`

![image](https://github.com/daglongg/ctf.nahamcon/assets/138242812/1fd25b9a-64a6-4d16-af1b-7af24fe7631d)
