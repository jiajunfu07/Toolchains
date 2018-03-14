# Toolchains

## 1. Install crosstool-NG

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

## 2. Build a toolchain for QEMU

Find a good base configuration
```
$ ./ct-ng list-samples
```
Use a generic target(arm-unknown-linux-gnueabi) for QEMU, run distclean first to make sure that there are no artifacts left over from a previous build
```
$ ./ct-ng distclean
$ ./ct-ng arm-unknown-linux-gnueabi
```
Review the configuration and make changes. In Paths and misc options, disable Render the toolchain read-only
```
$ ./ct-ng menuconfig
```
Build the toolchain
```
$ ./ct-ng build
```
### Error
The following error happen
```
[INFO ]  Performing some trivial sanity checks
[INFO ]  Build started 20180313.221654
[INFO ]  Building environment variables
[WARN ]  Directory '/home/jiajun/src' does not exist.
[WARN ]  Will not save downloaded tarballs to local storage.
[EXTRA]  Preparing working directories
[EXTRA]  Installing user-supplied crosstool-NG configuration
[EXTRA]  =================================================================
[EXTRA]  Dumping internal crosstool-NG configuration
[EXTRA]    Building a toolchain for:
[EXTRA]      build  = x86_64-pc-linux-gnu
[EXTRA]      host   = x86_64-pc-linux-gnu
[EXTRA]      target = arm-unknown-linux-gnueabi
[EXTRA]  Dumping internal crosstool-NG configuration: done in 0.37s (at 00:04)
[INFO ]  =================================================================
[INFO ]  Retrieving needed toolchain components' tarballs
[EXTRA]    Retrieving 'linux-4.3'
[ERROR]   
[ERROR]  >>
[ERROR]  >>  Build failed in step 'Retrieving needed toolchain components' tarballs'
[ERROR]  >>        called in step '(top-level)'
[ERROR]  >>
[ERROR]  >>  Error happened in: do_kernel_get[scripts/build/kernel/linux.sh@741]
[ERROR]  >>        called from: main[scripts/crosstool-NG.sh@590]
[ERROR]  >>
[ERROR]  >>  For more info on this error, look at the file: 'build.log'
[ERROR]  >>  There is a list of known issues, some with workarounds, in:
[ERROR]  >>      'docs/B - Known issues.txt'
[ERROR]   
[ERROR]  (elapsed: 4:52.69)
[04:53] / ct-ng:152: recipe for target 'build' failed
make: *** [build] Error 1
```
It seems to be a network problem. I tried many times and got success at the end. \
The build will take me 159:09.02. The toolchain is present in ~/x-tools/arm-unknown-linux-gnueabi

## 3. Add the directory to the path
```
$ vi ~/.bashrc
```
Add the following to the file
```
export PATH=$PATH:~/x-tools/arm-unknown-linux-gnueabi/bin
```
Save the file and source it
```
$ source ~/.bashrc
```
