# Summary
```
=================================================================
==5462==ERROR: AddressSanitizer: global-buffer-overflow on address 0x00000057af47 at pc 0x000000460e86 bp 0x7ffd205f2c00 sp 0x7ffd205f23b0
READ of size 46 at 0x00000057af47 thread T0
    #0 0x460e85  (/home/cszx/zhanggen/overflow/ncurses-6.2/build-orig-asan/mybin/bin/infocmp+0x460e85)
    #1 0x460782  (/home/cszx/zhanggen/overflow/ncurses-6.2/build-orig-asan/mybin/bin/infocmp+0x460782)
    #2 0x46167a in vfprintf (/home/cszx/zhanggen/overflow/ncurses-6.2/build-orig-asan/mybin/bin/infocmp+0x46167a)
    #3 0x461732 in fprintf (/home/cszx/zhanggen/overflow/ncurses-6.2/build-orig-asan/mybin/bin/infocmp+0x461732)
    #4 0x4ec939  (/home/cszx/zhanggen/overflow/ncurses-6.2/build-orig-asan/mybin/bin/infocmp+0x4ec939)
    #5 0x7f86926fa82f in __libc_start_main /build/glibc-LK5gWL/glibc-2.23/csu/../csu/libc-start.c:291
    #6 0x4190e8 in getenv (/home/cszx/zhanggen/overflow/ncurses-6.2/build-orig-asan/mybin/bin/infocmp+0x4190e8)

0x00000057af47 is located 0 bytes to the right of global variable 'options' defined in '../../progs/infocmp.c:1198:23' (0x57a920) of size 1575
SUMMARY: AddressSanitizer: global-buffer-overflow (/home/cszx/zhanggen/overflow/ncurses-6.2/build-orig-asan/mybin/bin/infocmp+0x460e85) 
Shadow bytes around the buggy address:
  0x0000800a7590: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0000800a75a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0000800a75b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0000800a75c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0000800a75d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0000800a75e0: 00 00 00 00 00 00 00 00[07]f9 f9 f9 f9 f9 f9 f9
  0x0000800a75f0: f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9
  0x0000800a7600: f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9
  0x0000800a7610: f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 f9 00 04 f9 f9
  0x0000800a7620: f9 f9 f9 f9 05 f9 f9 f9 f9 f9 f9 f9 00 00 00 00
  0x0000800a7630: 07 f9 f9 f9 f9 f9 f9 f9 00 03 f9 f9 f9 f9 f9 f9
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
  Left alloca redzone:     ca
  Right alloca redzone:    cb
==5462==ABORTING
```
# Version
ncurses-6.2
# Steps to reproduce
infocmp --help
# Platform
Ubuntu 16.04.6 LTS clang-3.8
