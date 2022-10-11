
### notes
```c
0x08048494  main
```

### 0x08048529 : main() : disassembly
- notebook: (to convert `hex` to `dec` and assign variable names for better reading)
```c

{
    int argc = ebp+0x8
    char **argv = ebp+12

    char *buffer1 = esp+28

    0x20 ... 32
    0x1c ... 28
    0x149c ... 5276
}
```
* __`<0> ➜ <+6> : prepare stack frame for main function with size 32`__
```c
0x08048494 <+0>:	push   ebp
0x08048495 <+1>:	mov    ebp,esp
0x08048497 <+3>:	and    esp,0xfffffff0
0x0804849a <+6>:	sub    esp,32
```
* __`<+9> ➜ <+40> : print to screen with puts`__
```c
0x0804849d <+9>:	mov    DWORD PTR [esp],0x80485f0
0x080484a4 <+16>:	call   0x8048390 <puts@plt>
0x080484a9 <+21>:	mov    DWORD PTR [esp],0x8048614
0x080484b0 <+28>:	call   0x8048390 <puts@plt>
0x080484b5 <+33>:	mov    DWORD PTR [esp],0x80485f0
0x080484bc <+40>:	call   0x8048390 <puts@plt>
print this to screen
***********************************
* 	     -Level00 -		  *
***********************************
```
* __`<+45> ➜ <+53> : print "password" to screen`__
```c
0x080484c1 <+45>:	mov    eax,0x804862c
0x080484c6 <+50>:	mov    DWORD PTR [esp],eax
0x080484c9 <+53>:	call   0x8048380 <printf@plt>
printf("Password:")
```
* __`<+58> ➜ <+74> : read a number from user and save it to buffer1`__
```c
0x080484ce <+58>:	mov    eax,0x8048636 // "%d"
0x080484d3 <+63>:	lea    edx,[buffer1]
0x080484d7 <+67>:	mov    DWORD PTR [esp+4],edx
0x080484db <+71>:	mov    DWORD PTR [esp],eax
0x080484de <+74>:	call   0x80483d0 <__isoc99_scanf@plt>
sscanf("%d", buffer1);
```
* __`<+79> ➜ <+119> : execute shell if the number taken from user is 5276 or return 0`__
```c
0x080484e3 <+79>:	mov    eax,DWORD PTR [buffer1]
0x080484e7 <+83>:	cmp    eax,5276
0x080484ec <+88>:	jne    0x804850d <main+121>
0x080484ee <+90>:	mov    DWORD PTR [esp],0x8048639 // "\nAuthenticated!"
0x080484f5 <+97>:	call   0x8048390 <puts@plt>
0x080484fa <+102>:	mov    DWORD PTR [esp],0x8048649 // "/bin/sh"
0x08048501 <+109>:	call   0x80483a0 <system@plt>
0x08048506 <+114>:	mov    eax,0
0x0804850b <+119>:	jmp    0x804851e <main+138>
if (buffer1 == 5276) {
    puts("\nAuthenticated!");
    system("/bin/sh");
} else {
    return (0)
}
```
* __`<+121> ➜ <+128> : print "\nInvalid Password!" to screen with puts function`__
```c
0x0804850d <+121>:	mov    DWORD PTR [esp],0x8048651
0x08048514 <+128>:	call   0x8048390 <puts@plt>
puts("\nInvalid Password!");
```
* __`<+133> ➜ <+139> : return 1`__
```c
0x08048519 <+133>:	mov    eax,1
0x0804851e <+138>:	leave  
0x0804851f <+139>:	ret
return (1);
```

---

### Code Prediction 
```c
int main(int argc(ebp+0x8), char **argv(ebp+12)) {

    int buffer1;

    puts("***********************************");
    puts("* \t     -Level00 -\t\t  *");
    puts("***********************************");

    printf("Password:");
    sscanf("%d", buffer1);

    if (buffer1 != 5276)
        return (0)
    
    puts("\nAuthenticated!");
    system("/bin/sh");

    return (1);
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
+-------------------+ <---EBP
[and esp,0xfffffff0 ] <--- stack alignement 
+-------------------+ +32 <------+
[                   ]            | buff1 
+-------------------+ +28 <------+
[                   ]
+-------------------+ +24
         *
         *
         *
+-------------------+ +8
[      &buffer1     ]
+-------------------+ +4
[     "/bin/sh"     ]
+-------------------+ <---ESP
```

---

### Process of the Exploit
- as you can see in the program simply takes a number from the user input and compare it to **5276** and execute shell otherwise print return and exit function

---

### Solution :

```shell
level00@OverRide:~$ ./level00 
***********************************
* 	     -Level00 -		  *
***********************************
Password:5276

Authenticated!
$ pwd
/home/users/level00
$ cd /	
$ cd /home	
$ cd users
$ cd level01
$ cat .pass
uSq2ehEGT6c9S24zbshexZQBXUGrncxn5sD5QfGL
$ su level01
Password: 
RELRO           STACK CANARY      NX            PIE             RPATH      RUNPATH      FILE
Partial RELRO   No canary found   NX disabled   No PIE          No RPATH   No RUNPATH   /home/users/level01/level01
level01@OverRide:~$
```
---

### Ressources :

N/A