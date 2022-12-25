# Override
If you thought [Rainfall][0] was easy, here’s a more daunting challenge. Override is last ISO that will have you search for faults present in the protected binaries, and re-build these binaries depending on their behavior. 

- #### Download [ISO here][4]

### Ressources (Important before start the project) :
| subject     | link          |
|:-----------:|------------------------|
| How Stack works | [link][2] |
| Assembly Basics | [link][3]|
| get buffer offset | [link][1]     |


### Flags:
| N°     | Name                   | Flag                        |
|:------:|------------------------|-----------------------------|
| Flag0  | just comparing numbers | level00 |
| Flag1  | shellcode | uSq2ehEGT6c9S24zbshexZQBXUGrncxn5sD5QfGL |
| Flag2  | GOT | PwBLgNa8p8MTKW57S7zxVAQCxnCpV8JqTTs9XEBv |
| Flag3  | debug logic | Hh74RPnuQ9sa5JAEXgNWCqz7sXGnh5J5M9KfPg3H |
| Flag4  | buffer overflow | kgv3tkEb9h2mLkRsPkXRfc2mHbjMxQzvb2FrgKkf |
| Flag5  | got + shell env | 3v8QLcN5SAhPaZZfEasfmXdwyR59ktDEMAwHF3aN |
| Flag6  | decode serial hashing algo | h4GtNnaMs2kZFN92ymTr2DcJHAzMfzLW25Ep59mq |
| Flag7  | intiger overflow | GbcPDRgsFK77LNnnuh7QyFYA2942Gp8yKj9KrWD8|
| Flag8  | symbol link | 7WJ6jFBzrcjEYXudxnM3kdW7n3qyxR6tk2xGrkSC|
| Flag9  | ---- | ----|


### GDB commands cheats :
- switch to intel + enable cursor scroll + set hook-stop with general details(asm, info frame, info registers, 40 address of the stack $ESP)
    ```
    set disassembly-flavor intel
    set height 0
    define hook-stop
    disass
    echo ------------------------- [FRAME] -------------------------\n
    info frame
    echo ------------------------- [REGISTERS] -------------------------\n
    info reg
    echo ------------------------- [ESP] -------------------------\n
    x/10wx $esp
    end
    ```
- .gdbinit
    ```
    set disassembly-flavor intel
    set height 0
    info fun
    ```
[0]: https://github.com/aallali/42-rainfall
[1]: https://wiremask.eu/tools/buffer-overflow-pattern-generator/
[2]: https://beta.hackndo.com/stack-introduction/
[3]: https://beta.hackndo.com/assembly-basics/
[4]: https://cdn.intra.42.fr/isos/OverRide.iso
