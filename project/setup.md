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
need to modify your PATH setting to contain it. For Bash, that is to put the
end of your `~/.bash_profile`:
```
export PATH=/usr/local/data/cs318/x86_64/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/data/cs318/x86_64/lib:$LD_LIBRARY_PATH
```
For tcsh (the default login shell in ugrad lab machines in the CS department), 
the syntax is different: add `set path = (/usr/local/data/cs318/x86_64/bin $path)` 
to the end of your `~/.tcshrc`.

Besides the lab machines, you may want to work on the projects on your own machines to be more productive. 
This page contains instructions to help you with the setup of the core development 
environment needed for Pintos.  They are intended for Unix and Mac OS machines. 
If you are running Windows, we recommend you to run a virtual machine with Linux 
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
  ├── dist
  └── src
  ```

  Then, set the environment variables (remember to replace `/path/to/setup` with the 
  *full path* to the actual setup directory you've created, e.g., `SWD=/home/ryan/318/toolchain`).
  ```bash
  $ SWD=/path/to/setup
  $ PREFIX=$SWD/dist
  $ export PATH=$PREFIX/bin:$PATH
  $ export LD_LIBRARY_PATH=$PREFIX/lib:$LD_LIBRARY_PATH
  ```
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
the PATH. Put <code class="highlighter-rogue">export PATH=/path/to/bin:$PATH</code> and 
<code class="highlighter-rogue">export LD_LIBRARY_PATH=/path/to/lib:$LD_LIBRARY_PATH</code>
to the end of your terminal config file (e.g., <code class="highlighter-rogue">.bash_profile</code>)
so that they are set automatically when you login. Remember to replace 
<code class="highlighter-rogue">/path/to/{bin,lib}</code> with the actual path, 
e.g., <code class="highlighter-rogue">~/318/toolchain/dist/bin</code>.
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
    There are some bugs in Bochs that should be fixed when used with Pintos. Thus,
    we need to install Bochs from source, and apply patches. We will build two
    versions of Bochs: one, simply named `bochs`, with the GDB stub enabled, and the
    other, named `bochs-dbg`, with the built-in debugger enabled.
  - [Download Link](https://sourceforge.net/projects/bochs/files/bochs/2.6.2/bochs-2.6.2.tar.gz/download)
  - Build script: `pintos/src/misc/bochs-2.6.2-build.sh`

### Pintos Utility Tools
The pintos source distribution comes with a few handy scripts that you will be
using frequently. They are located within `src/utils/`. The most important one is 
the `pintos` Perl script, which you will be using to start and run tests
in pintos. You need to make sure it can be found in your PATH environment
variable. You can either copy them to a directory within your PATH (e.g., 
`/usr/local/bin`) or you can just point PATH to the utility directory
(e.g., `export PATH=/path/to/pintos/src/utils:$PATH`). The Bochs emulator will
need the squish-pty in the util directory. You can compile it by typing `make`
in the `src/utils/` directory.

### Others
* Required: [Perl](http://www.perl.org). Version 5.8.0 or later.
* Recommended: [X](https://www.x.org/wiki), [ctags](http://ctags.sourceforge.net/), [cscope](http://cscope.sourceforge.net/)
