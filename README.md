# GitLab CE using docker-compose

usage

```
$ sudo docker-compose up -d
```

## FQDN

`gitlab-ce.example.org`でデプロイする構成です。

## port

GitLabは8443/TCP、コンテナイメージレジストリは25000/TCPでListenします。

## 証明書

CN:gitlab-ce.example.orgとして作成し、ホストOSの`/opt/gitlab-cert`以下に置きます。

```
$ sudo mkdir /opt/gitlab-cert
$ sudo openssl req -newkey rsa:4096 -nodes -sha256 -keyout /opt/gitlab-cert/gitlab-ce.example.org.key -x509 -days 3650 -out /opt/gitlab-cert/gitlab-ce.example.org.crt -subj '/CN=gitlab-ce.example.org/'
```

## RunnerのexecutorにDockerを使う場合

GitLab CE起動後`docker network ls`で"gitlab-network"が使用しているブリッジネットワークを引数に

`--docker-network-mode <gitlab-network-name>`

をオプション指定して`gitlab-runner register`を実行

## 参考

- [GitLab CEのDockerコンテナイメージを使って、ローカルにGitLab CEをサクッとたてる(https + Container Registry込み) - zaki work log](https://zaki-hmkc.hatenablog.com/entry/2020/01/31/083344)
- [パラメタの多いdocker runをdocker-composeを使ってYAMLで定義する(GitLab CE編) - zaki work log](https://zaki-hmkc.hatenablog.com/entry/2020/02/28/080516)
- [既存のGitLab CE on Dockerに、Runnerコンテナも追加してCI/CD環境をつくる - zaki work log](https://zaki-hmkc.hatenablog.com/entry/2020/03/13/081853)
- [GitLab CE/GitLab Runner on Docker環境でexecutorもDockerなCI/CD環境 - zaki work log](https://zaki-hmkc.hatenablog.com/entry/2020/03/14/194134)
