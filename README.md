# Instructions

- Install all needed libraries
```
$ sudo apt-get install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev libusb-1.0-0-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev device-tree-compiler pkg-config libexpat-dev python3
```

- Clone _riscv-gnu-toolchain_ and _riscv-tools_
```
$ git clone --recursive https://github.com/riscv/riscv-tools.git
$ git clone https://github.com/riscv/riscv-gnu-toolchain.git
```

- Create the install dir
```
$ mkdir build
$ export RISCV=`pwd`/build
$ export INSTALL_DIR=$RISCV
$ export PATH="$RISCV/bin:$PATH"
```

- Go to the _riscv-opcodes_ and create a file with your custom instructions. Then run the following command:
```
$ cat opcode ... | ./parse_opcodes -c > encoding.h
```

- Check _riscv-tools_ "Makefile" to see in which submodule directories the _encoding.h_ should be copied

- After copying _encoding.h_ to the appropriate folders, proceed with modifying the necessary files of _riscv-binutils-gdb_

- Proceed with installing _riscv-gnu-toolchain_ according to the instructions of the upstream repository
```
$ cd ./riscv-gnu-toolchain
$ ./configure --prefix=$INSTALL_DIR --enable-multilib
$ make -j 4
$ make install
```

- Proceed with installing riscv-tools according to the instructions of the upstream repository
```
$ ./build.sh
```
or install each repository individually, according to their respected instructions