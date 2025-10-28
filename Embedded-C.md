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
> The `stdio.h` file is at `/usr/include/` in Linux.



*******



## EP.3 Variables


