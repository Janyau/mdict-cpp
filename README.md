# MDICT CPP

[![License: BSD-3-Clause](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
[![Stars](https://img.shields.io/github/stars/dictlab/mdict-cpp?style=social)](https://github.com/dictlab/mdict-cpp/stargazers)
[![Forks](https://img.shields.io/github/forks/dictlab/mdict-cpp?style=social)](https://github.com/dictlab/mdict-cpp/network/members)
[![Build Status](https://github.com/dictlab/mdict-cpp/actions/workflows/build-and-test.yml/badge.svg)](https://github.com/dictlab/mdict-cpp/actions/workflows/build-and-test.yml)
[![Latest Release](https://img.shields.io/github/release/dictlab/mdict-cpp.svg)](https://github.com/dictlab/mdict-cpp/releases/latest)

A C++ implementation for interpreting MDX/MDD dictionary files. This library provides functionality to read and parse MDX/MDD dictionary files commonly used in electronic dictionaries.

## Features

- Parse MDX/MDD dictionary files
- Extract dictionary entries and definitions
- Support for both MDX (dictionary content) and MDD (resource files)
- Simple and efficient C++ implementation
- in-memory base64 encoding/decoding
- UTF8 global output for any dictionary
- low-level optimizations using advanced data structures

## Notable Projects using MDict-cpp:
- [Wazajisho](https://git.ajattix.org/hashirama/wazajisho): a in-memory, functional MDict viewer
- [MDict-hs](https://git.ajattix.org/hashirama/mdict-hs): the haskell bindings for MDict-cpp
 
## Installation

### Prerequisites

- CMake (version 3.10 or higher)
- C++ compiler with C++17 support
- Git

### Building from Source

1. Clone the repository:
```bash
git clone git@github.com:dictlab/mdict-cpp.git
cd mdict-cpp
```

2. Initialize and update submodules:
```bash
git submodule init
git submodule update --recursive
```

3. Build the project:
```bash
mkdir build
cd build
cmake ..
make
```

### System Installation

To install the library system-wide (requires root privileges):

```bash
mkdir build
cd build
cmake -DINSTALL_TO_SYSTEM=ON ..
make
sudo make install
```

it will install those files:
```
-- Installing: /usr/local/lib/libmdict.a
-- Installing: /usr/local/lib/libmdictminiz.a
-- Installing: /usr/local/lib/libmdictbase64.a
-- Up-to-date: /usr/local/include/mdict/mdict.h
-- Up-to-date: /usr/local/include/mdict/mdict_extern.h
-- Installing: /usr/local/bin/mydict
```


This will install:
- The library to `/usr/lib` (Linux) or `/usr/local/lib` (macOS/BSD)
- Headers to `/usr/include` (Linux) or `/usr/local/include` (macOS/BSD)

## Usage

### Building the Executable

```bash
mkdir build
cd build
cmake ..
make mydict
```
The executable will be generated at `build/bin/mydict`

### Running the Dictionary Tool

#### Query a word
*Warning:* Make sure to include backslashs at the end of each query, otherwise lookup can fail.
```bash
./build/bin/mydict your_mdx_file.mdx yourword
# output the resource binary as base64 format
./build/bin/mydict your_mdx_file.mdd \\xxx\\xx.png

# output the resource binary as hex string format
./build/bin/mydict -x your_mdx_file.mdd \\xxx\\xx.png
```

#### list all keys

```bash
./build/bin/mydict -l your_mdx_file.mdx

./build/bin/mydict -l your_mdx_file.mdd
```

### Building the Library

```bash
mkdir build
cd build
cmake ..
make mdict
```

The library will be generated at `target/lib/libmdict.a`

### Using the Library in Your Project with CMake

1. Include the header files:
```cpp
#include "mdict_extern.h"
```

2. Link against the library:
```cmake
target_link_libraries(your_project mdict)
```

### Or use g++ directly

```bash
# after make install
cd src
g++ -std=c++17 -I/usr/local/ -I. -L/usr/local/lib -lmdict -lmdictminiz -lmdictbase64 mydict.cc -o mmdict
```

## MDX File Format

The MDX/MDD file format is a dictionary format commonly used in electronic dictionaries. MDX files contain the dictionary content (text, HTML, etc.), while MDD files contain associated resources (images, audio, etc.).

### Format References
- [MDX Format Documentation](https://www.zhihu.com/question/22143768)
- [MDX/MDD File Format Specification](https://github.com/ilius/pyglossary/blob/master/doc/mdx.md)
- [MDict Format](https://www.mdict.cn/wp/?page_id=5227&lang=en)

### Format Structure
![MDX Format Structure](https://tva1.sinaimg.cn/large/008eGmZEly1go066lnewfj30u01bdb29.jpg)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the BSD-3-Clause License - see the LICENSE file for details.
