# Windows環境でMySQL

## サーバー側
### インストール
MySQL Community Server 5.6 をインストールする。

1. http://dev.mysql.com/downloads/mysql/ から「Windows (x86, 32-bit), MSI Installer」をダウンロード (64bitの分も含まれる)
1. mysql-installer-community-5.6.*.msi を実行
1. Choosing a Setup Type
  - Custom を選択
1. Select Products and Features
  - 「MySQL Server 5.6.* - X64」を選択
  - 右下の「Advanced Option」をクリックし、Pathを設定
    - Install Directory: `E:\System\MySQL\MySQL Server 5.6`
    - Data Directory: `E:\System\MySQL\data`
1. Installation
  - Execute
1. Type and Networking
  - Config Type: 今回は「Development Machine」を選択
1. Account and Roles
  - パスワードを設定
1. Windows Service
  - 「Configure MySQL Server as a Windows Service」にチェックを入れたまま
  - 「Standard System Account」を選択したまま
1. Apply Server Configuration
  - Execute
  - Finish

### 権限追加
外部からデータベース「test」にユーザー「user1」で接続できるようにする

1. 「MySQL 5.6 Command Line Client」を起動
1. インストール時に設定したパスワードを入力

```
mysql> grant select,insert,update,delete on test.* to user1@"%" identified by 'user1pass';
mysql> flush privileges;
mysql> select Host, User from mysql.user;
```

### 権限削除

```
mysql> delete from mysql.user where user = 'user1';
mysql> flush privileges;
mysql> select Host, User from mysql.user;
```

### アンインストール

1. コントロールパネルから、 管理ツール > サービス > MySQL56 を停止
1. コマンドプロンプトを管理者権限で起動
1. `cd /d "E:\System\MySQL\MySQL Server 5.6\bin"`
1. `mysqld -remove MySQL56`
  - Service successfully removed. と表示される
1. コントロールパネルのプログラムと機能から
  - MySQL Server 5.6 をアンインストール
  - MySQL Installer - Community をアンインストール
1. 必要に応じて `E:\System\MySQL\MySQL Server 5.5` を削除

## クライアント側

1. Visual Studio でプロジェクトを作成
  - テンプレート: C#/Windowsフォームアプリケーション
  - プロジェクト名: MySQLTest
- パッケージマネージャコンソールで以下を実行
  - `Install-Package MySql.Data`
  - `Install-Package Dapper`
- Form1 にボタンを追加して、クリックするとサーバ側の現在時を取得するようにする

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data.MySqlClient;
using Dapper;

namespace MySQLTest
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
            using (var conn = new MySqlConnection("Server=<サーバー名>;Database=test;Uid=test1;Pwd=<パスワード>"))
            {
                conn.Open();
                resultDate = conn.Query<DateTime>("SELECT NOW();").Single();
            }

            MessageBox.Show(resultDate.ToString());
        }
    }
}
```
