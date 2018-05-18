## js練習用リポジトリ

### 行った操作ログ
- Problem1
  - `npm install immutable`

- Problem2
  - `npm install lodash`
  - `npm install --save-dev glup`

- Problem3
  - pushまでのgit操作は省略
  - クローン: `git clone https://github.com/kaneko-takayuki/js-practice.git`
  - 開発環境でのライブラリセットアップ: `NODE_ENV=development npm install`
  - 本番環境でのライブラリセットアップ: `NODE_ENV=production npm install`
  - 本番環境でセットアップすると、immutableとlodashのみインストールされる

- Problem4
  - lodash削除: `npm uninstall lodash`
  
- Problem5
  - 前提知識: `X.Y.Z`というようなバージョン情報がある時
    - `X`をメジャーバージョン
    - `Y`をマイナーバージョン
    - `Z`をパッチバージョン と呼ぶ
  - 特にバージョンを指定せずに`npm install`コマンドでライブラリをインストールすると、npmはその時点での最新バージョンを探してインストールしてくる
  - その時、package.jsonのバージョン部分にハット`^`が付けられて保存される
  - *ハット`^`が付いている場合、npmはパッチバージョンの更新を許可する*ようになる(*チルダ`~`が付いている場合は、マイナーバージョンの変更を許可*する)
  - 例
    - 5/18時点で`npm install --save-dev glup`コマンドを叩く
    - その時の最新バージョンは`3.9.1`なので、それがインストールされ、package.jsonのバージョン部分にはハット`^`が付く
    - その後、6/1時点でバージョン`3.9.2`に上がっていたとして、その時に`npm install`コマンドを叩くとnpmはパッチバージョンを更新するためglupは`3.9.2`にアップグレードされる
  - バージョンを固定するには
    - `npm install`した時に`^`や`~`を付けないようにすれば良い
    - そのためには、`save-exact`をtrueに設定すれば良い
      - `npm config set save-exact true`で指定(デフォルトで`^`や`~`が付かなくなる)
      - `npm install --save-dev --save--exact glup`でもいける(デフォルトでは`^`や`~`が付くけど、この時だけ付与しないようにできる)
  - 検証
    - `npm uninstall --save-dev gulp`
    - `npm install gulp --save-dev --save-exact`
    - package.json内に`"gulp": "3.9.1"`と表示されている(`^`も`~`も付いていないので、バージョンの固定化に成功)

- Problem6
  - lodashのバージョン3.10.1をインストール(5/18時点での最新は4.17.10)
  - ライブラリのバージョンの指定は、`npm install {ライブラリ名}@{バージョン}`で指定可能
  - lodashを3.10.1でインストールし、更にバージョンを固定には、`npm install lodash@3.10.1 --save-exact`を叩く
  - package.json内に`"lodash": "3.10.1"`と記述されているのを確認(バージョン3.10.1がインストールされた)

- Problem7
  - まず、`npm ls -g | grep gulp`でgulpがグローバルインストールされているか確認する(インストールされていなければ、何も出力されない)
  - インストール時、`-g`オプションを付ければグローバルインストールになる
  - なので、`npm install -g gulp`を叩けば良い
    - 以下の出力が出る(グローバルインストールに成功)
    ```
    ├─┬ gulp@3.9.1
    │ ├─┬ gulp-util@3.0.8
    │ │ ├─┬ gulplog@1.0.0
    │ │ ├─┬ has-gulplog@0.1.0
    ```
