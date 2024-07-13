# One Day One Letter

![342585520-1b8decf8-0127-419d-9552-7796f7bef977](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/7d3c4d0f-dba7-40db-a883-b16e21c59904)


- Recon:

sau khi xem qua hành vi của 2 server time-server và content-server ta thấy rằng time-server 


=> cơ chế của time server là đang tạo ra key và verify timestamp qua public key để tạo ra signature của timestamp đó rồi send đến content server 

```
key = ECC.generate(curve='p256')
pubkey = key.public_key().export_key(format='PEM')

class HTTPRequestHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        if self.path == '/pubkey':
            self.send_response(HTTPStatus.OK)
            self.send_header('Content-Type', 'text/plain; charset=utf-8')
            self.send_header('Access-Control-Allow-Origin', '*')
            self.end_headers()
            res_body = pubkey
            self.wfile.write(res_body.encode('utf-8'))
            self.requestline
        else:
            timestamp = str(int(time.time())).encode('utf-8')
            h = SHA256.new(timestamp)
            signer = DSS.new(key, 'fips-186-3')
            signature = signer.sign(h)
            self.send_response(HTTPStatus.OK)
            self.send_header('Content-Type', 'text/json; charset=utf-8')
            self.send_header('Access-Control-Allow-Origin', '*')
            self.end_headers()
            res_body = json.dumps({'timestamp' : timestamp.decode('utf-8'), 'signature': signature.hex()})
            self.wfile.write(res_body.encode('utf-8'))

```

+ ta có thể thông qua time server để tạo 1 pubkey hợp lệ rồi cấu hình time stamp cho server của minh gửi đến content server


+ sử dụng expose time server dùng pagekite và server đấy có chứa pubkey mà mình tạo ra lấy thông tin của domain làm timeserver

![342613912-14d12d25-98a8-4837-be83-4277434d895a](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/1e66e0d5-e34f-4061-a20f-3a4c10f1bba0)


payload 

```
from Crypto.Hash import SHA256
from Crypto.PublicKey import ECC
from Crypto.Signature import DSS


key = ECC.generate(curve='p256')
pubkey = key.public_key().export_key(format='PEM')


print(key)
print(pubkey)

while (True):
    timestamp = str(int(input("Input your time stamp: "))).encode('utf-8')
    h = SHA256.new(timestamp)
    signer = DSS.new(key, 'fips-186-3')
    signature = signer.sign(h)
    print(signature.hex())
```

=> payload để tạo ra signature ứng với từng timestamp mình input rồi public timeserver có chứa pubkey 

![342040646-9d4ff3d7-9e4a-4a6e-bdfa-9834f56f3d86](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/953e2c0d-324e-4bdb-b586-b6055cbe5b99)


=> flag: FLAG{lyingthetime}
