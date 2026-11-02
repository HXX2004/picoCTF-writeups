### 題目:
Can you open this safe? I forgot the key to my safe but this program is supposed to help me with retrieving the lost key. Can you help me unlock my safe
### 解法:
觀察程式碼時，特別注意到以下兩個地方。

第一個是 Base64 編碼器：

```
java
Base64.Encoder encoder = Base64.getEncoder();
```

第二個是 `openSafe()` 裡面的固定字串：

```
java
String encodedkey = "cGwzYXMzX2wzdF9tM18xbnQwX3RoM19zYWYz";
```

我認為這兩個地方可能是解題關鍵，因此決定從 Base64 的方向開始分析。

### 分析密碼驗證方式

繼續查看程式碼，找到：

```
java
encodedkey = encoder.encodeToString(key.getBytes());
System.out.println(encodedkey);

isOpen = openSafe(encodedkey);
```

這段程式會先將使用者輸入的密碼轉成 Base64，再將編碼後的結果傳入 `openSafe()`。

接著在 `openSafe()` 中看到：

```
java
if (password.equals(encodedkey)) {
    System.out.println("Sesame open");
    return true;
}
else {
    System.out.println("Password is incorrect\n");
    return false;
}
```

這表示程式會將輸入密碼的 Base64 編碼結果，與程式中寫死的 `encodedkey` 比較。

因此，我推測只要將固定字串反向解碼，就能取得原始密碼，不需要一直猜測密碼。

### 使用 Base64 解碼取得密碼

找到固定字串：

```
text
cGwzYXMzX2wzdF9tM18xbnQwX3RoM19zYWYz
```

將它放入 Base64 解碼器，得到：

```
text
pl3as3_l3t_m3_1nt0_th3_saf3
```

這就是原始密碼。

### 組成 flag

將解碼後的內容放入題目的 flag 格式：

```
text
academy{pl3as3_l3t_m3_1nt0_th3_saf3}
```
### 旗子:
academy{pl3as3_l3t_m3_1nt0_th3_saf3}
