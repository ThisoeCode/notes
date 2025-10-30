# Thisoe's C & Linux Note

_[<< Back to Thisoe's Note](./README.md)_

- Course from [OJ Tube](https://www.youtube.com/playlist?list=PLz--ENLG_8TMdMJIwyqDIpcEOysvNoonf OJ Tube - C언어 강의) (lang: KR)

*******



## EP.2 Linux

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

Press `Esc` to exit editing. Then:
`:w` - save
`:q` - quit
`:q!` - quit without saving

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



## EP.3 Variables

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

`int`: 4 byte int
`unsigned int`: 0 ~ 4294967295

`long`: 16 bit (4 byte) int
`long long`: 64 bit (8 byte) int

- Charactors:

`char`: a 1 byte ASCII
```c
printf("%d\n", 97);  // 3
printf("%u\n", 97);  // a
```

`unsigned int`: 0 ~ 4294967295

- Decimals:

The storage and calculation method is different from (slower than) int, and even 
`float`: 4 byte decimal
`double`
```c
printf("%.20f\n", 0.1 + 0.2); // 0.1 + 0.2 = 0.30000000000000004441
```

### Summary
```c
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

"More principles you know, more easy computer science seems." -- OJ Tube



*******



## EP.4 


