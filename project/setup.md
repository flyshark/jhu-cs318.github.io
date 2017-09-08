---
layout: default
title: Project Setup
---

## Setup

To develop the Pintos projects, you'll need two essential sets of tools:
- 80x86 cross-compiler toolchain for 32-bit architecture including a C compiler, 
	assembler, linker, and debugger.
- x86 emulator, QEMU or Bochs

The CS department's [lab machines](https://support.cs.jhu.edu/wiki/Category:Linux_Clients)
already have these tools available under `/usr/local/data/cs318/x86_64`. You just
need to modify your PATH setting to include it. For Bash, that is to put the following
at the end of your `~/.bash_profile`:
```
export PATH=/usr/local/data/cs318/x86_64/bin:$PATH
```
For tcsh (the default login shell in ugrad lab machines in the CS department), 
the syntax is different: add `set path = (/usr/local/data/cs318/x86_64/bin $path)` 
to the end of your `~/.tcshrc`. Log out and re-login to let it take effect. 

Besides the lab machines, you may want to work on the projects on your own machines to be more productive. 
This page contains instructions to help you with the setup of the core development 
environment needed for Pintos on your own machines.  They are intended for Unix and 
Mac OS machines. If you are running Windows, we recommend you to run a virtual machine with Linux 
or you will have to setup [Cygwin](http://www.cygwin.com) first. This guide, and 
the course in general, assumes you are familiar with Unix commands.

### Compiler toolchain

The compiler toolchain are a collection of tools that turns source code into
executable binaries for a target architecture. Pintos is written in C and 
x86 assembly, and runs on 32-bit 80x86 machines. So we will need the C compiler (`gcc`),
assembler (`as`), linker (`ld`) and debugger (`gdb`). Your machines are probably
equipped with these tools already. But they should support 32-bit x86 architecture.
A quick test of the support is to run `objdump -i | grep elf32-i386`
in the terminal. If it returns matching lines, your system's default tool chain 
supports the target *so you can skip this section*{: .text-success}. Otherwise, you will need
to build the toolchain from source. To distinguish the new toolchain from your 
system's default one, we will add a `i386-elf-` prefix to the build target, *e.g.*,
`i386-elf-gcc`, `i386-elf-as`.

<div class="panel panel-info">
<div class="panel-heading">
<strong>Note</strong>
</div>
<div class="panel-body">
<b>We've provided a script (<code class="highlighter-rouge">pintos/src/misc/toolchain-build.sh</code>) 
that automates the following building instructions. So you can just run the script and 
modify your PATH setting after the build finishes. The script has been tested on 
recent version of Ubuntu, Mac OS and Fedora.</b>
</div>
</div>

* **Prerequisite**:
  - standard build tools including `make`, `gcc`, etc.. For Ubuntu, they are the
    `build-essential` package.
  - in building GDB, you may encounter errors due to missing the ncurses and textinfo 
    libraries. For Ubuntu, you can install them with `sudo apt-get install libncurses5-dev texinfo`.
  - `wget`

* Directory and environment variables:
  First, create a setup directory (e.g., `~/318/toolchain`) and subdirectories that
  look like this:
  ```bash
  /path/to/setup
  ├── build
  ├── x86_64
  └── src
  ```

  Then, set the environment variables (remember to replace `/path/to/setup` with the 
  *full path* to the actual setup directory you've created, e.g., `SWD=/home/ryan/318/toolchain`).
  ```bash
  $ SWD=/path/to/setup
  $ PREFIX=$SWD/x86_64
  $ export PATH=$PREFIX/bin:$PATH
  $ export LD_LIBRARY_PATH=$PREFIX/lib:$LD_LIBRARY_PATH
  ```
  For Mac users, the last command is `export DYLD_LIBRARY_PATH=$PREFIX/lib:$DYLD_LIBRARY_PATH` instead.

* GNU binutils:
  - **Download**: 
  ```bash
  $ cd $SWD/src 
  $ wget https://ftp.gnu.org/gnu/binutils/binutils-2.27.tar.gz && tar xzf binutils-2.27.tar.gz
  ```
  - **Build**:
  ```bash
  $ mkdir -p $SWD/build/binutils && cd $SWD/build/binutils
  $ ../../src/binutils-2.27/configure --prefix=$PREFIX --target=i386-elf \
    --disable-multilib --disable-nls --disable-werror
  $ make -j8
  $ make install
  ```

* GCC:  
  - **Download**: 
  ```bash
  $ cd $SWD/src
  $ wget https://ftp.gnu.org/gnu/gcc/gcc-6.2.0/gcc-6.2.0.tar.bz2 && tar xjf gcc-6.2.0.tar.bz2
  $ cd $SWD/src/gcc-6.2.0 && contrib/download_prerequisites
  ```
  - **Build**:
  ```bash
  $ mkdir -p $SWD/build/gcc && cd $SWD/build/gcc
  $ ../../src/gcc-6.2.0/configure --prefix=$PREFIX --target=i386-elf \
  --disable-multilib --disable-nls --disable-werror --disable-libssp \
  --disable-libmudflap --with-newlib --without-headers --enable-languages=c,c++
  $ make -j8 all-gcc 
  $ make install-gcc
  $ make all-target-libgcc
  $ make install-target-libgcc
  ```

* GDB:
  - **Download**:
  ```bash
  $ cd $SWD/src
  $ wget https://ftp.gnu.org/gnu/gdb/gdb-7.9.1.tar.xz  && tar xJf gdb-7.9.1.tar.xz
  ```
  - **Build**:
  ```bash
  $ mkdir -p $SWD/build/gdb && cd $SWD/build/gdb
  $ ../../src/gdb-7.9.1/configure --prefix=$PREFIX --target=i386-elf --disable-werror
  $ make -j8
  $ make install
  ```

<div class="panel panel-info">
<div class="panel-heading">
<b>Note</b>
</div>
<div class="panel-body">
After building and installing the toolchain, you need to make sure they are in 
the PATH. Put <code class="highlighter-rogue">export PATH=/path/to/swd/x86_64/bin:$PATH</code> 
to the end of your terminal config file (e.g., <code class="highlighter-rogue">.bash_profile</code>)
so that they are set automatically when you login. Remember to replace 
<code class="highlighter-rogue">/path/to/swd/x86_64/bin</code> with the actual path, 
e.g., <code class="highlighter-rogue">~/318/toolchain/x86_64/bin</code>. You may also
want to delete the source and build directories in <code>/path/to/swd/{src,build}</code> 
to save space.
</div>
</div>

### x86 Emulator

* **QEMU**:
  - QEMU is modern and fast. You can either install it from the package repository or
  build it from [source](https://www.qemu.org/download/).
    ```bash
    sudo apt-get install qemu libvirt-bin
    ```
* **Bochs**:
  - Bochs is slower than QEMU but provides full emulation (i.e., higher accuracy).
  For Lab 1, we will use Bochs as the default emulator and for Lab 2-4, we will
  use QEMU as the default emulator. Nevertheless, nothing will prevent you from using 
  one or another for all the labs. There are some bugs in Bochs that should be fixed 
  when using it with Pintos.  Thus, we need to install Bochs from source, and apply 
  the patches that we have provided under `pintos/src/misc/bochs*.patch`. We will 
  build two versions of Bochs: one, simply named `bochs`, with the GDB stub enabled, and the
  other, named `bochs-dbg`, with the built-in debugger enabled.

  - Version 2.6.2 has been tested to work with Pintos. Newer version of Bochs has 
  not been tested. <span class="text-info">We have provided a build script
  <code>pintos/src/misc/bochs-2.6.2-build.sh</code> that will download, patch and
  build two versions of the Bochs for you. But you need to make sure X11 and its
  library is installed. For Mac OS, you should install [XQuartz](https://www.xquartz.org).
  For Ubuntu, you should have `libx11-dev` and `libxrandr-dev` installed.

  - After build succeeds, make sure the `bochs` or `bochs-db` are in PATH. You
  can verify the install with `bochs --version`.

### Pintos Utility Tools
The Pintos source distribution comes with a few handy scripts that you will be
using frequently. They are located within `src/utils/`. The most important one is 
the `pintos` Perl script, which you will be using to start and run tests
in pintos. You need to make sure it can be found in your PATH environment
variable. In addition, the `src/misc/gdb-macros` is provided with a number of
GDB macros that you will find useful when you are debugging Pintos. The `pintos-gdb`
is a wrapper around the `i386-elf-gdb` that reads this macro file at start. 
It assumes the macro file resides in `../misc`.

The example commands to do the above setup for the Pintos utilities are:
(replace `/path/to/swd/x86_64` with the actual directory path)
```bash
$ cd pintos/src/utils && make
$ cp backtrace pintos Pintos.pm pintos-gdb pintos-set-cmdline pintos-mkdisk setitimer-helper squish-pty squish-unix /path/to/swd/x86_64/bin
$ mkdir /path/to/swd/x86_64/misc
$ cp pintos/src/gdb-macros /path/to/swd/misc
```

### Others
* Required: [Perl](http://www.perl.org). Version 5.8.0 or later.
* Recommended: 
  - [ctags](http://ctags.sourceforge.net/)
  - [cscope](http://cscope.sourceforge.net/)
  - [cgdb](https://cgdb.github.io)
  - [NERDTree](https://github.com/scrooloose/nerdtree)
  - [YouCompleteMe](https://github.com/Valloric/YouCompleteMe).
* Optional:
  - GUI IDEs like [Eclipse CDT](https://eclipse.org/cdt) or [clion](http://www.jetbrains.com/clion). 
    The instructor has not tried them. Vim or Emacs plus the standard Unix development
    tools would suffice for the course. But if you can't live without GUI IDEs. You
    may explore the setup yourself (potential 
    [reference](https://uchicago-cs.github.io/mpcs52030/pintos_eclipse.html)) and
    let us know if they are helpful!
