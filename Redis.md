# Redis
###### tags: `redis` `Docker` `Database`

## Docker 建立：
1. 先拉取想要的image
```linux=
$ docker pull redis:latest
```
2. Docker 啟動Redis
```linix=
$ docker run -itd --rm --name redis-test -p 6379:6379 redis
```
![](https://i.imgur.com/nKiwceT.png)

3. 進入Redis
```linux=
$ docker exec -it redis-test redis-cli
```
![](https://i.imgur.com/3wuG5F8.png)


## Redis 指令
1. 服務測試
![](https://i.imgur.com/D1TWtkh.png)

2. 建立鍵值對
```redis=
> set key = value
```
3. 設置資料expire期間
```linux=
> expire key seconds
> expireat key Timestamp
```
4. 讀取資料
```linux=
> get key
```
此處的

## 注意事項
1. 字串 – 文字或二進位資料，最大 512 MB

