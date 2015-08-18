# DapperでDateTime2

## 困ったこと
Dapperでは既定で、`System.DateTime`が`DbType.DateTime`にマッピングされています。
その為、場合によってはDbType.DateTimeの範囲外の値（0001-01-01≦x＜1753-1-1）で更新しようとして例外が発生したり、また、精度が落ちてしまうという事が考えられます。

```csharp
conn.Execute("INSERT INTO Table1 (Date1) VALUES (@Date1);", new { Date1 = new DateTime() })
```

### 例外の発生
> 型 'System.Data.SqlTypes.SqlTypeException' のハンドルされていない例外が System.Data.dll で発生しました

> 追加情報:SqlDateTime のオーバーフローです。1/1/1753 12:00:00 AM から 12/31/9999 11:59:59 PM までの間でなければなりません。

### 精度落ち

- 2015/08/09 06:09:38.1579152 - 期待した値
- 2015/08/09 06:09:38.1570000 - 実際の値

そこで、`System.DateTime`を`DbType.DateTime2`にマッピングさせます。

## 方法1) DynamicParametersで型のマッピングを行う
一部だけdatetime2を使っているなら、この方法が簡単です。

```csharp
var p = new DynamicParameters();
p.Add("Date1", new DateTime(), DbType.DateTime2);
conn.Execute("INSERT INTO Table1 (Date1) VALUES (@Date1);", p);
```

## 方法2) プログラムの開始時に全体のマッピングを書き換え
全体的にdatetime2を使っている場合、方法1では面倒です。

Program.csのMain()等、プログラムの開始時に一度だけ呼ばれるように以下を記述。

```csharp
Dapper.SqlMapper.AddTypeMap(typeof(System.DateTime), System.Data.DbType.DateTime2);
Dapper.SqlMapper.AddTypeMap(typeof(System.DateTime?), System.Data.DbType.DateTime2);
```
