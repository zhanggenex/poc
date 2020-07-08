# Summary
heap-buffer-overflow in ncurses/tinfo/captoinfo.c:644 in _nc_infotocap

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
==6353==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000efef at pc 0x000000439fe4 bp 0x7ffc97291260 sp 0x7ffc97291250
READ of size 1 at 0x60200000efef thread T0
    #0 0x439fe3 in _nc_infotocap ../../ncurses/tinfo/captoinfo.c:644
    #1 0x41b767 in fmt_entry ../../progs/dump_entry.c:1114
    #2 0x41dba5 in dump_entry ../../progs/dump_entry.c:1542
    #3 0x405eee in main ../../progs/tic.c:1041
    #4 0x7f29cd87282f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #5 0x402578 in _start (/home/cszx/zhanggen/overflow/ncurses-6.2-20200704/build-orig-asan/mybin/bin/tic+0x402578)

0x60200000efef is located 1 bytes to the left of 16-byte region [0x60200000eff0,0x60200000f000)
allocated by thread T0 here:
    #0 0x7f29cdcb4602 in malloc (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x98602)
    #1 0x425e72 in _nc_doalloc ../../ncurses/tinfo/doalloc.c:56
    #2 0x43c77f in _nc_tic_expand ../../ncurses/tinfo/comp_expand.c:86
    #3 0x41b67e in fmt_entry ../../progs/dump_entry.c:1108
    #4 0x41dba5 in dump_entry ../../progs/dump_entry.c:1542
    #5 0x405eee in main ../../progs/tic.c:1041
    #6 0x7f29cd87282f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)

SUMMARY: AddressSanitizer: heap-buffer-overflow ../../ncurses/tinfo/captoinfo.c:644 _nc_infotocap
Shadow bytes around the buggy address:
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9df0: fa fa fa fa fa fa fa fa fa fa fa fa fa[fa]00 00
  0x0c047fff9e00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e40: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==6353==ABORTING

```
