# Summary
stack-buffer-overflow in progs/dump_entry.c:1144 in fmt_entry

# Version 

ncurses-6.2-20200704

# How to build
```shell
CC=clang CXX=clang++ ../configure --disable-stripping --prefix=`pwd`/mybin CFLAGS="-g -O0 -fsanitize=address" CXXFLAGS="-g -O0 -fsanitize=address"
```

# Commandline
```shell
infotocap @@
```

# ASAN report

```txt
=================================================================
==9310==ERROR: AddressSanitizer: stack-buffer-overflow on address 0x7ffc5fdce244 at pc 0x00000041bae9 bp 0x7ffc5fdcd0d0 sp 0x7ffc5fdcd0c0
WRITE of size 1 at 0x7ffc5fdce244 thread T0
    #0 0x41bae8 in fmt_entry ../../progs/dump_entry.c:1144
    #1 0x41dba5 in dump_entry ../../progs/dump_entry.c:1542
    #2 0x405eee in main ../../progs/tic.c:1041
    #3 0x7f6b50a0482f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #4 0x402578 in _start (/home/cszx/zhanggen/overflow/ncurses-6.2-20200704/build-orig-asan/mybin/bin/tic+0x402578)

Address 0x7ffc5fdce244 is located in stack of thread T0 at offset 4212 in frame
    #0 0x419bff in fmt_entry ../../progs/dump_entry.c:907

  This frame has 2 object(s):
    [32, 43) 'boxchars'
    [96, 4212) 'buffer' <== Memory access at offset 4212 overflows this variable
HINT: this may be a false positive if your program uses some custom stack unwind mechanism or swapcontext
      (longjmp and C++ exceptions *are* supported)
SUMMARY: AddressSanitizer: stack-buffer-overflow ../../progs/dump_entry.c:1144 fmt_entry
Shadow bytes around the buggy address:
  0x10000bfb1bf0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10000bfb1c00: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10000bfb1c10: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10000bfb1c20: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10000bfb1c30: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x10000bfb1c40: 00 00 00 00 00 00 00 00[04]f4 f3 f3 f3 f3 00 00
  0x10000bfb1c50: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10000bfb1c60: f1 f1 f1 f1 04 f4 f4 f4 f2 f2 f2 f2 04 f4 f4 f4
  0x10000bfb1c70: f2 f2 f2 f2 00 00 00 00 00 00 00 00 00 f4 f4 f4
  0x10000bfb1c80: f2 f2 f2 f2 00 00 00 00 00 00 00 00 00 00 f4 f4
  0x10000bfb1c90: f2 f2 f2 f2 00 00 00 00 00 00 00 00 00 00 00 00
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Heap right redzone:      fb
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack partial redzone:   f4
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
==9310==ABORTING
```
