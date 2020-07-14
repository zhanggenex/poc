# Summary
heap-buffer-overflow Bento4-1.6.0-637/Source/C++/Core/Ap4AvccAtom.cpp:165:31 in AP4_AvccAtom::AP4_AvccAtom(unsigned int, unsigned char const*)

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
==32574==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60600000ef94 at pc 0x000000580c53 bp 0x7ffc2d062c50 sp 0x7ffc2d062c48
READ of size 1 at 0x60600000ef94 thread T0
    #0 0x580c52 in AP4_AvccAtom::AP4_AvccAtom(unsigned int, unsigned char const*) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AvccAtom.cpp:165:31
    #1 0x57f0c0 in AP4_AvccAtom::Create(unsigned int, AP4_ByteStream&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AvccAtom.cpp:95:16
    #2 0x576afc in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:499:20
    #3 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #4 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #5 0x51c2bd in AP4_SampleEntry::Read(AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4SampleEntry.cpp:115:9
    #6 0x521459 in AP4_VisualSampleEntry::AP4_VisualSampleEntry(unsigned int, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4SampleEntry.cpp:742:5
    #7 0x52305d in AP4_AvcSampleEntry::AP4_AvcSampleEntry(unsigned int, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4SampleEntry.cpp:994:5
    #8 0x574d99 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:318:24
    #9 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #10 0x52939c in AP4_StsdAtom::AP4_StsdAtom(unsigned int, unsigned char, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4StsdAtom.cpp:101:13
    #11 0x52891e in AP4_StsdAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4StsdAtom.cpp:57:16
    #12 0x5765c9 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:444:20
    #13 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #14 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #15 0x5ac31a in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:139:5
    #16 0x5abc43 in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:88:20
    #17 0x5785e3 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:796:20
    #18 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #19 0x5bf57f in AP4_DrefAtom::AP4_DrefAtom(unsigned int, unsigned char, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4DrefAtom.cpp:84:16
    #20 0x5bef6e in AP4_DrefAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4DrefAtom.cpp:50:16
    #21 0x577222 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:560:20
    #22 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #23 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #24 0x5ac31a in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:139:5
    #25 0x5abc43 in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:88:20
    #26 0x5785e3 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:796:20
    #27 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #28 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #29 0x5ac31a in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:139:5
    #30 0x5abc43 in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:88:20
    #31 0x5785e3 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:796:20
    #32 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #33 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #34 0x5ac31a in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:139:5
    #35 0x5abc43 in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:88:20
    #36 0x5785e3 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:796:20
    #37 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #38 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #39 0x5ac31a in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:139:5
    #40 0x530d34 in AP4_TrakAtom::AP4_TrakAtom(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4TrakAtom.cpp:165:5
    #41 0x5799fd in AP4_TrakAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4TrakAtom.h:58:20
    #42 0x576181 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:399:20
    #43 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #44 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #45 0x5ac31a in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:139:5
    #46 0x4fca1e in AP4_MoovAtom::AP4_MoovAtom(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4MoovAtom.cpp:79:5
    #47 0x57997d in AP4_MoovAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4MoovAtom.h:56:20
    #48 0x575f96 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:379:20
    #49 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #50 0x572e9e in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:153:12
    #51 0x4f908c in AP4_File::ParseStream(AP4_ByteStream&, AP4_AtomFactory&, bool) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4File.cpp:104:12
    #52 0x4f978d in AP4_File::AP4_File(AP4_ByteStream&, bool) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4File.cpp:78:5
    #53 0x4edbdc in main /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Apps/Mp42Aac/Mp42Aac.cpp:250:22
    #54 0x7f1b61a4e82f in __libc_start_main /build/glibc-LK5gWL/glibc-2.23/csu/../csu/libc-start.c:291
    #55 0x419218 in _start (/home/cszx/zhanggen/overflow/Bento4-1.6.0-637/build-orig-asan/mp42aac+0x419218)

0x60600000ef94 is located 0 bytes to the right of 52-byte region [0x60600000ef60,0x60600000ef94)
allocated by thread T0 here:
    #0 0x4eaa90 in operator new[](unsigned long) (/home/cszx/zhanggen/overflow/Bento4-1.6.0-637/build-orig-asan/mp42aac+0x4eaa90)
    #1 0x4f7587 in AP4_DataBuffer::AP4_DataBuffer(unsigned int) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4DataBuffer.cpp:55:16
    #2 0x57eccd in AP4_AvccAtom::Create(unsigned int, AP4_ByteStream&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AvccAtom.cpp:69:20
    #3 0x576afc in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:499:20
    #4 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #5 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #6 0x51c2bd in AP4_SampleEntry::Read(AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4SampleEntry.cpp:115:9
    #7 0x521459 in AP4_VisualSampleEntry::AP4_VisualSampleEntry(unsigned int, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4SampleEntry.cpp:742:5
    #8 0x52305d in AP4_AvcSampleEntry::AP4_AvcSampleEntry(unsigned int, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4SampleEntry.cpp:994:5
    #9 0x574d99 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:318:24
    #10 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #11 0x52939c in AP4_StsdAtom::AP4_StsdAtom(unsigned int, unsigned char, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4StsdAtom.cpp:101:13
    #12 0x52891e in AP4_StsdAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4StsdAtom.cpp:57:16
    #13 0x5765c9 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:444:20
    #14 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #15 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #16 0x5ac31a in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:139:5
    #17 0x5abc43 in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:88:20
    #18 0x5785e3 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:796:20
    #19 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #20 0x5bf57f in AP4_DrefAtom::AP4_DrefAtom(unsigned int, unsigned char, unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4DrefAtom.cpp:84:16
    #21 0x5bef6e in AP4_DrefAtom::Create(unsigned int, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4DrefAtom.cpp:50:16
    #22 0x577222 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:560:20
    #23 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #24 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12
    #25 0x5ac31a in AP4_ContainerAtom::AP4_ContainerAtom(unsigned int, unsigned long long, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:139:5
    #26 0x5abc43 in AP4_ContainerAtom::Create(unsigned int, unsigned long long, bool, bool, AP4_ByteStream&, AP4_AtomFactory&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:88:20
    #27 0x5785e3 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned int, unsigned int, unsigned long long, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:796:20
    #28 0x573d68 in AP4_AtomFactory::CreateAtomFromStream(AP4_ByteStream&, unsigned long long&, AP4_Atom*&) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AtomFactory.cpp:233:14
    #29 0x5ac5a3 in AP4_ContainerAtom::ReadChildren(AP4_AtomFactory&, AP4_ByteStream&, unsigned long long) /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4ContainerAtom.cpp:194:12

SUMMARY: AddressSanitizer: heap-buffer-overflow /home/cszx/zhanggen/overflow/Bento4-1.6.0-637/Source/C++/Core/Ap4AvccAtom.cpp:165:31 in AP4_AvccAtom::AP4_AvccAtom(unsigned int, unsigned char const*)
Shadow bytes around the buggy address:
  0x0c0c7fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c0c7fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c0c7fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c0c7fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c0c7fff9de0: 00 00 00 00 00 00 04 fa fa fa fa fa 00 00 00 00
=>0x0c0c7fff9df0: 00 00[04]fa fa fa fa fa 00 00 00 00 00 00 00 fa
  0x0c0c7fff9e00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c0c7fff9e10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c0c7fff9e20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c0c7fff9e30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c0c7fff9e40: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==32574==ABORTING
```
