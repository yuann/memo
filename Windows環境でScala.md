# Windows環境で Scala + IntelliJ IDEA

## JDK のインストール
<http://www.oracle.com/technetwork/java/javase/downloads/index.html> から、JDK(jdk-8u*-windows-x64.exe)をダウンロードしてインストール。

## Scala のインストール
- <http://www.scala-lang.org/download/> から、インストーラ(scala-2.11.*.msi)をダウンロードして実行。
- Custom Setup で Location を `D:\scala\` に変更。
- Install

## IntelliJ IDEA + Scalaプラグイン のインストール
- <http://www.jetbrains.com/idea/download/> から、IntelliJ IDEA 13 Community Edition をダウンロード。
- インストーラ(ideaIC-13.*.exe)を実行してインストール。
- IntelliJ IDEA を起動。
- 設定をインポートするか聞かれるので、インポートしない方を選択。
- configure > Settings を開く。
- "plugin" で検索。
- IDE Settings > Plugins > Browse repositories... をクリック。
- "Scala" で検索。
- Scala の右クリックメニューから Download and Install を選択。
- インストールが終わったら Browse repositories... を Close。
- Settings を OK で閉じる。
- 再起動するか聞かれるので Restart を選択。

## Hello World
### 新規プロジェクトの作成
- IntelliJ IDEA を起動。
- Create New Project を選択。
- Scala > Non-SBT を選択。
- 下記通り入力
  - project name: ScalaHelloWorld
  - project SDK: `C:\Program Files\Java\jdk1.8.*`
  - Scala settings:
    - Set Scala Home `C:\Program Files (x86)\scala`

### クラスの追加
- Projectタブで、srcフォルダ右クリック > New > Scala Class
  - Name: HelloWorld
  - Kind: Object
- HelloWorldオブジェクトの中に`main`と入力し、`Tabキー`を押すと、mainメソッドの雛形が作られる。
- mainメソッドの中に`println("Hello World!")`と入力。

```scala:HelloWorld.scala
object HelloWorld {
  def main(args: Array[String]) {
    println("Hello World!")
  }
}
```

### 実行
メニューバー > Run > Run > HelloWorld 選択。(or `Alt`+`Shift`+`F10`)

## 参考
- [【図解】Scala 2.10 + IntelliJ IDEA 12 で｢Hello World｣する](http://qiita.com/suin/items/33ba576b3a253d7fa709)
