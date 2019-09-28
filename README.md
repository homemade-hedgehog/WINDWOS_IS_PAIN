# WINDWOS_IS_PAIN
弊社はwindows限定なのだけど、program業界でWindwos縛りって割とクリティカルダメージでは？  
弊社内の方に送る打開策  
なお、弊社内の方はweb閲覧に意味不明なハードルがあるので、タブレット or スマホがあると調べ物が捗る  
- program業界では重要なwebページのドメインは".io"なのだが、割と弾かれる
- slide shareでいろいろな説明資料が上がっているけれど、アクセスできない
- 誰かが公開してくれたライブラリの保存先がgoogle driveやらstrageやらdropboxやらで、アクセスできずインストールできない
  - 手持ちのスマホなどでダウンロードしたものを社内に送って、頑張ってインストールする
  - 社内ルール的にアップロード不可の外部ファイルサーバーへのアクセスはOKなので注意の上よしなに

## 対策 -> Windowsのことは忘れよう
- 幸い、やっとwindwos10移行が本格化したのでwindows上で別システムを動かそう
  - 👎docker: docker on windowsだとgpuにアクセスできないというクリティカルな制約がある
  - 👍windows sub sysytem for linux: microsoft storeに標準ラインナップされているアプリ
  - git for windows + cygwin + make (+ and so on): 私はコレを使っているけど、ある意味エキスパート向け。謎エラーと謎結果オーライと再現性との戦い
  - virtualbox: Windowsソフトのvirtualbox(仮想マシン構築)を使ってwindows上に仮想マシンを立ち上げる。割と初心者フレンドリー。定期的にcloneを残してbackupすると全てが嫌になったときに巻き戻せるのでアグレッシブに色々できる
  
#### マメ
- windows userの最初の難関はコマンドラインインターフェースととっつきにくいviエディター
  - コマンドラインインターフェース: 気合一発、我慢して慣れる。python専用機と割り切れば覚えるコマンドは20もないはず
  - viエディター: 驚愕の使いにくさなので、別のエディターを入れる(vim, emacs)
    - for python user: pythonファイルを編集するときは、viエディター等は使わずIDE(統合開発環境)を使うのが良い
      - pycharm(free): 代表的なエディター。有料版(500円/月)もあるが無料でも行ける
      - visual studio: 有名なエディター。udemy等の教育サイトでは驚異の使用率
      - atom: ある程度使えるけど、設定がめんどくさい

---
### WSLの使い方
- installation @ ubuntu
  - linuxはいろいろな種類がある
    - centos: 業界デファクトと考えて良いくらいの普及率。真剣にlinuxでやっていくならコレ
    - ubuntu: windowsからの乗り換えのハードルが低い。普及率が拡大してきて、centoosを抜いたかもとアナウンスがあった
    - 他: おすすめしない。github repositoryのinstallationに記載があるのは大体 maxos, centos (, ubuntu)
  - この辺を見てやると良いと思う: [here](https://ygkb.jp/7291), [here](https://news.mynavi.jp/article/liunx_win-2/)
  - microsoft storeに複数あるversion
    - ubuntu: 最新のubuntu versionに自動的に乗り換えつつ行くらしい, for beginner
    - ubuntu 18.04LTS: ~ April 2023まで更新が保証されるubuntuバージョン...最新に見えるけど次のversionはApril 2020提供開始
    - ubuntu 16.04LTS: ...無理に使うこともないと思う
- how to boot ubuntu on wsl
  - アプリケーションの一覧に"ubuntu"というアイコンが登録されているのでクリック
  - 探すのが面倒な場合はwindowsのスタートボタン横の検索窓に"ubuntu"と入れて候補に上がったオレンジのアイコンをクリック
- ubuntuを起動したらコマメにアップデートを
  - 以下のコマンドをタイプして、聞かれたパスワードを入力してエンター
    - 上が更新問い合わせ
    - 下が更新実行
  ```
  sudo apt update
  sudo apt upgrade
  ```
  
---
### python life
- installation: 真面目にやるのとお手軽にやるのがある
  - 真面目: ubuntu標準のpythonを使って環境を構築していく。面倒なのでやる気がしない
  - お手軽: python科学計算セットのanacondaを使う
    - anaconda: coutinuum社が提供するパッケージライブラリからライブラリをダウンロードして使えるpython環境一式
    - [ここ](https://www.sejuku.net/blog/85373)を参照してインストールする
    - WARNING: pythonには標準のライブラリセットのpypiがある。
      - anacondaとpypiは同一名称別内容のライブラリが存在して、anaconda環境下でpypiを頻繁に使うと偶に破壊的なエラーに出くわす
      - ライブラリをインストールするときは
        1. anaconda.orgで探す
        2. 無いときはpypi or github
          - 別ライブラリを一緒にインストールするライブラリがあるので、ライブラリの説明ページにあるrequirements.txt参照で極力anacondaのを入れる
      - まぁ、面倒くさいので、破壊的なエラーに出くわしたらanacondaを再インストールするのが早い
        - 何かをインストールしたら手順は控えておくのがおすすめ
- 環境設定: gitとか
  - 言語処理界隈の人は以下のコマンドを入れたらだいたい戦えるはず  
  `sudo aptitude install mecab libmecab-dev mecab-ipadic-utf8 git make curl xz-utils file`
  
  
---
#### データ分析業界のbeginner  
とりあえず[これ](http://yutori-datascience.hatenablog.com/entry/2017/10/24/215647)を参照したら環境構築、分析コンペ、業界スタンダードライブラリなど一通りわかる
