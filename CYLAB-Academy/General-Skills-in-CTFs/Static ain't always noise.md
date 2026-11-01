### 題目:
Can you look at the data in this binary? The bash script might help!
### 解法:
先將題目給的2個檔案權限
```
chmod +x ./static
chmod +x ./ltdis.sh
```
再來執行
```
xinxian-academy@webshell:~$ ./static
Oh hai! Wait what? A flag? Yes, it's around here somewhere!
xinxian-academy@webshell:~$ ./ltdis.sh
Attempting disassembly of  ...
objdump: 'a.out': No such file
objdump: section '.text' mentioned in a -j option, but not found in any input file
Disassembly failed!
Usage: ltdis.sh <program-file>
Bye!
```
根據他的提示接著做
```
xinxian-academy@webshell:~$ ./ltdis.sh ./static
Attempting disassembly of ./static ...
Disassembly successful! Available at: ./static.ltdis.x86_64.txt
Ripping strings from binary with file offsets...
Any strings found in ./static have been written to ./static.ltdis.strings.txt with file offset
```
接著用
```
grep 'academy' ./static.ltdis.strings.txt
```
找到旗子
3020 academy{d15a5m_t34s3r_fac3431a}
### 旗子:
academy{d15a5m_t34s3r_fac3431a}
