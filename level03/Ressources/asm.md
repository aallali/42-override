
### 0x0804885a : main() : assembly
```c
0x0804885a <+0>:	push   ebp
0x0804885b <+1>:	mov    ebp,esp
0x0804885d <+3>:	and    esp,0xfffffff0
0x08048860 <+6>:	sub    esp,0x20
0x08048863 <+9>:	push   eax
0x08048864 <+10>:	xor    eax,eax
0x08048866 <+12>:	je     0x804886b <main+17>
0x08048868 <+14>:	add    esp,0x4
0x0804886b <+17>:	pop    eax
0x0804886c <+18>:	mov    DWORD PTR [esp],0x0
0x08048873 <+25>:	call   0x80484b0 <time@plt>
0x08048878 <+30>:	mov    DWORD PTR [esp],eax
0x0804887b <+33>:	call   0x8048500 <srand@plt>
0x08048880 <+38>:	mov    DWORD PTR [esp],0x8048a48
0x08048887 <+45>:	call   0x80484d0 <puts@plt>
0x0804888c <+50>:	mov    DWORD PTR [esp],0x8048a6c
0x08048893 <+57>:	call   0x80484d0 <puts@plt>
0x08048898 <+62>:	mov    DWORD PTR [esp],0x8048a48
0x0804889f <+69>:	call   0x80484d0 <puts@plt>
0x080488a4 <+74>:	mov    eax,0x8048a7b
0x080488a9 <+79>:	mov    DWORD PTR [esp],eax
0x080488ac <+82>:	call   0x8048480 <printf@plt>
0x080488b1 <+87>:	mov    eax,0x8048a85
0x080488b6 <+92>:	lea    edx,[esp+0x1c]
0x080488ba <+96>:	mov    DWORD PTR [esp+0x4],edx
0x080488be <+100>:	mov    DWORD PTR [esp],eax
0x080488c1 <+103>:	call   0x8048530 <__isoc99_scanf@plt>
0x080488c6 <+108>:	mov    eax,DWORD PTR [esp+0x1c]
0x080488ca <+112>:	mov    DWORD PTR [esp+0x4],0x1337d00d
0x080488d2 <+120>:	mov    DWORD PTR [esp],eax
0x080488d5 <+123>:	call   0x8048747 <test>
0x080488da <+128>:	mov    eax,0x0
0x080488df <+133>:	leave  
0x080488e0 <+134>:	ret    
```

### 0x08048747 : test() : assembly
```c
0x08048747 <+0>:	push   ebp
0x08048748 <+1>:	mov    ebp,esp
0x0804874a <+3>:	sub    esp,0x28
0x0804874d <+6>:	mov    eax,DWORD PTR [ebp+0x8]
0x08048750 <+9>:	mov    edx,DWORD PTR [ebp+0xc]
0x08048753 <+12>:	mov    ecx,edx
0x08048755 <+14>:	sub    ecx,eax
0x08048757 <+16>:	mov    eax,ecx
0x08048759 <+18>:	mov    DWORD PTR [ebp-0xc],eax
0x0804875c <+21>:	cmp    DWORD PTR [ebp-0xc],0x15
0x08048760 <+25>:	ja     0x804884a <test+259>
0x08048766 <+31>:	mov    eax,DWORD PTR [ebp-0xc]
0x08048769 <+34>:	shl    eax,0x2
0x0804876c <+37>:	add    eax,0x80489f0
0x08048771 <+42>:	mov    eax,DWORD PTR [eax]
0x08048773 <+44>:	jmp    eax
0x08048775 <+46>:	mov    eax,DWORD PTR [ebp-0xc]
0x08048778 <+49>:	mov    DWORD PTR [esp],eax
0x0804877b <+52>:	call   0x8048660 <decrypt>
0x08048780 <+57>:	jmp    0x8048858 <test+273>
0x08048785 <+62>:	mov    eax,DWORD PTR [ebp-0xc]
0x08048788 <+65>:	mov    DWORD PTR [esp],eax
0x0804878b <+68>:	call   0x8048660 <decrypt>
0x08048790 <+73>:	jmp    0x8048858 <test+273>
0x08048795 <+78>:	mov    eax,DWORD PTR [ebp-0xc]
0x08048798 <+81>:	mov    DWORD PTR [esp],eax
0x0804879b <+84>:	call   0x8048660 <decrypt>
0x080487a0 <+89>:	jmp    0x8048858 <test+273>
0x080487a5 <+94>:	mov    eax,DWORD PTR [ebp-0xc]
0x080487a8 <+97>:	mov    DWORD PTR [esp],eax
0x080487ab <+100>:	call   0x8048660 <decrypt>
0x080487b0 <+105>:	jmp    0x8048858 <test+273>
0x080487b5 <+110>:	mov    eax,DWORD PTR [ebp-0xc]
0x080487b8 <+113>:	mov    DWORD PTR [esp],eax
0x080487bb <+116>:	call   0x8048660 <decrypt>
0x080487c0 <+121>:	jmp    0x8048858 <test+273>
0x080487c5 <+126>:	mov    eax,DWORD PTR [ebp-0xc]
0x080487c8 <+129>:	mov    DWORD PTR [esp],eax
0x080487cb <+132>:	call   0x8048660 <decrypt>
0x080487d0 <+137>:	jmp    0x8048858 <test+273>
0x080487d5 <+142>:	mov    eax,DWORD PTR [ebp-0xc]
0x080487d8 <+145>:	mov    DWORD PTR [esp],eax
0x080487db <+148>:	call   0x8048660 <decrypt>
0x080487e0 <+153>:	jmp    0x8048858 <test+273>
0x080487e2 <+155>:	mov    eax,DWORD PTR [ebp-0xc]
0x080487e5 <+158>:	mov    DWORD PTR [esp],eax
0x080487e8 <+161>:	call   0x8048660 <decrypt>
0x080487ed <+166>:	jmp    0x8048858 <test+273>
0x080487ef <+168>:	mov    eax,DWORD PTR [ebp-0xc]
0x080487f2 <+171>:	mov    DWORD PTR [esp],eax
0x080487f5 <+174>:	call   0x8048660 <decrypt>
0x080487fa <+179>:	jmp    0x8048858 <test+273>
0x080487fc <+181>:	mov    eax,DWORD PTR [ebp-0xc]
0x080487ff <+184>:	mov    DWORD PTR [esp],eax
0x08048802 <+187>:	call   0x8048660 <decrypt>
0x08048807 <+192>:	jmp    0x8048858 <test+273>
0x08048809 <+194>:	mov    eax,DWORD PTR [ebp-0xc]
0x0804880c <+197>:	mov    DWORD PTR [esp],eax
0x0804880f <+200>:	call   0x8048660 <decrypt>
0x08048814 <+205>:	jmp    0x8048858 <test+273>
0x08048816 <+207>:	mov    eax,DWORD PTR [ebp-0xc]
0x08048819 <+210>:	mov    DWORD PTR [esp],eax
0x0804881c <+213>:	call   0x8048660 <decrypt>
0x08048821 <+218>:	jmp    0x8048858 <test+273>
0x08048823 <+220>:	mov    eax,DWORD PTR [ebp-0xc]
0x08048826 <+223>:	mov    DWORD PTR [esp],eax
0x08048829 <+226>:	call   0x8048660 <decrypt>
0x0804882e <+231>:	jmp    0x8048858 <test+273>
0x08048830 <+233>:	mov    eax,DWORD PTR [ebp-0xc]
0x08048833 <+236>:	mov    DWORD PTR [esp],eax
0x08048836 <+239>:	call   0x8048660 <decrypt>
0x0804883b <+244>:	jmp    0x8048858 <test+273>
0x0804883d <+246>:	mov    eax,DWORD PTR [ebp-0xc]
0x08048840 <+249>:	mov    DWORD PTR [esp],eax
0x08048843 <+252>:	call   0x8048660 <decrypt>
0x08048848 <+257>:	jmp    0x8048858 <test+273>
0x0804884a <+259>:	call   0x8048520 <rand@plt>
0x0804884f <+264>:	mov    DWORD PTR [esp],eax
0x08048852 <+267>:	call   0x8048660 <decrypt>
0x08048857 <+272>:	nop
0x08048858 <+273>:	leave  
0x08048859 <+274>:	ret    
```

### 0x0804885a : -----() : assembly
```c
```