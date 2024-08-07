# SURFING (EASY)

![image](https://hackmd.io/_uploads/ryutT26FA.png)
Easy nhưng không easy chút nào cả. Web sẽ nhận input của mình là 1 url nhưng chỉ nhận url bắt đầu với `http://google.com/`, và nó sẽ lấy 1 file png từ url đó. 

![image](https://hackmd.io/_uploads/rkRyAh6FA.png)
Trên html của web cũng có phần note sau. Vậy là challenge này sẽ là fetch đến localhost và login với admin để lấy flag nhưng mà url bắt đầu với `http://google.com/` thì làm sao mà fetch sang localhost được. 

Ban đầu mình nghĩ chall là command injection, đoán nó sử dụng lệnh curl để fetch nhưng test thì không được. 

Sau khi giải kết thúc mình mới biết đến cái gọi là [Google Accelerated Mobile Pages (AMP) open redirect](https://www.trustwave.com/en-us/resources/blogs/spiderlabs-blog/trusted-domain-hidden-danger-deceptive-url-redirections-in-email-phishing-attacks/)

> Google AMP là 1 open-source web component framework được sử dụng để khiến webpage load nhanh hơn trên các thiết bị di động. Nhưng bây giờ nó lại bị lợi dụng để phishing bằng các redirect. Khi người dùng click vào link thì họ sẽ bị redirect sang phishing page như ví dụ bên dưới là repl.co
![image](https://hackmd.io/_uploads/r1EIepTKC.png)

Vậy ở đây mình sẽ host 1 web mà redirect nó sang localhost port 8000 xem admin panel của challenge như thế nào. (Thử redirect nó luôn sang localhost kiểu `http://google.com/amp/s/http://localhost/...` hay `http://google.com/amp/s/localhost/...` sẽ lỗi nên host web rồi redirect nó sang localhost vậy)

Bây giờ mình sẽ host 1 web mà source code của nó sẽ redirect sang localhost của challenge.

```python=
#!/usr/bin/env python3
from flask import Flask, redirect

app = Flask(__name__)

@app.route('/')
def index():
    return redirect('http://localhost:8000/')

if __name__ == '__main__':
    app.run('0.0.0.0', port=80, debug=True)
```

Run nó trên máy ảo và sử dụng zrok để public port 80 của mình.
![image](https://hackmd.io/_uploads/HkGcSapt0.png)

Giờ mình sẽ dùng payload `http://google.com/amp/s/<zrok_url>/%23` để redirect web chall sang web của mình.

> `%23` là dấu `#`, web chall sẽ tự động thêm extension `.png` vào đuôi các url được cung cấp, và chúng ta muốn loại bỏ nó.

![image](https://hackmd.io/_uploads/H1vjSa6YA.png)

admin.php sử dụng GET method để lấy username và password. Vậy thì thay đổi source code của flask app kia để nó redirect sang `localhost/admin.php?username=admin&password=REDACTED`

Thực ra thì password của admin là `admin` luôn. Test thì cũng hơi lâu tí thui. Đăng nhập xong ta sẽ có flag.
![image](https://hackmd.io/_uploads/rymcU66FR.png)

Flag: `TFCCTF{18fd102247cb73e9f9acaa42801ad03cf622ca1c3689e4969affcb128769d0bc}`
