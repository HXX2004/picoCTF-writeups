### 題目:
This vault uses for-loops and byte arrays. The source code for this vault is here:
### 提示:
1.Make a table that contains each value of the loop variables and the corresponding buffer index that it writes to.
### 解法:
### 分析密碼長度
```
public boolean checkPassword(String password) {
    if (password.length() != 32) {
        return false;
    }

    char[] buffer = new char[32];
```
這裡可以得到：
- 密碼內容長度必須是 32 個字元。
- buffer 是一個長度 32 的字元陣列。
- 後面的程式會將密碼字元放到 buffer 的不同位置。
也就是說，輸入的密碼順序不一定等於最後拿來驗證的字串順序。
### 找出最後的驗證條件
```
String s = new String(buffer);

return s.equals(
    "jU5t_a_sna_3lpm15ge42_u_4_mbr248"
);
```
### 理解四段字元重組
第一段：前 8 個字元不變
```
for (i=0; i<8; i++) {
    buffer[i] = password.charAt(i);
}
```
第二段：第 8～15 個位置反向取值
```
for (; i<16; i++) {
    buffer[i] = password.charAt(23-i);
}
```
第三段：偶數位置重新排列
```
for (; i<32; i+=2) {
    buffer[i] = password.charAt(46-i);
}
```
第四段：奇數位置保持原位置
```
for (i=31; i>=17; i-=2) {
    buffer[i] = password.charAt(i);
}
```
### 利用 Python 還原密碼
現在我們已經知道：
1. 最終字串是固定的。
2. Java 程式將輸入重新排列後才進行比較。
3. 我們可以反過來，把最終字串的字元放回輸入應該所在的位置。
接下來建一個python，`nano slove_3.py`

```
target = "jU5t_a_sna_3lpm15ge42_u_4_mbr248"

password = [""] * 32

for i in range(8):
    password[i] = target[i]

for i in range(8, 16):
    password[23-i] = target[i]

for i in range(16, 32, 2):
    password[46-i] = target[i]

for i in range(31, 16, -2):
    password[i] = target[i]

print("".join(password))
```
再`python3  slove_3.py`得到`jU5t_a_s1mpl3_an4gr4m_4_u_2be258`
### 旗子:
academy{jU5t_a_s1mpl3_an4gr4m_4_u_2be258}
