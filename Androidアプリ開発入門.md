Windows環境でAndroidアプリ開発入門
==================================

## はじめに
<http://dotinstall.com/lessons/basic_android_v2> を参考にした。

## インストール
### Android Studio のインストール
- 予めJDKをインストールしておく。
- <http://developer.android.com/sdk/index.html> から Android Studio をダウンロードしてインストーラを起動。画面の指示に従う。
- Android SDK のインストールのために **3.2GB** の空き容量を要求してくるので、都合に応じてSDKのインストール先をシステムドライブ以外に変更。

### Android SDK のインストール
- Android Studio を起動。
- Welcome 画面 > Quick Start > Configure > SDK Manager
- Android SDK Manager が開く
  - 基本はチェックが既に入れられているのでそれに従う。
  - (最新版/例:Android 5.0.1) Android TV 等の開発をしないのであれば、「Android TV/Wear ...」「ARM EABI ...」等のチェックを外す。
  - (実機/例:Android 4.4.2) 「SDK Platform」「Intel x86 Atom System Image」「Google APIs」にチェックを入れる。
  - パッケージのインストール。

## プロジェクトの作成
- Android Studio を起動。
- Welcome 画面 > Quick Start > Start a new Android Studio Project
- アプリケーション名とドメインを入力。
- 以降はとりあえず規定値でいいと思うが、必要に応じて適宜選択する。

## エミュレータの起動
- Tools > Android > AVD Manager を起動。
- Create Virtual Device でエミュレータを追加する。(Nexus 6 の場合)
  - Phone > Nexus 6 を選択肢てNext。
  - Lollipop x86_64 を選択してNext。
  - Finish
- エミュレータを起動する。

### 動作確認
- Run > Run 'App' を選択。
- 実行中のエミュレータを選択してOK。

## その他
- プレビュー画面の右上にある歯車アイコンをクリックして`Include Device Frames`のチェックを外すと、実機イメージのフレーム部分が消える。
- text: @string/hello_world
- textSize: 32sp (フォントサイズの変更)
- onClick: changeLabel
- Alt+Enter > Import Class

```java
public void changeLabel(View view) {
  TextView tv = (TextView)findViewById(R.id.myTextView);
  tv.setText("Changed!");
}
```
