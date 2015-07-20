# Windows環境でMySQL

## サーバー側
MySQL Community Server 5.5.44 をインストールする。

1. http://dev.mysql.com/downloads/mysql/ から「Windows (x86, 64-bit), MSI Installer」をダウンロード
1. mysql-5.5.44-winx64.msi を実行
1. 「Choose Setup Type」で Custom を選択
1. 「Custom Setpup」で Location を `E:\System\MySQL\MySQL Server 5.5\` に変更
1. Install
1. 「Launch the MySQL Install Configration Wizard」にチェックが入った状態で Finish
1. MySQL Server Instance Configuration
  - configuration type: 「Detailed Configration」を選択
  - server type: 今回は「Developer Machine」を選択
  - database usage: 「Multifunctional Database」を選択
  - InnoDB Tablespace: `E:\System\MySQL\data` に変更
  - approximate number of concurrent connections to the server: 「Decision Support (DSS)/OLAP」を選択
  - networking options: そのまま
  - default character set: 「Best Support For Multilingualism」を選択
  - Install As Windows Server: チェックを入れたまま
  - Include Bin Directory in Windows PATH: チェックを入れる
  - Modify Security Settings: パスワードを設定
  - Execute
  - Finish

## クライアント側

1. Visual Studio 2013 でプロジェクトを作成
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
            using (var conn = new MySqlConnection("Server=localhost;Database=;Uid=root;Pwd=******"))
            {
                conn.Open();
                resultDate = conn.Query<DateTime>("SELECT NOW();").Single();
            }

            MessageBox.Show(resultDate.ToString());
        }
    }
}
```
