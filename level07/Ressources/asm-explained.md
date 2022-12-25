
### 0x08048723 : main() : assembly
```c
0x08048723 <+0>:     push   ebp
0x08048724 <+1>:     mov    ebp,esp
0x08048726 <+3>:     push   edi
0x08048727 <+4>:     push   esi
0x08048728 <+5>:     push   ebx
0x08048729 <+6>:     and    esp,0xfffffff0
0x0804872c <+9>:     sub    esp,0x1d0
0x08048732 <+15>:    mov    eax,DWORD PTR [ebp+0xc]
0x08048735 <+18>:    mov    DWORD PTR [esp + 0x1c],eax
0x08048739 <+22>:    mov    eax,DWORD PTR [ebp+0x10]
0x0804873c <+25>:    mov    DWORD PTR [esp + 0x18],eax
0x08048740 <+29>:    mov    eax,gs:0x14
0x08048746 <+35>:    mov    DWORD PTR [esp + 0x1cc],eax
0x0804874d <+42>:    xor    eax,eax
0x0804874f <+44>:    mov    DWORD PTR [esp + 0x1b4],0x0
int ret = 0; /* esp + 0x1b4 */

0x0804875a <+55>:    mov    DWORD PTR [esp + 0x1b8],0x0
char buffer[20]; /* esp + 0x1b8 */

0x08048765 <+66>:    mov    DWORD PTR [esp + 0x1bc],0x0
0x08048770 <+77>:    mov    DWORD PTR [esp + 0x1c0],0x0
0x0804877b <+88>:    mov    DWORD PTR [esp + 0x1c4],0x0
0x08048786 <+99>:    mov    DWORD PTR [esp + 0x1c8],0x0
0x08048791 <+110>:   lea    ebx,[esp + 0x24]
0x08048795 <+114>:   mov    eax,0x0
0x0804879a <+119>:   mov    edx,0x64
0x0804879f <+124>:   mov    edi,ebx
0x080487a1 <+126>:   mov    ecx,edx
0x080487a3 <+128>:   rep stos DWORD PTR es:[edi],eax
int tab[100] = 0; /* esp + 0x24 */

    0x080487a5 <+130>:   jmp    0x80487ea <main+199>

    0x080487a7 <+132>:   mov    eax,DWORD PTR [esp + 0x1c]
    0x080487ab <+136>:   mov    eax,DWORD PTR [eax]
    0x080487ad <+138>:   mov    DWORD PTR [esp + 0x14],0xffffffff
    0x080487b5 <+146>:   mov    edx,eax
    0x080487b7 <+148>:   mov    eax,0x0
    0x080487bc <+153>:   mov    ecx,DWORD PTR [esp + 0x14]
    0x080487c0 <+157>:   mov    edi,edx
    0x080487c2 <+159>:   repnz scas al,BYTE PTR es:[edi]
    0x080487c4 <+161>:   mov    eax,ecx
    0x080487c6 <+163>:   not    eax
    0x080487c8 <+165>:   lea    edx,[eax-0x1]
    // edx = strlen(argv[i]) - 1
    0x080487cb <+168>:   mov    eax,DWORD PTR [esp + 0x1c]
    0x080487cf <+172>:   mov    eax,DWORD PTR [eax]
    0x080487d1 <+174>:   mov    DWORD PTR [esp + 0x8], edx
    0x080487d5 <+178>:   mov    DWORD PTR [esp + 0x4], 0
    0x080487dd <+186>:   mov    DWORD PTR [esp],eax
    0x080487e0 <+189>:   call   0x80484f0 <memset@plt>
    // memset(argv[i], 0, strlen(argv[i]) - 1)
    0x080487e5 <+194>:   add    DWORD PTR [esp + 0x1c], 4
    // *argv + 4 == argv[i + 1]
    0x080487ea <+199>:   mov    eax,DWORD PTR [esp + 0x1c]
    0x080487ee <+203>:   mov    eax,DWORD PTR [eax]
    0x080487f0 <+205>:   test   eax,eax
    // eax = argv[i] == 0 ?
    0x080487f2 <+207>:   jne    0x80487a7 <main+132>
    // if eax != 0
for (int i = 0; argv[i] != 0; i++) {
    memset(argv[i], 0, strlen(argv[i]) - 1);
}   
    0x080487f4 <+209>:   jmp    0x8048839 <main+278>

    0x080487f6 <+211>:   mov    eax,DWORD PTR [esp + 0x18]
    0x080487fa <+215>:   mov    eax,DWORD PTR [eax]
    0x080487fc <+217>:   mov    DWORD PTR [esp + 0x14],0xffffffff
    0x08048804 <+225>:   mov    edx,eax
    0x08048806 <+227>:   mov    eax,0x0
    0x0804880b <+232>:   mov    ecx,DWORD PTR [esp + 0x14]
    0x0804880f <+236>:   mov    edi,edx
    0x08048811 <+238>:   repnz scas al,BYTE PTR es:[edi]
    0x08048813 <+240>:   mov    eax,ecx
    0x08048815 <+242>:   not    eax
    0x08048817 <+244>:   lea    edx,[eax-0x1]
    0x0804881a <+247>:   mov    eax,DWORD PTR [esp + 0x18]
    0x0804881e <+251>:   mov    eax,DWORD PTR [eax]
    0x08048820 <+253>:   mov    DWORD PTR [esp + 0x8],edx
    0x08048824 <+257>:   mov    DWORD PTR [esp + 0x4],0x0
    0x0804882c <+265>:   mov    DWORD PTR [esp],eax
    0x0804882f <+268>:   call   0x80484f0 <memset@plt>
    0x08048834 <+273>:   add    DWORD PTR [esp + 0x18],0x4

    0x08048839 <+278>:   mov    eax,DWORD PTR [esp + 0x18]
    0x0804883d <+282>:   mov    eax,DWORD PTR [eax]
    0x0804883f <+284>:   test   eax,eax
    0x08048841 <+286>:   jne    0x80487f6 <main+211>
for (int i = 0; env[i] != 0, i++) {
    memset(env[i], 0, strlen(env[i] - 1));
}
    0x08048843 <+288>:   mov    DWORD PTR [esp],0x8048b38
    0x0804884a <+295>:   call   0x80484c0 <puts@plt>
puts("----------------------------------------------------\n"\
    "\n  Welcome to wil's crappy number storage service!   \n"\
    "----------------------------------------------------"\
    "\n Commands:                                     ");
while(true){
        0x0804884f <+300>:   mov    eax,0x8048d4b
        0x08048854 <+305>:   mov    DWORD PTR [esp],eax
        0x08048857 <+308>:   call   0x8048470 <printf@plt>
    printf("Input command: ");
        0x0804885c <+313>:   mov    DWORD PTR [esp + 0x1b4],0x1
    ret = 1;
        0x08048867 <+324>:   mov    eax,ds:0x804a040 // stding
        0x0804886c <+329>:   mov    DWORD PTR [esp + 0x8],eax
        0x08048870 <+333>:   mov    DWORD PTR [esp + 0x4],0x14 //
        0x08048878 <+341>:   lea    eax,[esp + 0x1b8]
        0x0804887f <+348>:   mov    DWORD PTR [esp],eax
        0x08048882 <+351>:   call   0x80484a0 <fgets@plt>
    fgets(&buffer, 20, stdin);
        0x08048887 <+356>:   lea    eax,[esp + 0x1b8]
        0x0804888e <+363>:   mov    DWORD PTR [esp + 0x14],0xffffffff
        0x08048896 <+371>:   mov    edx,eax
        0x08048898 <+373>:   mov    eax,0x0
        0x0804889d <+378>:   mov    ecx,DWORD PTR [esp + 0x14]
        0x080488a1 <+382>:   mov    edi,edx
        0x080488a3 <+384>:   repnz scas al,BYTE PTR es:[edi]
        0x080488a5 <+386>:   mov    eax,ecx
        0x080488a7 <+388>:   not    eax
        0x080488a9 <+390>:   sub    eax,0x1
        0x080488ac <+393>:   sub    eax,0x1
        0x080488af <+396>:   mov    BYTE PTR [esp + eax*1+0x1b8],0x0
    buffer[strlen(buffer) - 2] = 0;
        0x080488b7 <+404>:   lea    eax,[esp + 0x1b8]
        0x080488be <+411>:   mov    edx,eax
        0x080488c0 <+413>:   mov    eax,0x8048d5b // "store"
        0x080488c5 <+418>:   mov    ecx,0x5
        0x080488ca <+423>:   mov    esi,edx
        0x080488cc <+425>:   mov    edi,eax
        0x080488ce <+427>:   repz cmps BYTE PTR ds:[esi],BYTE PTR es:[edi]
        0x080488d0 <+429>:   seta   dl
        0x080488d3 <+432>:   setb   al
        0x080488d6 <+435>:   mov    ecx,edx
        0x080488d8 <+437>:   sub    cl,al
        0x080488da <+439>:   mov    eax,ecx
        0x080488dc <+441>:   movsx  eax,al
        0x080488df <+444>:   test   eax,eax
        0x080488e1 <+446>:   jne    0x80488f8 <main+469>
    if (strncmp("store", buffer, 5) == 0) {
            0x080488e3 <+448>:   lea    eax,[esp + 0x24]
            0x080488e7 <+452>:   mov    DWORD PTR [esp],eax
            0x080488ea <+455>:   call   0x8048630 <store_number>
            0x080488ef <+460>:   mov    DWORD PTR [esp + 0x1b4],eax
        ret = store_number(&tab);
            0x080488f6 <+467>:   jmp    0x8048965 <main+578>
            0x080488f8 <+469>:   lea    eax,[esp + 0x1b8]
            0x080488ff <+476>:   mov    edx,eax
            0x08048901 <+478>:   mov    eax,0x8048d61 // "read"
            0x08048906 <+483>:   mov    ecx,0x4
            0x0804890b <+488>:   mov    esi,edx
            0x0804890d <+490>:   mov    edi,eax
            0x0804890f <+492>:   repz cmps BYTE PTR ds:[esi],BYTE PTR es:[edi]
            0x08048911 <+494>:   seta   dl
            0x08048914 <+497>:   setb   al
            0x08048917 <+500>:   mov    ecx,edx
            0x08048919 <+502>:   sub    cl,al
            0x0804891b <+504>:   mov    eax,ecx
            0x0804891d <+506>:   movsx  eax,al
            0x08048920 <+509>:   test   eax,eax
            0x08048922 <+511>:   jne    0x8048939 <main+534>
    } else if (strncmp("read", buffer, 4) == 0) {
            0x08048924 <+513>:   lea    eax,[esp + 0x24]
            0x08048928 <+517>:   mov    DWORD PTR [esp],eax
            0x0804892b <+520>:   call   0x80486d7 <read_number>
            0x08048930 <+525>:   mov    DWORD PTR [esp + 0x1b4],eax
        ret = read_number(&tab);
            0x08048937 <+532>:   jmp    0x8048965 <main+578>
            0x08048939 <+534>:   lea    eax,[esp + 0x1b8]
            0x08048940 <+541>:   mov    edx,eax
            0x08048942 <+543>:   mov    eax,0x8048d66
            0x08048947 <+548>:   mov    ecx,0x4
            0x0804894c <+553>:   mov    esi,edx
            0x0804894e <+555>:   mov    edi,eax
            0x08048950 <+557>:   repz cmps BYTE PTR ds:[esi],BYTE PTR es:[edi]
            0x08048952 <+559>:   seta   dl
            0x08048955 <+562>:   setb   al
            0x08048958 <+565>:   mov    ecx,edx
            0x0804895a <+567>:   sub    cl,al
            0x0804895c <+569>:   mov    eax,ecx
            0x0804895e <+571>:   movsx  eax,al
            0x08048961 <+574>:   test   eax,eax
            0x08048963 <+576>:   je     0x80489cf <main+684>
    } else if (strncmp("quit", buffer, 4) == 0) {
        return 0;
    }
        0x08048965 <+578>:   cmp    DWORD PTR [esp + 0x1b4],0x0
        0x0804896d <+586>:   je     0x8048989 <main+614>
    if (ret != 0) {
            0x0804896f <+588>:   mov    eax,0x8048d6b
            0x08048974 <+593>:   lea    edx,[esp + 0x1b8]
            0x0804897b <+600>:   mov    DWORD PTR [esp + 0x4],edx
            0x0804897f <+604>:   mov    DWORD PTR [esp],eax
            0x08048982 <+607>:   call   0x8048470 <printf@plt>
        printf(" Failed to do %s command\n", buffer);
            0x08048987 <+612>:   jmp    0x80489a1 <main+638>
        } else {
            0x08048989 <+614>:   mov    eax,0x8048d88 // " Completed %s command successfully\n"
            0x0804898e <+619>:   lea    edx,[esp + 0x1b8]
            0x08048995 <+626>:   mov    DWORD PTR [esp + 0x4],edx
            0x08048999 <+630>:   mov    DWORD PTR [esp],eax
            0x0804899c <+633>:   call   0x8048470 <printf@plt>
        printf(" Completed %s command successfully\n", buffer);
    }
        0x080489a1 <+638>:   lea    eax,[esp + 0x1b8]
        0x080489a8 <+645>:   mov    DWORD PTR [eax],0x0
        0x080489ae <+651>:   mov    DWORD PTR [eax+0x4],0x0
        0x080489b5 <+658>:   mov    DWORD PTR [eax+0x8],0x0
        0x080489bc <+665>:   mov    DWORD PTR [eax+0xc],0x0
        0x080489c3 <+672>:   mov    DWORD PTR [eax+0x10],0x0
    bzero(buffer, 20);
        0x080489ca <+679>:   jmp    0x804884f <main+300> // LOOP
}
0x080489cf <+684>:   nop
0x080489d0 <+685>:   mov    eax,0x0
0x080489d5 <+690>:   mov    esi,DWORD PTR [esp + 0x1cc]
0x080489dc <+697>:   xor    esi,DWORD PTR gs:0x14
0x080489e3 <+704>:   je     0x80489ea <main+711>
0x080489e5 <+706>:   call   0x80484b0 <__stack_chk_fail@plt>
0x080489ea <+711>:   lea    esp,[ebp-0xc]
0x080489ed <+714>:   pop    ebx
0x080489ee <+715>:   pop    esi
0x080489ef <+716>:   pop    edi
0x080489f0 <+717>:   pop    ebp
0x080489f1 <+718>:   ret
return 0;
```

### 0x080486d7 : read_number(int *tab) : assembly
```c
0x080486d7 <+0>:     push   ebp
0x080486d8 <+1>:     mov    ebp,esp
0x080486da <+3>:     sub    esp,0x28 // 40

    0x080486dd <+6>:     mov    DWORD PTR [input],0x0
unsigned int input = 0; /* ebp-0xc */

    0x080486e4 <+13>:    mov    eax,0x8048add
    0x080486e9 <+18>:    mov    DWORD PTR [esp],eax
    0x080486ec <+21>:    call   0x8048470 <printf@plt>
printf(" Index: ");

    0x080486f1 <+26>:    call   0x80485e7 <get_unum>
    0x080486f6 <+31>:    mov    DWORD PTR [input],eax
input = get_unum(); 

0x080486f9 <+34>:    mov    eax,DWORD PTR [input]
0x080486fc <+37>:    shl    eax,0x2

    0x080486ff <+40>:    add    eax,DWORD PTR [ebp+0x8]
    0x08048702 <+43>:    mov    edx,DWORD PTR [eax]
    0x08048704 <+45>:    mov    eax,0x8048b1b // " Number at data[%u] is %u\n"
    0x08048709 <+50>:    mov    DWORD PTR [esp + 0x8],edx

    0x0804870d <+54>:    mov    edx,DWORD PTR [input]
    0x08048710 <+57>:    mov    DWORD PTR [esp + 0x4],edx

    0x08048714 <+61>:    mov    DWORD PTR [esp],eax
    0x08048717 <+64>:    call   0x8048470 <printf@plt>
printf(" Number at data[%u] is %u\n", input, tab[input]);
    0x0804871c <+69>:    mov    eax,0
    0x08048721 <+74>:    leave  
    0x08048722 <+75>:    ret
return 0;
```

### 0x08048630 : store_number(int *tab) : assembly
```c
0x08048630 <+0>:     push   ebp
0x08048631 <+1>:     mov    ebp,esp
0x08048633 <+3>:     sub    esp,0x28
// stack size : 40
    0x08048636 <+6>:     mov    DWORD PTR [ebp-0x10],0x0
unsigned int input = 0; /* ebp-0x10 */
    0x0804863d <+13>:    mov    DWORD PTR [ebp-0xc],0x0
unsigned int index = 0; /* ebp-0xc */
    0x08048644 <+20>:    mov    eax,0x8048ad3 // " Number: "
    0x08048649 <+25>:    mov    DWORD PTR [esp],eax
    0x0804864c <+28>:    call   0x8048470 <printf@plt>
printf(" Number: ");
    0x08048651 <+33>:    call   0x80485e7 <get_unum>
    0x08048656 <+38>:    mov    DWORD PTR [ebp-0x10],eax
input = get_unum();
    0x08048659 <+41>:    mov    eax,0x8048add
    0x0804865e <+46>:    mov    DWORD PTR [esp],eax
    0x08048661 <+49>:    call   0x8048470 <printf@plt>
printf(" Index: ");
    0x08048666 <+54>:    call   0x80485e7 <get_unum>
    0x0804866b <+59>:    mov    DWORD PTR [ebp-0xc],eax
index = get_unum();
    0x0804866e <+62>:    mov    ecx,DWORD PTR [ebp-0xc]
    0x08048671 <+65>:    mov    edx,0xaaaaaaab          
    0x08048676 <+70>:    mov    eax,ecx                 
    0x08048678 <+72>:    mul    edx                     // edx = 0xaaaaaaab * index = division / 3 = index / 3                   
    0x0804867a <+74>:    shr    edx,1                   // edx = edx / 2
    0x0804867c <+76>:    mov    eax,edx                 // eax = edx
    0x0804867e <+78>:    add    eax,eax                 // eax = eax *2
    0x08048680 <+80>:    add    eax,edx                 // eax = eax + edx ; eax = edx + edx / 2 ;  reverse the division
    0x08048682 <+82>:    mov    edx,ecx
    0x08048684 <+84>:    sub    edx,eax                 // edx = index - (index / 3) ; modulo
    0x08048686 <+86>:    test   edx,edx                 // == 0 ?
    0x08048688 <+88>:    je     0x8048697 <store_number+103>

    0x0804868a <+90>:    mov    eax,DWORD PTR [ebp-0x10]
    0x0804868d <+93>:    shr    eax,0x18
    0x08048690 <+96>:    cmp    eax,0xb7
    0x08048695 <+101>:   jne    0x80486c2 <store_number+146>
if ( index % 3 == 0 || (input >> 24) == 183 ) {
        0x08048697 <+103>:   mov    DWORD PTR [esp],0x8048ae6
        0x0804869e <+110>:   call   0x80484c0 <puts@plt>
    puts(" *** ERROR! ***");
        0x080486a3 <+115>:   mov    DWORD PTR [esp],0x8048af8
        0x080486aa <+122>:   call   0x80484c0 <puts@plt>
    puts("   This index is reserved for wil!");
        0x080486af <+127>:   mov    DWORD PTR [esp],0x8048ae6
        0x080486b6 <+134>:   call   0x80484c0 <puts@plt>
    puts(" *** ERROR! ***");
        0x080486bb <+139>:   mov    eax,0x1
        0x080486c0 <+144>:   jmp    0x80486d5 <store_number+165>
    return 1;
}

    0x080486c2 <+146>:   mov    eax,DWORD PTR [ebp-0xc]
    0x080486c5 <+149>:   shl    eax,0x2
    0x080486c8 <+152>:   add    eax,DWORD PTR [ebp+0x8]
    0x080486cb <+155>:   mov    edx,DWORD PTR [ebp-0x10]
    0x080486ce <+158>:   mov    DWORD PTR [eax],edx
tab[index] = input;

    0x080486d0 <+160>:   mov    eax,0x0
    0x080486d5 <+165>:   leave  
    0x080486d6 <+166>:   ret 
return (0);
```

### 0x080485e7 : get_unum() : assembly
```c
    0x080485e7 <+0>:	push   ebp
    0x080485e8 <+1>:	mov    ebp,esp
    0x080485ea <+3>:	sub    esp,0x28

    0x080485ed <+6>:	mov    DWORD PTR [input],0x0
unsigned int input;

    0x080485f4 <+13>:	mov    eax,ds:0x804a060
    0x080485f9 <+18>:	mov    DWORD PTR [esp],eax
    0x080485fc <+21>:	call   0x8048480 <fflush@plt>
fflush(stdout);

    0x08048601 <+26>:	mov    eax,0x8048ad0 // "%u"
    0x08048606 <+31>:	lea    edx,[input]
    0x08048609 <+34>:	mov    DWORD PTR [esp+0x4],edx
    0x0804860d <+38>:	mov    DWORD PTR [esp],eax
    0x08048610 <+41>:	call   0x8048500 <__isoc99_scanf@plt>
scanf("%u", input);

    0x08048615 <+46>:	call   0x80485c4 <clear_stdin>
clear_stdin();

    0x0804861a <+51>:	mov    eax,DWORD PTR [input]
    0x0804861d <+54>:	leave  
    0x0804861e <+55>:	ret
return(input);
```