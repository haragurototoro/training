不要なパッケージ削除
***

古いバージョンのものをアンインストールします
```
yum remove docker*
```
Docker環境構築
***
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
```

自動起動を有効化します
```
systemctl enable docker
```

Dockerを起動します
```
systemctl start docker
```

確認作業
***
サービスの起動確認
```
systemctl status docker
```
インストールしたDockerをバージョン確認します
```
docker -v
```