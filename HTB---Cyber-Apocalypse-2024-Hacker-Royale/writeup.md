### FORENSIC
## Urgent:
* Đề bài cho chúng ta một file eml và khi mình cat ra thì có một đoạn mã base64 thì mình decode

![Screenshot 2024-03-29 203936](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/3164a97a-98b9-430e-983f-b09cff6613ab)

* Có vẻ đây là URL encode nên mình decode trên cyberchef và tìm được flag

![Screenshot 2024-03-29 204353](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/1b701b24-c067-4d53-92d4-6b8b6aa77c0e)

![Screenshot 2024-03-29 204415](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/59548d4f-f22a-41ab-8d45-e59f3ef88c30)

`Flag: HTB{4n0th3r_d4y_4n0th3r_ph1shi1ng_4tt3mpT}`

## It has begun
* Mình mở cat file script.sh thì thấy có một đoạn flag bị viết ngược user@tS_u0y_ll1w{BTH -> HTB{w1ll_y0u_St
* Sau đó mình tìm thấy một chuỗi base64, decode và tìm thấy phần cuối của flag

![Screenshot 2024-03-29 205029](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/21733d68-bba0-471d-8742-ff84307bb7c6)

`Flag: HTB{w1ll_y0u_St4nd_y0uR_Gr0uNd!!}`

## An unusual sighting
* đây là một câu trả lời question để lấy flag
* 1. What is the IP Address and Port of the SSH Server (IP:PORT)
  * Ở trong file sshd.log chúng ta có server đang listen đến một địa chỉ IP nào đó tại cổng 2221
  * Sau đó đã cố kết nối tới ip 100.107.36.130 tại port 2221
  ![Screenshot 2024-03-29 210943](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/25c119f4-7d68-4c75-8807-383e76f2b4e2)

`Answer: 100.107.36.130:2221`

* 2. What time is the first successful Login
  * Sau một số lần cố gắng kết nối đến ip đó nhưng bị sai password thì lúc 2024-02-13 11:29:50 password đã được chấp nhận

![Screenshot 2024-03-29 211343](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/41aea291-85db-4928-a322-6fe4df682978)

`Answer: 2024-02-13 11:29:50`

* 3. What is the time of the unusual Login
  * Mình nhìn trong file sshd.log thì không thấy được sự khác lạ nên mình đã thử sang file bash_history.txt và tìm thấy một số điểm khác lạ

![Screenshot 2024-03-29 212346](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/90992b2b-51ac-4bcb-931a-5fa5b506eadd)

  * Nếu mà là chủ của địa chỉ ip này thì có thể sẽ không sử dụng những lệnh như whoami, cat shadow nên khá kì lạ, đối chiếu với mốc thời gian sử dụng câu lệnh với thời gian login ở bên file sshd.log thì tìm thấy thời gian truy cập bất thường

![Screenshot 2024-03-29 212706](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/811684df-6c6c-4736-a31a-463d16fb1bcf)

`Answer: 2024-02-19 04:00:14`

* 4. What is the Fingerprint of the attacker's public key
  * cũng trong thời gian đó thì một public key được sử dụng để đăng nhập vào địa chỉ ip đó

![Screenshot 2024-03-29 212706](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/a53a4821-007b-49e7-8a2c-361d7d0a3886)

`Answer: OPkBSs6okUKraq8pYo4XwwBg55QSo210F09FCe1-yj4`

* 5. What is the first command the attacker executed after logging in
  * Câu lệnh đầu tiên khi kẻ tấn công vào là whoami

`Answer: whoami`

* 6. What is the final command the attacker executed before logging out
  * Thời gian disconect khỏi địa chỉ ip đó là 2024-02-19 04:38:17
  * Đối chiếu với câu lệnh cuối cùng trước thời gian đó là ./setup

`Answer: ./setup`

* Sau khi trả lời hết câu hỏi thì chúng ta được flag

`Flag: HTB{B3sT_0f_luck_1n_th3_Fr4y!!}`

## Fake Boost
* Sau khi mở file pcap đề cho thì mình đã tìm thấy có 3 object http và mình đã export ra

![Screenshot 2024-03-29 213832](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/220233bd-5f14-4fff-aef0-c6d31ee858d1)

* Mở file freediscordnitro.ps1 thì mình được một đoạn code

![Screenshot 2024-03-29 214046](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/1f581414-d44e-4561-9d19-d6e546168dce)

* Đoạn code này đã bị reverse và base64 encode nên mình đã đảo ngược và ra được một đoạn code powershell

![Screenshot 2024-03-29 214354](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/52bd5218-54c7-48bd-92ac-1c08759b3b99)

* Mình tìm thấy part1 bị base64 encode, decode và được: HTB{fr33_N17r0G3n_3xp053d!_

![Screenshot 2024-03-29 214519](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/51ab06e6-bbf5-4348-b2f3-c69768520887)

* Đoạn code này tạo ra một số dãy chữ random giả làm discord nitro và bên trong đó còn một đoạn code truy cập vào các trình duyệt trên máy và đánh cắp dữ liệu người dùng
* Mình tìm thấy đoạn AES key nên mình đã nghĩ đến việc part2 của flag bị mã hóa aes

![Screenshot 2024-03-29 215023](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/668f327d-32e0-4da8-9023-04a3747c7271)

* Sau khi đọc đoạn code dưới thì nó sử dụng file plaintext từ địa chỉ URL http://192.168.116.135:8080/rj1893rj1joijdkajwda và key là Y1dwaHJOVGs5d2dXWjkzdDE5amF5cW5sYUR1SWVGS2k= đã bị mã hóa base64
* trong 2 function sử dụng aes thì nó sử dụng mode CBC với độ rộng là 256
* mình đã decrypt bằng tool online https://www.devglan.com/online-tools/aes-encryption-decryption

![Screenshot 2024-03-29 215959](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/22baa982-d816-4f02-a9fb-dafb45808d79)

* Sau khi decrypt thì mình được một đoạn base64, decode ra thì được

![Screenshot 2024-03-29 220203](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/8bbb9a3c-83e1-4e27-9c12-cda30e380f69)

* decode base64 email thì ra phần cuối của flag: b3W4r3_0f_T00_g00d_2_b3_7ru3_0ff3r5}

![Screenshot 2024-03-29 220245](https://github.com/LDV-SpaceK/HTB---Cyber-Apocalypse-2024-Hacker-Royale---After-Party-/assets/151914246/4ef7fcc9-1a97-42bb-ae75-adcf79ab83e2)

`Flag: HTB{fr33_N17r0G3n_3xp053d!_b3W4r3_0f_T00_g00d_2_b3_7ru3_0ff3r5}`





