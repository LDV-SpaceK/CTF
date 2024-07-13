# bad Worker 

![image](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/889915c4-ffc9-471e-a74f-54c7c7033d70)


- bài này ta có 2 cách để làm:

=> check chức năng của web trong đó có chức năng fetch data thì ta nhận được flag 

![image](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/90016a79-df54-4cfa-9409-0150dbb0c5fc)


=> ta có thể check qua source ctrl u thì ta thấy chức năng 

![image](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/eacbb71c-7124-4784-a238-096db72c8652)


```
<script>navigator.serviceWorker.register('service-worker.js');</script>
```

check qua path thì ta thấy được 2 file FLAG.txt và dummy.txt thì chạy path FLAG.txt thi ta được

=> flag=FLAG{pr0gr3ssiv3_w3b_4pp_1s_us3fu1} 
