# LICENSE

![image](https://github.com/user-attachments/assets/57ab35b6-4a35-4aaf-9587-e693995c0a74)

Kiểm tra file bằng exeinfo và tôi thấy rằng file này được compile bằng GCC

![image](https://github.com/user-attachments/assets/cdc3b867-b542-4698-a2ae-29e369eb801e)

Sử dụng IDA để dạo qua code 1 vòng và ta thấy rằng. Chương trình bắt ta nhập 1 đoạn key có độ dài là 17. Đoạn key này sẽ được tách ra làm 3 phần

* Phần đầu bao gồm 8 kí tự và được copy vào `dest` sau đó sẽ thông qua hàm `sub_5592815D4209` để kiểm tra
* Phần hai bao gồm 1 kí tự là `-`
* Phần ba tương tự như phần 1 và được kiểm tra bằng hàm `sub_5592815D4345`

![image](https://github.com/user-attachments/assets/50ff9b89-cb19-44e6-9dc9-510e98feacd8)
  
Với phần đầu ta thấy rằng tác giả đã mã hóa và sau đó là so sánh với `aXsl3bdxp`. 

![image](https://github.com/user-attachments/assets/3e77d507-2ec6-4b1c-8812-72347992296d)

Đây là đoạn giải mã phần đầu:

```

def find_a1(v5):
    a1 = [0] * 8  # Khởi tạo mảng a1 với 8 phần tử

    # Khôi phục giá trị trước khi XOR với 0x33
    temp = [val ^ 0x33 for val in v5]

    for i in range(8):
        if i % 3 == 2:
            a1[i] = temp[i] + 37
        elif i % 3 == 1:
            a1[i] = temp[i] - 16
        else:
            a1[i] = temp[i] ^ 0x5A

    return a1

# Chuyển đổi chuỗi ký tự v5 thành mã ASCII
v5 = [0x58,0x73,0x6C,0x33,0x42,0x44,0x78,0x50]
a1 = find_a1(v5)

print(a1)

```
Ở đây tôi có nửa đầu của flag là: `0x31,0x30,0x84,0x5a,0x61,0x9c,0x11,0x53`

Tiếp tới là nửa còn lại. Hàm này bao gồm 2 phần. Phần đầu là xử lý chữ thường, và phần tiếp theo sẽ là xử lý các kí tự còn lại.

![image](https://github.com/user-attachments/assets/cd843a70-f4bb-4863-ba85-5f523cc97088)

Nếu tinh mắt ta có thể thấy rằng phần biến đổi chữ thường họ đang lùi đi 5 đơn vị. Tức là nếu bạn nhập chữ a thì sẽ chuyển thành f trên bảng chữ cái. Logic đơn giản và vậy. Còn với phần còn lại là lùi đi 17 lần.

Đây là đoạn giải mã phần sau:

```
a = 'mzXaPLzR'
for i in a:
 if ord(i) < ord('a'):
  print(chr(((ord(i) - 0x11) - ord('A'))% 26 + ord('A')),end = '')
 else:
  print(chr(((ord(i) - 0x5) - ord('a'))% 26 + ord('a')),end = '')

  ```

Sau đó là nc vào sever để lấy flag. 

Đây là flag của bài: `TFCCTF{ac1da9096a8ad2fcb839565621bf09e892a470a6a7a0498b6259e09525096b9d}`
