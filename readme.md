### 実行環境
- os/version: ubuntu 20.04 (64 bit)
- os/kernel: 5.10.16.3-microsoft-standard-WSL2 (x86_64)
- os/type: linux
- os/arch: amd64
- go/version: go1.17.9
- go/linking: static
- go/tags: none
# rcloneとは
- クラウドのファイル管理をしてくれるシステム
- 公式URL[https://rclone.org/]

## 何ができるの？
- ブラウザからのGUIダウンロードだとファイル移動に手間がかかる
- Linuxのディレクトリをエクスプローラで参照しようとするとGUI起動は遅い
- drive → Douwnloads → 格納したいフォルダではなく直接ディレクトリにDLしたい(windows,linux問わず)
- driveのCRUD操作も可能な為、コマンドのalias化をすれば動作の軽減になる

### 情報求
- 共有ドライブの認証設定
###
## 作業手順
### DL
curl https://rclone.org/install.sh | sudo bash
### config
  - rclone config
  - 参考URL
    - 公式[https://rclone.org/drive/]
    - 見やすい[https://www.nextdoorwith.info/wp/se/how-to-control-google-drive-from-linux-rclone/]
    - その2[https://takuya-1st.hatenablog.jp/entry/2017/12/27/205346]
  - 詰まりそうな所
    - googleDriveの場合
      - GCPの登録 クレカ必要 (PlaceとかのAPI叩くのにも必要だから設定しといて損はない)
      - Drive API の認証情報作成 で OAuth クライアントID クライアントシークレットを取得
      - OAuth 同意画面でアプリを設定
        - スコープでdrive関連のAPIを追加
    - auto config失敗しやすかったのでno
      - rclone authorize "drive" "client Id入れると出てくるはず~~~" 別ターミナルで実行
      - 401err 出るなら 一時的だけど rclone authorize "drive"
      - If your browser doesn't open automatically go to the following link　自動でされない場合ctrl + click でアクセス
      - 返ってきたトークン値を貼り付け

### mount (driveのフォルダをローカルで見れる)
  -
### 基本動作 remote = gdに自分は設定
## 詳しくは[https://rclone.org/commands/rclone/]

### 自分が使っているalias
#rclone alias
rc-alias()
{
  alias rc='rclone'
  alias rcmd='rclone mkdir'
  alias rcto='rclone touch'
  alias rcdl='rcclone purge'
}
#### ls系 (一覧確認)
  - rc lsd gd: (フォルダ一覧)
  - rc ls gd: (ファイル一覧)
  - rc tree gd: (階層表示) option[https://rclone.org/commands/rclone_tree/]
#### フォルダ作成
  - rcmd gd:test
#### ファイル作成
  - rcto name:test/test.txt
#### 削除
  - rcdl name:test(指定したディレクトリ以下削除)
  - rc rmdir (空フォルダのみ削除)

#### フォルダ同期
  - rc sync -i ローカルdir gd: driveDir [https://rclone.org/commands/rclone_sync/]



### その他
#### ファイルに書き込み
  - echo "test" | rc rcat gd:test/test.txt
#### フォルダサイズ
  - rc size gd:test

#### アプデ
  - rclone selfupdate
