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
sudo yum install docker-ce -y 
```

自動起動を有効化します
```
sudo systemctl enable docker
```

Dockerを起動します
```
sudo systemctl start docker
```

インストールしたDockerをバージョン確認します
```
docker -v
```