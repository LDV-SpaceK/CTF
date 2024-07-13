### Packer

Điều đầu tiên là tôi sẽ xác định file này thật chất là file gì thông qua 1 tool tên là Exeinfo PE

![image](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/c518fd46-8e76-452f-b667-4061bfb9d863)


Ở đây nó đã giúp ta phát hiện ra là file này đã được UPX. Vậy UPX là gì ?
UPX - Untimate Packer for eXecutables: Là một công cụ nén và giải nén các file thực thi máy tính (executable files) trong hệ điều hành. Công dụng chính là giảm dung lương file, che dấu mã nguồn, bảo vệ chống phân tích ngược.
 => Vậy ta suy ra rằng tác giả đã sử dụng UPX để có thể che dấu mã nguồn của hệ thống.

Tôi sẽ show cho các bạn để các bạn thấy được sự khác nhau của chúng:

Đây là chương trình khi được UPX, chúng ta có thể nhận ra rằng chương trình này không có main và đang được rút gọn

![image](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/2b2cf1bd-720c-4c49-ac73-a7a17c198b6c)

Còn đây là chương trình sau khi được giải nén UPX, có đầy đủ main và các hàm khác

![image](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/3cc9cbc5-8f3e-44f9-baad-96f0385dffe5)

Đến đây việc chúng ta cần làm là xem chương trình này hoạt động như nào. Ta thấy được ở dòng 23 có 1 string và có vẻ khi chương trình yêu cầu ta nhập từ bàn phím vào thì nó sẽ so sánh với string ấy. Nếu đúng thì nó hiển thị ra string ấy. Còn nếu sai thì sẽ hiện ra là Access denied.

![image](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/eaa209f9-bd61-43c1-9817-b23ddfac0ee0)

Cho string ấy vào Cipher Identifier để xác định định dạng gốc và ta có flag là : 

![image](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/575d4f6f-9a11-44bd-96bc-2354327fb0a0)

### FactCheck

Mình cho cho file này vào exeinfo pe để xem nó là file gì

![318418677-3a3c15e5-76ac-48e6-9a9a-8ed6296d60d8](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/47434eca-c2d7-4952-863f-a013e9a0fc05)


Mình sẽ đọc file này với IDA để xem chương trình này hoạt động như nào. Ta thấy được rằng tác giả đã cho 1 nửa của flag và muốn ta hoàn thành nửa con lại.

![318419175-4b99f7aa-f95b-444b-b382-8a32b6727be9](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/725f508a-1b84-4fc2-9fa6-5acf756a05f6)


Tại dòng 91 đến dòng 109 ta thấy được các câu lệnh if. Nếu đúng với điều kiện thì ta sẽ ra được flag

![318419481-0bd007b0-e0f5-435c-b8eb-d1ac8574c113](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/d920d97b-2d4b-4411-91a1-7ce1d8b71a8c)

Tôi đã viết 1 đoạn script bằng python để mô phỏng lại cách hoạt động của các câu lệnh if và tôi có flag

![318420277-7501a3dd-55f8-4b5e-90fd-dd41b4df0d1f](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/5935be07-4836-4cfd-a1bf-86ed13443263)


### Classic_Crackme_0x100

Sử dụng công cụ exeinfo pe để xem file này file gì

![318421808-83a1a6e3-a5b3-4eec-9761-ba74733b3fc4](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/9782a0eb-f709-4178-b590-b1bed5cce929)


Có vẻ đây là 1 file bình thường. K có dấu hiệu của việc bị nén. Nên tôi sẽ cho vào IDA để phân tích tĩnh

![318422051-f619f2bc-d194-4c49-8a03-961bfc0c9832](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/b7017495-a2d9-404f-ba7d-44b215f770cf)

Hmmm. Chương trình sẽ yêu cầu ta nhập mật khẩu, sẽ mật khẩu của ta sẽ được tính toán và kết quả sẽ được so sánh với string ban đầu. Và chúng ta sẽ nc vào server của pico và nếu đúng thì ta sẽ được trả ra 1 cái flag. Vì bài này tôi làm sau giải nên ng ta đã đóng cổng kết nối. Nhưng tôi vẫn sẽ cung cấp cho các bạn đoạn script bằng python.

![318422990-9eab987c-c34f-4f53-a52d-53098d0c6c7d](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/9355ccc4-7964-4c3e-8868-cadeb8bb71a0)

Lúc này tôi đã nhập pass và tôi đã có flag

### WinAntiDbg0x100

Với bài này thì ngay từ cái tên tác giả đã gợi ý cho chúng ta biết được rằng tác giả sẽ sử dụng antidebug. Vậy antidebug là gì ?

"Antidbg" là một khái niệm trong lĩnh vực phân tích động của phần mềm và kỹ thuật phòng thủ chống lại việc phát hiện và phân tích bởi các công cụ gỡ lỗi (debugging tools) như gdb, lldb, hay WinDbg. Các kỹ thuật antidbg thường được sử dụng trong phần mềm độc hại (malware) hoặc các ứng dụng yêu cầu bảo mật cao để gây khó khăn hoặc ngăn chặn quá trình phân tích, phát hiện và ngăn chặn bởi các công cụ gỡ lỗi.

Trước khi phân tích mình sẽ dùng tool `Exeinfo PE` để xem nó là file gì. Đây là file 32 bit, tôi sẽ phân tích tĩnh nó với IDA

![320013274-eba45589-57e3-4379-96c0-a9868cb36e28](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/9d94f93c-2b6c-4b4b-a0a5-e38b5a48b6b0)


Đây là file 32 bit, tôi sẽ phân tích tĩnh nó với IDA. Nhìn qua đây tôi có thể nhìn thấy funtion `OutputDebugStringW`. Hàm này có trách nhiệm ghi lại thông tin quan trọng, cảnh báo hoặc dữ liệu debug trong quá trình chạy của ứng dụng. Khi được gọi, nội dung của chuỗi được truyền vào hàm sẽ được gửi đến bảng điều khiển gỡ lỗi. 
Và `IsDebuggerPresent` là một hàm API trong Windows API được sử dụng để kiểm tra xem một ứng dụng đang chạy có đang được gỡ lỗi hay không. Hàm này trả về TRUE nếu ứng dụng đang chạy dưới chế độ gỡ lỗi và FALSE nếu không.

![320014697-723d54f9-a2b6-462e-9bed-08f9f1ff9fd1](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/56ba92d7-514f-42d4-8be0-767ae711158c)

Chúng ta nhìn xuống thì thấy tác giả đã chú thích rõ flag nằm ở đâu. Việc của chúng ta chỉ cần vượt qua các hàm debug. Và ta có flag là `picoCTF{d3bug_f0r_th3_Win_0x100_17712291}`

### WinAntiDbg0x200

Trước khi bắt đầu thì tôi sẽ dùng tool `Exeinfo PE` để có thể biết được các thông tin cơ bản của file.

![320211158-17c4bf60-2047-4e4f-92f6-d51c2bd6d896](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/8e397e3b-983d-4488-a38c-4ed85aa8a0a9)

Tôi sẽ cho vào IDA để phân tích động nó. Ở đây tác giả đã chia ra làm 2 level, ở đây ta có thể thấy rất nhiều các hàm antidbg như
`OutputDebugStringW` và `IsDebuggerPresent`. 2 hàm này tôi đã đề cập trong phần trước.

![320211574-7213883b-b993-4f85-b6d9-02d8d14b4afd](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/0564741d-405a-4be9-9d59-07021b889b06)

Điều cần làm là chúng ta sẽ vượt qua các hàm này và tôi có flag là `picoCTF{0x200_debug_f0r_Win_ce2f78e8}`

### WinAntiDbg0x300

Trước hết tôi vẫn sẽ dùng tool `Exeinfo Pe` để check xem các thông tin cơ bản của file. File này đã được nén lại (UPX). Tác dụng của UPX thì như tôi đã để cập trước đó là dùng để ẩn đi chương trình gốc

![320213059-481971cd-8420-4a17-b671-e006d47d1646](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/f450bfbc-807c-4aef-8a3f-79e1444f478c)

 Đây là chương trình lúc chưa được UPX, 1 chương trình mà chỉ có 1 funtion duy nhất, đây cũng là dấu hiệu cho thấy chương trình đã được nén, hay được can thiệp

![320213377-84dc3a2c-0b0f-4a15-a986-e6e9acd00ca2](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/b1958904-4392-454a-b81f-6b35a1a221a2)

 Tôi sẽ dùng câu lệnh `upx -d WinAntiDbg0x300.exe` để giải né UPX. Chương trình sau khi giải nén thì rất rõ ràng. 
![320281891-410e087a-2099-4d37-bb6a-400f6a74a23a](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/530ab2f4-6b45-4b27-b68f-eabd1c3f8df2)


Tại bài này tác giả đã không gợi ý rõ ràng cho chúng ta biết flag đang nằm ở đâu. Việc chúng ta cần làm là xem từng funtion 1 chức năng là gì và làm như nào. Ở đây ta thấy được funtion `offset StartAddress`. Ở đây tác giả đã khéo léo khi giấu flag ở đây. 

![320282013-7aea0a8a-b28b-44c4-9277-bfa5b64b3f1d](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/156caa1b-2735-4731-b099-f8cb036f3735)

Vượt qua mọi thứ và ta có flag

### WeirdSnake

Cho file vào exeinfo pe để xem có điều gì bất thường không. Và ohhhhhhhhh đây là file txt chứ không phải exe. Có thể tác giả đã cố tình cho vào để đánh lạc hướng.

![318424266-214dfbaa-a881-4bce-91e6-435b14b1362a](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/3bde3a40-77f2-433a-9c78-2bfffb0b65b4)

Đổi đuôi file thành .txt và mở lên ta sẽ được 1 file có nội dung như này

![318425040-9dd009be-0461-408c-9d9b-9758e8ea32df](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/6792c793-39a9-433b-bc13-7f5228ac206e)

Với sự trợ giúp của chatGPT tôi đã xác định được đây là mã bytecode được disassemble từ một chương trình Python. Sau khi viết lại theo logic của bài ta có flag

![318425437-0b17f1a9-1918-49e1-b18f-a6269ca9e755](https://github.com/LDV-SpaceK/PicoCTF2024-Team/assets/104505732/539e4fad-c7ab-445a-b6d2-a5047572bbba)


Ở đây ta cần chú ý vài điểm như sau:
1. Phải đọc kĩ đoạn key xem nó đang đúng chưa vì khi key sai thì kết quả sẽ là 1 kết quả rất khác.
2. ChatGPT rất tuyệt nhưng chúng ta cần phải chỉnh lại 1 số thứ chứ k phải lệ thuộc vào nó.
