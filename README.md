# Reversing ELF THM Walkthrough

ELF: Executable and Linkable Files.

## Task 1

Give Permissions and execute.
```
chmod 777 crackme1
./crackme1 
```
![Img1](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/0ae18958-067b-4ac9-a74d-ae242ac0dee4) <br>


## Task 2 

Give Permissions and check strings.
```
chmod 777 crackme2
./crackme2
strings ./crackme2
./crackme2 super_secret_password
```
![Img2](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/948bc08b-cc12-4bb5-a329-3e3914238423) <br>
![Img3](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/c31d80c1-7b45-4793-b1ef-76fb75d2f3bd) <br>


## Task 3

Give Permissions and run strings. Later, decode base64. We can use this website. [CyberChef](https://gchq.github.io/CyberChef/)

```
chmod +x crackme3
strings ./crackme3
```
![Img4](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/3cb91199-c930-4d4f-8ca5-13089e1e6150) <br>
![Img5](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/cd5b5ec6-a315-4670-bda1-d6877f5a87c1) <br>


## Task 4

Give Permissions and run strings, which suggests us to check strcmp function.
```
chmod +x crackme4
strings ./crackme4
```
![Img6](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/28fb5c54-4634-441b-b8cf-8723a562216c) <br>

We'll use gdb debugger and check functions used.
```
gdb crackme4
info functions
```
![Img7](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/0d147ae9-906e-4335-a0eb-e1b2b065f5c2) <br>

We'll now create a breakpoint at strcmp fundtion, run test and check register values.
```
b *0x0000000000400520
run test
info register
```
![Img8](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/56559d83-c955-4db3-8372-1a07ec05411f) <br>

rax and rdx register seem intersting, let's check their values.
```
x/s 0x7fffffffdda0
```
```
x/s 0x7fffffffe290
```
![Img9](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/4d4f9bb7-951e-4888-b121-b938e0bf4f3c) <br>


## Task 4

Give Permissions and run strings, which suggests us to check strcmp function.
```
chmod +x crackme5
strings ./crackme5
```
![Img10](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/d6dc71f3-ffe4-488f-b2f2-8aa77139f3e3) <br>

We'll use gdb debugger and check functions used.
```
gdb crackme4
info functions
```
![Img11](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/a9d6ae0a-0e0d-4b80-b047-0b45dad34a0c) <br>

We'll now create a breakpoint at strncmp fundtion.
```
b *0x0000000000400560
```
![Img12](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/556e5970-109e-4977-9dc9-f7127923c766) <br>

Let's run test and check register values.
rax and rcx register seem intersting, let's check their values.
```
run test
info register
x/s 0x7fffffffdd90
x/s 0x7fffffffddb0
```
![Img13](https://github.com/MajesticFires3010/Reversing-ELF-THM/assets/96762636/ddc53f02-abee-4aef-bb82-a299daf2418a) <br>

## We can easily solve rest of the tasks via Ghidra.
