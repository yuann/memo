# Windows環境でGitBucketにGistプラグインを導入

## プラグインの入手
https://github.com/takezoe/gitbucket-gist-plugin/releases から gitbucket-gist-plugin_2.11-*.jar をダウンロード

### ※ソースコードから生成する場合

1. [JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) をインストール
1. https://github.com/takezoe/gitbucket-gist-plugin から「Download ZIP」でダウンロード
1. gitbucket-gist-plugin-master.zip を解凍
1. プロキシの設定（必要なら）
  - sbt.bat を開き、`java` の後ろに ` -Dhttp.proxyHost=<プロキシサーバのホスト名> -Dhttp.proxyPort=<ポート番号>` を記述
1. sbt.bat を実行して暫く待つ
1. プロンプトが表示されたら `package` と入力して Enter
1. また暫く待つ
1. プロンプトが表示されたら `exit`
1. `target/scala-2.11/gitbucket-gist-plugin_2.11-*.jar` が生成されている

## プラグインの配置

1. GitBucketのバージョンを最新にする
1. `gitbucket-gist-plugin_2.11-*.jar` を `GITBUCKET_HOME/plugins` にコピー
1. GitBucketを再起動
