### 題目:
This vault uses ASCII encoding for the password. The source code for this vault is here
### 提示:
1.Use a search engine to find an "ASCII table"
2.You will also need to know the difference between octal, decimal, and hexadecimal numbers.
### 解法:
直接看程式碼的重點
```
public boolean checkPassword(String password) {
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 070 , 070 ,
            'a' , '3' , '1' , 'd' , 'a' , 'd' , '6' , 'c' ,
        };
        for (int i=0; i<32; i++) {
            if (passBytes[i] != myBytes[i]) {
                return false;
            }
        }
```
根據提示解密後
第一排jU5t_4_b，第二排UnCh_0f，第三排bYt3s88，第四排a31dad6c
### 旗子:
academy{jU5t_4_bUnCh_0fbYt3s88a31dad6c}
