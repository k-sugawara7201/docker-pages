# mkdocsの環境構築
## 前提条件
- pythonがインストールされていること

## 手順
- pythonの仮想環境を作成します  
  ```
  python -m venv .venv
  ```

- 仮想環境を有効化します
  - windowsの場合  
    ```
    ./.venv/Scripts/activate
    ```
  - linuxの場合  
    ```
    ./.venv/bin/activate
    ```

- 必要なライブラリをインストールします  
  ```
  pip install -r requirements.txt
  ```

- mkdocsのローカルサーバを起動します  
  ```
  mkdocs serve
  ```

- localhost:8000にアクセスします
