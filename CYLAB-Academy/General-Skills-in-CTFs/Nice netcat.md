### 題目:
There is a nice program that you can talk to by using this command in a shell:
### 提示:
1.You can practice using netcat with this Challenge Library problem:what's a netcat?
2.You can practice reading and writing ASCII with this Challenge Library problem:Let's Warm Up
### 解法:
用nc去連接到題目給的實例。

`nc chatelaine.cylabacademy.net 28970`
會得到以下輸出
```
97 
99 
97 
100 
101 
109 
121 
123 
103 
48 
48 
100 
95 
107 
49 
116 
116 
121 
33 
95 
110 
49 
99 
51 
95 
107 
49 
116 
116 
121 
33 
95 
54 
100 
49 
101 
54 
125 
10
```
再將這些ASCII 十進位數值轉換為文字後，得到的旗子
### 旗子:
academy{g00d_k1tty!_n1c3_k1tty!_6d1e6}
