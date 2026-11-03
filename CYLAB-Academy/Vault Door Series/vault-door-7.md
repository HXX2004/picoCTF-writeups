### 題目:
This vault uses bit shifts to convert a password string into an array of integers. Hurry, agent, 
we are running out of time to stop Dr. Evil's nefarious plans! The source code for this vault is here:
### 提示:
1.Use a decimal/hexadecimal converter such as this one: https://www.mathsisfun.com/binary-decimal-hexadecimal-converter.html
2.You will also need to consult an ASCII table such as this one: https://www.asciitable.com/
### 解法:
### 分析題目程式
題目提供 `VaultDoor4.java`，說明每個字元可以用 ASCII 編碼表示成一個 byte，而 4 個 byte 可以透過位元運算合併成一個 32-bit 的整數。
在 `passwordToIntArray()` 中，程式每 4 個字元合併成一個整數，最後將 32 個字元的密碼轉換成包含 8 個整數的陣列。
```
x[i] = hexBytes[i*4]   << 24
     | hexBytes[i*4+1] << 16
     | hexBytes[i*4+2] << 8
     | hexBytes[i*4+3];
```
而 `checkPassword()` 則會將轉換後的 8 個整數，與程式中寫死的數值逐一比較。因此，只要反向拆解這些整數，就能還原原始密碼。
### 將十進位整數轉成二進位
先從 `checkPassword()` 找出 8 個整數，依序將它們轉換成二進位。
轉換時需要注意，每個整數代表固定的 32 bits。如果轉換結果不足 32 bits，必須在最左側補上 `0`，避免後續分組錯誤。
例如，第 0 個整數轉換後為：
```
1000001010111110110001000110001
```
由於只有 31 bits，因此在最左側補上 `0`：
```
01000001010111110110001000110001
```
### 每 8 bits 分成一組
每個整數由 4 個 byte 組成，因此將 32 bits 從左到右切成 4 組，每組 8 bits。
第 0 組的結果如下：
```
01000001 01011111 01100010 00110001
```
這 4 組分別代表原始密碼中的 4 個字元。
### 將二進位轉成十六進位
接著將每組 8 bits 轉換成兩位十六進位數字。
第 0 組的轉換結果：
```
01000001 → 41
01011111 → 5f
01100010 → 62
00110001 → 31
```
因此，第 0 個整數對應的十六進位資料為：
```
41 5f 62 31
```
### 查詢 ASCII 並還原密碼
將十六進位數值對照 ASCII 字元表，可以得到：
| 索引 | 十六進位 | ASCII 字串 |
|---|---|---|
| 0 | `41 5f 62 31` | `A_b1` |
| 1 | `74 5f 30 66` | `t_0f` |
| 2 | `5f 62 31 74` | `_b1t` |
| 3 | `5f 73 68 31` | `_sh1` |
| 4 | `66 54 69 4e` | `fTiN` |
| 5 | `67 5f 35 37` | `g_57` |
| 6 | `35 66 33 36` | `5f36` |
| 7 | `30 32 61 64` | `02ad` |

將 8 組字串依序串接，得到原始密碼：
```
A_b1t_0f_b1t_sh1fTiNg_575f3602ad
```
最後加上題目要求的旗子格式：
```
academy{A_b1t_0f_b1t_sh1fTiNg_575f3602ad}
```
### 解題流程

```
讀取 VaultDoor4.java
        ↓
找出 checkPassword() 中的 8 個整數
        ↓
將十進位整數轉成 32 bits 二進位
        ↓
不足 32 bits 時在左側補 0
        ↓
每 8 bits 分成一組
        ↓
將每組二進位轉成十六進位
        ↓
查詢 ASCII 字元
        ↓
依序串接 32 個字元
        ↓
取得完整 flag
```
### 旗子:
academy{A_b1t_0f_b1t_sh1fTiNg_575f3602ad}
