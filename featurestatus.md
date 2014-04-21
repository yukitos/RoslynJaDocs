# 言語機能の実装ステータス

原文：[Language feature implementation status](http://roslyn.codeplex.com/wikipage?title=Language%20Feature%20Status)

* **Exists**: 以前のリリースで実装済み
* **Done**: 今回のリリースで実装済み
* **Planned**: 今回のリリースで実装予定
* **Maybe**: おそらく今回のリリースで実装予定
* **No**: 今回のリリースでは実装予定無し
* **N/A**: この言語では意味をなさない

すべての項目が変更されうるという点に注意してください。
既に実装済みの機能であったとしても、
フィードバックの結果を反映してデザインが改善される可能性があります。

現行の [End User Preview](http://go.microsoft.com/fwlink/?LinkId=394641)
に対する機能説明については以下を参照してください：

* [C#](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=824694)
* [Visual Basic](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=826498)

| 機能                             | 例                                                              | [C#][link01] | [VB][link02] |
|:---------------------------------|:----------------------------------------------------------------|:-------------|:-------------|
| プライマリコンストラクタ         | class Point**(int x, int y)** { ... }                           | Done         | Maybe        |
| 自動実装プロパティ初期化子       | public int X { get; set; } **= x;**                             | Done         | Exists       |
| ゲッターのみの自動実装プロパティ | public int Y **{ get; }** = y;                                  | Done         | Done         |
| staticメンバーのusing            | using System.**Console;** ... **Write**(4);                     | Done         | Exists       |
| ディクショナリ初期化子           | new JObject { **["x"]** = 3, **["y"]** = 7 }                    | Done         | Planned      |
| インデックス付きメンバー初期化子 | new JObject { **$x** = 3, **$y** = 7 }                          | Done         | Planned      |
| インデックス付きメンバーアクセス | c.**$name** = c.**$first** + " " + c.**$last**;                 | Done         | Exists       |
| 宣言式                           | int.TryParse(s, out **var x**);                                 | Done         | Maybe        |
| catch/finally内でのawait         | try ... catch { **await** ... } finally { **await** ... }       | Done         | Planned      |
| 例外フィルター                   | catch(E e) **if (e.Count > 5)** { ... }                         | Done         | Exists       |
| 型ケース                         | Select Case o : Case **s As String :** ...                      | No           | Done         |
| ガードケース                     | Select Case i : Case Is > 0 **When i Mod 2 = 0**                | No           | Done         |
| 部分モジュール                   | **Partial Module** M1                                           | N/A          | Done         |
| 部分インターフェイス             | **Partial Interface** I1                                        | Exists       | Done         |
| 複数行文字列リテラル             | "Hello**<newline>**World"                                       | Exists       | Done         |
| 年を先頭にした日付リテラル       | Dim d = #**2014-04-03**#                                        | N/A          | Done         |
| 2進数リテラル                    | **0b00000100**                                                  | Planned      | Done         |
| 桁セパレーター                   | 0xEF_FF_00_A0                                                   | Planned      | Done         |
| 行継続コメント                   | Dim addrs = From c in Customers **' comment**                   | N/A          | Done         |
| TypeOf IsNot                     | If **TypeOf** x **IsNot** Customer Then ...                     | N/A          | Done         |
| 式をボディに持つメンバー         | public double Dist **=> Sqrt(X * X + Y * Y);**                  | Planned      | No           |
| イベント初期化子                 | new Customer { **Notify +=** MyHandler };                       | Planned      | Planned      |
| [Null伝搬](link03)               | customer**?.**Orders**?**\[5\]**?.**$price                        | Planned      | Planned      |
| セミコロン演算子                 | (var x = Foo()**;** Write(x)**;** x * x)                        | Planned      | Maybe        |
| private protected                | **private protected** string GetId() { ... }                    | Planned      | Planned      |
| params IEnumerable               | int Avg(**paras IEnumerable<int>** numbers) { ... }             | Planned      | Planned      |
| コンストラクタの推論             | new **Tuple**(3, "three", true);                                | Planned      | Planned      |
| [文字列補完][link04]             | "**\{**p.First**} \{**p.Last**}** は **\{**p.Age**}** 歳です。" | Maybe        | Maybe        |
| nullableに対するTryCast          | Dim x = **TryCast**(u, **Integer?**)                            | Exists       | Planned      |
| +を使用したデリゲートの連結      | d1 **+=** d2                                                    | Exists       | Planned      |
| 明示的な実装                     | Class C : **Implicitly** Implements I                           | Exists       | Planned      |
| NameOf 演算子                    | string s = **nameof(**Console.Write**);**                       | Planned      | Planned      |
| [Strictモジュール][link05]       | **Strict** Module M                                             | Exists       | Planned      |

[link01]: csharp_languagedesign.md
[link02]: vb_languagedesign.md
[link03]: http://roslyn.codeplex.com/discussions/540883
[link04]: http://roslyn.codeplex.com/discussions/540869
[link05]: http://roslyn.codeplex.com/discussions/540507

