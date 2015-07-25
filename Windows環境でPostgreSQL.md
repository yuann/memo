# Windows環境でPostgreSQL

## サーバー側
### インストール
PostgreSQL 9.4.4 をインストールする。

1. http://www.enterprisedb.com/products-services-training/pgdownload から Version 9.4.4 の Win x86-64 のインストーラをダウンロード
1. postgresql-9.4.4-*-windows-x64.exe を実行
1. Installation Directory: `E:\System\PostgreSQL\9.4`
1. Data Directory: `E:\System\PostgreSQL\9.4\data`
1. Password: パスワードを設定（ユーザー「postgres」のパスワードになる）
1. Port: そのまま（`5432`だった）
1. Advanced Options
  - Locale: `C`
1. 「Stack Builder ...」のチェックを外して Finish

## クライアント側

1. Visual Studio でプロジェクトを作成
  - テンプレート: C#/Windowsフォームアプリケーション
  - プロジェクト名: PostgresTest
- パッケージマネージャコンソールで以下を実行
  - `Install-Package Npgsql -Version 2.2.5` (latest stable を使用)
  - `Install-Package Dapper`
- Form1 にボタンを追加して、クリックするとサーバ側の現在時を取得するようにする

```csharp
using System;
using System.Linq;
using System.Windows.Forms;
using Npgsql;
using Dapper;

namespace PostgresTest
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            DateTime resultDate;
            using (var conn = new NpgsqlConnection("Server=<サーバー名>;Database=postgres;Uid=postgres;Pwd=<パスワード>"))
            {
                conn.Open();
                resultDate = conn.Query<DateTime>("SELECT NOW();").Single();
            }

            MessageBox.Show(resultDate.ToString());
        }
    }
}
```

## 外部リンク

- [WindowsでPostgreSQLを使ってみよう](http://lets.postgresql.jp/documents/tutorial/windows/)
