# What is "bash tricks" ?

![image](https://wizardzines.com/images/uploads/bash-tricks.png)

## In comics

於 [wizard zines comic - bash tricks](https://wizardzines.com/comics/bash-tricks/) 中有提供了一些 `bash` 的小技巧：

1. `ctrl+R` 搜尋歷史紀錄，可搜尋以往於 `bash` 中執行的指令。
2. `{}` 可以想像成「分配率」，如範例所提 `file.{jpg, png}`，結果會為 `file.jpg` & `file.png`  
    你也可以試試看：

    ```bash
    echo file.{jpg,png}

    // result: file.jpg file.png
    ```

3. `!!` 為「重複執行上一次指令」，如圖例提到的 `sudo !!`  
    實際運用：

    ```bash
    mv file.{jpg,png}
    sudo !!

    //result: sudo mv file.{jpg,png}
    ```

4.
5. `$()` 命令替換，可將 `()` 中執行結果，變成值串接於後方
    如圖例：

    ```bash
    echo date -I //result: 2025-08-06
    echo file-$(date -I) //result: file-2025-08-06
    ```

6.
