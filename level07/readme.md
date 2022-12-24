### notes
```c
0x08048879  main
0x08048748  auth
```
---
### 0x08048879 : main() : disassembly
- notebook: (to convert `hex` to `dec` and assign variable names for better reading)
```c
// 0x50 ... 80
// 0x1c ... 28
// 0x4c ... 76
// 0x20 ... 32
// 0x2c ... 44
// 0x28 ... 40
char *loginBuffer = esp+44
int serialBuffer = esp+40
```
```c

```


### Code Prediction
```c
int auth(login, serial) {

}
int main(int argc(ebp + 8), char **argv(ebp+12)) {

	return 0
}
```

### Stack Illustration
N/A

### Process of the Exploit
-
##### debug process

---

### Solution :
- enter the login with its equivalent serial to access the shell.

```shell
```
|**`flag : GbcPDRgsFK77LNnnuh7QyFYA2942Gp8yKj9KrWD8`**
---

### Ressources :
N/A