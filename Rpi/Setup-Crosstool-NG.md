## Setup Crosstool-NG
[original guide](https://mborgerson.com/cross-compiling-for-the-raspberry-pi)
### Install tools
```sh
sudo apt-get install autoconf automake libtool-bin libexpat1-dev \
libncurses5-dev bison flex patch curl cvs texinfo git bc \
build-essential subversion gawk python-dev gperf unzip \
pkg-config wget help2man
```

### Getting lastest Crosstool-ng (at this time, 1.22.0)
```sh
wget http://crosstool-ng.org/download/crosstool-ng/crosstool-ng-1.22.0.tar.bz2
cd crosstool-ng
./configure --enable-local
make
make install
```

### Configure the toolchain
add cd-ng to global variable
```sh
PATH=`pwd`:$PATH
./ct-ng menuconfig
```

Configure, Build, and Install the Toolchain
   - Paths and misc options.
      - Enable Try features marked as EXPERIMENTAL.
      - Set Prefix directory to ${HOME}/your/toolchain/path/${CT_TARGET}.
      - Enable Use a mirror.
      - Set Number of parallel jobs to twice the number of HW threads (eg for a 4-core CPU with HyperThreading, use 16).
   - Target options.
      - Set Target Architecture to arm.
      - Floating point:
         - hardware (FPU)
      - append 'hf' to the tuple (EXPERIMENTAL)
   - Operating System.
      - Target OS to Linux.
   - Binary Utility.
      - Set binutils version to 2.25.1
   - C complier.
      - Enable Show Linaro versions.
      - Enable C++.
   - Debug Facilities.
      - Enable gdb.
         - Enable Build a static cross gdb.
         - Set Cross-gdb extra config to --with-expat.
      - Enable ltrace.
      - Enable strace.

Change folder to build folder.
```sh
./ct-ng build
```

Than take a break. The build took about 30  minutes for me.   
When it done. Your toolchain will be at /your/toolchain/path/
cd into that folder add to path variable
```sh
PATH=$PATH:`pwd`
```

Complie C source file with this command.
```sh
arm-unknown-linux-gnueabihf-gcc -o hello hello.c
```

C source code
```c
#include <stdlib.h>
#include <stdio.h>
 
int main (void)
{
	printf( "Hello world!\n" );
	return EXIT_SUCCESS;
}
```

### SFTP to RPi
```sh
sftp pi@IP-Address:/path/to/destination/folder
lcd path/to/local/floder
cd path/to/remote/folder
put hello
bye
```

ssh into RPi then run hello.
```sh
./hello
Hello world!
```

### Download, Build, and Install the Broadcom VideoCore Libraries
to be continue   

