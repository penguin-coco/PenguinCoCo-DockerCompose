## PenguinCoCo Docker Compose 部署步驟

### 前端

專案版本如果更新，只需更換**/docker/nginx/dist資料夾**

### 後端

專案版本如果更新，只需更換**/docker/backend/jar檔案**

### 部署及關閉方式

1. 在當前目錄下，運行指令如下：

   ```bash
   docker-compose up -d
   ```

   即可運行所有**docker-compose.yml**內定義的container。

   Note：**-d**參數代表背景運行

2. 在當前目錄下，運行指令如下：

   ```b
   docker-compose down
   ```

   即可關閉所有**docker-compose.yml**內定義的container。

   Note：如果添加**--volume**參數，代表一併刪除volume。

### PostgreSQL 備份及還原資料庫的指令

第一次在主機上透過docker部署的需透過以下指令來建置資料庫，先將host端的資料庫檔案透過docker指令複製到container裡面，再進行container裡面進行資料庫還原的動作。

docker複製指令：

```bash
docker cp <hostFilePath> <containerId:containerFilePath>
```

docker進入container指令：

```bash
docker exec -it <containerId> </bin/bash or /bin/sh>
```

備份指令：

```bash
pg_dump -h <host> -p <port> -U <username> -W -F <fileFormat> -b -v -f <outputFilePath> <dbName>
```

Note：**<fileFormat>**可以為**c(custom形式，最靈活)**、**t(tar檔形式)**

還原指令：

```bash
pg_restore -h <host> -p <port> -U <username> -W -d <dbName> -v <backupFilePath>
```

Note：**<dbName>**該資料庫需要先建立，否則會報錯