## 常用Command
+ **docker `ps -a`** - 列出所有Container
+ **docker `system prune`** - 刪除硬碟裡面所有Containers及Image cache
+ **docker `create image command`** - 建立Container
+ **docker `start` image_id** - 啟動/重新啟動Container
+ **docker `logs` image_id** - 顯示Container output
+ **docker `stop` image_id** - 停止Container
+ **docker `kill` image_id** - 中止Container
+ **docker `exec -it` image_id command** - 透過Docker client執行Container指令

## 自訂 Image
1. 製作Dockerfile
  + 選擇kernel或是os，通常稱base image
  + kernel指令安裝redis或是其他軟體
  + 指定啟動container執行命令
```
# 選擇kernel/OS
# alpine是最小的linux kernel
FROM alpine

# 安裝redis
RUN apk add --update redis

# 指定啟動container後執行命令
# 啟動redis，要下redis-server指令，可以參考官網
CMD ["redis-server"]
```
2. Build Dockerfile
```
docker build .
```
