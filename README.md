# Toolchains

## 1. crosstool-NG

crosstool-NG is used to build the toolchain. before getting crosstool-NG. I need to install the packages.
```
$ sudo apt install automake bison chrpath flex g++ git gperf\
  gawk libexpatl-dev libncurses5-dev libsdl1.2-dev libtool\
  python2.7-dev texinfo help2man
```
Clone, build and install
```
$ git clone https://github.com/crosstool-ng/crosstool-ng.git
$ cd crosstool-ng
$ git checkout crosstool-ng-1.23.0
$ ./bootstrap 
$ ./configure --enable-local 
$ make 
$ make install 
```
