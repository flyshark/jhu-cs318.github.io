---
layout: default
---

## Setup

To develop the Pintos projects, you'll need two essential sets of tools:
- 80x86 cross-compiler toolchain for 32-bit architecture including a C compiler, 
	assembler, linker, and debugger.
- x86 emulator, QEMU or Bochs

The CS department's [lab machines](https://support.cs.jhu.edu/wiki/Category:Linux_Clients)
already have these tools available. But you may want to work on the projects on
your own machines. This page contains instructions to help you setup the development
environment. They are intended for Unix and Mac OS machines. If you
are running Windows, we recommend you run a virtual machine with Linux or you will 
have to setup [Cygwin](http://www.cygwin.com) first. This guide, and the course
in general, assumes you are familiar with Unix commands.


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

**We've provided a script (`pintos/src/misc/build_toolchain.sh`) that automates the following.**

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

### x86 Emulator
