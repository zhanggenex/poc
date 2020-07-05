# Summary

```
=================================================================
==20911==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000eb33 at pc 0x000000459d45 bp 0x7fff719a92a0 sp 0x7fff719a8a50
READ of size 6 at 0x60200000eb33 thread T0
    #0 0x459d44 in __interceptor_memcpy.part.42 (/home/cszx/zhanggen/overflow/tiff-4.1.0/build-orig-asan/mybin/bin/tiff2pdf+0x459d44)
    #1 0x7f231a8c84e8  (/usr/lib/x86_64-linux-gnu/libtiff.so.5+0x1a4e8)
    #2 0x7f231a8f1349 in TIFFWriteEncodedStrip (/usr/lib/x86_64-linux-gnu/libtiff.so.5+0x43349)
    #3 0x503873 in t2p_readwrite_pdf_image_tile /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2pdf.c:3247:17
    #4 0x4ef97c in t2p_write_pdf /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2pdf.c:5600:16
    #5 0x4ed345 in main /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2pdf.c:810:2
    #6 0x7f23197a282f in __libc_start_main /build/glibc-LK5gWL/glibc-2.23/csu/../csu/libc-start.c:291
    #7 0x41a6e8 in _start (/home/cszx/zhanggen/overflow/tiff-4.1.0/build-orig-asan/mybin/bin/tiff2pdf+0x41a6e8)

0x60200000eb33 is located 0 bytes to the right of 3-byte region [0x60200000eb30,0x60200000eb33)
allocated by thread T0 here:
    #0 0x4ba818 in malloc (/home/cszx/zhanggen/overflow/tiff-4.1.0/build-orig-asan/mybin/bin/tiff2pdf+0x4ba818)
    #1 0x502195 in t2p_readwrite_pdf_image_tile /home/cszx/zhanggen/overflow/tiff-4.1.0/tools/tiff2pdf.c:3020:30

SUMMARY: AddressSanitizer: heap-buffer-overflow (/home/cszx/zhanggen/overflow/tiff-4.1.0/build-orig-asan/mybin/bin/tiff2pdf+0x459d44) in __interceptor_memcpy.part.42
Shadow bytes around the buggy address:
  0x0c047fff9d10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9d20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9d30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9d40: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9d50: fa fa fa fa fa fa fa fa fa fa 00 fa fa fa 00 fa
=>0x0c047fff9d60: fa fa fd fa fa fa[03]fa fa fa fd fa fa fa 02 fa
  0x0c047fff9d70: fa fa fd fa fa fa fd fa fa fa fd fa fa fa fd fd
  0x0c047fff9d80: fa fa 00 07 fa fa fd fa fa fa fd fa fa fa fd fa
  0x0c047fff9d90: fa fa fd fa fa fa fd fa fa fa fd fd fa fa fd fa
  0x0c047fff9da0: fa fa fd fa fa fa fd fa fa fa fd fa fa fa fd fa
  0x0c047fff9db0: fa fa fd fd fa fa fd fa fa fa fd fa fa fa fd fa
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
==20911==ABORTING
```

# Version

tiff-4.1.0

# Steps to reproduce

tiff2pdf id:000001,sig:06,src:000648+000501,op:splice,rep:2

# Platform

Ubuntu 16.04.6 LTS clang-3.8
