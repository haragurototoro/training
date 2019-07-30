### #一括コンテナ作成の定義ファイル作成
***
1. dockerのコンテナ作成の定義ファイルを作成する  
(1)command
```
vi /etc/docker/docker-compose.yml
```

1. 定義内容は以下の通りに記載します  
(1)記載内容
```
version: '3'

services:
  nginx-proxy:
    image: jwilder/nginx-proxy
    ports:
      - 80:80
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro

  web:
    image: nginx
    environment:
      - VIRTUAL_HOST=web.localhost

  web2:
    image: nginx
    environment:
      - VIRTUAL_HOST=web2.localhost

  web3:
    image: nginx
    environment:
      - VIRTUAL_HOST=web3.localhost
```

#### #複数コンテナ起動の動作確認
***
1. dockerのコンテナ作成の定義ファイルを実行します
```
 docker-compose up -d
```

1. docker環境に定義ファイルで記載したコンテナが作成されたことを確認します
```
docker ps
```
