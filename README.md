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
