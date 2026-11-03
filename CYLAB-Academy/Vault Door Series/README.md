# 這一系列學到了什麼
一、整體學習歷程
從這 7 題可以看出，你的解題方式逐漸從「閱讀原始碼找答案」，進展到「理解程式的資料轉換方式，再利用 Python 反向還原」。
1. Vault Door 1：從原始碼找出密碼
   透過 charAt() 與索引位置，將散落在 Java 程式中的字元重新排列，並使用 Python 自動擷取字元與索引。
   
2. Vault Door 3：分析迴圈與字元排列
   從 buffer 的寫入位置與 password.charAt() 的取值位置，理解不同迴圈如何重新排列密碼，再反向還原原始輸入。
   
3. Vault Door 4：理解不同進位表示
   將十進位、十六進位、八進位以及直接寫入的字元轉換成 ASCII，組合成完整密碼。
   
4. Vault Door 5：處理多層編碼
   分析 Java 中的 URL Encoding 與 Base64 Encoding，理解必須按照原本的編碼順序反向解碼。
   
5. Vault Door 6：利用 XOR 還原資料
   從 passBytes[i] ^ 0x55 的驗證條件，推導原始字元，並透過 Python 對 myBytes 逐一 XOR 還原密碼。
   
6. Vault Door 7：理解位元移位與整數打包
   將 32-bit 整數轉換成二進位，拆成 4 個 8-bit byte，再轉換成 ASCII 字元，還原原始密碼。

7. Vault Door 8：反向分析位元交換
   整理混亂的 Java 程式碼，分析 scramble() 與 switchBits()，將位元交換操作按照相反順序執行，還原原始字元。
