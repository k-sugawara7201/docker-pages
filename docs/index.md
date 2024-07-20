# はじめに
Dockerを使用して開発を行っている現場がたくさんあります。  
しかし、Dockerって何？なんで便利なの？までは皆さん考えずに使っていると思います。  
そこで自分なりに調べてDockerについて簡単にまとめました。  
ご一読いただければ幸いです。  

## Dockerとは？
Dockerとは、1台のサーバー上で様々なアプリケーションを手軽に仮想化・実行できるようにするためのプラットフォームのことを指しています。  
Dockerコンテナと呼ばれるアプリケーションを実行するための環境を1台のサーバー上に作成することができます。  
コンテナを作成するための設計図として、イメージというものが存在しており、そのイメージを使用することで  
誰でも簡単に同じ開発環境のコンテナを作成することができます。  

## Dockerコンテナについて
Dockerコンテナは環境であると説明しましたが、ローカル環境と何が違うのかと思うかもしれません。  
Dockerコンテナの環境とローカル環境の違いについて説明します。

- 開発に必要なライブラリ  
  開発を行う際に必要なライブラリについて、ローカル環境でインストールすると、以前開発していたものが残っている可能性があります。  
  残っていたライブラリが原因で、開発に不具合が出てしまっては元も子もありません。  
  一方Dockerコンテナでは現在開発しているアプリに必要なライブラリだけをコンテナの中にインストールすることができるため、
  クリーンな環境で開発を進めることができます。  

- 環境の構築のしやすさ  
  例えば、開発に`node`や`npm`が必要な場合、ローカル環境では自分で必要なバージョンをインストールしなければなりません。  
  しかしDockerコンテナのイメージというものを使用すると、一発で条件に沿った環境を作成することができます。 

このように、コンテナとローカルではクリーンな環境であったり環境構築のしやすさで異なる点があります。

## Dockerでよく使われるファイル・ソフト
- Dockerfile  
  Dockerイメージを作成するための設計書のファイル。  
  このファイルを使用して、コンテナを作成する。  
  下記はDockerfileの構成例です
  ```yml
  FROM node:latest
  WORKDIR /app
  COPY ./app .
  RUN npm install
  EXPOSE 3000
  ```

- docker-compose  
  複数のコンテナを一度に操作することができる機能  
  この機能の設定ファイルとして docker-compose.yml ファイルが存在している。  
  このdocker-compose.ymlファイルには複数のコンテナ間の関係や環境変数などを記載します。  
  ```yml
  version: "3"
  services:
    spring-boot:
      build:
        context: ./web-spring2
        dockerfile: Dockerfile
      ports:
        - "8080:8080"
      depends_on:
        mysql:
          condition: service_started
      entrypoint: "java -jar /app/app.jar"
      networks:
        - app-net
    mysql:
      build:
        context: ./mysql
        dockerfile: Dockerfile
      ports:
        - "3306:3306"
      volumes:
        - ./mysql/settings:/etc/mysql/conf.d/
        - ./mysql/data/:/var/lib/mysql/
      environment:
        MYSQL_DATABASE: study
        MYSQL_ROOT_PASSWORD: riku0456
      networks:
        - app-net
  networks:
    app-net:
      driver: bridge
  ```

- Docker Desktop  
  WindowsやMacOSでDocker環境を構築・利用するためのツール  
  本来dockerはコマンドラインで操作しますが、このDocker DesktopはUIを使用してコンテナを操作することができます。  


では、実際にDockerを使える環境を作成してみましょう！