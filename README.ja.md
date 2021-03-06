# MapK Project Home @github
このページは`MapK`プロジェクトのポータルページです。

`MapK`プロジェクトは`Kotlin`の優れたリフレクション機能を利用し、従来の`Java`ライブラリに代わる安全なマッピングライブラリを提供します。

# 「安全なマッピング」とは
## これまでの`Java`ライブラリ
従来の`Java`ライブラリは、基本的に以下の手順でオブジェクトを初期化していました。

1. 引数無しコンストラクタによるインスタンス生成
2. セッターによるフィールドの初期化

一方この形での初期化は、`Kotlin`のように`immutability`を重視するモダンな言語との相性が非常に悪いです。

マッピング対象のクラスは`POJO`のままとしたり、`Kotlin no-arg plugin`を用いた黒魔術的な手段によって、`Kotlin`でこれまでの`Java`ライブラリを利用することも可能ですが、この手法は以下のような危険性が有ります。

- `null`安全が壊れる
  - `non-null`なフィールドにも`null`をセットできてしまう
- フィールドにアクセスするまで初期化の成否が判定できない
  - 初期化に必要な引数が足りていなくてもインスタンスが得られてしまう
  - よく分からない場所で発生する`NullPointerException`に怯えなければならない

## `Kotlin`のリフレクションが実現する「安全なマッピング」
`Kotlin`のリフレクションは、`Java`のリフレクションに比べ以下のような利点が有ります。

- メソッド、コンストラクタの引数名がデフォルトで取得できる
  - リフレクションによる呼び出しを容易に実装できる
- アクセス可能なデータがプロパティという形で一元的に管理されている
  - 引数名とプロパティの一致を見るのに余計な変換処理が不要

これによって、以下の手順でオブジェクトの初期化を行うことが可能です。

1. データソースから必要な引数を抽出
2. 1からコンストラクタ、ファクトリーメソッド等を呼び出して初期化

この方法で初期化を行うことには以下のようなメリットが有ります。

- 関数を呼び出すため、マッピングに失敗するとその場で例外となる
- オブジェクトの必要な引数が足りないという状況が発生しない（当然`null`安全が保たれる）
- 初期化のロジックを自分で書くことができる

このようなメリットを享受することで、コード量削減・手で書かないことによるバグ抑制といった従来の`Java`ライブラリに有るメリットはそのままに、より安全なマッピングを実現することができます。

# プロダクト一覧
## KMapper
`Kotlin` to `Kotlin`のマッピングライブラリです。

- [ProjectMapK/KMapper: Mapper Libraly for Kotlin\.](https://github.com/ProjectMapK/KMapper)
- [ProjectMapK / KMapper](https://jitpack.io/#ProjectMapK/KMapper)

## KRowMapper
`Kotlin`向け`RowMapper`ライブラリです。
`BeanPropertyRowMapper`のように機能します。

- [ProjectMapK/KRowMapper: RowMapper for Kotlin\.](https://github.com/ProjectMapK/KRowMapper)
- [ProjectMapK / KRowMapper](https://jitpack.io/#ProjectMapK/KRowMapper)
