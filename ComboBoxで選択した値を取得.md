# WinFormsのComboBoxで選択した値を取得
悪い取得例も含めて記述する。

## 目標
comboBox1で選択した値をdata.Valueへ反映させる。未選択状態の場合はnull。


## 準備

```csharp
Item[] items = new Item[]{ new Item(0, "アルファ"), new Item(1, "ベータ"), new Item(2, "ガンマ") };
Data data = new Data();

private void Form1_Load(object sender, EventArgs e)
{
    comboBox1.DataSource = items;
    comboBox1.ValueMember = nameof(Item.Value);
    comboBox1.DisplayMember = nameof(Item.Name);
}

class Item
{
    public int Value { get; set; }
    public string Name { get; set; }

    public Item(int value, string name)
    {
        Value = value;
        Name = name;
    }
}

class Data
{
    public int? Value { get; set; }
}
```

## Lv -1
IndexとValueが偶然同じなために同一視してしまった人が書く。問題外。

```csharp
if (comboBox1.SelectedIndex > -1)
{
    data.Value = comboBox1.SelectedIndex;
}
else
{
    data.Value = null;
}
```

## Lv 0
一旦文字列に変換してからParseする。例外が発生しない書き方を模索した結果、間違った方法を選択したものと思われる。

```csharp
if (comboBox1.SelectedIndex > -1)
{
    var strSelectedValue = comboBox1.SelectedValue.ToString();
    data.Value = int.Parse(strSelectedValue);
}
else
{
    data.Value = null;
}
```

## Lv 1
キャスト。

```csharp
data.Value = (int?)comboBox1.SelectedValue;
```

or

```csharp
data.Value = comboBox1.SelectedValue as int?;
```

## Lv 2
事前に以下のバインディングを行っておくことで自動的にdata.Valueに値が反映されるようにする。

```csharp
// 事前
comboBox1.DataBindings.Add(nameof(ComboBox.SelectedValue), data, nameof(TestItem.Value), true, DataSourceUpdateMode.OnPropertyChanged);
```

UI側でValueの型を考えなくてもよくなる。
