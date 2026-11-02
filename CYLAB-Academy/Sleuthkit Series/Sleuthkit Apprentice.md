### 題目:
Download this disk image and find the flag.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
### 解法:
先進入 `/tmp`，再下載及解壓縮題目提供的檔案。
```
cd /tmp
```
接著使用題目提供的下載網址執行 `wget`，再解壓縮並確認檔案：

```
wget https://challenge-files.cylabacademy.net/library/699d021acdedf3ce7c6944b6f3e16046a82b3a1f7ee2e79716132292ce4adbbd/disk.flag.img.gz
gunzip disk.flag.img.gz
ls -lh
```
解壓縮後得到 `disk.flag.img`，作為後續分析的磁碟映像檔。

### 嘗試直接搜尋旗子

先使用 `srch_strings` 擷取映像檔中的可讀字串，再以 `grep` 篩選符合旗子格式的內容。

```
srch_strings /tmp/disk.flag.img | grep -i "academy{"
```

這次沒有任何輸出，因此改用 TSK 工具分析磁碟結構，確認旗子可能位於哪個分割區及檔案中。

### 分析磁碟映像檔的分割區

```
mmls /tmp/disk.flag.img
```
輸出顯示磁碟映像檔使用 DOS Partition Table，並包含三個主要區域：

- 起始 sector `2048`：Linux 分割區。
- 起始 sector `206848`：Linux Swap / Solaris x86 分割區。
- 起始 sector `360448`：另一個 Linux 分割區。

這代表不能只假設旗子位於第一個 Linux 分割區，必須根據題目目標逐一檢查可能的分割區。

### 在第三個分割區尋找 flag 檔案

根據 `mmls` 的結果，第三個分割區從 sector `360448` 開始，因此執行：
```
fls -o 360448 -r /tmp/disk.flag.img | grep -i "flag"
```
參數說明：
- `fls`：列出檔案系統中的檔案與目錄。
- `-o 360448`：指定第三個分割區的起始 sector。
- `-r`：遞迴搜尋子目錄。
- `grep -i "flag"`：篩選名稱包含 `flag` 的項目。

輸出結果：
```
++ r/r * 2082(realloc): flag.txt
++ r/r 2371:    flag.uni.txt
```
這裡找到兩個與 flag 相關的檔案：
- `flag.txt`：metadata address 為 `2082`，並標示為已刪除的項目。
- `flag.uni.txt`：metadata address 為 `2371`。
其中，`*` 通常表示該項目已被刪除；即使如此，仍可嘗試讀取其內容。

### 讀取檔案內容取得旗子

使用 `icat` 讀取第一個檔案：

```
icat -o 360448 /tmp/disk.flag.img 2082
```
再讀取第二個檔案：
```
icat -o 360448 /tmp/disk.flag.img 2371
```
`icat` 會依照指定的分割區起始位置及 metadata address 讀取檔案內容。透過檢查輸出，即可找到題目要求的 flag。

### 完整解題流程

```text
下載並解壓縮磁碟映像檔
             |
             v
 srch_strings + grep 搜尋旗子
             |
             v
       沒有搜尋結果
             |
             v
       mmls 查看分割區
             |
             v
 確認第三個 Linux 分割區
 起始 sector = 360448
             |
             v
 fls -o 360448 -r 搜尋檔案
             |
             v
 找到 flag.txt 和 flag.uni.txt
             |
             v
 icat 讀取兩個檔案內容
             |
             v
          取得旗子
```
### 旗子:
academy{by73_5urf3r_6395be48}
