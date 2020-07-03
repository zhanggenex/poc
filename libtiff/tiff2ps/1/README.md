# ASAN output
```
=================================================================
==9301==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000eea0 at pc 0x0000004f9c42 bp 0x7ffeed2863f0 sp 0x7ffeed2863e8
READ of size 1 at 0x60200000eea0 thread T0
    #0 0x4f9c41 in PSDataColorContig /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:2479:20
    #1 0x4f1cb5 in PSpage /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:2361:4
    #2 0x4edb62 in TIFF2PS /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:1610:10
    #3 0x4ec0ed in main /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:477:9
    #4 0x7f3dbc1ea82f in __libc_start_main /build/glibc-LK5gWL/glibc-2.23/csu/../csu/libc-start.c:291
    #5 0x419c38 in _start (/home/cszx/zhanggen/overflow/tiff-4.1.0/build-orig-asan/bin/tiff2ps+0x419c38)

0x60200000eea0 is located 0 bytes to the right of 16-byte region [0x60200000ee90,0x60200000eea0)
allocated by thread T0 here:
    #0 0x4b9d68 in malloc (/home/cszx/zhanggen/overflow/tiff-4.1.0/build-orig-asan/bin/tiff2ps+0x4b9d68)
    #1 0x4f9b15 in PSDataColorContig /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:2452:29
    #2 0x4f1cb5 in PSpage /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:2361:4
    #3 0x4edb62 in TIFF2PS /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:1610:10
    #4 0x4ec0ed in main /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:477:9
    #5 0x7f3dbc1ea82f in __libc_start_main /build/glibc-LK5gWL/glibc-2.23/csu/../csu/libc-start.c:291

SUMMARY: AddressSanitizer: heap-buffer-overflow /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2ps.c:2479:20 in PSDataColorContig
Shadow bytes around the buggy address:
  0x0c047fff9d80: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9d90: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9dd0: fa fa 00 00[fa]fa 00 07 fa fa fd fa fa fa 00 fa
  0x0c047fff9de0: fa fa fd fa fa fa 00 fa fa fa fd fa fa fa 00 03
  0x0c047fff9df0: fa fa fd fd fa fa 02 fa fa fa fd fa fa fa 00 00
  0x0c047fff9e00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==9301==ABORTING
```
