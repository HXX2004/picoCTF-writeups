### 題目:
This vault uses some complicated arrays! I hope you can make sense of it, special agent. 
### 提示:
1.Look up the charAt() method online.
### 解法:
### 分析題目提示
提示特別提到 Java 的 `charAt()` 方法，因此我判斷可以透過閱讀原始碼，找出密碼中每個字元的位置，而不需要進行暴力破解。
### 閱讀原始碼
使用 `cat` 查看程式碼：
```
cat VaultDoor1.java
```
在程式碼中找到：
```
String input = userInput.substring(
    "academy{".length(),
    userInput.length() - 1
);
```
這段程式碼會移除輸入內容的 `academy{` 前綴與最後的 `}`，只留下大括號內的密碼。
接著找到 `checkPassword()` 方法，其中包含多個條件，例如：
```
password.charAt(0)  == 'd'
password.charAt(1)  == '3'
password.charAt(2)  == '5'
password.charAt(3)  == 'c'
```
這些條件直接指出密碼各個索引位置應該放置的字元。
### 理解 charAt() 並還原密碼
Java 的 `charAt(index)` 可以取得字串指定索引位置的字元，索引從 `0` 開始。
例如：
```
password.charAt(0) == 'd'
```
代表密碼第 1 個字元是 `d`。
由於原始碼中的條件並未按照索引順序排列，因此需要將每個字元依照索引重新組合。
為了避免手動排列出錯，我使用 Python 自動整理原始碼中的索引與字元對應關係。
建立 `slove.py`：

```
import re
​
source = open("VaultDoor1.java", encoding="utf-8").read()
​
password = [""] * 32
​
for index, char in re.findall(
    r"password\.charAt\((\d+)\)\s*==\s*'([^']*)'",
    source
):
    password[int(index)] = char
​
result = "".join(password)
​
print("Password:", result)
print("Flag:", f"academy{{{result}}}")
```
​
執行程式：
​
```
python3 slove.py
```
​
程式會自動擷取 `charAt()` 的索引與字元，將字元放回正確位置，再組合成完整密碼與 flag。
​
### 完整解題流程
```
查看 VaultDoor1.java
          |
          v
找到 substring() 與 checkPassword()
          |
          v
理解 charAt(index) 的索引規則
          |
          v
取得各索引對應的字元
          |
          v
使用 Python 自動排列
          |
          v
組合 academy{...}
          |
          v
取得 flag
```
### 旗子:
academy{d35cr4mbl3_tH3_cH4r4cT3r5_d66e42}
