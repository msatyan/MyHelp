
### Cleanup corrupted shared memory segment of IDS servers without rebooting the UNIX host ******
```bash
Key: RVH
ASCII value of R=82 and its Hex is 0x52
ASCII value of V=86 and its Hex is 0x56
ASCII value of H=72 and its Hex is 0x48

RV + SERVNUM in Hex followed by 4801 (hex).
0x5256 + SERVNUM followed by 4801 (hex).

For Example the Server num 50 is Hex 0x32

0xR  (0xV + 0xServerNum) 0xH  XX
0x52  (0x56 + 0x32) 0x48 = 0x528848xx



g:lxvm-l154:/work/db2ids/srv/ids0>root ipcs | grep 528848
0x52884801 1048590    root       660        7028736    9
0x52884802 1081359    root       660        8192000    9
0x52884803 1114128    root       660        9035776    9
0x52884804 1146897    root       660        8388608    9
0x52884805 1179666    root       660        8388608    9
0x52884806 1212435    root       660        16207872   9
0x52884807 1245204    root       660        8388608    9


root ipcrm -m 1048590 -m 1081359 -m 1114128 -m 1146897 -m 1179666 -m 1212435 -m 1245204
```