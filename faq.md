# .NET Compiler Platform ("Roslyn") FAQ

原文：[.NET Compiler Platform (“Roslyn”) FAQ](http://roslyn.codeplex.com/wikipage?title=FAQ)

このFAQはよくある質問や、以前のRoslyn CTPから受け継いだすばらしい質疑応答だけでなく、
学習用および初心者向けの質問なども含まれています。
チームが介入せずにコミュニティーユーザー同士で
問題が解決されているようなものもあります。
すばらしいことです！
このページ内をキーワードまたはフレーズ検索すれば、
きっと手がかりとなるものが見つかることでしょう。

<a name="faq0"></a>
**多くの質問には関連するコードスニペットがあります。
サンプルコードおよびテストコードはチームからリリースされた
[SDK Preview](http://go.microsoft.com/fwlink/?LinkId=394641)の
`%installdir%\{CSharp|VisualBasic}\APISampleUnitTests\faq.{cs|vb}`
にあります。**
コードが利用できる質問に対しては、回答文に`FAQ(27)`というようなタグが
1つ以上含まれています。
ソースコードを開いて同じ名前のタグを検索すれば
コードが見つけられるようになっています。
このドキュメントにすべてのコードが記載されているわけではないので、
そのままでは動作しないコードもあることに注意してください。
samples/testプロジェクトには常に最新のAPIに対する変更が反映されています。


## コンテンツ

* [プロジェクト/横断的な質問](#q1)
  * [Roslynにはどのようなドキュメントが用意されていますか？](#q1-1)
  * [標準的なVisual Studio 2010 SP1あるいはVisual Studio 2012とともにRoslynをSxSでインストールできますか？](#q1-2)
  * [コンパイラーパイプラインの中でソースコードを変更できますか？](#q1-3)
  * [RoslynのDLLを自分で作成したサンプルとともに配布したり、コードをブログに掲載してもいいですか？](#q1-4)
  * [製品環境下でEnd User PreviewやSDKを使用できますか？「go-live」EULAはありますか？](#q1-5)
  * [インストール後、あるいはRoslynのインストールを行わずにRoslynのEULAを確認できますか？](#q1-6)
  * [RoslynのAPIはVSのCode ModelやCodeDomとどのような関係がありますか？](#q1-7)
  * [代わりにConnectにバグを登録してもらえますか？](#q1-8)
* [情報の取得に関する質問](#q2)
  * [どうすれば明示的、あるいは('var'により)暗黙的に型が指定された変数宣言に対する型情報を取得できますか？](#q2-1)
  * [どうすれば特定のコードの位置で利用可能な、特定の型の変数をすべて取得できますか？](#q2-2)
  * [どうすれば特定のコードの位置で補完リストあるいはアクセス可能なシンボルの一覧を取得できますか？](#q2-3)
  * [どうすればアクセス可能な型のメンバーに対する補完リストを取得できますか？](#q2-4)
  * [どうすればcaller/calleeの情報を取得できますか？](#q2-5)
  * [どうすればISolutionからシンボルまたは型に対するすべての参照を検索できますか？](#q2-6)
  * [どうすれば特定の名前空間に属するメソッドの呼び出し一覧を取得できますか？](#q2-7)
  * [どうすれば1つの(あるいは参照するすべての)アセンブリに含まれるすべてのシンボルを取得できますか？](#q2-8)
  * [どうすれば式ノードの型を取得できますか？](#q2-9)
  * [どうすれば一般的なAPIを使用して引数やローカルで宣言された変数の型情報を取得できますか？](#q2-10)
  * [どうすれば特定の識別子(あるいはIdentifierNameSyntaxノード)に対応するセマンティックモデルから型情報(TypeSymbol)を取得できますか？](#q2-11)
  * [どうすれば(場合によっては添付されているトリヴィアを無視して)シンタックスノードを比較できますか？](#q2-12)
  * [コメントはどのようにしてシンタックスツリー内に格納されていますか？(また、どうやってSyntax Visualizerを使用すればよいでしょうか？)](#q2-13)
  * [構造的トリヴィアとは何ですか？またどうやって取得できますか？](#q2-14)
  * [シンタックスツリーを視覚的に操作できるような可視化機能あるいはツールはありますか？](#q2-15)
  * [どうすればシンボルに関連づけられた型が既知かどうかを判別できますか？独自にAssemblyQualifiedNameを構築することは可能ですか？](#q2-16)
  * [どうすればSymbolが同じかどうか判断できますか？](#q2-17)
  * [どうすればセマンティックモデルがシンタックスノードに関する情報を提供できるかどうか判別できますか？](#q2-18)
  * [どうすればISymbolからメタデータトークンを取得できますか？](#q2-19)
  * [(SyntaxTokenなどの)識別子はなぜNameではなくValueというプロパティを持つのでしょう？また、ValueとValueText、GetTextにはどのような関連がありますか？](#q2-20)
  * [なぜ単にChildrenではなくChildNodesAndTokensになっているのでしょうか？](#q2-21)
  * [どうすればエラーを通知するための行および列番号を取得できますか？](#q2-22)
  * [どうすれば特定のカインドを持つ構文的サブツリーをすべて取得できますか？](#q2-23)
  * [どうすれば定義された型名に対する完全修飾名を取得できますか？](#q2-24)
  * [どうすれば特定のコールサイトにバインドされたオーバーロードを特定できますか？](#q2-25)
  * [どうすれば特定の式に対するTypeSymbolに対して特定の位置にあるTypeSymbolを割り当てられるかどうか判別できますか？](#q2-26)
  * [どうすればSyntaxTree内のテキストを単にパースするのではない方法でローカル変数宣言に対する完全修飾された型名を取得できますか？](#q2-27)
  * [どうすれば.NET Frameworkのバージョンを取得できますか？](#q2-28)
  * [どうすればプロジェクト内にある各ドキュメントや項目に対して、プロジェクトのアセンブリシンボルや参照、シンタックスツリーを取得できますか？](#q2-29)
  * [どうすれば特定の(派生)型に対するアノテーションを展開できますか？](#q2-30)
  * [なぜワークスペースAPIではもっと多くのVSのコンセプト(ネストされたドキュメントや非コードファイルなど)をサポートしないのですか？](#q2-31)
  * [どうすれば継承元の型や実装されたインターフェイスを取得できますか？また、どのメンバーがオーバーライドしている、あるいは親のメンバーを実装しているか判別することはできますか？](#q2-32)
  * [どうすればシンボルを使用して、メソッドに適用された属性を検索あるいは調査できますか？](#q2-33)
* [ツリーの構築および更新に関連する質問](#q3)
  * [どうすればクラスにメソッドを追加できますか？](#q3-1)
  * [どうすれば部分的な式や宣言などを置き換えられますか?](#q3-2)
  * [どうすれば宣言サイトおよびすべての参照サイトにあるシンボルの名前を変更できますか？](#q3-3)
  * [シンタックスやシンボルに独自の情報を追加することはできますか？](#q3-4)
  * [どうすればSyntaxRewriterを使用してステートメントを削除できますか？](#q3-5)
  * [どうすれば指定された型に対するポインタ型や配列型を生成できますか？](#q3-6)
  * [どうすればSyntaxRewriterを使用して(構造的トリヴィアである)#regionおよび#endregionを削除できますか？](#q3-7)
  * [どうすれば特定のカインドのステートメントすべて(たとえば変数の中身など)をログに残せますか？](#q3-8)
  * [どうすればコードファイルからすべてのコメントを削除できますか？](#q3-9)
* [スクリプティング、REPL、コード実行に関連する質問](#q4)
  * [REPLとホスト用スクリプティングAPIに何が起きたのですか？](#q4-1)
  * [Roslyn APIとLINQの式ツリーあるいは式ツリー v2とはどのような関係がありますか？メタプログラミングとDSLの実装のどちらに適していますか？](#q4-2)
* [その他の質問](#q5)
  * [エラスティックトリヴィア(elastic trivia)とは何ですか？](#q5-1)
  * [なぜSyntaxファクトリーは要求していないエラスティックトリヴィアを添付するのですか？](#q5-2)
  * [どうすればツリーあるいはノードをテキスト的な表現に整形できますか？](#q5-3)
  * [どうすればMSBuildタスクにRoslynを組み込んだ際にメタデータの取得を止めて、再入による競合を回避できますか？](#q5-4)
  * [プログラムをILにコンパイルするまでを行う一揃いの(Emit APIの)サンプルはありますか？](#q5-5)
  * [どうすればコンパイル要素から出力されたILやデバッグ情報、ドキュメントコメントをキャプチャできますか？](#q5-6)
  * [Roslynプロジェクトを使用して作成されたVS拡張を利用するにはどうすればいいですか？](#q5-7)
  * [Roslynのオブジェクトモデルのチャート図、あるいは型の継承関係ダイアグラムはありますか？](#q5-8)


### <a name="q1"></a>プロジェクト/横断的な質問
#### <a name="q1-1"></a>Roslynにはどのようなドキュメントが用意されていますか？

機能仕様書、言語機能の議論に関する設計メモがいくつかあります。
また、ドキュメントコメントはすべて揃えられています。
しかし現時点ではチームはAPIリファレンスを作成していません。
[Documentation](http://roslyn.codeplex.com/documentation)
([日本語](index.md))
を参照してください。

> 訳注：APIリファレンスは[NuDoq](http://www.nudoq.org/#!/Projects/Roslyn)
  のものが参考になるでしょう。

#### <a name="q1-2"></a>標準的なVisual Studio 2010 SP1あるいはVisual Studio 2012とともにRoslynをSxSでインストールできますか？

RoslynプレビューはVisual Studio 2013 RTMを対象としています。
したがってVisual Studio 2012を含めて、以前のバージョンのVSには
インストールできません。

#### <a name="q1-3"></a>コンパイラーパイプラインの中でソースコードを変更できますか？

開発者はコンパイラーパイプラインのそれぞれのステージにおいて
シンタックスパースや、セマンティック解析、アルゴリズム最適化、コード生成などを
行うことができるため、Roslynではプラグインアーキテクチャはサポートされていません。
しかしプレビルドのルールを使用することによって解析を行ったり、
MSBuildがcsc.exeあるいはvbc.exeにコードを渡す前に
異なるコードを生成したりすることができます。
Roslynを使用すればコードをパースしたり、コードを意味的に解析したりした後、
ツリーを書き換えたり参照を変更させたりすることができます。
そして変更結果を新しいコンパイル要素としてコンパイルすることができます。

#### <a name="q1-4"></a>RoslynのDLLを自分で作成したサンプルとともに配布したり、コードをブログに掲載してもいいですか？

サンプルコードや学習用途であればRoslynのDLLはRoslyn NuGetパッケージ
([Microsoft.CodeAnalysis](http://www.nuget.org/packages/Microsoft.CodeAnalysis))
として再配布する方法が推奨されます。

#### <a name="q1-5"></a>製品環境下でEnd User PreviewやSDKを使用できますか？「go-live」EULAはありますか？

End User CTPはプレリリースのソフトウェアです。
使用に際しての正確な使用条件やライセンス条件についてはCTPインストール時に表示される
EULAを参照してください。
既にCTPをインストール済みの場合、インストーラを再度実行すれば
使用条件が表示されるので、その後はCancelをクリックしてインストーラを終了します。

ツールのSDKのzipファイルには独自のEULAが同梱されています。
様々なRoslyn Nugetパッケージにもそれぞれ固有のEULAがあります。
これらのEULAはツールSDKをインストールした後、
Visual Studioのメインメニューにある[NuGetパッケージの管理]コマンドを実行して
「ライセンス」のリンクを開くことで確認できます。

またroslyn.codeplex.comからソースコードをダウンロードして、
Apache 2.0ライセンスの下に作業をすることもできます。

#### <a name="q1-6"></a>インストール後、あるいはRoslynのインストールを行わずにRoslynのEULAを確認できますか？

詳細については
[製品環境下でEnd User PreviewやSDKを使用できますか？「go-live」EULAはありますか？](#q1-5)
を参照してください。
ただしEULAはインストールまたは再インストール時にしか表示されないため、
EULAを確認した後はインストールをキャンセルするとよいでしょう。

#### <a name="q1-7"></a>RoslynのAPIはVSのCode ModelやCodeDomとどのような関係がありますか？

CodeDomはプログラム的なコード生成および
サーバー上におけるASP.NETのコンパイルを対象とするものです。
これは一部のツールが使用できるように後から追加されたもので、
既存のコードをモデル化してコード生成の機能を実現するためのものです。

VSのCode ModelはISV
(訳注：independent software vendor：パッケージソフトウェア開発・販売会社)
がコードをパースせずともコード指向のVS拡張を公開できるようにするためのものです。
VSのCode Modelはコードから型、メンバー、引数に至るまでを表現するものでした
(また、貧弱ながらコード生成機能もサポートしていました)。

Roslyn APIはC#およびVBのコードを完全にモデル化し、
完全なコード生成およびコード変更機能を有しています。
最終的にはVSのCode ModelをRoslyn APIで再実装することになるでしょう。
CodeDomはC#やVBチームとは別に開発されたテクノロジーなので、
(たとえ新しいRoslyn APIで書き換えたいと思う人がいたとしても)
変更する必要はありません

#### <a name="q1-8"></a>代わりにConnectにバグを登録してもらえますか？

Microsoft Open Techのメンバーたちはフォーラムやメールを通じて
様々な話し合いを行っているわけなので、皆さんの手間を減らすためにも
内部のバグであれば喜んで登録処理をします。
我々がバグを登録するといった場合には、バグ登録を行って、
顧客案件と同じ重要度が割り当てられることを保証します。
もしも皆さんがバグを追跡して、バグに対する変更を随時受け取りたいのであれば、
我々はConnectにバグ登録を行うことになります。

いくつかの理由により、我々が代わりにバグ登録を行うのでは無く、
皆さんがConnectへのバグ登録を行うようリクエストすることがあります。
1つめの理由としては、
我々の機能が原因で顧客を憤慨させるようなことは避けたいわけなので、
バグ報告者に対してバグが顧客から報告されない場合についてConnectのバグレビュー中に
問い合わせることがあるからです。
また、Connectのバグは常に顧客からの報告を受け付けられるようになっているため、
バグの再現手順や再現する環境についての問い合わせを行うことがある
というのが2つめの理由です。

Open Techのメンバーが代わりにConnectへバグ報告した場合、
Connectに対する更新情報は顧客ではなくメンバーに対してメールで通知されます。
これにより、バグを報告したメンバーから別のチームに対して、
バグと思われる問題が受け渡されます。
顧客情報や連絡先などは消去されることがあります。
これは厳密なポリシーではありません。
また、顧客と長期的なパートナー関係にある場合には
顧客の代わりにConnectへバグ報告することがあるということを意味しています。
ただしこれは我々の一般的なワークフローではありません。

我々としては顧客がフィードバックを送信したり
フィードバックをログに残したりする手順を極々簡単にしたいと考えていますので、
我々がなるべくバグ登録を行うようにするつもりです。
しかし皆さんが更新メールを受信してバグを追跡したい場合には
Connectへバグ報告をお願いすることがあります。
Connectへ報告する場合は
[VS Feedback](http://visualstudiogallery.msdn.microsoft.com/f8a5aac8-0418-4f88-9d34-bdbe2c4cfe72)
ツールを使用する方法が比較的簡単です。

### <a name="q2"></a>情報の取得に関する質問
#### <a name="q2-1"></a>どうすれば明示的、あるいは('var'により)暗黙的に型が指定された変数宣言に対する型情報を取得できますか？

'var'が指定された識別子 (C#) または型名が指定された識別子 (VB) をモデル化する
`IdentifierNameSyntax`から型情報を取得する方法については、
サンプルコードの`FAQ(1)`タグが指定された部分を参照してください
([インストール先についてはこちらを参照](#faq0))。
'var'宣言全体 (C#) またはローカル型の推論が有効な状態(`Option Infer On`)
での'Dim'宣言 (VB) をモデル化する`VariableDeclaratorSyntax`から
型情報を取得する方法については、
サンプルコードの`FAQ(2)`タグが指定された部分を参照してください

#### <a name="q2-2"></a>どうすれば特定のコードの位置で利用可能な、特定の型の変数をすべて取得できますか？

特定の型の名前すべてを取得する方法、
およびメンバーの種類あるいはスコープによってそれらをフィルタする方法については
サンプルコードの`FAQ(4)`タグが指定されたコードにいくつかの例があります
([インストール先についてはこちらを参照](#faq0))。
`SemanticModel.LookupSymbols` APIを呼ぶと特定の位置で利用可能な、
単純な名前で参照できるすべてのSymbolが取得できます。
ただし少し注意点があります。

`LookupSymbols` はたとえば匿名型に対してなど、
C#では記述できないシンボルを返すことがあります。
このような場合は `Symbol` の `CanBeReferencedByName` プロパティを
チェックするとよいでしょう。

結果として返されるシンボルにはローカルのシンボルだけでなく、
メソッドやフィールド、型、名前空間などより広いスコープのシンボルも含まれます。
ローカル変数だけを対象にするのであれば、
サンプルコードにあるように`Symbol`の`Kind`をチェックすればよいでしょう。

`LookupSymbols` は技術的にはスコープ内にあるものの、
参照できないようなシンボルを返すことがあります。
たとえばC#には関数スコープに昇格されるような構文があるため、
関数内で後から宣言されたシンボルがローカルシンボルとして見えることがあります。
しかしこれは宣言するよりも前に参照する形になるため、意味的には不正な状態です。

#### <a name="q2-3"></a>どうすれば特定のコードの位置で補完リストあるいはアクセス可能なシンボルの一覧を取得できますか？

特定の型の名前すべてを取得する方法、
およびメンバーの種類あるいはスコープによってそれらをフィルタする方法については
サンプルコードの`FAQ(4)`タグが指定されたコードにいくつかの例があります
([インストール先についてはこちらを参照](#faq0))。
この質問は「どうすれば特定のコードの位置で利用可能な、
特定の型の変数をすべて取得できますか？」という質問とよく似ていますが、
そちらの回答のままではVisual Studioで補完リストを表示させる際に
対処しなければならない問題がいくつか残されています。

#### <a name="q2-4"></a>どうすればアクセス可能な型のメンバーに対する補完リストを取得できますか？

アクセス可能な型のメンバーを取得する方法については
サンプルコードの`FAQ(5)`タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-5"></a>どうすればcaller/calleeの情報を取得できますか？

caller/calleeの情報を取得する方法については
サンプルコードの `FAQ(6)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
ただしサンプルは必ずしも完全ではない点に注意してください。
たとえば解析後のコードでは関数をデリゲート変数に割り当てた後に
呼び出していることがありますが、サンプルコードではこのような状況を考慮していません。

#### <a name="q2-6"></a>どうすればISolutionからシンボルまたは型に対するすべての参照を検索できますか？

参照を取得する方法については
サンプルコードの `FAQ(7)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
なお `FindReferences` のような拡張メソッドを活用するためには
`Roslyn.Services.dll` および `Roslyn.Services.{CSharp|VisualBasic}.dll` を
参照に追加した後、 `Roslyn.Services` 名前空間をオープンする必要があります。

#### <a name="q2-7"></a>どうすれば特定の名前空間に属するメソッドの呼び出し一覧を取得できますか？

特定のメソッド呼び出しに必要な名前空間(あるいは特定の名前空間に属するメソッド)
を検索する方法については
サンプルコードの `FAQ(8)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-8"></a>どうすれば1つの(あるいは参照するすべての)アセンブリに含まれるすべてのシンボルを取得できますか？

サンプルコードの `FAQ(9)` および `FAQ(10)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
前者はすべての名前空間のシンボルを走査して、次に型のシンボル、さらに
簡略のためにフィールドおよびメソッド定義のシンボルだけを走査しています。
後者は参照されたシンボルを見つけるためにすべての式を走査しています。

#### <a name="q2-9"></a>どうすれば式ノードの型を取得できますか？

式に対する型情報を取得する方法については
サンプルコードの `FAQ(3)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-10"></a>どうすれば一般的なAPIを使用して引数やローカルで宣言された変数の型情報を取得できますか？

変数の型情報を取得する方法については
サンプルコードの `FAQ(3)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
なおRoslynはパラメーターとローカル変数に対して、
それぞれ `ParameterSymbol` と `LocalSymbol` という異なる方法で
モデル化している点に注意してください。
これはパラメーターであれば ref/out を指定したり、デフォルト値を指定出来るという
違いがあることに由来します。

#### <a name="q2-11"></a>どうすれば特定の識別子(あるいはIdentifierNameSyntaxノード)に対応するセマンティックモデルから型情報(TypeSymbol)を取得できますか？

'var'が指定された識別子をモデル化する `IdentifierNameSyntax` から
型を取得する方法については
サンプルコードの `FAQ(1)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-12"></a>どうすれば(場合によっては添付されているトリヴィアを無視して)シンタックスノードを比較できますか？

ツリーやノードに対する比較を行ういくつかの方法については
サンプルコードの `FAQ(11)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-13"></a>コメントはどのようにしてシンタックスツリー内に格納されていますか？(また、どうやってSyntax Visualizerを使用すればよいでしょうか？)

Roslynツリーはコメントをトークンのトリヴィアとして格納します。
トリヴィアはこれまでの経験則から、
それに続くトークンに対してアタッチされます
(つまりトークンを含むノードの前にトリヴィアがあることになります)。
しかし特定の行にある最後のトークンよりも後にトリヴィアがある場合、
これらは前方にあるトークンに対してアタッチされます
(つまりトリヴィアが後方にあることになります)。

以下の例では1番目のコメントは後ろで宣言されている `int` トークンに対して
`LeadingTrivia` としてアタッチされます。
また、`int` トークンを含む `LocalDeclarationStatementSyntax` ノードの
前方トリヴィアにもあります。
1番目のコメントトリヴィアはコメント行に全くトークンが存在しないため、
`int` が別の行で記述されているにもかかわらず、このトークン以降にある
最初のトークンにアタッチされます。

```csharp
    int method1() {
        int a = 1;
        // comment1
        int b = 1; // comment 2
    }
```

2番目のコメントはセミコロンの `TrailingTrivia` としてアタッチされます。
したがって `LocalDeclarationStatementSyntax` ノード上にもあります。

Syntax Visualizerツールを簡単に説明すると、
このツールを使用するとRoslynがシンタックスツリーを構築する方法を理解したり、
コードの一部を視覚的にチェックしたりすることができます。
詳細については
[こちら](http://roslyn.codeplex.com/wikipage?title=Syntax%20Visualizer&referringTitle=FAQ)
を参照してください。

SyntaxWalkerを使用してコード内にあるコメントを収集し、
構造的なドキュメントコメントと区別する方法については
サンプルコードの `FAQ(29)` タグが指定された部分に若干サンプルがあります
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-14"></a>構造的トリヴィアとは何ですか？またどうやって取得できますか？

多くのトリヴィア(たとえば `WhitespaceTrivia` や `SingleLineCommentTrivia`)は
単に `Kind` プロパティを比較するだけでそれぞれのトリヴィアの種類を区別できます。
すべてのトリヴィアはいずれも構造体 `SyntaxTrivia` です。

一部のトリヴィア(ディレクティブやxmlドキュメントコメントなど)は
`SyntaxNode` から派生した型を使用して構造的にモデル化されています。
トリヴィアが構造を持つかどうかチェックする場合は
`HasStructure` プロパティの値で識別できます。
トリヴィアが構造的である場合、トリヴィアの `GetStrucure` メソッドを呼び出せば
`SyntaxNode` が取得できます。
たとえば `IfDirective` トリヴィアに対して `GetStructure` メソッドを呼び出すと
`IfDirectiveSyntax` ノードが取得できます。
このノードには `HasToken` や `IfKeyword`、
条件に対する `ExpressionSyntax` ノードなどが含まれます。

#### <a name="q2-15"></a>シンタックスツリーを視覚的に操作できるような可視化機能あるいはツールはありますか？

あります！
Syntax Visualizerツールの詳細については
[こちら](syntax_visualizer.md)
を参照してください。

#### <a name="q2-16"></a>どうすればシンボルに関連づけられた型が既知かどうかを判別できますか？独自にAssemblyQualifiedNameを構築することは可能ですか？

ベストな方法としては `Equals()` を使用することです。
Symbolは演算子 `==` をオーバーロードしているため、これでうまくいく場合もありますが、
Common Symbol API (`ISymbol`) と組み合わせる場合にはうまくいきません。
既知の型とシンボルの型を比較する方法としては、
`Compilation.GetTypeByMetadataName` メソッドを使用して既知の型を取得してから
`Equals()` を使用して比較する方法が一番簡単です。
シンボルの比較については
サンプルコードの `FAQ(12)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

非常に一般的な型(たとえば `Int32` や `String` )や、
コンパイラにとって特別な型など、一部の型については
`TypeSymbol.SpecialType` プロパティを参照することによってそれが
特別な型かどうかをチェックすることができます。
シンボルが特別な型かどうかをチェックする方法については
サンプルコードの `FAQ(12)` タグが指定されたコードを参照してください

コンパイル要素が異なるシンボル同士を比較した場合の結果は未定義です。

#### <a name="q2-17"></a>どうすればSymbolが同じかどうか判断できますか？

ベストな方法としては `Equals()` を使用することです。
Symbolは演算子 `==` をオーバーロードしているため、これでうまくいく場合もありますが、
Common Symbol API (`ISymbol`) と組み合わせる場合にはうまくいきません。
シンボルの比較については
サンプルコードの `FAQ(12)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

全く同じ引数オブジェクトに対してAPIを呼び出した場合であっても、
同じ `Symbol` オブジェクトが返される保証はありません。

非常に一般的な型(たとえば `Int32` や `String` )や、
コンパイラにとって特別な型など、一部の型については
`TypeSymbol.SpecialType` プロパティを参照することによってそれが
特別な型かどうかをチェックすることができます。
シンボルが特別な型かどうかをチェックする方法については
サンプルコードの `FAQ(12)` タグが指定されたコードを参照してください

コンパイル要素が異なるシンボル同士を比較した場合の結果は未定義です。

#### <a name="q2-18"></a>どうすればセマンティックモデルがシンタックスノードに関する情報を提供できるかどうか判別できますか？

ツリーやノード、セマンティックモデルが関連するかどうかチェックする方法については
サンプルコードの `FAQ(13)` タグが指定されたコードにいくつか例があります
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-19"></a>どうすればISymbolからメタデータトークンを取得できますか？

この機能はRoslyn APIとildasmのような外部ツールとを連携させる場合に
必要になるものだと思われます。
現在のところ、このような機能はありません。

#### <a name="q2-20"></a>(SyntaxTokenなどの)識別子はなぜNameではなくValueというプロパティを持つのでしょう？また、ValueとValueText、GetTextにはどのような関連がありますか？

`ParameterList.Parameters[0].Identifier.Value` に対して、
`Value` よりも `Name` では駄目だったのでしょうか？

識別子に対する `.Value` と `.Name` に関して言うと、
我々は識別子を `SyntaxToken` として表現しています。
SyntaxToken は他にも、ソースコード中にあるリテラルや句読点など、
多数の要素すべてを表現するものです。
SyntaxTokenには名前という概念がありませんが、
一方でこれはテキストをモデル化するものです。
`SyntaxToken.GetText()` はソースコードのパース時に読み取ったテキストを
そのまま返します。
`SyntaxTokne.Value` は SyntaxToken によって表現されるテキストの
オブジェクト「値」を返します。
`SyntaxToken.ValueText` はこの値のテキスト表現を返します。

たとえば `long @long = 1L` というコードがあるとします。
エスケープされた識別子 `@long` に対する `SyntaxToken.Value` と
`SyntaxToken.ValueText` の値はいずれも文字列 `long` を返します。
しかし `SyntaxToken.GetText()` は文字列 `@long` を返します。
同様に、リテラル `1L` に対する `SyntaxToken.Value` は
ボックス化された整数値 `1` を返します。
`SyntaxToken.ValueText` は文字列 `1` を返します。
`SyntaxToken.GetText()` はコードからパースされたテキストである `1L` を返します。

サンプルコードの `FAQ(14)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-21"></a>なぜ単にChildrenではなくChildNodesAndTokensになっているのでしょうか？

元々は `Children` というプロパティがありました。
ユーザビリティテストの結果得られたフィードバックによると、
シンタックスAPIを呼んでこのコレクションを処理する際に重大な問題があるとのことでした。
そのため、ノードとトークンの違いを強調し、
デフォルトでは `SyntaxNodeOrToken` 型が使用されることのないように
名前が変更されたという経緯があります。

#### <a name="q2-22"></a>どうすればエラーを通知するための行および列番号を取得できますか？

ツリーやノードから位置情報を取得する方法については
サンプルコードの `FAQ(16)` および `FAQ(17)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-23"></a>どうすれば特定のカインドを持つ構文的サブツリーをすべて取得できますか？

SyntaxWalker を使用して特定のカインドを持つノードやトークンを処理する方法については
サンプルコードの `FAQ(18)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
その他のいくつかのサンプル(たとえば `FAQ(1)`)では
`node.DescendentNodes().OfType<>()` を使用してサブツリーを取得しています。
あるいは別のサンプル(たとえば `FAQ(11)`)では
`node.DescendentNodes().First(t => t.Kind == SyntaxKind...)` というような
コードを使用しています。

#### <a name="q2-24"></a>どうすれば定義された型名に対する完全修飾名を取得できますか？

オープンなジェネリック型やクローズドなジェネリック型も含めて、
型の完全な名前を取得したり比較したりする方法については
サンプルコードの `FAQ(19)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

> 訳注：オープンなジェネリック型とは型引数が指定されていないもの、
  クローズドなジェネリック型とは型引数が指定されたもののこと。

#### <a name="q2-25"></a>どうすれば特定のコールサイトにバインドされたオーバーロードを特定できますか？

オーバーロードを解決する方法については
サンプルコードの `FAQ(20)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-26"></a>どうすれば特定の式に対するTypeSymbolに対して特定の位置にあるTypeSymbolを割り当てられるかどうか判別できますか？

割り当て可能かどうかを特定する方法、ならびに
割り当て可能であればどのような制限があるのかを特定する方法については
サンプルコードの `FAQ(21)` および `FAQ(22)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-27"></a>どうすればSyntaxTree内のテキストを単にパースするのではない方法でローカル変数宣言に対する完全修飾された型名を取得できますか？

サンプルコードの `FAQ(19)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-28"></a>どうすれば.NET Frameworkのバージョンを取得できますか？

サンプルコードの `FAQ(23)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
ただし本質的には `SpecialType.System_Object` を含むアセンブリの
バージョンを取得することになります。

#### <a name="q2-29"></a>どうすればプロジェクト内にある各ドキュメントや項目に対して、プロジェクトのアセンブリシンボルや参照、シンタックスツリーを取得できますか？

参照設定やドキュメント1つに対するツリーを取得する方法については
サンプルコードの `FAQ(23)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
なおコードを書き換えて、すべてを処理するようにすることも難しくないでしょう。

#### <a name="q2-30"></a>どうすれば特定の(派生)型に対するアノテーションを展開できますか？

特定の型にアノテーションを追加したり、
特定の型のアノテーションが指定されたトークンを検索する方法については
サンプルコードの `FAQ(25)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
サンプルコードにはありませんが、ノードに対しても同じような処理が通用します。

#### <a name="q2-31"></a>なぜワークスペースAPIではもっと多くのVSのコンセプト(ネストされたドキュメントや非コードファイルなど)をサポートしないのですか？

ワークスペースAPIはソリューションやプロジェクトのビュー、
およびC#やVBの現gのサービスが実際に使用するドキュメントのビューを表すものです。
ワークスペースのモデルにはC#やVBのソースコード、参照、コンパイルオプション、
その他細々としたものが含まれています。
しかしワークスペースAPIはxamlのモデル化やリソースファイルなど、
Visual Studioのプロジェクトシステムにある機能を
すべて表現しているわけではありません。
ワークスペースモデルはVisual Studioと独立して機能するようになっています。

Visual Studioのプロジェクトにある項目をすべて取得したい場合んいは
.NET Frameworkに同梱されているMSBuild APIを使用します。
コードがVisual Studio内で実行されるのであれば、
IVsHierarchy APIを使用してプロジェクトの項目を走査することができます。
このAPIを使用すると、Visual Studioによって管理されている
ネストされたドキュメントにアクセスすることもできます。
C#やVBファイルに対してセマンティック解析を行いたいのであれば
ワークスペースを使用することになります。

#### <a name="q2-32"></a>どうすれば継承元の型や実装されたインターフェイスを取得できますか？また、どのメンバーがオーバーライドしている、あるいは親のメンバーを実装しているか判別することはできますか？

型を名前で取得したり、親クラスや実装クラスを取得したり、
virtual、override、sealedといった情報を元にしてメンバーを検索したりする方法については
サンプルコードの `FAQ(37)` および `FAQ(38)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q2-33"></a>どうすればシンボルを使用して、メソッドに適用された属性を検索あるいは調査できますか？

属性を処理するための基本的なメカニズムについては
サンプルコードの `FAQ(39)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

### <a name="q3"></a>ツリーの構築および更新に関連する質問
#### <a name="q3-1"></a>どうすればクラスにメソッドを追加できますか？

サンプルコードの `FAQ(26)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q3-2"></a>どうすれば部分的な式や宣言などを置き換えられますか?

クラスの宣言を置き換える方法については
サンプルコードの `FAQ(26)` タグが指定されたコード、
部分式を置き換える方法については
サンプルコードの `FAQ(27)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

なおRoslyn言語サービスがロードされた状態で、
Visual Studio上では複数のワークスペースが
アクティブになっていることがある点に注意してください：

* Roslyn言語サービスがロードされるとVisual Studio内でアクティブなソリューションが
  ワークスペースとしてモデル化されます。
* Roslyn言語サービスがロードされるとVS上で開かれている雑多な .cs および
  .vb ファイルに対応したソリューションやプロジェクト
  (その他のファイル用プロジェクトを参照)が
  ワークスペースとしてモデル化されます。
* VS上で開かれている雑多な .csx ファイルに対応したソリューションやプロジェクトが
  ワークスペースとしてモデル化されます。
* インタラクティブウィンドウ内の一連のセッションが
  ワークスペースとしてモデル化されます。

Roslyn言語サービスの機能は `IWorkspace` に対して行われるため、
上記のワークスペースいずれに対しても機能するようになっています。

#### <a name="q3-3"></a>どうすれば宣言サイトおよびすべての参照サイトにあるシンボルの名前を変更できますか？

名前を変更する方法については
サンプルコードの `FAQ(28)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
なおこのサンプルではジェネリックの名前を処理していません。
また、名前を変更しようとしている型に応じて、
それぞれ異なる SyntaxRewriter
(たとえばクラスの宣言やコンストラクタの宣言は処理しないようなもの)を
作成する必要があるかもしれません

#### <a name="q3-4"></a>シンタックスやシンボルに独自の情報を追加することはできますか？

特定の型にアノテーションを追加したり、
特定の型のアノテーションが指定されたトークンを検索する方法については
サンプルコードの `FAQ(25)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

Symbolに対する機能はありません。

#### <a name="q3-5"></a>どうすればSyntaxRewriterを使用してステートメントを削除できますか？

ステートメントを削除したり、
メソッドの処理中に単にnullを返していい場合と
`Syntax.EmptyStatement()` を返すべき場合を区別したりする方法については
サンプルコードの `FAQ(30)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q3-6"></a>どうすれば指定された型に対するポインタ型や配列型を生成できますか？

サンプルコードの `FAQ(31)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q3-7"></a>どうすればSyntaxRewriterを使用して(構造的トリヴィアである)#regionおよび#endregionを削除できますか？

これらのディレクティブを削除する方法については
サンプルコードの `FAQ(32)` および `FAQ(33)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q3-8"></a>どうすれば特定のカインドのステートメントすべて(たとえば変数の中身など)をログに残せますか？

サンプルコードの `FAQ(34)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。

#### <a name="q3-9"></a>どうすればコードファイルからすべてのコメントを削除できますか？

\#regionディレクティブを削除する方法については
サンプルコードの `FAQ(32)` および `FAQ(33)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
このコードを書き換えて、 `SyntaxKind.SingleLineCommentTrivia` や
`SyntaxKind.MultiLineCommentTrivia` が対象になるようにすればよいでしょう。

### <a name="q4"></a>スクリプティング、REPL、コード実行に関連する質問
#### <a name="q4-1"></a>REPLとホスト用スクリプティングAPIに何が起きたのですか？

以前のCTPには同梱されていたこれらのコンポーネントは、
再導入の前にチームによってデザインレビューが行われているところです。
現在、チームはインタラクティブ/スクリプトコードの言語意味論を
完成させる作業を行っています。

#### <a name="q4-2"></a>Roslyn APIとLINQの式ツリーあるいは式ツリー v2とはどのような関係がありますか？メタプログラミングとDSLの実装のどちらに適していますか？

式ツリー v2(ETs v2: Expressoin Trees v2)は
文法を再構成したような形式の意味的モデルになっています。
これは一部の制御フローや割り当てステートメント、再帰などをサポートします。
しかし一方で型定義など、C#やVBが持つ言語機能の多くがサポートされていません。
Roslyn APIにはC#やVBの文法や意味的バインディング、コード生成といった機能が
完全にそろっています。

ドメイン固有言語(DSL: Domain Specific Language)やETs v2は
メタプログラミングの機能を部分的にサポートしますが、
本質的には.NET上で動的言語をサポートするためのものであり、
これらをアプリケーション上でホストすることによって
スクリプティング機能を実現できるようにするためのものです。

DSLを埋め込むことだけが目的であるならば、これらよりもRoslyn APIの方が適切で、
おそらくは他の選択肢を考慮する必要もないでしょう。
埋め込みDSLはコア言語のコードをコンパイルする間、
あるいは実行以前の時点で新しい構文に特定の意味を割り当てたいような場合において、
言語の構文を拡張するためのものです。
言語内でDSLをサポートする例としては
[Dylan language](http://opendylan.org/books/dpg/db_329.html)
などが参考になります。
構文拡張が不要なのであれば、DSLはC#のような汎用の言語とは反対に、
SQLのような単にドメインに強く依存する言語だというだけで、
通常の言語と代わりありません。
Roslyn APIはC#やVBを拡張できるような機能をサポートしているため、
DSLやET v2よりも明らかに制限が少なくなっています。

### <a name="q5"></a>その他の質問
#### <a name="q5-1"></a>エラスティックトリヴィア(elastic trivia)とは何ですか？

エラスティックトリヴィアは通常、空白要素を柔軟に表現するために
シンタックスツリー内に手動で追加されるものです。
パーサーから返されたツリーでは、ソースコード内の空白がそのまま表現されています。
エラスティックな空白を使用することにより、
生成されたツリーで空白要素を推測し、トークン同士が互いに直結していないことを
保証できるようになります。
フォーマッターやその他のツリー処理ツールでは
元々のソースコードに対する復元性を損なうこと無く、
自由にエラスティックな空白を省略、追加、変更することができます。

#### <a name="q5-2"></a>なぜSyntaxファクトリーは要求していないエラスティックトリヴィアを添付するのですか？

エラスティックな空白は推測された空白を表すものですが、
ツリーをテキストとして描画する場合には0個以上の空白としてエラスティックな空白を
表示することになるでしょう。
一部のファクトリーは空白が必要な2つの要素同士が意図せずに連結されることがないように、
あるいはツールがフォーマットオプションを適用できるように
エラスティックな空白を追加します。
当然ながら、レンダラーには一部のトークン間に空白を適切に挿入するような
便利な機能が備えられているべきではありますが、
たとえば開き波括弧の前にある空白をすべて削除するようなフォーマットオプションが
設定されているような場合もあるわけです。

エラスティックトリヴィアはツリーをテキストにマッピングする場合には
削除することができるものなので、長さが0になっています。

(ほとんどあり得ないことですが)必要であれば以下のようにすることで
ファクトリーから返された結果からエラスティックトリヴィアを削除することもできます：

```csharp
Syntax.Token(SyntaxKind.SemicolonToken).WithLeadingTrivia().WithTrailingTrivia()
```

#### <a name="q5-3"></a>どうすればツリーあるいはノードをテキスト的な表現に整形できますか？

フォーマットのいくつかの例については
サンプルコードの `FAQ(35)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
このサンプルには `SimplifyNames()` のような、Documentに対するサービスの
使用方法も含まれています。
また、サンプルコードの `FAQ(35)` タグが指定されたコードには
`SyntaxNode.Format()` の例があります。

#### <a name="q5-4"></a>どうすればMSBuildタスクにRoslynを組み込んだ際にメタデータの取得を止めて、再入による競合を回避できますか？

今のところすばらしい回答はありません。
RoslynはMSBuildを内部的に使用してワークスペースを生成しています。
そのためTask内からワークスペースを生成しようとした場合、
再入による競合が発生しうるという問題があります。
実際には動作したとしても、機能的にも空間的にも多数重複することになるため
別の問題が残ることになります。
正しい方法としてはTaskから派生して、既に存在するMSBuildの情報を使用している
RoslynTaskを使用することです。
今のところのワークアラウンドとしては、MSBuild Task内で一部の情報から
Roslynのコンパイル要素を作成して、それを使用するようにするとよいでしょう。
しかしコンパイルされるコードを変更したり、MSBuildターゲットに
ファイルを追加・削除したりする場合は完全な解決策にはなりません。

以下のコードはあまり立派な回答ではないのでサンプル/テストプロジェクトには
同梱されていませんが、質問に対する回答としては十分で、
皆さんの手がかりにはなるのではないかと思われます：

```csharp
    public class MyTask : Task {
        public override bool Execute() {
              var projectFileName = this.BuildEngine.ProjectFileOfTaskNode;
                  var project = ProjectCollection.GlobalProjectCollection.
                                GetLoadedProjects(projectFileName).Single();
                  var compilation = CSharpCompilation.Create(
                                        project.GetPropertyValue("AssemblyName"),
                                        syntaxTrees: project.GetItems("Compile").Select(
                                          c => SyntaxFactory.ParseCompilationUnit(
                                                   c.EvaluatedInclude).SyntaxTree),
                                        references: project.GetItems("Reference")
                                                           .Select(          
                                          r => new MetadataFileReference
                                                       (r.EvaluatedInclude)));
                 // 以降でコンパイル要素を処理します...
        }
    }
```

#### <a name="q5-5"></a>プログラムをILにコンパイルするまでを行う一揃いの(Emit APIの)サンプルはありますか？

次の [どうすればコンパイル要素から出力されたILやデバッグ情報、ドキュメントコメントをキャプチャできますか？](#q5-6) を参照してください。

#### <a name="q5-6"></a>どうすればコンパイル要素から出力されたILやデバッグ情報、ドキュメントコメントをキャプチャできますか？

サンプルコードの `FAQ(34)` タグが指定されたコードを参照してください
([インストール先についてはこちらを参照](#faq0))。
このサンプルにはコンパイルおよびバイナリを実行するような `Execute()` メソッドが
定義されています。

#### <a name="q5-7"></a>Roslynプロジェクトを使用して作成されたVS拡張を利用するにはどうすればいいですか？

Roslyn Visual Studio拡張機能プロジェクトをデバッグする際に起動されるVisual Studioの
インスタンスはRoslyn「ハイヴ」(あるいはVSが拡張を見つけ出すレジストリ階層)
と呼ばれる環境下で実行されます。
コマンドラインから
`devenv.exe /rootsuffix Roslyn`
を実行すれば、同じ環境で動作するVisual Studioのインスタンスが使用できます。

Roslyn VS拡張はRoslyn言語サービスにアクセスする必要があるため、
拡張機能をメインのVisual Studio「ハイヴ」で使用するためには
Roslyn End User Previewをインストールする必要があります。

#### <a name="q5-8"></a>Roslynのオブジェクトモデルのチャート図、あるいは型の継承関係ダイアグラムはありますか？

拡縮や検索をサポートするような型の継承関係ダイアグラムを作成できます。
Visual Studio 2010 Ultimateを用意した後、
[こちらの記事](http://social.msdn.microsoft.com/Forums/en-US/roslyn/thread/705b090b-58ac-4a94-b7b5-d1408205bc90)
を参考にしてダイアグラムを作成してください。
