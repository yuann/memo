# LocalDB を使う

1. Visual Studio 2015 でプロジェクトを作成
  - テンプレート: C#/Windowsフォームアプリケーション
  - プロジェクト名: LocaldbTest
- プロジェクト > 新しい項目の追加
  - サービスベースのデータベース
  - 名前: `SampleDatabase`
- 新しいデータソースの追加 > データベース > データセット
  - データベース: `SampleDatabase.mdf`
  - 接続文字列: `SampleDatabaseConnectionString`
  - データセット名: `SampleDatabaseDataSet`
- パッケージマネージャコンソールで以下を実行
  - `Install-Package Dapper`
- Form1 にボタンを追加して、クリックするとサーバ側の現在時を取得するようにする

```csharp
using System;
using System.Linq;
using System.Windows.Forms;
using System.Data.SqlClient;
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
            using (var conn = new SqlConnection(Properties.Settings.Default.SampleDatabaseConnectionString))
            {
                conn.Open();
                resultDate = conn.Query<DateTime>("SELECT GETDATE();").Single();
            }

            MessageBox.Show(resultDate.ToString());
        }
    }
}
```
