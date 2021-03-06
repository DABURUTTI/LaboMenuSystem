# LaboMenuSystem
ラボメニューのgitへようこそ！

ここでは、メイン端末で動いているラボメニューのコードと、APIサーバー側のコード、さらにWEB_GUIのコードがアップされています。

前者に関しては、ログ程度の気持ちでアップしているだけので割愛します。

## APIサーバーのインストール
ApiサーバーはNodeで書かれています。
フォルダを適当な場所に配置して、 `$ npm install`　でインストール出来ます。
実行する場合は、pm2の使用を強く推奨します。

    $ npm install pm2
    $ cd path/to/APIServer
    $ pm2 start bin/Cafe-API
    $ pm2 save
次回起動時に自動的に復帰します

## APIリファレンス

すべてのAPIは以下のBASE-URLから始まります*ポートなどの設定は各自でどうぞ。

`http://www.yourhost.jp:3000/api`

### GET
- `/guid`
    - GUIDの情報を取得します、GUIDは主にポーリングに使用します。
        - 200-正常
        - 500-サーバーエラー
- `/guid/apdate`
    - 新たにGUIDを発行し、置き換えます、レスポンスには新たなGUIDが返ってきます。
        - 200-正常
        - 500-サーバーエラー
- `/img/?`
    - 画像ファイルを取得します。オプションに指定されたファイルを取得できます。
        - 200-正常
        - 404-ファイルが存在なかった。
        - 500-サーバーエラー
- `/json/menus.json`
    - メニューデータをJsonとして受け取ります。
        - 200-正常
        - 500-サーバーエラー

### POST
- `/post/`
    - ファイルをアップロードします。アップロードする際に、FileNameを`file`に指定した場合、名前が保持されます、それ以外を指定した場合、Filenameに設定された名前が使用されます。アップロードされたデータが画像データだった場合、サーバー内で自動的にトリミング処理を行います。さらに、WEB_GUI用にサイズの小さいサムネイルを生成します。サムネイルのファイル名には`-sm`が追加されます。
        - 200-正常
        - 500-サーバーエラー
- `/post/json`
    - メニューデータをアップする場合に使用します。
        - 200-正常
        - 500-サーバーエラー

## ToDo
- 認証機能を追加する
    - だれでも更新しまくれるのはちょっと...

- レスポンスを早くしたい
    - 非同期なのに...非同期じゃない！（なんでさ）

© DABU
