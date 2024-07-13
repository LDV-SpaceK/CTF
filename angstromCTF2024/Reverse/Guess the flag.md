![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/91a48f83-cd5d-465d-8935-3bea1b9337c6)

* mình mở file bằng ida
* xem hàm main

![ảnh](https://github.com/LDV-SpaceK/-ngstromCTF2024/assets/151914246/7afdebb9-d67f-4ae4-83ce-18c8d5d11a0b)

```
int __fastcall main(int argc, const char **argv, const char **envp)
{
  char *v3; // rbx
  char _0[72]; // [rsp+0h] [rbp+0h] BYREF
  unsigned __int64 vars48; // [rsp+48h] [rbp+48h]

  vars48 = __readfsqword(0x28u);
  puts("Go ahead, guess the flag: ");
  v3 = _0;
  fgets(_0, 63, stdin);
  while ( strlen(_0) > v3 - _0 )
    *v3++ ^= 1u;
  if ( !strcmp(_0, secretcode) )
    puts("Correct! It was kinda obvious tbh.");
  else
    puts("Wrong. Not sure why you'd think it'd be that.");
  if ( vars48 != __readfsqword(0x28u) )
    start();
  return 0;
}
```

* chương trình cho mình nhập vào một chuỗi sau đó tiến hành xor từng kí tự với 1, sau đó so sánh với secretcode nếu đúng thì trả ra correct, sai thì wrong
```
`bugzbnllhuude^un^uid^md`ru^rhfohghb`ou^chu|
```
* mình code python để xor secretcode với 1 để xem mình phải nhập vào input nào

```
secret_code="`bugzbnllhuude^un^uid^md`ru^rhfohghb`ou^chu|"
xor_key=1
result=""
for i in secret_code:
    result+=chr(ord(i)^xor_key)
print(result)
```
* sau khi xor thì mình tìm được flag

`actf{committed_to_the_least_significant_bit}`
