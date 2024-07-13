![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/7daae0ed-9dce-4283-ab38-0eb3e076c025)

* Sau khi kiểm tra thì mình thấy đây là file mft

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/dd3bfca5-0222-4d72-aaf8-96339a504953)

* mình dùng `MFTCmd.exe` để dump ra và xem các file bên trong

`.\MFTECmd.exe -f .\Evidence_001 --csv evidence.csv`

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/889c7623-17cc-4cb1-a001-2c5b7f0dad86)

* Mình thử tìm file như là `flag`

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/cbcd2de2-4587-476c-896a-b30fca97d43e)

* mình tìm thấy một file `flag.txt`
* mình đọc thông tin của file đó với entrynumber: 24369 và sequencenumber: 4

`.\MFTECmd.exe -f .\Evidence_001 --de 24369-4`

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/8baa8efa-044d-4243-a420-4a6531fd5ebf)

* có một chuỗi có vẻ bị decode `gAAAAABmS9s32v5Ju181EaJhh2vYMsR6MJ31SK-9mDwgiCz3_MBWopjqqynjoY_-HNOw3tX1T3RthBZHz9ylmyqckZ0gUZ_6T7UUxprMHoCAaTV3m1q0weznBg98RL7dRVhRn0cX6Xta`
* mình không tìm thấy thông tin nào hữu ích ở trong file này nữa nên mình đã thử tìm ở file khác
* cũng tại directory đó mình tìm thấy hai file `ransom.py` và `ransom.py:key`

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/905357f4-e927-44b8-89f8-04dff5eb014b)

```
from cryptography.fernet import Fernet
import subprocess

key = subprocess.run(["powershell", "-EncodedCommand", "RwBlAHQALQBDAG8AbgB0AGUAbgB0ACAALQBQAGEAdABoACAAIgByAGEAbgBzAG8AbQAuAHAAeQAiACAALQBTAHQAcgBlAGEAbQAgACIAawBlAHkAIgA="], capture_output=True, text=True).stdout.strip()

print(key)
with open('flag.txt', 'r') as reader:
    message = reader.read()
f = Fernet(key)

encrypted_message = f.encrypt(message.encode())
print(encrypted_message)
with open('flag.txt', 'w') as writer:
    writer.write(encrypted_message.decode('ascii'))
```

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/c07dd712-c0d0-499b-b626-69a75c74ccd5)

* đoạn code trên sử dụng mã hóa Fernet để encode flag bằng key từ file key và mở file flag.txt sau khi decode
* mình sử dụng CyberChef để decode

![ảnh](https://github.com/LDV-SpaceK/NahamconCTF2024/assets/151914246/32440138-69ee-4e37-9875-0b6b11aa47dd)

`flag{a4096cd70d8859d38cf8e7487b4cd0fa}`






