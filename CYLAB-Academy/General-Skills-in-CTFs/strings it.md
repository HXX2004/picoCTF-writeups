### 題目:
Can you find the flag in file without running it?
### 提示:
1.strings
### 解法:
下載檔案後
```
chmod +x string
./strings
```
```
Maybe try the 'strings' function? Take a look at the man page
```
```
man strings
```
看到最上面的`strings - print the sequences of printable characters in files`按q退出後
```
strings strings
```
會跑出很多東西出來，透過grep篩選字串
```
strings strings | grep "academy"
```
### 旗子:
academy{5tRIng5_1T_b1e21039}
