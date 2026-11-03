### 題目:
In the last challenge, you mastered octal (base 8), decimal (base 10), and hexadecimal (base 16) numbers, 
but this vault door uses a different change of base as well as URL encoding! The source code for this vault is here:
### 提示:
1.You may find an encoder/decoder tool helpful
2.Read the wikipedia articles on URL encoding and base 64 encoding to understand how they work and what the results look like.
### 解法:
看程式的重點
```
public boolean checkPassword(String password) {
        String urlEncoded = urlEncode(password.getBytes());
        String base64Encoded = base64Encode(urlEncoded.getBytes());
        String expected = "JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm"
                        + "JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2"
                        + "JTM0JTVmJTY1JTMzJTM0JTMwJTYzJTMzJTY1JTY0";
        return base64Encoded.equals(expected);
    }
```
將

`JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm,JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM,JTM0JTVmJTY1JTMzJTM0JTMwJTYzJTMzJTY1JTY0`

64轉碼後變

`%63%30%6e%76%33%72%74%31%6e%67%5f%66%72%30%6d%5f%62%61%35%65%5f%36%34%5f%65%33%34%30%63%33%65%64`

再用URL解碼後得到`c0nv3rt1ng_fr0m_ba5e_64_e340c3ed`
### 旗子:
academy{c0nv3rt1ng_fr0m_ba5e_64_e340c3ed}
