**不要なパッケージ削除**
***

古いバージョンのものをアンインストールします
```
yum remove docker*
```
**Docker環境構築**
***

epel-releaseをダウンロードする
```
wget https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-11.noarch.rpm
```

epel-releaseをアップデートする
```
rpm -Uvh epel-release*rpm
```

```
yum install -y yum-utils device-mapper-persistent-data lvm2
```

リポジトリを追加します
```
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

Docker CEをインストールします
```
yum install docker-ce -y 
yum install docker-compose
```

自動起動を有効化します
```
systemctl enable docker
```

Dockerを起動します
```
systemctl start docker
```

**確認作業**
***
サービスの起動確認
```
systemctl status docker
```
インストールしたDockerをバージョン確認します
```
docker -v
```

**仮想コンテナ作成**
***
```
  wordpress:
    image: wordpress
    container_name: some-wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_PASSWORD: my-secret-pw

  mysql:
    image: mysql:5.7
    container_name: some-mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: my-secret-pw「
```