## About
コンテナオーケストレーションツールのハンズオンです。  
このドキュメントではハンズオン形式でdocker-compose, swarm, ECS, Kubernetes(GKE)を学習してもらうことを目的としています。 

## 想定する読者層
- Dockerを触ったことがある
    - まだDockerを触ったことが無い方の場合 [入門 Docker](https://y-ohgi.github.io/introduction-docker/) からはじめることをおすすめします
- コンテナオーケストレーションツールをこれから触ろうとしている
    - Kubernetes
    - ECS

## 必要な環境
- [Docker Hub](https://hub.docker.com/) のアカウント
    - Docker公式レジストリ
- [Play with Docker](https://labs.play-with-docker.com/)
    - DockerをWeb上で動かせる環境
- AWSアカウント
    - [クラウドならアマゾン ウェブ サービス 【AWS 公式】](https://aws.amazon.com/jp/)
- Docker for Mac/Windows
    - [Docker CE — Docker-docs-ja 17.06.Beta ドキュメント](http://docs.docker.jp/engine/installation/docker-ce.html)
    - Mac: `$ brew cask install docker`
- AWS CLI
    - [AWS Command Line Interface をインストールする - AWS Command Line Interface](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-chap-install.html)
    - Mac: `$ brew install awscli`
    - Windows: `> choco install awscli`

## 備考
- GitHub
    - [y-ohgi/orchestration-docker](https://github.com/y-ohgi/orchestration-docker)
- 筆者
    - [@_y_ohgi](https://twitter.com/_y_ohgi)
- [Privacy Policy](privacy-policy.md)
    - Google Analytics によって各章の滞在時間を把握することが目的です。

---
DMM.comの社内勉強会に使用した資料の一部を公開したものです。  
[DMM採用情報 | DMM.com Group](https://dmm-corp.com/recruit/top)
