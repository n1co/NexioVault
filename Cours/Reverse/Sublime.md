chercher par patter dans ghidra (en big endian):
80 79 05 00 0F 94 C2

Patcher en:

0:  c6 41 05 01             mov    BYTE PTR [rcx+0x5],0x1  
4:  b2 00                   mov    dl,0x0  (pour cette ligne il va proposer jsute le B2 00 sinon pas possible d'ajouter le NOP dessous)
6:  90                      nop


En hex on patch
PATCH_BYTES = bytes([0x80, 0x79, 0x05, 0x00, 0x0F, 0x94, 0xC2])

Vers ça:
PATCH_BYTES_UNLIMITED = bytes([0xC6, 0x41, 0x05, 0x01, 0xB2, 0x00, 0x90])