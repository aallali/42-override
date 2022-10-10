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
| Flag1  | ---- | uSq2ehEGT6c9S24zbshexZQBXUGrncxn5sD5QfGL |
| Flag2  | ---- | ----|
| Flag3  | ---- | ----|
| Flag4  | ---- | ----|
| Flag5  | ---- | ----|
| Flag6  | ---- | ----|
| Flag7  | ---- | ----|
| Flag8  | ---- | ----|
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

[0]: https://github.com/aallali/42-rainfall
[1]: https://wiremask.eu/tools/buffer-overflow-pattern-generator/
[2]: https://beta.hackndo.com/stack-introduction/
[3]: https://beta.hackndo.com/assembly-basics/
[4]: https://cdn.intra.42.fr/isos/OverRide.iso
