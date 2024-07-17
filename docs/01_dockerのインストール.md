# dockerのインストール手順

## カレントディレクトリの移動
- 下記のコマンドで、カレントディレクトリを移動します  
  ```
  cd ~
  ```
## dockerのインストール
- dockerがインストールされていないことを確認します  
  ```
  docker -v
  ```

- dockerインストール用のスクリプトをダウンロードします  
  ```
  curl https://get.docker.com -o get-docker.sh
  ```  

- インストール用スクリプトの存在確認をします  
  ```
  ls
  ```  
  ファイル一覧が表示されるので、その中に`get-docker.sh`といいファイルがあればOKです

- ダウンロードしたスクリプトを実行します  
  ```
  sudo sh get-docker.sh
  ```
  ※この時、docker-desktopのインストールを推奨する表示がされますが、  
  　そのまま放置で問題ありません

- dockerのインストール確認をします  
  ```
  docker -v
  ```  
  下記のようにバージョンが表示されればOKです  
  ```
  Docker version 27.0.3, build 7d4bcd8
  ```

## dockerの動作確認
バージョンが表示される確認はしましたが、実際にコンテナが起動するかどうかも確かめます  
下記のコマンドを実行します  
```
docker run hello-world
```

下記のような表示が出ればOKです
```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

## dockerでpermission deniedが表示されるとき
dockerコマンドを入力する際に、`permission denied`と表示される場合の対処方法を記載します

- 下記のコマンドで現在ログインしているユーザ名を確認します  
  ```
  whoami
  ```

- 表示されたユーザ名をコピーし、下記の`${USER_NAME}`の部分を置き換えて実行します
  ```
  sudo usermod -aG docker ${USER_NAME}
  ```

- 再度dockerコマンドを入力し、sudo無しで実行できることを確認します  
  ※`docker -v`はsudoの有無が関係ないため、それ以外のコマンドで確かめてください

## 最後に
dockerの動作確認で実行したコンテナのキャッシュやイメージなどを削除します  

- 下記のコマンドを実行します
  ```
  docker system prune --all
  ```  
  y/Nの入力を求められるので、`y`を入力します  
  `Are you sure you want to continue? [y/N]`  

- 不要なデータが削除されたかどうか確認します  
  ```
  docker system df
  ```  
  下記のように表示されていれば削除完了です  
  ```
  TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
  Images          0         0         0B        0B
  Containers      0         0         0B        0B
  Local Volumes   0         0         0B        0B
  Build Cache     0         0         0B        0B
  ```
