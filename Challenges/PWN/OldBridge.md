```console
root@kali:/mnt/hgfs/HackTheBox/Challenges/OldBridge# file oldbridge 
oldbridge: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=30d49dc8bfda0dfd78b99f11b938bbee5601ddc9, not stripped
root@kali:/mnt/hgfs/HackTheBox/Challenges/OldBridge# binwalk oldbridge 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             ELF, 64-bit LSB shared object, AMD x86-64, version 1 (SYSV)

root@kali:/mnt/hgfs/HackTheBox/Challenges/OldBridge# readelf -h oldbridge 
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Shared object file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0xa30
  Start of program headers:          64 (bytes into file)
  Start of section headers:          11624 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         9
  Size of section headers:           64 (bytes)
  Number of section headers:         30
  Section header string table index: 29
root@kali:/mnt/hgfs/HackTheBox/Challenges/OldBridge# readelf -l oldbridge 

Elf file type is DYN (Shared object file)
Entry point 0xa30
There are 9 program headers, starting at offset 64

Program Headers:
  Type           Offset             VirtAddr           PhysAddr
                 FileSiz            MemSiz              Flags  Align
  PHDR           0x0000000000000040 0x0000000000000040 0x0000000000000040
                 0x00000000000001f8 0x00000000000001f8  R      0x8
  INTERP         0x0000000000000238 0x0000000000000238 0x0000000000000238
                 0x000000000000001c 0x000000000000001c  R      0x1
      [Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]
  LOAD           0x0000000000000000 0x0000000000000000 0x0000000000000000
                 0x00000000000011a8 0x00000000000011a8  R E    0x200000
  LOAD           0x0000000000001de8 0x0000000000201de8 0x0000000000201de8
                 0x00000000000002d4 0x00000000000002d8  RW     0x200000
  DYNAMIC        0x0000000000001df8 0x0000000000201df8 0x0000000000201df8
                 0x00000000000001e0 0x00000000000001e0  RW     0x8
  NOTE           0x0000000000000254 0x0000000000000254 0x0000000000000254
                 0x0000000000000044 0x0000000000000044  R      0x4
  GNU_EH_FRAME   0x0000000000000ff4 0x0000000000000ff4 0x0000000000000ff4
                 0x0000000000000054 0x0000000000000054  R      0x4
  GNU_STACK      0x0000000000000000 0x0000000000000000 0x0000000000000000
                 0x0000000000000000 0x0000000000000000  RW     0x10
  GNU_RELRO      0x0000000000001de8 0x0000000000201de8 0x0000000000201de8
                 0x0000000000000218 0x0000000000000218  R      0x1

 Section to Segment mapping:
  Segment Sections...
   00     
   01     .interp 
   02     .interp .note.ABI-tag .note.gnu.build-id .gnu.hash .dynsym .dynstr .gnu.version .gnu.version_r .rela.dyn .rela.plt .init .plt .plt.got .text .fini .rodata .eh_frame_hdr .eh_frame 
   03     .init_array .fini_array .dynamic .got .got.plt .data .bss 
   04     .dynamic 
   05     .note.ABI-tag .note.gnu.build-id 
   06     .eh_frame_hdr 
   07     
   08     .init_array .fini_array .dynamic .got 
root@kali:/mnt/hgfs/HackTheBox/Challenges/OldBridge# 
```
From Magic
7f 45 4c 46 ==> ELF File
02 ==> 64Bit
01 ==> little endian
