**ネットワークの設定と再起動**
***
ネットワークの設定ファイルを開きます
```
vi /etc/sysconfig/network-scripts/ifcfg-eth0
```
動的にサーバにIPを割り当てます
```
#ONBOOT=no
ONBOOT=yes
```
ネットワークの設定を更新します
```
systemctl restart network
```

## Docker構築手順書

**ポート確認と解放作業**
***
現在解放されているポートを確認します
```
firewall-cmd --list-all
```

WEBサーバのポート開放
```
firewall-cmd --zone=public --add-port=80/tcp --permanent
```

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

古いミドルウェアのバージョンを最新版のミドルウェアのバージョンに交換します。
```
yum update -y
```

Dockerの依存関係があるミドルウェアをインストールします
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
yum install docker-compose -y
```

必要なパッケージ導入後にDockerの初期のサービス状態を確認します
```
systemctl status docker
```

Dockerのサービスをサーバ再起動時に自動起動するように有効化の設定をします
```
systemctl enable docker
```

Dockerのサービスが停止しているため起動させます
```
systemctl start docker
```

**確認作業**
***
Dockerのサービスの起動後に正常に動作しているかを確認します
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
version: '3.3'

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root-pass
      MYSQL_DATABASE: wordpress
      MYSQL_USER: db-user
      MYSQL_PASSWORD: db-pass

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: db-user
      WORDPRESS_DB_PASSWORD: db-pass
      WORDPRESS_DB_NAME: wordpress
volumes:
   db_data: {} 
```

**dockerの確認コマンド**
***
Dockerのイメージがダウンロードされていることを確認します
```
Docker imges ls -a
```
Dockerの仮想コンテナが起動していることを確認します
```
Docker ps -a
```
