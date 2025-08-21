# What is "unix permissions" ?

![image](https://wizardzines.com/images/uploads/permissions.png)

## 1. 三種基本權限操作：
1. read 讀取 (r)
2. write 寫入 (w)
3. execute 執行 (x)


## 2. 實際操作
以下使用 [線上 bash 工具 glot](https://glot.io)操作

### 2.1 列出檔案權限
假設有一個檔案 `main.sh`
```bash
# input
ls -l

# output
total 4
-rw-r--r-- 1 glot glot 5 Aug 19 14:17 main.sh
```
- `total 4`: 每個目錄下檔案的磁碟區塊數（blocks），非檔案數量，而是空間單位。通常一個 block = 4KB，total 4 代表約佔用 16KB 磁碟區塊）
- `-rw-r--r--`
  * `-`：一般檔案（若是目錄會是 d）
  * `rw-`: 擁有者 (user)，有讀、寫權限
  * `r--`: 群組 (group)，只有讀
  * `r--`: 其他人 (others)，只有讀


- `1`: 硬連結數（hard link count）
- `glot`: 檔案擁有者 (user)
- `glot`: 檔案所屬群組 (group)
- `5`: 檔案大小，單位是「位元組 (bytes)」
- `Aug 19 14:17`: 檔案最後修改時間
- `main.sh`: 檔案名稱

檔案權限由 12 位元（bits）表示：
- 前 3 個位元：特殊權限（setuid, setgid, sticky bit）
- 後 9 個位元：使用者權限、群組權限、其他人權限

### 2.2 練習時間：自行建立一個檔案看看吧
```bash
# input
touch file.txt
ls -l file.txt

#output
-rw-r--r--  1 wanghan2  staff  0  8 19 22:45 file.txt
```

* wanghan2（user）read & write
* staff（group）read
* other（anyone）read

## 3. 圖解權限
![](https://i.meee.com.tw/ve5isma.png)
* 前三個: 特殊權限
  * setuid(Set User ID, s)
  * setgid(Set Group ID, s)
  * sticky(sticky bit, t)
* 後三個:  user、group、other
* 每組以二進位表示：rwx = 111, rw- = 110, r-- = 100

## 4. 改變檔案權限
```bash
# input
chmod 644 file.txt
```
* `chmod`: 在 Unix 中修改檔案或資料夾權限 (change mode)
* 第一個數字 -> user
* 第二個數字 -> group
* 第三個數字 -> others
* 110 100 100 換算為 6 4 4，即增加三個權限 `rw-` `r--` `r--`(r=4, w=2, x=1)


## 5. setuid 和 setgid 的特別效果
![](https://i.meee.com.tw/sPTUGAD.png)
### 5.1 setuid
```bash
# input
ls -l /bin/ping

# output
rws r-x r-x root root
```
> 原本 user 權限應該是 `rwx`，但 `x` 被 `s` 取代，代表啟用了 `setuid`，ping 每次執行時會以 root 身份運行

### 5.2 setgid
> `setgid` 的行為會因可執行檔、目錄、檔案而不同，比 setuid 更難直觀理解

## 6. 補充
### 6.1 刪除權限
> 如果要「拿掉」某一個權限，可以用 `chmod` 配合 `-` （如 `chmod a-w filename`）；
* `a` 代表「all」，即檔案的 user, group, anyone
* `a-w`: → 現在所有人只能寫（覆蓋 `echo 'hi' > file.txt`，但不能看到自己寫的東西 `cat...`）

### 6.2 sticky
* 只對目錄有意義，主要用在共享目錄
* 設定之後，目錄裡的檔案，任何人都可寫入（如果有 w），但只有檔案的擁有者、目錄擁有者或 root 才能刪除或改名
* 常見例子：/tmp 目錄
```bash
drwxrwxrwx   9 root root 4096 Aug 20 23:30 tmp
```