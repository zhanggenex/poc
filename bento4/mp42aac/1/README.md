# Summary
heap-buffer-overflow Bento4-1.6.0-637/Source/C++/Core/Ap4HvccAtom.cpp:282:24 in AP4_HvccAtom::AP4_HvccAtom(unsigned int, unsigned char const*)

# Version

Bento4-1.6.0-637

# How to build
```shell
cmake -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ -DCMAKE_INSTALL_PREFIX=`pwd`/mybin -DCMAKE_C_FLAGS="-g -O0 -fsanitize=address" -DCMAKE_CXX_FLAGS="-g -O0 -fsanitize=address" ../
```

# Commandline
```shell
mp42aac @@ a.aac
```

# ASAN report

```txt
=================================================================
==9947==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60300000ef36 at pc 0x0000005d0fac bp 0x7ffdd5010f00 sp 0x7ffdd5010ef8
READ of size 1 at 0x60300000ef36 thread T0
    #0 0x5d0fab in AP4_HvccAtom::AP4_HvccAtom(unsigned int, unsigned char const*) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4HvccAtom.cpp:282:24
    #1 0x5cba32 in AP4_HvccAtom::Create(unsigned int, AP4_ByteStream&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4HvccAtom.cpp:90:16
    #2 0x576b75 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:504:20
    #3 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #4 0x572e9e in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:153:12
    #5 0x4f908c in AP4_File::ParseStream(AP4_ByteStream&, AP4_AtomFactory&, bool) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4File.cpp:104:12
    #6 0x4f978d in AP4_File::AP4_File(AP4_ByteStream&, bool) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4File.cpp:78:5
    #7 0x4edbdc in main /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Apps/Mp42Aac/Mp42Aac.cpp:250:22
    #8 0x7f39dce1582f in __libc_start_main /build/glibc-LK5gWL/glibc-2.23/csu/../csu/libc-start.c:291
    #9 0x419218 in _start (/home/cszx/zhanggen/overflow/Bento4-1.6.0-637/build-orig-asan/mp42aac+0x419218)

0x60300000ef36 is located 0 bytes to the right of 22-byte region [0x60300000ef20,0x60300000ef36)
allocated by thread T0 here:
    #0 0x4eaa90 in operator new[](unsigned long) (/home/cszx/zhanggen/overflow/Bento4-1.6.0-637/build-orig-asan/mp42aac+0x4eaa90)
    #1 0x4f7587 in AP4_DataBuffer::AP4_DataBuffer(unsigned int) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4DataBuffer.cpp:55:16
    #2 0x5cb96b in AP4_HvccAtom::Create(unsigned int, AP4_ByteStream&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4HvccAtom.cpp:86:20
    #3 0x576b75 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:504:20
    #4 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #5 0x572e9e in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:153:12
    #6 0x4f908c in AP4_File::ParseStream(AP4_ByteStream&, AP4_AtomFactory&, bool) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4File.cpp:104:12
    #7 0x4f978d in AP4_File::AP4_File(AP4_ByteStream&, bool) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4File.cpp:78:5
    #8 0x4edbdc in main /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Apps/Mp42Aac/Mp42Aac.cpp:250:22
    #9 0x7f39dce1582f in __libc_start_main /build/glibc-LK5gWL/glibc-2.23/csu/../csu/libc-start.c:291

SUMMARY: AddressSanitizer: heap-buffer-overflow /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4HvccAtom.cpp:282:24 in AP4_HvccAtom::AP4_HvccAtom(unsigned int, unsigned char const*)
Shadow bytes around the buggy address:
  0x0c067fff9d90: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa 00 00
=>0x0c067fff9de0: 06 fa fa fa 00 00[06]fa fa fa 00 00 00 fa fa fa
  0x0c067fff9df0: 00 00 00 fa fa fa 00 00 00 fa fa fa 00 00 00 fa
  0x0c067fff9e00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9e10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9e20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9e30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==9947==ABORTING
```
