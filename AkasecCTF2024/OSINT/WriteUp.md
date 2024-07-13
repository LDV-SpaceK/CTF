# Th3Hun7 1

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/beaa32fb-6c51-4d0e-a505-7863ef9b5be9)

Ở đây tôi sẽ đọc hint mà tác giả đã cho. Có vẻ trang duy nhất của giải này.

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/81ee84f7-f4e2-4d3e-a7b0-d6afbde563c4)

Mình đã tìm kiếm với từ khóa `akasec` thì kết quả dãn tôi đến trang web có vẻ là trang chủ chính. Nhưng tôi nghĩ đây kphai là hướng đúng. Thử thay đổi từ khóa thành `akasec.club` và tôi có 1 trang có vẻ là web của giải lần này `https://www.akasec.club/`

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/83c29d4e-8f2d-48e1-9330-b000e3733ecf)

Thử mở với mã nguồn của trang web hiện tại và tôi để ý tới dòng thứ 54. 

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/e8da75db-91d6-4207-b93c-bfc947e0f904)

Ở đây ta thấy thuộc tính src chứa đường dẫn tới tệp hình ảnh. Trong trường hợp này, nó trỏ đến một tệp JPEG được lưu trữ trong thư mục tĩnh của ứng dụng Next.js. Thử pass theo đường link đó và tôi có flag đầu tiên

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/4ab4b2c5-18e1-40c4-9a0c-1a7fb6811f0c)

Flag: `AKASEC{Wh4T_a_PfP_:3}`

# Th3Hun7 2

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/013b7eb2-22d4-43c0-9722-35279e8f683d)

Tiếp tục theo luồng trên tôi thấy ở dòng 63 có đường link github là `https://github.com/l3rnds`

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/a34500ca-6504-4bb7-917e-ba3f8e2dc0db)

Ở đây tôi đã check tất cả các repo và nhận ra trong repo Minishell có 2 cái commit. 

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/93210de5-0ce0-40f0-8292-2729cbf1ac76)

Kiểm tra chúng thì tôi phát hiện ở commit của `l3rnds`, các chữu cái đầu có vẻ là `akasec`

![image](https://github.com/daglongg/ctf.akasec/assets/138242812/37562d33-363b-47af-ad27-4f0d84e7a191)

Và flag ở đây là `AKASEC{H1dd3n_fl4g_1n_C0mM!t5_1snT_Th4t_HARD_hh}`
