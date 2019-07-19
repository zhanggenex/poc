# bento4

## version 

    bento4 1.5.1.0

## description

```txt
mp42acc 1.0
```

## download link

    https://www.bento4.com/

## others

    please send email to  teamseri0us360@gmail.com if you have any questions.

---------------------

## AP4_BitReader::SkipBits@Ap4Utils.cpp-548___heap-buffer-overflow

### description

    An issue was discovered in bento4 1.5.1.0, There is a/an heap-buffer-overflow in function AP4_BitReader::SkipBits at Ap4Utils.cpp-548

### commandline

    mp42aac @@ a.aac

### source

```c
 544          m_BitsCached = AP4_WORD_BITS-n;
 545          m_Position += AP4_WORD_BYTES;
 546       } else {
 547          m_BitsCached = 0;
 548          m_Cache = 0;
 549       }
 550    }
 551 }
 552 
 553 /*----------------------------------------------------------------------

```

### bug report

```txt
=================================================================
==26617==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60400000de7c at pc 0x0000004867b1 bp 0x7ffc1efd5fc0 sp 0x7ffc1efd5fb0
READ of size 4 at 0x60400000de7c thread T0
    #0 0x4867b0 in AP4_BitReader::SkipBits(unsigned int) /src/bento4/Source/C++/Core/Ap4Utils.cpp:548
    #1 0x5bb555 in AP4_Dac4Atom::AP4_Dac4Atom(unsigned int, unsigned char const*) /src/bento4/Source/C++/Core/Ap4Dac4Atom.cpp:174
    #2 0x5bc562 in AP4_Dac4Atom::Create(unsigned int, AP4_ByteStream&) /src/bento4/Source/C++/Core/Ap4Dac4Atom.cpp:56
    #3 0x57e158 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:724
    #4 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #5 0x5735f8 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:194
    #6 0x521289 in AP4_SampleEntry::Read(AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4SampleEntry.cpp:115
    #7 0x521289 in AP4_AudioSampleEntry::AP4_AudioSampleEntry(unsigned int, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4SampleEntry.cpp:420
    #8 0x57c49a in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:324
    #9 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #10 0x53034e in AP4_StsdAtom::AP4_StsdAtom(unsigned int, unsigned char, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4StsdAtom.cpp:101
    #11 0x532124 in AP4_StsdAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4StsdAtom.cpp:57
    #12 0x57e3fb in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:424
    #13 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #14 0x5712f9 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:194
    #15 0x5712f9 in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:139
    #16 0x57212e in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:88
    #17 0x57b67e in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:764
    #18 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #19 0x472604 in AP4_DrefAtom::AP4_DrefAtom(unsigned int, unsigned char, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4DrefAtom.cpp:84
    #20 0x472af7 in AP4_DrefAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4DrefAtom.cpp:50
    #21 0x57d243 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:535
    #22 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #23 0x5712f9 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:194
    #24 0x5712f9 in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:139
    #25 0x57212e in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:88
    #26 0x57b67e in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:764
    #27 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #28 0x5712f9 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:194
    #29 0x5712f9 in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:139
    #30 0x57212e in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:88
    #31 0x57b67e in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:764
    #32 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #33 0x5712f9 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:194
    #34 0x5712f9 in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:139
    #35 0x57212e in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:88
    #36 0x57b67e in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:764
    #37 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #38 0x5712f9 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:194
    #39 0x5712f9 in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:139
    #40 0x46d252 in AP4_TrakAtom::AP4_TrakAtom(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4TrakAtom.cpp:165
    #41 0x57de8a in AP4_TrakAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4TrakAtom.h:58
    #42 0x57de8a in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:379
    #43 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #44 0x5712f9 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:194
    #45 0x5712f9 in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:139
    #46 0x4fa8dc in AP4_MoovAtom::AP4_MoovAtom(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4MoovAtom.cpp:80
    #47 0x57baf9 in AP4_MoovAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4MoovAtom.h:56
    #48 0x57baf9 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:359
    #49 0x58185d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #50 0x58185d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:151
    #51 0x5002c7 in AP4_File::ParseStream(AP4_ByteStream&, AP4_AtomFactory&, bool) /src/bento4/Source/C++/Core/Ap4File.cpp:104
    #52 0x5002c7 in AP4_File::AP4_File(AP4_ByteStream&, bool) /src/bento4/Source/C++/Core/Ap4File.cpp:78
    #53 0x43ec52 in main /src/bento4/Source/C++/Apps/Mp42Aac/Mp42Aac.cpp:250
    #54 0x7f7ea76dd82f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #55 0x442c18 in _start (/src/aflbuild/installed/bin/mp42aac+0x442c18)

0x60400000de7c is located 0 bytes to the right of 44-byte region [0x60400000de50,0x60400000de7c)
allocated by thread T0 here:
    #0 0x7f7ea80b86b2 in operator new[](unsigned long) (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x996b2)
    #1 0x5071d5 in AP4_DataBuffer::ReallocateBuffer(unsigned int) /src/bento4/Source/C++/Core/Ap4DataBuffer.cpp:210
    #2 0x5071d5 in AP4_DataBuffer::SetBufferSize(unsigned int) /src/bento4/Source/C++/Core/Ap4DataBuffer.cpp:136

SUMMARY: AddressSanitizer: heap-buffer-overflow /src/bento4/Source/C++/Core/Ap4Utils.cpp:548 AP4_BitReader::SkipBits(unsigned int)
Shadow bytes around the buggy address:
  0x0c087fff9b70: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c087fff9b80: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c087fff9b90: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c087fff9ba0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c087fff9bb0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c087fff9bc0: fa fa fa fa fa fa fa fa fa fa 00 00 00 00 00[04]
  0x0c087fff9bd0: fa fa 00 00 00 00 00 03 fa fa 00 00 00 00 00 03
  0x0c087fff9be0: fa fa 00 00 00 00 00 00 fa fa 00 00 00 00 00 02
  0x0c087fff9bf0: fa fa 00 00 00 00 00 00 fa fa 00 00 00 00 00 00
  0x0c087fff9c00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c087fff9c10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==26617==ABORTING

```

### others

    from fuzz project pwd-bento4-mp42aac-00
    crash name AP4_BitReader::SkipBits@Ap4Utils.cpp-548___heap-buffer-overflow
    Auto-generated by pyspider at 2019-07-16 17:39:41

    please send email to  teamseri0us360@gmail.com if you have any questions.

## AP4_Dec3Atom::AP4_Dec3Atom@Ap4Dec3Atom.cpp-97___heap-buffer-overflow

### description

    An issue was discovered in bento4 1.5.1.0, There is a/an heap-buffer-overflow in function AP4_Dec3Atom::AP4_Dec3Atom at Ap4Dec3Atom.cpp-97

### commandline

    mp42aac @@ a.aac

### source

```c
  93         m_SubStreams[i].acmod       = (payload[1]>>1) & 0x7;
  94         m_SubStreams[i].lfeon       = (payload[1]   ) & 0x1;
  95         m_SubStreams[i].num_dep_sub = (payload[2]>>1) & 0xF;
  96         if (m_SubStreams[i].num_dep_sub) {
  97             m_SubStreams[i].chan_loc = (payload[2]<<7 | payload[3]) & 0x1F;
  98             payload      += 4;
  99             payload_size -= 4;
 100         } else {
 101             m_SubStreams[i].chan_loc = 0;
 102             payload      += 3;

```

### bug report

```txt
=================================================================
==858==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000eeff at pc 0x000000673435 bp 0x7ffdd9983710 sp 0x7ffdd9983700
READ of size 1 at 0x60200000eeff thread T0
    #0 0x673434 in AP4_Dec3Atom::AP4_Dec3Atom(unsigned int, unsigned char const*) /src/bento4/Source/C++/Core/Ap4Dec3Atom.cpp:97
    #1 0x673ac8 in AP4_Dec3Atom::Create(unsigned int, AP4_ByteStream&) /src/bento4/Source/C++/Core/Ap4Dec3Atom.cpp:56
    #2 0x57ce5f in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:717
    #3 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #4 0x5735f8 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /src/bento4/Source/C++/Core/Ap4ContainerAtom.cpp:194
    #5 0x521289 in AP4_SampleEntry::Read(AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4SampleEntry.cpp:115
    #6 0x521289 in AP4_AudioSampleEntry::AP4_AudioSampleEntry(unsigned int, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4SampleEntry.cpp:420
    #7 0x4e2d5d in AP4_EncaSampleEntry::AP4_EncaSampleEntry(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4Protection.cpp:74
    #8 0x57c570 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:285
    #9 0x582669 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #10 0x53034e in AP4_StsdAtom::AP4_StsdAtom(unsigned int, unsigned char, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4StsdAtom.cpp:101
    #11 0x532124 in AP4_StsdAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /src/bento4/Source/C++/Core/Ap4StsdAtom.cpp:57
    #12 0x57e3fb in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:424
    #13 0x58185d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:221
    #14 0x58185d in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, AP4_Atom*&) /src/bento4/Source/C++/Core/Ap4AtomFactory.cpp:151
    #15 0x5002c7 in AP4_File::ParseStream(AP4_ByteStream&, AP4_AtomFactory&, bool) /src/bento4/Source/C++/Core/Ap4File.cpp:104
    #16 0x5002c7 in AP4_File::AP4_File(AP4_ByteStream&, bool) /src/bento4/Source/C++/Core/Ap4File.cpp:78
    #17 0x43ec52 in main /src/bento4/Source/C++/Apps/Mp42Aac/Mp42Aac.cpp:250
    #18 0x7f83e4c7182f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #19 0x442c18 in _start (/src/aflbuild/installed/bin/mp42aac+0x442c18)

0x60200000eeff is located 0 bytes to the right of 15-byte region [0x60200000eef0,0x60200000eeff)
allocated by thread T0 here:
    #0 0x7f83e564c6b2 in operator new[](unsigned long) (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x996b2)
    #1 0x506326 in AP4_DataBuffer::AP4_DataBuffer(unsigned int) /src/bento4/Source/C++/Core/Ap4DataBuffer.cpp:55
    #2 0xe  (<unknown module>)

SUMMARY: AddressSanitizer: heap-buffer-overflow /src/bento4/Source/C++/Core/Ap4Dec3Atom.cpp:97 AP4_Dec3Atom::AP4_Dec3Atom(unsigned int, unsigned char const*)
Shadow bytes around the buggy address:
  0x0c047fff9d80: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9d90: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa 00 07 fa fa 00[07]
  0x0c047fff9de0: fa fa 00 fa fa fa 01 fa fa fa fd fa fa fa 04 fa
  0x0c047fff9df0: fa fa 00 00 fa fa 00 00 fa fa 00 00 fa fa 00 00
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
==858==ABORTING

```

### others

    from fuzz project pwd-bento4-mp42aac-00
    crash name AP4_Dec3Atom::AP4_Dec3Atom@Ap4Dec3Atom.cpp-97___heap-buffer-overflow
    Auto-generated by pyspider at 2019-07-17 17:12:37

    please send email to  teamseri0us360@gmail.com if you have any questions.

