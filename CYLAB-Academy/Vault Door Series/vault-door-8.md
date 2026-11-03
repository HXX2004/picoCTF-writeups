### 題目:
Apparently Dr. Evil's minions knew that our agency was making copies of their source code, 
because they intentionally sabotaged this source code in order to make it harder for our agents to analyze and crack into! The result is a quite mess, 
but I trust that my best special agent will find a way to solve it. The source code for this vault is here:
### 提示:
1.Clean up the source code so that you can read it and understand what is going on.
2.Draw a diagram to illustrate which bits are being switched in the scramble() method, then figure out a sequence of bit switches to undo it. 
You should be able to reuse the switchBits() method as is.
### 解法:
### 分析題目程式
題目提供的 `VaultDoor8.java` 原始碼格式較混亂，因此先透過其他工具整理程式碼，方便閱讀與分析。
閱讀程式後，發現主要有三個部分：
1. `scramble(String password)`：依序交換每個字元的特定位元。
2. `switchBits(char c, int p1, int p2)`：交換字元中兩個指定位置的位元。
3. `checkPassword(String password)`：將輸入的密碼經過 `scramble()` 處理，再與 `expected` 陣列比較。
其中，`expected` 陣列存放了經過位元交換後的數值，例如：
```
char[] expected = {
    0xF4, 0xC0, 0x97, 0xF0, 0x77, 0x97, 0xC0, 0xE4,
    0xF0, 0x77, 0xA4, 0xD0, 0xC5, 0x77, 0xF4, 0x86,
    0xD0, 0xA5, 0x45, 0x96, 0x27, 0xB5, 0x77, 0x95,
    0x94, 0xC1, 0xE1, 0xD2, 0xE1, 0xE1, 0xD0, 0x95
};
```
因此，解題方向是將這些數值反向還原，而不是直接將它們轉成 ASCII 字元。
### 理解 switchBits() 的原理

`switchBits()` 會交換字元中指定的兩個位元位置。

```
public char switchBits(char c, int p1, int p2) {
    char mask1 = (char)(1 << p1);
    char mask2 = (char)(1 << p2);

    char bit1 = (char)(c & mask1);
    char bit2 = (char)(c & mask2);
    char rest = (char)(c & ~(mask1 | mask2));

    char shift = (char)(p2 - p1);
    char result = (char)((bit1 << shift)
                       | (bit2 >> shift)
                       | rest);

    return result;
}
```
程式會先利用位元遮罩取得指定位置的位元，再將兩個位元移動到對方的位置，最後與其他未改變的位元合併。
例如，若原本兩個位元分別為 `01`，交換後就會變成 `10`。
由於交換操作本身具有可逆性，因此同一組位元交換執行兩次，就能恢復原本的位元排列。
### 找出 scramble() 的交換順序

在 `scramble()` 中，每個字元都會依序執行以下交換：

```
c = switchBits(c, 1, 2);
c = switchBits(c, 0, 3);
c = switchBits(c, 5, 6);
c = switchBits(c, 4, 7);
c = switchBits(c, 0, 1);
c = switchBits(c, 3, 4);
c = switchBits(c, 2, 5);
c = switchBits(c, 6, 7);
```

要還原原始字元，就必須按照相反順序執行：

| 加擾順序 | 位元交換 | 還原順序 |
|---:|---|---:|
| 1 | `(1, 2)` | 8 |
| 2 | `(0, 3)` | 7 |
| 3 | `(5, 6)` | 6 |
| 4 | `(4, 7)` | 5 |
| 5 | `(0, 1)` | 4 |
| 6 | `(3, 4)` | 3 |
| 7 | `(2, 5)` | 2 |
| 8 | `(6, 7)` | 1 |

另外，程式中被註解的 `switchBits()` 呼叫不會執行，因此不需要將它們納入還原流程。

### 使用 Python 反向還原

為了避免手動處理 32 個字元，可以使用 Python 將 `expected` 中的數值逐一反向交換。

`nano slove_8.py`

```
expected = [
    0xF4, 0xC0, 0x97, 0xF0, 0x77, 0x97, 0xC0, 0xE4,
    0xF0, 0x77, 0xA4, 0xD0, 0xC5, 0x77, 0xF4, 0x86,
    0xD0, 0xA5, 0x45, 0x96, 0x27, 0xB5, 0x77, 0x95,
    0x94, 0xC1, 0xE1, 0xD2, 0xE1, 0xE1, 0xD0, 0x95
]

def switch_bits(c, p1, p2):
    bit1 = (c >> p1) & 1
    bit2 = (c >> p2) & 1

    if bit1 != bit2:
        c ^= (1 << p1) | (1 << p2)

    return c

def unscramble(c):
    pairs = [
        (6, 7),
        (2, 5),
        (3, 4),
        (0, 1),
        (4, 7),
        (5, 6),
        (0, 3),
        (1, 2)
    ]

    for p1, p2 in pairs:
        c = switch_bits(c, p1, p2)

    return c

password = ''.join(chr(unscramble(c)) for c in expected)

print("Password:", password)
print("Flag:", f"academy{{{password}}}")
```
程式執行步驟：
1. 將 Java 程式中的 `expected` 數值複製到 Python。
2. 定義 `switch_bits()`，交換指定位置的兩個位元。
3. 在 `unscramble()` 中按照原本操作的相反順序執行位元交換。
4. 對 `expected` 的每個數值進行還原。
5. 使用 `chr()` 將還原後的數值轉成字元，再串接成密碼。
6. 在密碼外加上 `academy{}`，取得完整旗子。

`python3 slove_8.py`

得到旗子
### 解題流程
```
取得並整理 VaultDoor8.java
              ↓
分析 scramble() 與 switchBits()
              ↓
找出 expected 陣列
              ↓
記錄所有位元交換順序
              ↓
將交換順序反轉
              ↓
使用 Python 逐一還原每個數值
              ↓
將數值轉成字元並串接
              ↓
取得原始密碼與 flag
```
### 旗子:
academy{s0m3_m0r3_b1t_sh1fTiNg_ea469661e}
