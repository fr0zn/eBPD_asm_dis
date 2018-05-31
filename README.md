# eBPF

eBPD disassembler and assembler written in python

## Disassembler example

Example program

```
$ xxd program.bin
00000000: b409 0000 ffff ffff 5509 0200 ffff ffff  ........U.......
00000010: b700 0000 0000 0000 9500 0000 0000 0000  ................
00000020: 1819 0000 0300 0000 0000 0000 0000 0000  ................
00000030: bf91 0000 0000 0000 bfa2 0000 0000 0000  ................
00000040: 0702 0000 fcff ffff 620a fcff 0000 0000  ........b.......
00000050: 8500 0000 0100 0000 5500 0100 0000 0000  ........U.......
00000060: 9500 0000 0000 0000 7906 0000 0000 0000  ........y.......
00000070: bf91 0000 0000 0000 bfa2 0000 0000 0000  ................
00000080: 0702 0000 fcff ffff 620a fcff 0100 0000  ........b.......
00000090: 8500 0000 0100 0000 5500 0100 0000 0000  ........U.......
000000a0: 9500 0000 0000 0000 7907 0000 0000 0000  ........y.......
000000b0: bf91 0000 0000 0000 bfa2 0000 0000 0000  ................
000000c0: 0702 0000 fcff ffff 620a fcff 0200 0000  ........b.......
000000d0: 8500 0000 0100 0000 5500 0100 0000 0000  ........U.......
000000e0: 9500 0000 0000 0000 7908 0000 0000 0000  ........y.......
000000f0: bf02 0000 0000 0000 b700 0000 0000 0000  ................
00000100: 5506 0300 0000 0000 7973 0000 0000 0000  U.......ys......
00000110: 7b32 0000 0000 0000 9500 0000 0000 0000  {2..............
00000120: 5506 0200 0100 0000 7ba2 0000 0000 0000  U.......{.......
00000130: 9500 0000 0000 0000 7b87 0000 0000 0000  ........{.......
00000140: 9500 0000 0000 0000                      ........
```
Output

```
$ python disassembler.py program.bin

0x0000:   b4 09 00 00 ff ff ff ff      mov32     r9,       #-1
0x0001:   55 09 02 00 ff ff ff ff      jne       r9,       #-1, +2
0x0002:   b7 00 00 00 00 00 00 00      mov       r0,       #0
0x0003:   95 00 00 00 00 00 00 00      exit
0x0004:   18 19 00 00 03 00 00 00      lddw      r9,       #3
0x0005:   00 00 00 00 00 00 00 00      ldw       r0,       #0
0x0006:   bf 91 00 00 00 00 00 00      mov       r1,       r9
0x0007:   bf a2 00 00 00 00 00 00      mov       r2,       r10
0x0008:   07 02 00 00 fc ff ff ff      add       r2,       #-4
0x0009:   62 0a fc ff 00 00 00 00      stw       [r10-4],  #0
0x000a:   85 00 00 00 01 00 00 00      call      #1
0x000b:   55 00 01 00 00 00 00 00      jne       r0,       #0,  +1
0x000c:   95 00 00 00 00 00 00 00      exit
0x000d:   79 06 00 00 00 00 00 00      ldxdw     [r0]
0x000e:   bf 91 00 00 00 00 00 00      mov       r1,       r9
0x000f:   bf a2 00 00 00 00 00 00      mov       r2,       r10
0x0010:   07 02 00 00 fc ff ff ff      add       r2,       #-4
0x0011:   62 0a fc ff 01 00 00 00      stw       [r10-4],  #1
0x0012:   85 00 00 00 01 00 00 00      call      #1
0x0013:   55 00 01 00 00 00 00 00      jne       r0,       #0,  +1
0x0014:   95 00 00 00 00 00 00 00      exit
0x0015:   79 07 00 00 00 00 00 00      ldxdw     [r0]
0x0016:   bf 91 00 00 00 00 00 00      mov       r1,       r9
0x0017:   bf a2 00 00 00 00 00 00      mov       r2,       r10
0x0018:   07 02 00 00 fc ff ff ff      add       r2,       #-4
0x0019:   62 0a fc ff 02 00 00 00      stw       [r10-4],  #2
0x001a:   85 00 00 00 01 00 00 00      call      #1
0x001b:   55 00 01 00 00 00 00 00      jne       r0,       #0,  +1
0x001c:   95 00 00 00 00 00 00 00      exit
0x001d:   79 08 00 00 00 00 00 00      ldxdw     [r0]
0x001e:   bf 02 00 00 00 00 00 00      mov       r2,       r0
0x001f:   b7 00 00 00 00 00 00 00      mov       r0,       #0
0x0020:   55 06 03 00 00 00 00 00      jne       r6,       #0,  +3
0x0021:   79 73 00 00 00 00 00 00      ldxdw     [r7]
0x0022:   7b 32 00 00 00 00 00 00      stxdw     [r2],     r3
0x0023:   95 00 00 00 00 00 00 00      exit
0x0024:   55 06 02 00 01 00 00 00      jne       r6,       #1,  +2
0x0025:   7b a2 00 00 00 00 00 00      stxdw     [r2],     r10
0x0026:   95 00 00 00 00 00 00 00      exit
0x0027:   7b 87 00 00 00 00 00 00      stxdw     [r7],     r8
0x0028:   95 00 00 00 00 00 00 00      exit
```
