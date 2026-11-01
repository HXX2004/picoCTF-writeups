### 題目:
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?
### 提示:
1.Remember the flag format is academy{XXXX}
2.What's a pipe? No not that kind of pipe...
### 解法:
用nc連接題目後會跳出一堆資料
```
This is defintely not a flag
Not a flag either
I don't think this is a flag either
I don't think this is a flag either
Again, I really don't think this is a flag
I don't think this is a flag either
I don't think this is a flag either
This is defintely not a flag
Not a flag either
This is defintely not a flag
I don't think this is a flag either
This is defintely not a flag
Not a flag either
I don't think this is a flag either
Not a flag either
I don't think this is a flag either
Not a flag either
Not a flag either
Not a flag either
Not a flag either
Not a flag either
I don't think this is a flag either
This is defintely not a flag
Not a flag either
Again, I really don't think this is a flag
I don't think this is a flag either
```
這不是我們要的為了找到我們要的旗子，所以再後面加上grep去尋照關鍵字
```
nc xebec.cylabacademy.net 44196 | grep "academy"
```
### 旗子:
academy{digital_plumb3r_dFED73D2}
