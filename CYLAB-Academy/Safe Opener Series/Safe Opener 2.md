### 題目:
What can you do with this file? I forgot the key to my safe but this file is supposed to help me with retrieving the lost key. Can you help me unlock my safe?
### 提示:
1.Download and try to decompile the file.
### 解法:
題目提供 `SafeOpener.class`，並提示可以利用這個檔案找回遺失的保險箱密碼。

`.class` 是 Java 編譯後的位元碼，不能像一般 `.java` 原始碼一樣直接閱讀。因此，題目希望我們嘗試反編譯（Decompile），還原成較容易理解的 Java 程式碼。

### 反編譯並分析程式碼

利用線上反編譯器，取得以下關鍵程式碼：

```
public static boolean openSafe(String password) {
    String encodedkey = "academy{SAf3_0p3n3rr_y0u_solv3d_it_87a1d928}";
    if (password.equals(encodedkey)) {
        System.out.println("Sesame open");
        return true;
    } else {
        System.out.println("Password is incorrect\n");
        return false;
    }
}
```

觀察 `openSafe()`，可以發現：

1. `encodedkey` 直接儲存了一個完整的 `academy{...}` 字串。
2. 程式透過 `password.equals(encodedkey)` 比較輸入與固定字串。
3. 這個固定字串就是題目要找的 flag，不需要另外猜密碼。

因此，flag 為：

`academy{SAf3_0p3n3rr_y0u_solv3d_it_87a1d928}`

### 為什麼不用真的破解密碼？

雖然 `main()` 會使用 Base64 編碼：

```
encodedkey = encoder.encodeToString(key.getBytes());
```

但這不代表我們一定要破解 Base64。

從反編譯結果可以直接看到 `openSafe()` 的比較目標。題目的重點是學會從編譯後的 `.class` 檔案還原程式邏輯，並找出硬編碼在程式中的敏感資訊。
### 旗子:
academy{SAf3_0p3n3rr_y0u_solv3d_it_87a1d928}
