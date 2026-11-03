### 題目:
A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher? 
### 提示:
1.Try a frequency attack. An online tool might help.
### 解法:
提示中的 Frequency Attack 指的是「頻率分析攻擊」，透過統計密文中各個字母的出現次數，並利用英文常見字母與單字的分布特性，推測原始明文。
觀察題目內容，可以發現：
- 第一行 `HRZUEVABDLIOJYTGNXCMWPKSQF` 是由 26 個英文字母組成的字母表。
- 文章中有大量重複的字串，例如 `Mbe`、`h`、`hyu`，顯示密文可能使用固定的字母替換規則。
- 文章最後的旗子也經過相同的字母替換，因此需要先還原密文，才能取得正確的旗子內容。
### 使用線上工具分析密文
由於題目提示可以使用線上工具，因此搜尋單字母替換密碼的解密工具，使用 dCode 的 Monoalphabetic Substitution 工具進行分析。
工具網址：https://www.dcode.fr/monoalphabetic-substitution
操作步驟：
1. 將題目提供的英文密文複製到解密工具的輸入欄位。
2. 保留原本的空格與標點符號，方便工具分析英文單字的結構。
3. 執行自動解密，觀察工具推測的明文。
4. 再利用題目提供的 26 個字母對照表，確認解密結果。
### 利用字母表還原密文
題目提供的字母表為：
```
HRZUEVABDLIOJYTGNXCMWPKSQF
```
將它與標準英文字母表對照：
```
明文字母：ABCDEFGHIJKLMNOPQRSTUVWXYZ
密文字母：HRZUEVABDLIOJYTGNXCMWPKSQF
```
例如，密文中的 `Mbe` 可以依照字母對照表還原成 `The`。
因為每個密文字母都固定對應一個明文字母，所以只要建立反向對照表，就能將整段文章中的字母逐一還原，並保留原本的空格與標點符號。
這類密碼稱為單字母替換密碼（Monoalphabetic Substitution Cipher）。頻率分析可以在替換規則未知時協助推測字母對應；本題則另外提供了字母表，能直接利用它還原密文。
### 取得旗子
將文章最後的密文：
```
Mbe voha dc: hzhuejq{5WR5717W710Y_3P0OW710Y_4VRU1ER7}
```
依照字母表還原後，可得到旗子：
```
academy{5UB5717U710N_3V0LU710N_4FBD1EB7}
```
## 五、解題流程
```
閱讀題目與提示
        ↓
辨認單字母替換密碼
        ↓
搜尋線上解密工具
        ↓
輸入題目提供的密文
        ↓
利用字母表建立反向對照
        ↓
還原英文文章與旗子
```
### 旗子:
academy{5UB5717U710N_3V0LU710N_4FBD1EB7}
