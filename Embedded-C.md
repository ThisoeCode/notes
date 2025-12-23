# Thisoe's C & Linux Note

_[<< Back to Thisoe's Note](./README.md)_

- Course from [OJ Tube](https://www.youtube.com/playlist?list=PLz--ENLG_8TMdMJIwyqDIpcEOysvNoonf OJ Tube - C언어 강의) (lang: KR)

*******

# Menu

- 1\. Intro

- [2. Linux](#ep2-linux)
> Bash <br> Vim <br> `gcc`

- [3. Variables](#ep3-variables)
> Data types

- [4. Constants](#ep4-constants)
> `gdb` <br> view Assembly code <br> Calcullating operations

- [5. Operators](#ep5-operators)
> Priorities <br> Bit operators

- [6. Bit Operations](#ep6-bit-operations-for-embedded-programming)
> Lighting a bulb<br>Type Converting

- [7. `if` `else`, `switch` `case`](#ep7-if-else-switch-case)
> `scanf()`<br>String

- [8. Loops](#ep8-loops)
> `for`, `while`, `do`...`while`

- [9. Loops 2, Function](#ep9-function)
> `continue`, `break`<br>`goto`<br>Function

- [10. Pointer](#ep10-pointer)
> Array<br>Pointer datatype and operator





*******



## [Ep.2](https://youtu.be/Fzd5MEjXOLE) Linux

### Linux beginner's bash commands
```bash
sudo xxx  # admin prefix
su -      # login as root
sudo passwd root  # change root password

cd /    # move to top dir
cd ~    # move to `/home/user/` or `/root/`
cd proj # use TAB to auto finish name => cd project/

ls    # list files and dirs under current dir
ls -l # ... with details
pwd   # return current path

mkdir acme  # make new dir
rm -rf acme # force remove everything under the dir

man rm  # help
```

### Ubuntu
```bash
apt-get update      # update apps from Ubuntu server store

apt-get install vim # Vi is ver.1, Vim is ver.2
> y

apt-get install gcc # GCC is the Linux compiler
> y
gcc # test: if is installed successfully, return `gcc: fatal error: no input files`
```

### Vim

Create file if not exist:
```bash
vi hello.c
```

After entering the editor, press `i` to start inserting (editing) the file.

Press `Esc` to exit editing. Then:<br>
`:w` - save<br>
`:q` - quit<br>
`:q!` - quit without saving

Combinations are OK, e.g. `:wq` - save then quit

### gcc

```bash
gcc hello.c # compiles and outputs an `a.out` executable
./a.out     # runs the exe
```

Full options: `gcc -o &lt;output-file-name&gt; &lt;input&gt;
> E.G.
> ```bash
> gcc -o test hello.c
> ```

### viewing files
```bash
cat hello.c     # returns the file content
hexdump hello.c # see ASCII code of the file content
xxd hello.c     # ... a better `hexdump`
```

### C
Including Standard Input-Output head file
```c
#include <stdio.h>
```
> In Linux, the `stdio.h` file is at `/usr/include/`.



*******



## [Ep.3](https://youtu.be/hwW9l0N5QdE) Variables

### `printf` function
```c
printf("%d\n", 3);    // 3    (with +-)
printf("%u\n", 123);  // 123  (without +-)
printf("%c\n", 'b');  // b
printf("%f\n", 12.3); // 12.300000
printf("%X\n", 15);   // F
printf("%x\n", 15);   // f
```

### data types
[wiki](https://en.wikipedia.org/wiki/C_data_types "C data types")

- Integers:

`int`: 4 byte int<br>
`unsigned int`: 0 ~ 4294967295

`long`: 16 bit (4 byte) int<br>
`long long`: 64 bit (8 byte) int

- Characters:

`char`: a 1 byte ASCII
```c
printf("%d\n", 97);  // 3
printf("%u\n", 97);  // a
```

`unsigned int`: 0 ~ 4294967295

- Decimals:

The storage and calculation method is different from (slower than) int.

`float`: 4 byte decimal<br>
`double`:
```c
printf("%.20f\n", 0.1 + 0.2); // 0.1 + 0.2 = 0.30000000000000004441
```

### Summary
```c
// data_type.c
#include <stdio.h>

void main(){
  int i=1;
  unsigned int ui=2;

  char c=3;
  unsigned char uc=4;

  short s=5;
  unsigned short us=6;
  long l=7;
  unsigned long ul=8;

  float f=9.0;
  double d=11.0;

  long long ll=12;
  unsigned long long ull=13;

  printf("%d\n",i);
  printf("%u\n",ui);
  printf("%d\n",c);
  printf("%hd\n",uc);

  printf("%d\n",s);
  printf("%d\n",us);
  printf("%ld\n",l);
  printf("%lu\n",ul);

  printf("%f\n",f);
  printf("%lf\n",d);
  printf("%lld\n",ll);
  printf("%llu\n",ull);
}
```

> "More principles you know, more easy computer science seems." -- OJ Tube



*******



## [Ep.4](https://youtu.be/ajoQujYfVl0) Constants

### Cross Compiler
Programs compiled by `gcc` only runs in Linux CPU, but cannot run in IOT / embedded CPUs; <br>
`gdb` can.

> `gdb` is also for:
> - run debugs
> - view Assembly src

```bash
apt-get install gdb
> y
```

### Use `gdb`

To prepare the use of `gdb`, add `-g` option to `gcc` which adds debugging information into the executable.
```bash
gcc -g data_type.c -o debug.exe
gdb debug.exe

(gdb) run # runs the exe

(gdb) l # view src code (first 10 lines)
(gdb) l 20 # view src code (line 15 ~ 24)
(gdb) l main # view `main` function
(gdb) # Enter to view 10 more lines

(gdb) b 21 # set a breakpoint at line 21
(gdb) run # stops at the breakpoint
# Breakpoint 1, main () at data_types.c:21
# 21        printf("%d\n",i);

(gdb) p i # view the value of var `i`
# $1 = 1
(gdb) p uc
# $2 = 4 '\004'
(gdb) p d
# $3 = 11

(gdb) q # quit
```

### Understand the "Physics" of Variables

View Assembly code:
```bash
(gdb) disas main
# Dump  of assembler code for function main:
#   0x0000555555555149 <+0>:     endbr64
#   0x0000555555555155 <+12>:    movl   $0x1,-0x34(%rbp)
#   ...
```

E.G.
For `int i = 1;`, the value is `0x1` which is "1", and is stored at physical location `-0x34`.<br>
⭐ So it's safe to say that variable names stand for physical locations (pointer) under the hood.

> **Bonus** 
> In C, to print out the location:
> ```c
> printf("%p\n", &a);
> ```
> - `&` is "address-of operator";
> - `%p` stands for Pointer datatype.

### `sizeof`
```c
#include <stdio.h>
int main(){
  int a=8;
  printf("Val of \"a\": %d;\nSize: %ld\n\n",a,sizeof(a));
  return 0;
}
```

### Constants

When running, the constants are stored in different physical part than variables in memory.<br>
**Constants** -- in Text Segment (or Code Segment) i.e. *read only* segment;<br>
**Variables** -- in Data Segment where vars can be modified during program execution.
 
> Constants Naming:
> - Cannot start with numbers;
> - Reserved keywords NG;
> - `-` NG; operation characters NG.

`const` variables cannot be changed.<br>
Also use `#define` defines contants.<br>
`#ifdefine` (maybe mention in later Ep.s)<br>
// TODO: Make a link of `#ifdefine` when mentioned

Difference:<br>
`const` is an unchangeable var stored in read-only memory;<br>
`#define`: before compiling, the defined const is directly "rewritten" to the set value.

E.g.
```c
// config
const int eyeNum = 2;
#define EYES 233;

// in-code
int catEye = eyeNum;
int dogEye = eyeNum;
int flyEye = EYES; // -> int flyEye = 233;
```

### Calcullating & Comparison Operations
```c
int a = 2 + 3;
int b = 2 - 1;

int c = 1;
int d = 3;
int f = c + d;

int m = 2 * 3;
int n = 15 / 4; // n = 3

int x = 3%1; // 0
int y = 3%2; // 1
int z = 3%3; // 0

// Example usage
int kk = 57;

printf("/ 10 : %d", kk/10); // cut one digit => 5
printf("%% 10 : %d", kk%10); // get the last digit => 7
```
- `x++` return x then plus 1;
- `++x` return x+1 and also let x plus 1;
- `x--` return x then minus 1;
- `--x` return x-1 and also let x minus 1.



*******



## [Ep.5](https://youtu.be/m_qObdtatVg) Operators

```c
// Calculating Operators 산술
+
-
*
/
%

// Assignment
=

// Logical Operators 논리
||
&&
>
<
>=
<=
==

// Bit Operators 비트 연산자
|
&
<<
>>
^ // XOR

// Ternary Operator 삼항 연산자
? :

// Funcs
sizeof()
```

### Order of Operations

> **It is MUCH BETTER to use `()` in real codes instead of remembering the priority list.**
> 
> With `()`, others can better understand your code, and also we get less bugs and much easy to debug.

- 1
```c
x++
x--
()
[]
. // (obj)
-> // (pointer)
(type){value}
```
<br>

- 2
```c
++x
--x
+x // posite x
-x // negate x
! // bool NOT
~ // bit NOT (flip bit)
(type)
*x // (pointer)
&x // address of `x`
sizeof()
```
<br>

- 3<br>
`*`<br>
`/`<br>
`%`<br>

- 4<br>
`+`<br>
`-`<br>

- 5<br>
`<<`<br>
`>>`<br>

- 6<br>
`<`<br>
`<=`<br>
`>`<br>
`>=`<br>

- 7<br>
`==`<br>
`!=`<br>

- 8<br>
`&`<br>

- 9<br>
`^`<br>

- 10<br>
`|`<br>

- 11<br>
`&&`<br>

- 12<br>
`||`<br>

- 13<br>
`? :`<br>

- 14
```c
=
+=
-=
*=
/=
%=
<<=
>>=
&=
^=
|=
```
<br>

- 15<br>
`,`
```c
// E.g.
int i,j;
for (i = 0, j = 10; i < j; i++, j--) {
  printf("%d %d\n", i, j);
}
```
<br>

> `a = falseFunc() && trueFunc()`
> 
> `b = trueFunc() || falseFunc()`
>
> In these situations, the second part is IGNORED (functions will not run).

### Bit Operators

> Bit operators are a MUST LEARN for embedded programming.

```c
char a = 8;
char b = 4;
char c = 24;
```
In this situation:
- `a` is `0000 1000`
- `b` is `0000 0100`
- `b` is `0001 1000`

1. `|`
```c
char a = 8;
char b = 4;
char c;
c = a | b; // 12

0000 1000
 |
0000 0100
 =
0000 1100
```

2. `&`
```c
char a = 8;
char b = 4;
char c;
c = a & b; // 0

0000 1000
 |
0000 0100
 =
0000 0000
```

3. `<<`
```C
char a = 24;
char x;
x = a << 1; // 48

0001 1000
 <<
 =
0011 0000
```

4. `>>`
```C
char a = 24;
char x;
x = a >> 1; // 48

0001 1000
 >>
 =
0000 1100
```

> For **unsigned** or **positive** values:
> 
> `b = a << 1;` is equivalent to `b = a * 2;`<br>
> `b = a >> 1;` is equivalent to `b = a / 2;`
> 
> For the CPU's pov, the `<<` and `>>` operators are MUCH FASTER than `*` and `/`.
> 
> > ChatGPT's comment:
> > 
> > "Modern optimizers (like GCC) detect constant powers of two and replace them into bit operation automatically."
> > 
> > "E.g. `b = a / 8;` shifts right by 3 bits."



*******



## [Ep.6](https://youtu.be/h4YXQxKcpwI) Bit Operations for Embedded Programming

### Lit a bulb with `|`

Say we have a chip `a` with 8 pins linked to 8 light bulbs, and has `0x30` as the current value.
```c
unsigned char a = 0x30; // 0b00110000
```
This means that the 5th & 6th bulbs are on.

Now we want the 4th bulb to lit up. We do:
```c
a |= (1 << 3);

// (equivalent to)
a = a | (1 << 3);
```
First, `(1 << 3)` is to move `0b0001` left 3 digits, i.e. `0b0100`.

Then we `|` to `a`:
```c
     a = 0b00110000;
 orVal = 0b00001000;
result = 0b00111000;
```
So as a result of `a |= (1 << 3);`, the 4th bulb is lit and others stay the same.

### "Flipping" Operator `~` (Logical NOT)

```c
unsigned char x;
x = 0b00001000;
x = ~x;
//x=0b11110111
```

### Turn off a bulb with `&`

Say now the `a` chip is:
```c
unsigned char a = 21; // 0b00010101
```

Let's turn off the 3rd bulb. We do:
```c
a &= ~(1 << 2);
```

Breakdown:

From `1 << 2` we get `0b00000100`;<br>
then flip it to get only 3rd one is off;<br>
finally with `&`:
```c
prepare = 0b00000100;
 andVal = 0b11111011;
      a = 0b00010101;
 result = 0b00010001;
```
So that we cleared only bit 3, leaving others unchanged.

### `? :` Operator
```c
int a = 3;
int b = 2;
(a>b) ? printf("yay\n") : printf("nope\n");

// yay
```

> In C, there is no bool type.<br>
> `0` is CONSIDERED AS falsy; all other numbers are truthy.

### `sizeof()`
```c
#include <stdio.h>

void main(){
  int a;
  char b;
  double c;
  int d[5];

  printf("%ld\n",sizeof(a)); // 4 (bytes)
  printf("%ld\n",sizeof(b)); // 1
  printf("%ld\n",sizeof(c)); // 8
  printf("%ld\n",sizeof(d)); // 20
}
```

### Type Converting
```c
double d = 3.4;
int i = 2;

printf("%f\n",(d+i)); // 5.400000

printf("%d\n",((int)d+i)); // 5
```

> ⚠️ **Precautions**<br>
> When converting type from different sizes (e.g. `int` and `char`) or different storing method (e.g. `int` and `float`), unexpected value could occur!
> 
> E.g.
> ```c
> int i = 500;
> printf("%u\n", (unsigned char)i ); // 244
> ```
> `500` is `0001 1111 0100`,
> but `char` only got 1 byte, only storing `1111 0100` which is `244`.

### Others
You can do this when init-ing multiple vars:
```c
int a=1, b=3, c=9;
```

> **_btw_**<br>
> In Bash, we can also use `&&`.
> 
> E.g.
> ```bash
> gcc test.c && ./a.out
> ```



*******



## [Ep.7 `if` `else`, `switch` `case`](https://youtu.be/ZFyRHyIXlv4)

### `scanf()`

Bad case:
```c
#include <stdio.h>
int main(){
  int a;
  printf("Input: ___\b\b");
  scanf("%c",&a);
  printf("Got: %d\n",a);
  return 0;
}
```

We got a `char` but put into an `int`, so the 1 byte data is stored into only the first byte of `int a`. We will get a random value with garbage data printed.

So, *IT'S IMPORTANT TO SET AN INIT VALUE WHEN DECLARING A NEW VAR.* <br>E.g. `int a=0;`

(Correction omitted)

### `if`, `else`
```c
#include <stdio.h>
int main(){

  int a=0;

  if(0){
    a=1;
    printf("Inside IF");
  }

  printf("a: %d\n",a);

  // without curly brackets
  // not recommended
  if(9)
    a=2;
  else
    a=9;

  printf("aa: %d\n",a);

  // else if chain
  if(0){
    a=3;
  }else if(!0){
    a=233;
  }else if(1){
    a=123;
  }else{
    a=8;
  }

  printf("aaa: %d\n",a);

  return 0;
}
```

> When using `else if` chains, put the most possibly truthy statement on top, and the least at bottom for better program efficiency.
> ```c
> if(very_possibly_1){
>   // ...
> }else if(half_possibe){
>   // ...
> }else if(very_0){
>   // ...
> }
> ```

### `switch`
```c
#include <stdio.h>

int main(){

  int op=0, a=0;
  scanf("%d",&op);

  switch(op){
    case 1:
    case 2:
    case 3:
      a=100;
      break;
    case 4:
      a=4;
      break;
    case 5:
      a=5;
      break;
    default:
      a=99;
      break;
  }

  printf("Result: %d\n",a);

  return 0;
}
```

### String
```c
char str[9] = "hello";
printf("%s\n",str);
```
This is as same as:
```c
char str[9];
str[0] = 'h';
str[1] = 'e';
str[2] = 'l';
str[3] = 'l';
str[4] = 'o';
str[5] = '\0'; // String Terminator
printf("%s\n",str);
```
Physically, string is stored next to each other in order, different than:
```c
char ch1 = 'h';
char ch2 = 'e';
char ch3 = 'l';
char ch4 = 'l';
char ch5 = 'o';
printf("%c%c%c%c%c\n",ch1,ch2,ch3,ch4,ch5);
```

> The `'\0'` is a **MUST** to prevent garbage data following after.

> `'\0'` is the same as `0x00` and `(int)0`.



*******



## [Ep.8 Loops](https://youtu.be/TdzCyRviW7w)

### While Loop
Eg.1
```c
int a = 10;

while(a){
  a--;
  printf("a : %d\n",a);
}
```

Eg.2
```c
int a = 10, b=3;

while(a>b){
  a--;
  printf("a : %d\n",a);
}
```

### For Loop

`for(` setInitialIndex `;` condition `;` modifyIndexAfterEachIteration `)`
```c
int a;
for(a=0; a>10; a++){
>   printf("a : %d\n",a);
}
```

> Unformal but works:<br>
> `for(` runOnceAtFirst `;` condition `;` Run `)`
> ```c
> int a=0;
> for(;a<9;){
>   a++;
>   printf("a : %d\n",a);
> }
> ```

> A test:
> ```c
> #include <stdio.h>
> int func0(){
>   printf("call func1\n");
>   return 0;
> }
> int func1(){
>   printf("call func2\n");
>   return 1;
> }
> 
> int main(){
>   int a;
>   for(a=0; func0(); func1()){
>     printf("Inside for");
>   }
> }
> ```
> - Result:
> ```
> call func1
> ```
> 
> **Conclusion**<br>
> The running order of for loop is:
> ```c
> for( 1 ; 2 ; 4 ){
>   3;
> }
> ```
> - `1` only runs once at the beginning.
> - When `2` (condition) is `0`, we get out of the loop without running `3` and `4`.

### Do... While
```c
do{
  // ...
}while(0);
```



*******



## [Ep.9 Function](https://youtu.be/s7xnTuSb8U8)

### Practice `for` loop
Multiplication Table
```c
for(int i=1;i<=9;i++){
  printf("\n[%d]\n",i);
  for(int j=1;j<=20;j++){
    printf("%d * %d = %d\n",i,j,i*j);
  }
}
```

### `continue`
In the Multiplication Table above, if we want only the odds as second value:
```c
for(int i=1;i<=9;i++){
  printf("\n[%d]\n",i);
  for(int j=1;j<=20;j++){
    if(j % 2 == 0){
      continue; // Skip to the next iteration
    }
    printf("%d * %d = %d\n",i,j,i*j);
  }
}
```

### `break`
```c
int isRunning = 1;
while(1){
  if(isRunning == 0){
    printf("User turns off the system.\n");
    break;
  }
  printf("Input 0 to exit: _\b");
  scanf("%d",&isRunning);
  getchar();
  printf("(You inputted '%d')",isRunning);
}
```

### `goto`
The "jump to" keyword.
> **NOT RECOMMENDED IN REAL CODING**
```c
#include <stdio.h>
int main(){

  printf("START!\n");
  goto ojw;
  printf("NEXT!\n");
  ojw: printf("HI!!!\n");
  printf("END!\n");

  return 0;
}
```

### Functions

The function name is similar with variable / constant names. <br>
Functional commands are stored in a block of memory, and the
function name is a "pointer" of the starting point of the block's starting address.

```c
int funcA(float a){
  // ...
  return 1;
}
```
- `int`: The return value type.
- `funcA`: Function name.
- `float a`: Param, values the function "eats".
- `// ...`: Program logic.
- `return`: Values the function "poops".

When the function does not return:
```c
void funcA(int b){
  // ...
}
```

E.g.
```c
#include <stdio.h>

int sum(int a, int b){
  int c = 0;
  c=a+b;
  return c;
}

int main(){
  printf("Start\n");

  int x = sum(1,2);

  printf("%d\n",x);

  return 0;
}
```

- Doesn't matter how you place functions in whatever order.
- You can pre-define a function just like pre-declaring a var. At compile, prototypes tell the compiler what types to expect when calling.
```c
#include <stdio.h>

// Compiler ignores the param name here.
// This is called the `prototype`.
int sum(int firstNum, int secondNum);

int main(){
  printf("Start\n");
  int x = sum(1,2);
  printf("%d\n",x);
  return 0;
}

int sum(int a, int b){
  int c = 0;
  c=a+b;
  return c;
}
```

> In bigger projects, function prototypes are written in a separate header file for better "linking".
```c
#include <stdio.h>
#include "func.h"
// main...
```
```c
// func.h
int sum(int a,int b);
void call();
// ...
```



*******



## [Ep.10 Pointer](https://youtu.be/po80VB5prlY)

### Array

To declare an array:
```c
// set an array that has a length of 10 items
int arrA[10];
```
> Say `arrA` begins at 0x233 in storage:
>   |content|size|
>   |:------|:-----|
>   |arrA[0]|4 byte|
>   |arrA[1]|4 byte|
>   |arrA[2]|4 byte|
>   | ... | ... |
>   |arrA[9]|4 byte|
> - **Physically sticking together** in a row by order;
> - `int` defines each item's **size**.

Example code
```c
#include <stdio.h>
int main(){
  int arrA[9];
  for(int i=0; i<10; i++){
    arrA[i]=i*2;
  }
  for(int i=0; i<10; i++){
    printf("arr[%d]=%d\n",i,arrA[i]);
  }
  return 1;
}
```
(Adds define)
```c
#include <stdio.h>
#define MAX 10000
int main(){
  int arrA[MAX];
  for(int i=0; i<MAX; i++){
    arrA[i]=i*2;
    printf("arr[%d]=%d\n",i,arrA[i]);
  }
  return 1;
}
```

### "Physical" location...?

```c
int x = arrA;
printf("\nx = %d\n",x);
```
What is `x`? <br>
When ran multiple times, each time `x` shows a different value.
That is the **starting location** of the array , i.e. `arrA[0]`.

### Pointer

Pointer stores a value of "physical location".

- To declare a pointer, add `int * pa`;
- To get the location value of a variable, use `&`;
- To go to the pointer's location, call `*pa`.

E.g.
```c
#include <stdio.h>
int main(){

  int a;
  int * pa;

  a=3;
  printf("1) a = %d\n",a);
  printf("2) &a = %p\n",&a);

  pa = &a;
  printf("3) pa = %p\n",pa);
  printf("4) &pa = %p\n",&pa);
  printf("5) *pa = %d\n",*pa);

  return 1;
}
```

> ### Double pointer
> ```c
> int n = 10;
> int *ptr1 = &n;
> int **ptr2 = &ptr1;
> printf("5) **ptr2 = %d\n",**ptr2); // 10
> ```

**The asterisks are different!**

In `int *pa;`, the `int *` part is ***datatype***;<br>
In `x = *pa;`, the `*` is an operator.


*******


