# Linux
###### tags: `Linux`

# SSH
## SSH-Key
### 建立並管理key
1. 建立指定檔案名稱的ssh-key
```linux=
$ ssh-keygen -t rsa -C [email]
```
![](https://i.imgur.com/MewTK2d.png)

2. 密碼可略過，若有設定則為每次使用ssh_key登入時，也必須使用ssh-key的密碼。

3. 查看產生的公鑰和私鑰，副檔名'.pub'為公鑰，另一則為私鑰。
![](https://i.imgur.com/Jnll2CE.png)
<font color="DE1056">*公鑰是為了放進去欲ssh連線的server中，私鑰是連線時和公鑰的匹配，放置於本機端，且絕不可外洩。</font>

4. 將本地的私鑰確保權限為600。


### 放置公鑰到Server
1. 檢查有沒有.ssh/目錄，若沒有則建立，且權限為700
```linux=
$ mkdir .ssh/
$ chmod 700 .ssh/
```
2. 進入/.ssh資料夾查看是否有authorized_keys這個檔案，若沒有則建立，且權限為600。
```Linux=
$ cd .ssh/
$ touch authorized_keys
$ chmod 600 authorized_keys
```

3. 擷取上面建好的公鑰內容，並貼進去authorized_keys檔案，若已經有其他紀錄，則換下一行貼上。
```Linux=
$ cat xxx.pub >> authorized_keys
```


## SSH 連線
### 透過ssh-key連線
```Linux=
$ ssh -i .ssh/xxx userID@host
```

### 透過帳號密碼連線
```Linux=
$ ssh userID@host
````
接著會需要輸入密碼。

### 透過config設定連線
1. 在.ssh/中建立config檔

2. .ssh/config編輯範例
> **Host 連線名稱**
>     **HostName 連線IP**
>     **Port 連線port號，通常為22**
>     **User 連線的server使用者名稱**
>     **IdentityFile ~/.ssh/私鑰**
![](https://i.imgur.com/gp2ytE5.png)

3. 透過設定好的config內容做連線
```Linux=
$ ssh 連線名稱
# Example:
$ ssh linode3
```
<font color="DE1056">*若有IdentityFile則會透過ssh-key連線，沒有則會要求輸入密碼。</font>

---


