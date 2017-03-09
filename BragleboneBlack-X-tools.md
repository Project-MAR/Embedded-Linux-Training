## BragleboneBlack-X-tools.md

Use 1.22.0 (Released version)
```sh
wget http://crosstool-ng.org/download/crosstool-ng/crosstool-ng-1.22.0.tar.bz2
cd crosstool-ng/
autoreconf
./configure --enable-local
make
make install
./ct-ng arm-unknown-linux-gnueabi
./ct-ng menuconfig
./ct-ng build

```

Note: BeagleBone Black use 1-GHz Sitara™ ARM® Cortex®-A8 32-Bit
```sh
./ct-ng list-samples
./ct-ng arm-cortexa5-linux-uclibcgnueabihf ***
```

---

### C library
glibc   
   - Designed for performance, standards compliance and portability
   - Quite big
   
uClibc-ng
   - A continuation of the old uClibc project
   - Lightweight C library for small embedded systems
   - Supports no-MMU architectures (ARM Cortex-M, etc)
   - Approx 3.5 times smaller than glibc
   - Used on a large number of production embedded products, including consumer electronic devices
   
musl C
   - A lightweight, fast and simple library for embedded systems
   - In particular, great at making small static executables
   - Supported by build systems such as Buildroot

---

#### Base on Training document from [freeelectron](http://free-electrons.com/training/)
   
