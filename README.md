# Instructions

- Install all needed libraries
```
$ sudo apt-get install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev libusb-1.0-0-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev device-tree-compiler pkg-config libexpat-dev python3
```

- Clone _riscv-gnu-toolchain_ and _riscv-tools_ + update the _riscv-tools_ repository
```
$ git clone --recursive https://github.com/riscv/riscv-tools.git
$ git clone --recursive https://github.com/riscv/riscv-gnu-toolchain.git
$ cd ./riscv-tools && git submodule foreach --recursive git pull origin master
```

- The order to access the repos is:
1. riscv-opcodes: Running `make`, the result is an `encoding.h` file that includes all the RISC-V instructions located inside the repo. In order to add the instructions to the toolchain, edit the `riscv-opc.h` file located in the `/riscv-gnu-toolchain/riscv-gdb/include/opcode/` directory and in `/riscv-gnu-toolchain/riscv-binutils/include/opcode/` directory, by adding the definitions of the instructions which are stored in the `encoding.h` file. Lastly, edit the `riscv-opc.c` file located in the `/riscv-gnu-toolchain/riscv-gdb/opcodes/` directory and in the `/riscv-gnu-toolchain/riscv-binutils/opcodes/` directory, specifically the `riscv_opcodes` struct. You could use [this diploma thesis](http://hdl.handle.net/10889/15019) as reference - see chapter 6.6 (specifically 6.6.6 and onwards)
2. riscv-gnu-toolchain: Necessary step for all the remaining repos.
3. riscv-isa-sim
4. riscv-pk
5. riscv-tests
6. riscv-openocd
