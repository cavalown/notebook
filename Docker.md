# Docker
###### tags: `Docker`

`Read: Docker專業養成`
`https://ithelp.ithome.com.tw/articles/10191016`

# Install 安裝
* ### Mac OS
    1. Docker 官網下載Docker for Mac壓縮檔(Docker.dmg)，直接解壓放到application資料夾，啟動應用程式即可。
    2. Mac版本的Docker只要安裝好就包含了docker-compose，不用另外安裝》
* ### Ubuntu
    1. [直接參考官方安裝方式，照做即可。](https://docs.docker.com/engine/install/ubuntu/)
    2. 要注意的是，Ubuntu的Docker，docker-engine和docker-compose是要分開安裝的。

---
# Image 映像檔
* ### 映像檔名稱：
    #### 組成有三個部分： “**Namespace/Repository:Tag**：”
    1. Namespace: 印象檔的命名空間，通常會有建制印象的單位或人的名稱代號在裡面。
    2. Repository: 印象檔的名稱，通常會和裡面包含的應用程式有關。
    3. Tag:用以區分版本。

* ### 取得映像檔 
    
    * #### 下載docker映像檔：docker pull
    1. 未給予映像的命名空間時，會是下載Docker官方管理的映像。
    2. 未給予印象的tag時，會下載最新版本latest
    ```docker
    $ sudo docker pull imageName
    # example:
    $ sudo docker pull ubuntu
    # example 有映像空間和tag
    $ sudo docker pull registry.hub.docker.com/ubuntu:latest
    ```
    * #### 搜尋docker映像檔：docker search
    1. 透過搜尋官方的映像倉庫Docker hub
    ```docker
    $ docker search imageName
    # example:
    $ docker search php
    ```
    2. 搜尋的結果會包含幾項資訊：
        ![](https://i.imgur.com/TZlIDKl.png)
        * Name: 映像檔名稱。
        * Description: 描述。
        * Stars: 映像檔受歡迎程度。
        * Official: 是否為官方Docker維護的映像檔。
        * Automated: 映像檔是否自動建構。
        
* ### 常用指令：
    #### 1. 檢視已存在的映象檔  `$ sudo docker images`
    ![](https://i.imgur.com/DEvKpF1.png)
        * Repository: 名稱
        * Tag: 標籤
        * Image ID: id 
        * Created: 建立時間
        * Size: 大小

    #### 2. 刪除映像檔：`$ sudo docker rmi id_or_name`
    * 若是此映像檔正有container在執行，則可用強制刪除的方式：`$ sudo docker rmi -f id_or_name `，但一般來說不建議用此方式。

---
# Repository
#### use dockerhub( to be continue...)

---
# Container
* ### 建立container並運行
    #### 1. 前台運行，可在終端機上觀察到
    ```docker
    $ sudo docker run -it image_name
    ```
    #### 2. 後台運行
    ```docker
    $ sudo docker run -d image_name
    ```
    #### 3. 為container命名
    ```docker
    $ sudo docker run -d --name container_name image_name
    ```

* ### 停止container
```docker
$ sudo docker stop id_or_name
```

* ### 啟動container
```docker
$ sudo docker start id_or_name
```

* ### 重啟container = docker stop + docker start
```docker
$ sudo docker restart id_or_name
```

* ### 刪除container
    1. 刪除已停止的container
    ```docker
    $ sudo docker rm id_or_name
    ```
    2. 強制刪除運行中的container
    ```docker
    $ sudo docker rm -f id_or_name
    ```
    
* ### 常用指令
    #### 1. 檢視container
    ![](https://i.imgur.com/uU13MXH.png)
    * 檢視所有運行中的container
    ```docker
    $ sudo docker ps
    ```
    * 檢視所有container
    ```docker
    $ sudo docker ps -a
    ```
    * 檢視最後一個建立的container
    ```docker
    $ sudo docker ps -l
    ```
    * 檢視最後x個建立的container
    ```docker
    $ sudo docker ps -n x
    ```
    

---
# Data Volume 資料卷
因為docker container本身並非永久存在，一旦刪除裡面的資料和log會消失，但有時候會有需要保存的資料，就會需要透過volumn將container裡面的資料夾和外面連動，即便container掛掉或刪掉，該保留的資料並不會受影響。
* ### 建立volume
    #### 1. 隨container建立 (-v folder_path)
    * 使用 -v 指定掛載的資料夾
    ```docker
    $ sudo docker create --name container_name -v folder_path image_name
    ```
    * 可同時掛載多個資料夾
    ```docker
    $ sudo docker create --name container_name -v folder1 -v folder2 image_name
    ```
    
    #### 2. 直接建立volume(之後啟動docker run 時，再指定掛載的資料夾。)
    ```docker
    $ sudo docker volume create --name volumn_name
    ```
    
    
* ### 掛載volumn
    #### 1. 將外部資料夾掛載到已經建立的volume
    ```docker
    $ sudo docker volume create --name volume_name
    $ sudo docker run -it  --name container_name -v out_folder:volume_name image name
    # example:
    $ sudo docker volume create --name html
    $ sudo docker run -it --name website -v /home/users/xxxx/websites/html:html ngix
    ```
    
    #### 2. Volume container ( --volumes-from)
    (to be continue...)

* ### 刪除volomn
    #### 1. 直接刪除volume
    **不建議這種方式，因為可能有其他container正在使用這個volume而導致錯誤**
    ```docker
    $ sudo docker volume rm volume_name 
    ```
    
    #### 2. 隨container一起刪除volume(-v)
    **建議採用此種方式！**
    ```docker
    $ sudo docker rm -v container_name
    ```


---
# Dockerfile
**用來自動化的建立image**
1. 建立並編輯Dockerfile
2. 用dockerfile建立image
    此指令會自動尋找當前目錄的dockerfile
    ```docker
    $ sudo docker build image_name
    ```


---
