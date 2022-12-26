### 0x0000000000000aa8 : main() : assembly
```c
0x0000000000000aa8 <+0>:     push   rbp
0x0000000000000aa9 <+1>:     mov    rbp,rsp
0x0000000000000aac <+4>:     lea    rdi,[rip+0x15d]        # 0xc10
0x0000000000000ab3 <+11>:    call   0x730 <puts@plt>
0x0000000000000ab8 <+16>:    call   0x8c0 <handle_msg>
0x0000000000000abd <+21>:    mov    eax,0x0
0x0000000000000ac2 <+26>:    pop    rbp
0x0000000000000ac3 <+27>:    ret  
```

### 0x00000000000008c0 : handle_msg() : assembly
```c
0x00000000000008c0 <+0>:     push   rbp
0x00000000000008c1 <+1>:     mov    rbp,rsp
0x00000000000008c4 <+4>:     sub    rsp,0xc0
0x00000000000008cb <+11>:    lea    rax,[rbp-0xc0]
0x00000000000008d2 <+18>:    add    rax,0x8c
0x00000000000008d8 <+24>:    mov    QWORD PTR [rax],0x0
0x00000000000008df <+31>:    mov    QWORD PTR [rax+0x8],0x0
0x00000000000008e7 <+39>:    mov    QWORD PTR [rax+0x10],0x0
0x00000000000008ef <+47>:    mov    QWORD PTR [rax+0x18],0x0
0x00000000000008f7 <+55>:    mov    QWORD PTR [rax+0x20],0x0
0x00000000000008ff <+63>:    mov    DWORD PTR [rbp-0xc],0x8c
0x0000000000000906 <+70>:    lea    rax,[rbp-0xc0]
0x000000000000090d <+77>:    mov    rdi,rax
0x0000000000000910 <+80>:    call   0x9cd <set_username>
0x0000000000000915 <+85>:    lea    rax,[rbp-0xc0]
0x000000000000091c <+92>:    mov    rdi,rax
0x000000000000091f <+95>:    call   0x932 <set_msg>
0x0000000000000924 <+100>:   lea    rdi,[rip+0x295]        # 0xbc0
0x000000000000092b <+107>:   call   0x730 <puts@plt>
0x0000000000000930 <+112>:   leave  
0x0000000000000931 <+113>:   ret
```

### 0x00000000000009cd : set_username() : assembly
```c
0x00000000000009cd <+0>:     push   rbp
0x00000000000009ce <+1>:     mov    rbp,rsp
0x00000000000009d1 <+4>:     sub    rsp,0xa0
0x00000000000009d8 <+11>:    mov    QWORD PTR [rbp-0x98],rdi
0x00000000000009df <+18>:    lea    rax,[rbp-0x90]
0x00000000000009e6 <+25>:    mov    rsi,rax
0x00000000000009e9 <+28>:    mov    eax,0x0
0x00000000000009ee <+33>:    mov    edx,0x10
0x00000000000009f3 <+38>:    mov    rdi,rsi
0x00000000000009f6 <+41>:    mov    rcx,rdx
0x00000000000009f9 <+44>:    rep stos QWORD PTR es:[rdi],rax
0x00000000000009fc <+47>:    lea    rdi,[rip+0x1e1]        # 0xbe4
0x0000000000000a03 <+54>:    call   0x730 <puts@plt>
0x0000000000000a08 <+59>:    lea    rax,[rip+0x1d0]        # 0xbdf
0x0000000000000a0f <+66>:    mov    rdi,rax
0x0000000000000a12 <+69>:    mov    eax,0x0
0x0000000000000a17 <+74>:    call   0x750 <printf@plt>
0x0000000000000a1c <+79>:    mov    rax,QWORD PTR [rip+0x201595]        # 0x201fb8
0x0000000000000a23 <+86>:    mov    rax,QWORD PTR [rax]
0x0000000000000a26 <+89>:    mov    rdx,rax
0x0000000000000a29 <+92>:    lea    rax,[rbp-0x90]
0x0000000000000a30 <+99>:    mov    esi,0x80
0x0000000000000a35 <+104>:   mov    rdi,rax
0x0000000000000a38 <+107>:   call   0x770 <fgets@plt>
0x0000000000000a3d <+112>:   mov    DWORD PTR [rbp-0x4],0x0
0x0000000000000a44 <+119>:   jmp    0xa6a <set_username+157>
0x0000000000000a46 <+121>:   mov    eax,DWORD PTR [rbp-0x4]
0x0000000000000a49 <+124>:   cdqe   
0x0000000000000a4b <+126>:   movzx  ecx,BYTE PTR [rbp+rax*1-0x90]
0x0000000000000a53 <+134>:   mov    rdx,QWORD PTR [rbp-0x98]
0x0000000000000a5a <+141>:   mov    eax,DWORD PTR [rbp-0x4]
0x0000000000000a5d <+144>:   cdqe   
0x0000000000000a5f <+146>:   mov    BYTE PTR [rdx+rax*1+0x8c],cl
0x0000000000000a66 <+153>:   add    DWORD PTR [rbp-0x4],0x1
0x0000000000000a6a <+157>:   cmp    DWORD PTR [rbp-0x4],0x28
0x0000000000000a6e <+161>:   jg     0xa81 <set_username+180>
0x0000000000000a70 <+163>:   mov    eax,DWORD PTR [rbp-0x4]
0x0000000000000a73 <+166>:   cdqe   
0x0000000000000a75 <+168>:   movzx  eax,BYTE PTR [rbp+rax*1-0x90]
0x0000000000000a7d <+176>:   test   al,al
0x0000000000000a7f <+178>:   jne    0xa46 <set_username+121>
0x0000000000000a81 <+180>:   mov    rax,QWORD PTR [rbp-0x98]
0x0000000000000a88 <+187>:   lea    rdx,[rax+0x8c]
0x0000000000000a8f <+194>:   lea    rax,[rip+0x165]        # 0xbfb
0x0000000000000a96 <+201>:   mov    rsi,rdx
0x0000000000000a99 <+204>:   mov    rdi,rax
0x0000000000000a9c <+207>:   mov    eax,0x0
0x0000000000000aa1 <+212>:   call   0x750 <printf@plt>
0x0000000000000aa6 <+217>:   leave  
0x0000000000000aa7 <+218>:   ret
```

### 0x0000000000000932 : set_msg() : assembly
```c
0x0000000000000932 <+0>:     push   rbp
0x0000000000000933 <+1>:     mov    rbp,rsp
0x0000000000000936 <+4>:     sub    rsp,0x410
0x000000000000093d <+11>:    mov    QWORD PTR [rbp-0x408],rdi
0x0000000000000944 <+18>:    lea    rax,[rbp-0x400]
0x000000000000094b <+25>:    mov    rsi,rax
0x000000000000094e <+28>:    mov    eax,0x0
0x0000000000000953 <+33>:    mov    edx,0x80
0x0000000000000958 <+38>:    mov    rdi,rsi
0x000000000000095b <+41>:    mov    rcx,rdx
0x000000000000095e <+44>:    rep stos QWORD PTR es:[rdi],rax
0x0000000000000961 <+47>:    lea    rdi,[rip+0x265]        # 0xbcd
0x0000000000000968 <+54>:    call   0x730 <puts@plt>
0x000000000000096d <+59>:    lea    rax,[rip+0x26b]        # 0xbdf
0x0000000000000974 <+66>:    mov    rdi,rax
0x0000000000000977 <+69>:    mov    eax,0x0
0x000000000000097c <+74>:    call   0x750 <printf@plt>
0x0000000000000981 <+79>:    mov    rax,QWORD PTR [rip+0x201630]        # 0x201fb8
0x0000000000000988 <+86>:    mov    rax,QWORD PTR [rax]
0x000000000000098b <+89>:    mov    rdx,rax
0x000000000000098e <+92>:    lea    rax,[rbp-0x400]
0x0000000000000995 <+99>:    mov    esi,0x400
0x000000000000099a <+104>:   mov    rdi,rax
0x000000000000099d <+107>:   call   0x770 <fgets@plt>
0x00000000000009a2 <+112>:   mov    rax,QWORD PTR [rbp-0x408]
0x00000000000009a9 <+119>:   mov    eax,DWORD PTR [rax+0xb4]
0x00000000000009af <+125>:   movsxd rdx,eax
0x00000000000009b2 <+128>:   lea    rcx,[rbp-0x400]
0x00000000000009b9 <+135>:   mov    rax,QWORD PTR [rbp-0x408]
0x00000000000009c0 <+142>:   mov    rsi,rcx
0x00000000000009c3 <+145>:   mov    rdi,rax
0x00000000000009c6 <+148>:   call   0x720 <strncpy@plt>
0x00000000000009cb <+153>:   leave  
0x00000000000009cc <+154>:   ret
```

### 0x000000000000088c : secret_backdoor() : assembly
```c
0x000000000000088c <+0>:     push   rbp
0x000000000000088d <+1>:     mov    rbp,rsp
0x0000000000000890 <+4>:     add    rsp,0xffffffffffffff80
0x0000000000000894 <+8>:     mov    rax,QWORD PTR [rip+0x20171d]   # 0x201fb8
0x000000000000089b <+15>:    mov    rax,QWORD PTR [rax]
0x000000000000089e <+18>:    mov    rdx,rax
0x00000000000008a1 <+21>:    lea    rax,[rbp-0x80]
0x00000000000008a5 <+25>:    mov    esi,0x80
0x00000000000008aa <+30>:    mov    rdi,rax
0x00000000000008ad <+33>:    call   0x770 <fgets@plt>
0x00000000000008b2 <+38>:    lea    rax,[rbp-0x80]
0x00000000000008b6 <+42>:    mov    rdi,rax
0x00000000000008b9 <+45>:    call   0x740 <system@plt>
0x00000000000008be <+50>:    leave  
0x00000000000008bf <+51>:    ret
```