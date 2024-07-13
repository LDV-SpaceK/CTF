# Exam
 ![image](https://github.com/LDV-SpaceK/angstromCTF2024/assets/138242812/c16e1de5-2f86-4db9-8fd2-92c2a1d45e68)

Xác định thông tin của file 

![image](https://github.com/LDV-SpaceK/angstromCTF2024/assets/138242812/122468a9-cd93-4ef1-b7c7-9110cfc0f0ad)

 
Ở đây ta thấy chương trình sẽ yêu cầu ta nhập input đầu vào. Và input đó sẽ được so sánh xem có lớn hơn hoặc bằng không hay không để đảm bảo ta sẽ phải nhập số dương.
Sau đó input sẽ được biến thành số âm. Giá trị của threshold là 2147483646. 

![image](https://github.com/LDV-SpaceK/angstromCTF2024/assets/138242812/6e453173-fd1c-48df-a23d-ce395fe96626)

 

Ý tưởng là tôi sẽ nhập 1 số là giới hạn của int là 2147483647 và sau khi tôi nhập giá trị của tôi sẽ nhập them 2 lần string ‘I confirm..’. Để giá trị của nó sẽ bị bị đè.

![image](https://github.com/LDV-SpaceK/angstromCTF2024/assets/138242812/14d748e3-5213-4724-bbb1-4c939c292988)

 
Đến đây tôi sẽ nc vào sever của bài và tôi có flag  là: actf{manifesting_those_fives}




# Presidential
Đoạn mà này là đoạn mà . Sau khi phân tích tôi nhận ra đoạn mã Python này làm các bước sau:
1.	Thông báo: In ra một thông báo châm biếm về an toàn bộ nhớ trong Python.
2.	Thiết lập bộ nhớ: Tạo một vùng bộ nhớ có thể đọc, ghi, và thực thi.
3.	Nhập dữ liệu: Yêu cầu người dùng nhập dữ liệu dưới dạng chuỗi hex.
4.	Ghi và thực thi: Ghi dữ liệu vào vùng bộ nhớ và thực thi nó như mã máy.
5.	Dọn dẹp: Xóa con trỏ và đóng vùng bộ nhớ.

 ![image](https://github.com/LDV-SpaceK/angstromCTF2024/assets/138242812/67159fdc-bd67-4156-bffa-cfff891c36a5)


Ý tưởng là sau tôi sẽ dùng shellcode injection. 

 ![image](https://github.com/LDV-SpaceK/angstromCTF2024/assets/138242812/09fd5c32-878b-4909-b4e9-58eddfdd1233)


Nhạp vào đoạn hex và tôi có flag là. actf{python_is_memory_safe_4a105261}


