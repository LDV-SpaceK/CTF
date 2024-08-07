# SIGNAL

![image](https://github.com/user-attachments/assets/34d749bb-df6f-4711-8650-7746f4e7dc73)

Kiểm tra các thông tin cơ bản của file bằng exeinfo và ta thấy rằng file này là file được compile bằng GCC

![image](https://github.com/user-attachments/assets/687de8dc-8d70-499e-a8a7-233a3492c999)

Sử dụng IDA để phân tích file. Chúng ta thấy rằng file này đang kiểm tra đối số đầy vào có bằng 2 hay không. Nếu k bằng thì in ra ?.

![image](https://github.com/user-attachments/assets/3f124692-ee25-479e-9cfb-0566e796e4fd)

Đối số thứ nhất sẽ được kiểm tra. Tại đây tôi chú ý tới hàm `gHandlears` đây là hàm sẽ kiểm tra đối số. Viết 1 đoạn script đơn giản và chúng ta có được flag.

```void __noreturn CheckInput()
{
    unsigned char expected[] = {
        98, 49, 49, 101, 56, 48, 55, 102, 54, 53, 98, 50, 55, 100, 99, 102,
        56, 50, 101, 55, 48, 99, 52, 98, 97, 100, 54, 51, 97, 51, 101, 98
    };

    for (int i = 0; i < 32; ++i)
    {
        if ((unsigned char)gInput[i] != expected[i])
        {
            puts("Nope");
            exit(1);
        }
    }

    puts("Correct!");
    exit(0);
}
````
Flag: `TFCCTF{	b11e807f65b27dcf82e70c4bad63a3eb}`
