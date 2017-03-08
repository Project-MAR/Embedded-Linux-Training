## BragleboneBlack-X-tools.md
```sh
git clone https://github.com/crosstool-ng/crosstool-ng.git
cd crosstool-ng/
git checkout -b crosstool-ng-1.22.0
autoreconf
./configure --enable-local
make
make install
./ct-ng arm-unknown-linux-gnueabi
./ct-ng menuconfig
./ct-ng build

```
./ct-ng list-samples
./ct-ng arm-cortexa5-linux-uclibcgnueabihf
