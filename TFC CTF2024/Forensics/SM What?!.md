## SM WHAT?!

![ảnh](https://github.com/user-attachments/assets/547bb5d4-5dc0-44ed-a177-cb91eb16dbbc)

### Windows Forensics

* file: Challenge.evtx

### Overall

* Identify the tool attacker used to connect, the service it connected to, its IP address, and the shared resources folder

### Solution

![ảnh](https://github.com/user-attachments/assets/2334165f-f782-48b8-8d0b-40fd7683e056)

* This command: `cmd.exe /Q /c cd \ 1> \\127.0.0.1\ADMIN$\__1619425227.894209 2>&1` from parent process `WmiPrvSE.exe`
* after searching, I found that the tool used to connect is Impacket's `wmiexec`

https://labs.withsecure.com/publications/attack-detection-fundamentals-discovery-and-lateral-movement-lab-5

* this tool use to share file so the service is `SMB`
* share folder is `ADMIN$`
* ip is localhost `127.0.0.1`

`TFCCTF{wmiexec_smb_127.0.0.1_admin$}`


