# bento4

## version 

    bento4 1.5.1.0

## description

```txt
None
```

## download link

    https://www.bento4.com/

## others

    please send email to  teamseri0us360@gmail.com if you have any questions.

---------------------

## AP4_AvccAtom::Create@Ap4AvccAtom.cpp-88___heap-buffer-overflow

### description

    An issue was discovered in bento4 1.5.1.0, There is a/an heap-buffer-overflow in function AP4_AvccAtom::Create at Ap4AvccAtom.cpp-88

### commandline

    mp4compact @@ a.mp4

### source

```c
  84         if (cursor+2 > payload_size) return NULL;
  85         cursor += 2+AP4_BytesToInt16BE(&payload[cursor]);
  86         if (cursor > payload_size) return NULL;
  87     }
  88     unsigned int num_pic_params = payload[cursor++];
  89     if (cursor > payload_size) return NULL;
  90     for (unsigned int i=0; i<num_pic_params; i++) {
  91         if (cursor+2 > payload_size) return NULL;
  92         cursor += 2+AP4_BytesToInt16BE(&payload[cursor]);
  93         if (cursor > payload_size) return NULL;

```

### bug report

```txt
=================================================================
==5329==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000ef96 at pc 0x000000505821 bp 0x7ffc86645ff0 sp 0x7ffc86645fe0
READ of size 1 at 0x60200000ef96 thread T0
    #0 0x505820 in AP4_AvccAtom::Create(unsigned int, AP4_ByteStream&) /src/bento4/Source/C++/Core/Ap4AvccAtom.cpp:88
    #1 0x45092f in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:502
    #2 0x45425d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #3 0x45425d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:151
    #4 0x4a5886 in AP4_Processor::Process(AP4_ByteStream&, AP4_ByteStream&, AP4_ByteStream*, AP4_Processor::ProgressListener*, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4Processor.cpp:441
    #5 0x43e7a0 in main /src/bento4/Source/C++/Apps/Mp4Compact/Mp4Compact.cpp:220
    #6 0x7f3dd43b882f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #7 0x441d88 in _start (/src/aflbuild/installed/bin/mp4compact+0x441d88)

0x60200000ef96 is located 0 bytes to the right of 6-byte region [0x60200000ef90,0x60200000ef96)
allocated by thread T0 here:
    #0 0x7f3dd4d936b2 in operator new[](unsigned long) (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x996b2)
    #1 0x5aeb46 in AP4_DataBuffer::AP4_DataBuffer(unsigned int) /src/bento4/Source/C++/Core/Ap4DataBuffer.cpp:55
    #2 0x5  (<unknown module>)

SUMMARY: AddressSanitizer: heap-buffer-overflow /src/bento4/Source/C++/Core/Ap4AvccAtom.cpp:88 AP4_AvccAtom::Create(unsigned int, AP4_ByteStream&)
Shadow bytes around the buggy address:
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9df0: fa fa[06]fa fa fa 00 00 fa fa 00 00 fa fa 00 00
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
==5329==ABORTING

```

### others

    from fuzz project pwd-bento4-mp4compact-00
    crash name AP4_AvccAtom::Create@Ap4AvccAtom.cpp-88___heap-buffer-overflow
    Auto-generated by pyspider at 2019-07-11 14:36:49

    please send email to  teamseri0us360@gmail.com if you have any questions.

### input

[input](https://github.com/zhanggenex/poc/blob/master/bento4/mp4compact/AP4_AvccAtom::Create%40Ap4AvccAtom.cpp-88___heap-buffer-overflow)

## AP4_RtpAtom::AP4_RtpAtom@Ap4RtpAtom.cpp-51___heap-buffer-overflow

### description

    An issue was discovered in bento4 1.5.1.0, There is a/an heap-buffer-overflow in function AP4_RtpAtom::AP4_RtpAtom at Ap4RtpAtom.cpp-51

### commandline

    mp4compact --verbose @@ a.mp4

### source

```c
  47     int str_size = size-(AP4_ATOM_HEADER_SIZE+4);
  48     if (str_size) {
  49         char* str = new char[str_size+1];
  50         stream.Read(str, str_size);
  51         str[str_size] = '\0'; // force null-termination
  52         m_SdpText = str;
  53         delete[] str;
  54     }
  55 }
  56 

```

### bug report

```txt
=================================================================
==7361==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000ef8f at pc 0x0000005e5041 bp 0x7ffffdbbf8c0 sp 0x7ffffdbbf8b0
WRITE of size 1 at 0x60200000ef8f thread T0
    #0 0x5e5040 in AP4_RtpAtom::AP4_RtpAtom(unsigned int, AP4_ByteStream&) /src/bento4/Source/C++/Core/Ap4RtpAtom.cpp:51
    #1 0x45015b in AP4_RtpAtom::Create(unsigned int, AP4_ByteStream&) /src/bento4/Source/C++/Core/Ap4RtpAtom.h:53
    #2 0x45015b in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:644
    #3 0x45425d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #4 0x45425d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:151
    #5 0x4a5886 in AP4_Processor::Process(AP4_ByteStream&, AP4_ByteStream&, AP4_ByteStream*, AP4_Processor::ProgressListener*, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4Processor.cpp:441
    #6 0x43e7a0 in main /src/bento4/Source/C++/Apps/Mp4Compact/Mp4Compact.cpp:220
    #7 0x7fa4b718382f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #8 0x441d88 in _start (/src/aflbuild/installed/bin/mp4compact+0x441d88)

0x60200000ef8f is located 1 bytes to the left of 1-byte region [0x60200000ef90,0x60200000ef91)
allocated by thread T0 here:
    #0 0x7fa4b7b5e6b2 in operator new[](unsigned long) (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x996b2)
    #1 0x5e4faa in AP4_RtpAtom::AP4_RtpAtom(unsigned int, AP4_ByteStream&) /src/bento4/Source/C++/Core/Ap4RtpAtom.cpp:49

SUMMARY: AddressSanitizer: heap-buffer-overflow /src/bento4/Source/C++/Core/Ap4RtpAtom.cpp:51 AP4_RtpAtom::AP4_RtpAtom(unsigned int, AP4_ByteStream&)
Shadow bytes around the buggy address:
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9df0: fa[fa]01 fa fa fa 00 00 fa fa 00 00 fa fa 00 00
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
==7361==ABORTING

```

### others

    from fuzz project pwd-bento4-mp4compact-01
    crash name AP4_RtpAtom::AP4_RtpAtom@Ap4RtpAtom.cpp-51___heap-buffer-overflow
    Auto-generated by pyspider at 2019-07-11 09:34:29

    please send email to  teamseri0us360@gmail.com if you have any questions.

### input
[input](https://github.com/zhanggenex/poc/blob/master/bento4/mp4compact/AP4_RtpAtom::AP4_RtpAtom%40Ap4RtpAtom.cpp-51___heap-buffer-overflow)

## AP4_AvccAtom::AP4_AvccAtom@Ap4AvccAtom.cpp-165___heap-buffer-overflow

### description

    An issue was discovered in bento4 1.5.1.0, There is a/an heap-buffer-overflow in function AP4_AvccAtom::AP4_AvccAtom at Ap4AvccAtom.cpp-165

### commandline

    mp4compact --verbose @@ a.mp4

### source

```c
 161                 cursor += param_length;
 162             }
 163         }
 164     }
 165     AP4_UI08 num_pic_params = payload[cursor++];
 166     m_PictureParameters.EnsureCapacity(num_pic_params);
 167     for (unsigned int i=0; i<num_pic_params; i++) {
 168         if (cursor+2 <= payload_size) {
 169             AP4_UI16 param_length = AP4_BytesToInt16BE(&payload[cursor]);
 170             cursor += 2;

```

### bug report

```txt
=================================================================
==19872==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000ef9c at pc 0x0000005048e0 bp 0x7fff67ebef30 sp 0x7fff67ebef20
READ of size 1 at 0x60200000ef9c thread T0
    #0 0x5048df in AP4_AvccAtom::AP4_AvccAtom(unsigned int, unsigned char const*) /src/bento4/Source/C++/Core/Ap4AvccAtom.cpp:165
    #1 0x505662 in AP4_AvccAtom::Create(unsigned int, AP4_ByteStream&) /src/bento4/Source/C++/Core/Ap4AvccAtom.cpp:95
    #2 0x45092f in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:502
    #3 0x45425d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #4 0x45425d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:151
    #5 0x4a5886 in AP4_Processor::Process(AP4_ByteStream&, AP4_ByteStream&, AP4_ByteStream*, AP4_Processor::ProgressListener*, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4Processor.cpp:441
    #6 0x43e7a0 in main /src/bento4/Source/C++/Apps/Mp4Compact/Mp4Compact.cpp:220
    #7 0x7f9dba4ef82f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #8 0x441d88 in _start (/src/aflbuild/installed/bin/mp4compact+0x441d88)

0x60200000ef9c is located 0 bytes to the right of 12-byte region [0x60200000ef90,0x60200000ef9c)
allocated by thread T0 here:
    #0 0x7f9dbaeca6b2 in operator new[](unsigned long) (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x996b2)
    #1 0x5aeb46 in AP4_DataBuffer::AP4_DataBuffer(unsigned int) /src/bento4/Source/C++/Core/Ap4DataBuffer.cpp:55
    #2 0xb  (<unknown module>)

SUMMARY: AddressSanitizer: heap-buffer-overflow /src/bento4/Source/C++/Core/Ap4AvccAtom.cpp:165 AP4_AvccAtom::AP4_AvccAtom(unsigned int, unsigned char const*)
Shadow bytes around the buggy address:
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa 00 04
=>0x0c047fff9df0: fa fa 00[04]fa fa 00 00 fa fa 00 00 fa fa 00 00
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
==19872==ABORTING

```

### others

    from fuzz project pwd-bento4-mp4compact-01
    crash name AP4_AvccAtom::AP4_AvccAtom@Ap4AvccAtom.cpp-165___heap-buffer-overflow
    Auto-generated by pyspider at 2019-07-13 21:51:25

    please send email to  teamseri0us360@gmail.com if you have any questions.

### input
[input](https://github.com/zhanggenex/poc/blob/master/bento4/mp4compact/AP4_AvccAtom::AP4_AvccAtom%40Ap4AvccAtom.cpp-165___heap-buffer-overflow)

