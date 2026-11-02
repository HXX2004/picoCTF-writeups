### 題目:
Download the disk image and use mmls on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
### 解法:
先依照題意進入/tmp
```
cd /tmp
```
再將檔案下載並解壓縮
```
wget https://challenge-files.cylabacademy.net/library/d8718cbbc14dcd9f9aad532a51d7a01b00e1715ca3b1d654dfef687d0b15cbf5/disk.img.gz
gunzip disk.img.gz
```
透過mmls來顯示磁碟映像檔的分割區配置表
```
mmls disk.img
```
得到以下輸出
```
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
```
接著連上題目給的
```
nc chatelaine.cylabacademy.net 13468
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752
```
輸入完後就能拿到旗子
Great work!
academy{mm15_f7w!}
### 旗子:
academy{mm15_f7w!}
