### 題目:
Unzip this archive and find the flag.
### 提示:
1.Can grep be instructed to look at every file in a directory and its subdirectories?
### 解法:
下載檔案後用`unzip big-zip-files.zip`解壓縮會看到一堆檔案接著利用
`grep -r "academy"`

就能找到旗子了
### 旗子:
academy{gr3p_15_m4g1c_ef8790dc}
