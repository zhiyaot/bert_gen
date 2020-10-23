# bert_gen

## Compile Instruction and Makefile

### Compile Environment

- REQUIRE `cmake 3.10` or higher version, `python3`
- Current working environment: `Ubuntu 64-bit`, `OpenSUSE 64-bit Leap 15.1`, `Windows Subsystem for Linux 2 on Windows 10 Pro for Workstation`


### Makefile Instruction

Compiling with CMake generated Makefile in Unix environment:

- run `cmake CMakeLists.txt` to generate make file
- run `make` to build executables
- you can also run `make help` to see all available option

## Feature for Unix

- `gen.sh` is a bash script wrapper for Unix environment that runs full flow from DCP to the files you need to use with bert (mydesign.h,c)
- run `./gen.sh -h` for usage help
- run `./gen.sh -gen dcp headerName` to generate `headerName.c` and `headerName.h` under `dirname $dcp` using dcp file
- `headerName.c` and `headerName.h` resides in `dirname $dcp`


### Partial Flow

The following are components of `gen.sh` 

- run `./bert_gen baseDir headerName` to just run `bert_gen` on some given output from `gen_map.py`
- run `gen_map.py baseDir mddName` to just run `gen_map.py` to produce intermediate file for runing `ber_gen.cpp`


TODO: are there specific case where a user need to use these in pieces
rather than calling `gen.sh`?  Like, if our
code (like compression) has problems with specific files, is it necessary
to hand edit .list in order for it to skip particular memories that we
don't currently support?

## Auxiliary Files

The current version of `bert_gen` generate auxiliary files in the base directory of the provided `dcp` file. Below is a list of the usage and meaning.

- `.ll` Logic Location file, generated through `Vivado`
- `.bit` bitstream file, generated through `vivado`
- `.mdd` Memory Description Data, pertaining information about each physical BRAM
- `.list` Accociation between logical memeory names and a `mem_i` label, where `i` is the index number
- `.info` Mapping between logical bits and physical BRAM
- `.bram` List of all BRAMs associated with `mem_i` where `i` is the index number
- `..._uncompressed.c` Uncompressed version of bert header, replace `...` with desired headerName
- `..._uncompressed.h`, `...h` bert header for `#include`, replace `...` with desired headerName

## Debugging bert_gen

The following is a flow chart for debugging bert_gen.  This is the full
flow that is run by `bert_gen`


![Flow Chart](https://github.com/byuccl/bert_dev/blob/master/bert_gen/data/flow.png)

TODO: show compression?

TODO: show bitstream generation?

TODO: mark files and programs differently.

TODO: show consumption of files by programs.
