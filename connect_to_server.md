# Connect to Server

初次登入server

## 1. 在本機創建 SSH 秘鑰
`$ ssh-keygen`  
`$ cat ~/.ssh/id_rsa.pub`  # 用滑鼠全選並複製裡面的秘鑰

## 2. 複製秘鑰到server上
`$ ssh username@10.20.32.12`  # 第一次登入會要求輸入密碼  
`$ cd ~/.ssh`  
`$ vi authorized_keys`  
貼上剛剛複製的id_rsa.pub內的秘鑰進去，然後按 `Esc` 鍵，輸入 `:wq` 退出即可。

### 至此，已建立好本機與server的 SSH 通信。
以上這兩步驟可以簡化為  
`$ ssh-copy-id username@10.20.32.12`

## 3. 設定本機 config 檔，方便連接 server
為方便起見，可在本機設定 config 文檔，避免每次登入都要輸入一長串的 IP 位址 username@10.12.32.12  
`$ touch ~/.ssh/config`  
`$ vi ~/.ssh/config`  

在文檔裡輸入以下內容：
```
Host alias_name  # what alias name?
    Hostname 10.20.32.12  # key-in the server address
    Port 22  # generally 22
    User your_username  # key-in your username
    ForwardX11 yes  # do you want GUI function?
```
輸入完畢後按 `Esc` 鍵，輸入 `:wq` 退出即可。 之後只需 `$ ssh alias_name` 即可連上 server。

## 4. 設定 server 的 .bashrc 文檔
`$ ssh alias_name`  
#`$ touch ~/.bashrc`  # If the .bashrc file doesn't exist  
`$ vi ~/.bashrc`  
```
module load slurm
module load ucsc
```
`$ source ~/.bashrc`  

之後每次登入 server 都會自動載入這些套件。