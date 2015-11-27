# Windows環境で Visual Studio Code

## インストール
https://code.visualstudio.com/ からインストーラーをダウンロードして実行。

## CSS設定
### MarkdownPreview用にCSSファイルを用意

今回は、 `C:\Users\<ユーザー名>\Work\_vscode` に [github.css](https://gist.github.com/andyferra/2554919) と user.css を配置した。

user.css へは、以下のようにフォント設定を記述。

```css:user.css
* {
  font-family: "Meiryo";
}

code, code span {
  font-family: "MS Gothic";
}
```

### エディタのフォント設定とMarkdownPreviewへのCSS適用
File > Preferences > User Settings を開き、 settings.json へ以下のように記述。

```json:settings.json
// Place your settings in this file to overwrite the default settings
{
	"editor.fontFamily": "MS Gothic",
	"markdown.styles": [
		"file://C:/Users/<ユーザー名>/Work/_vscode/github.css",
		"file://C:/Users/<ユーザー名>/Work/_vscode/user.css"]
}
```

`与` や `化` 等が日本の字形で表示されれば問題ない。

### github.css を使う場合の微調整
[github.css](https://gist.github.com/andyferra/2554919) を使う場合、余白が多いなど気に入らない点があったので、 user.css で微調整。

```css:user.css
body {
  padding-top: 0px;
}

h1 {
  margin-top: 0px;
}

li, li ul {
  margin-top: 0px;
  margin-bottom: 0px;
}

hr {
  border: 1px solid;
  height: 0;
}
```

## その他の設定
必要に応じて `settings.json` へ追記。

```json:settings.json
{
    
    // ウィンドウ幅に合わせて折り返し
    "editor.wrappingColumn": 0,
    
    // 半角スペースやタブの表示
    "editor.renderWhitespace": true,
    
    // タブでスペース挿入
    "editor.insertSpaces": true,

    // プロキシ設定
    "http.proxy":"http://..."
}
```

## Extensionの導入

### Install

- `F1`を押す
- `extensions`と入力していくと`Extensions: Install Extension`が候補に出てくるので選択
- 続けてextension名を入力してEnter
- extensionがインストールされる

### Uninstall

- `F1`を押す
- `extensions`と入力していくと`Extensions: Show Installed Extensions`が候補に出てくるので選択
- 対象extensionの:x:ボタンを押してアンインストール
