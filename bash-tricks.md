# What is "bash tricks" ?

![image](https://wizardzines.com/images/uploads/bash-tricks.png)

## In comics

於 [wizard zines comic - bash tricks](https://wizardzines.com/comics/bash-tricks/) 中有提供了一些 `bash` 的小技巧：

> comics 範例中的 `convert` 因為找尋不到，所以以下範例透過 `echo` 替代。

1. `ctrl+R` 搜尋歷史紀錄，可搜尋以往於 `bash` 中執行的指令。
2. `{}` 可以想像成「分配率」，如範例所提 `file.{jpg, png}`，結果會為 `file.jpg` & `file.png`  
    你也可以試試看：

    ```bash
    echo file.{jpg,png} # result: file.jpg file.png
    ```

3. `!!` 為「重複執行上一次指令」，如圖例提到的 `sudo !!`
    實際運用：

    ```bash
    mv file.{jpg,png}
    sudo !! # result: sudo mv file.{jpg,png}
    ```

4. `loops` 顧名思義就是迴圈，不過 comic 提供的範例沒有預期迴圈效果，查詢後可透過以下方式，實現迴圈效果（ `for` 後方的變數參數可直接拿來使用）

    ```bash
    for i in {1..5}; do echo $i.jpg; done
    # result: 1.jpg 2.jpg 3.jpg 4.jpg 5.jpg
    ```

5. `$()` 命令替換，可將 `()` 中執行結果，變成值串接於後方
    如圖例：

    ```bash
    date -I # result: 2025-08-06
    echo file-$(date -I) # result: file-2025-08-06
    ```

6. 許多的快速鍵：

- `Ctrl + A`：指標回到字首
- `Ctrl + E`：指標回到字尾
- `Ctrl + L`：清除畫面
- `Ctrl + D`：離開 `bash`

## So... what is "bash"?

`bash` 是 `Unix shell`的一種命令處理器，它准許於終端機中使用，且於 `Linux`、`macOS` 系統中，都能夠直接使用。

發明於 1987 年，由美國程式設計師 [Brian J. Fox](https:# zh.wikipedia.org/wiki/%E5%B8%83%E8%90%8A%E6%81%A9%C2%B7%E7%A6%8F%E5%85%8B%E6%96%AF) 為了 GNU 計劃而生。
> 想看更多詳細故事，可以參考 [Bash 維基百科](https://zh.wikipedia.org/zh-tw/Bash)

## Helps with Development

寫一份 `.sh` 的檔案吧！

1. 於終端機中透過 `vim` 建立 `example.sh`

    ```shell
    vim example.sh
    ```

2. 透過 `vim` 製作 `.sh` 腳本，並透過 `esc` + `:wq` 存檔

    ```vim
    WHO="Uncle Lin"

    echo $WHO is handsome!
    ```

3. 於終端機中執行

    ```shell
    bash example.sh # result: Uncle Lin is handsome!
    ```

### Set variables

1. 於終端機中透過 `vim` 建立 `example.sh`

    ```shell
    vim whoIsHandsome.sh
    ```

2. 透過 `vim` 製作 `.sh` 腳本，並透過 `esc` + `:wq` 存檔
    > 注意 `$0` 會保留給 `shell command` 使用

    ```vim
    echo $1 is handsome!
    ```

3. 於終端機中執行

    ```shell
    bash whoIsHandsome.sh 'Uncle Lin'  # result: Uncle Lin is handsome!
    ```

## Further Reading

- [10 分鐘 Bash 指令入門](https://codelove.tw/@tony/post/AqJe4a)
