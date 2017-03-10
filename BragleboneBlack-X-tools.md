## BragleboneBlack-X-tools.md

Use 1.22.0 (Released version)
```sh
wget http://crosstool-ng.org/download/crosstool-ng/crosstool-ng-1.22.0.tar.bz2
cd crosstool-ng/
autoreconf
./configure --enable-local
make
make install
```

Note: BeagleBone Black use 1-GHz Sitara™ ARM® Cortex®-A8 32-Bit   
config for arm-cortex_a8-linux-uclibcgnueabihf
```sh
./ct-ng list-samples
./ct-ng arm-cortex_a8-linux-gnueabi
```

### fix missing iPV6 support
[patch](https://github.com/crosstool-ng/crosstool-ng/pull/286/files)
   
in "config/libc/uClibc.in.2"

```sh
       If so, please report the issue, so we can default this
       to off if too many people complain.
 
+config LIBC_UCLIBC_IPV6
+    bool
+    prompt "Add support for IPv6"
+    help
+      Say y if you want uClibc to support IPv6.
+
 config LIBC_UCLIBC_WCHAR
     bool
     prompt "Add support for WCHAR"
```

in "scripts/build/libc/uClibc.sh"

```sh
@@ -427,6 +427,13 @@ manage_uClibc_config() {
         CT_KconfigDisableOption "UCLIBC_HAS_WCHAR" "${dst}"
     fi
 
+    # IPv6 support
+    if [ "${CT_LIBC_UCLIBC_IPV6}" = "y" ]; then
+        CT_KconfigEnableOption "UCLIBC_HAS_IPV6" "${dst}"
+    else
+        CT_KconfigDisableOption "UCLIBC_HAS_IPV6" "${dst}"
+    fi
+
     # Force on options needed for C++ if we'll be making a C++ compiler.
     # I'm not sure locales are a requirement for doing C++... Are they?
     if [ "${CT_CC_LANG_CXX}" = "y" ]; then
```

---
   
run menu config
```sh
./ct-ng menuconfig
```
Set
   - ucLib
   - hf
   - enable iPV6 Suppport
   - Cross-gdb
   - static gdbserver

---
   
then

```sh
./ct-ng build
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
   
