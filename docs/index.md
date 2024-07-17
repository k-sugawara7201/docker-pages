# WSL2の環境構築
## WSL2のインストール
- windows powershellを**管理者として実行**で起動します
- 下記のコマンドを入力&実行します  
  ```
  wsl --install
  ```
- インストールが完了したら、PCを再起動します  
  ※コンソールでユーザ名の入力が求められた場合は、再起動不要です
- 再起動後、windowsの検索バーに「Ubuntu」と入力し、コンソールを開く
- ユーザー名、パスワードを設定します
- 設定後、一度コンソールを閉じ、コマンドプロンプトを起動します  
- 下記のコマンドを入力&実行し、wsl2の動作確認をします  
  ```
  wsl -l -v
  ```  
  下記のように表示されていればOKです  
  ```
    NAME              STATE           VERSION
  * Ubuntu            Running         2
  ```

## WSL2のアンインストール
- windows powershellを**管理者で実行**で起動します
- 下記のコマンドを入力し、linuxの状態を確認します  
  ```
  wsl -l -v
  ```
- 下記のコマンドで、wslを停止します
  ※wsl内のコマンドで停止することはできないので、必ずpowershell、もしくはコマンドプロンプトで実行してください  
  ```
  wsl --shutdown
  ```
- 再度下記のコマンドを実行し、wslが停止していることを確認します  
  ```
  wsl -l -v
  ```
- 下記のコマンドで、Ubuntuの登録を解除します  
  ※このコマンドを実行しないと、再度wslを使用する際に当時の状態で復元されてしまいます  
  ```
  wsl --unregister ubuntu
  ```
- 最後に、インストールされているUbuntuのアプリケーションをアンインストールします  
- 続いて、windowsの設定を変更します  
  内容については[こちら](https://qiita.com/zakoken/items/61141df6aeae9e3f8e36#%E6%89%8B%E9%A0%86%EF%BC%92wsl2-%E3%81%A8%E5%91%A8%E8%BE%BA%E3%82%A2%E3%83%97%E3%83%AA%E6%A9%9F%E8%83%BD%E3%81%AE%E7%84%A1%E5%8A%B9%E5%8C%96)を参照ください

## Docker Desktopがインストールされている場合
Docker Desktopがすでにインストールされている場合は  
`wsl -l -v` コマンドを実行すると、下記のように表示されます  
(`docker-desktop`に`*`がついています)  
```
  NAME              STATE           VERSION
* docker-desktop    Running         2
  Ubuntu            Stopped         2
```

この場合は、docker-desktopのディストリビューションが使用される設定になっているので、  
Ubuntuに切り替える必要があります  

- 下記のコマンドを実行します  
  ```
  wsl -s Ubuntu
  ```
- ディストリビューションの設定が変更できているか確認します  
  ```
  wsl -l -v
  ```
- 下記のような表示になっていれば切り替えOKです  
  (`Ubuntu`に`*`がついています)  
  ```
    NAME              STATE           VERSION
  * Ubuntu            Running         2
    docker-desktop    Running         2
  ```