# .NET コンパイラー プラットフォーム ("Roslyn") 概要

(ダウンロード: [roslyn-overview.pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822125))

## コンテンツ

* [イントロダクション](#introduction)
* [公開されているコンパイラーのAPI](#exposing_the_compiler_apis)
  * [コンパイラーパイプラインの機能領域](#compiler_pipeline_functional_areas)
  * [APIレイヤー](#api_layers)
    * [コンパイラーAPI](#compiler_apis)
    * [ワークスペースAPI](#workspaces_apis)
* [シンタックスに対する処理](#working_with_syntax)
  * [シンタックスツリー](#syntax_trees)
  * [シンタックスノード](#syntax_nodes)
  * [シンタックストークン](#syntax_tokens)
  * [シンタックストリヴィア](#syntax_trivia)
  * [スパン](#spans)
  * [カインド](#kinds)
  * [エラー](#errors)
* [セマンティクスに対する処理](#working_with_semantics)
  * [コンパイル](#compilation)
  * [シンボル](#symbols)
  * [セマンティックモデル](#semantic_model)
* [ワークスペースに対する処理](#working_with_a_workspace)
  * [ワークスペース](#workspace)
  * [ソリューション、プロジェクト、ドキュメント](#solutions_projects_documents)
* [まとめ](#summary)

## <a name="introduction"></a>イントロダクション

コンパイラーは伝統的にブラックボックスなものです。
つまり一方からソースコードを入力して、中で何か魔法が起こり、
他方からオブジェクトファイルやアセンブリが出てくるといった具合です。
コンパイラーがこの魔法を行うためには、処理対象のソースコードに対する知識を
非常に詳しく積む必要があるわけですが、
コンパイラーを実装するウィザード以外がこの知識を得ることはできません。
また、翻訳済みの出力結果が生成されると、この知識は即座に忘れ去られてしまいます。

何年もの間、この作法はそういうものだと納得されてきたのですが、
しかし今はそういうわけにもいかなくなっています。
統合開発環境(IDE: integrated development environment)のIntelliSenseや
リファクタリング、高機能な名前変更、「すべての参照の検索」、「定義に移動」
といった機能を頼りにすることで生産性を向上できるようになってきています。
あるいはコードの品質を向上するためにコード分析ツールを使用したり、
アプリケーションを構築するためにコード生成機能を使用したりするようになっています。
これらのツールがより賢くなるにつれて、コンパイラしか知り得ないような
コードの深い知識がツール側でも必要になってきているわけです。
.NET コンパイラー プラットフォーム("Roslyn")の中核をなすミッションはここにあります。
ブラックボックスの蓋を開けて、コンパイラーの持つコードに関する知識を
ツールやエンドユーザーが共有できるようにするというのがこのプロジェクトの目的です。
入力されるソースコードをオブジェクトコードとして出力するトランスレーターを
不透明にせず、.NET コンパイラー プラットフォーム("Roslyn")を通すことによって
コンパイラーをプラットフォーム、つまり独自のツールやアプリケーションにおいて
コードに関するタスクを処理する際に使用できるようなAPIを提供できるようにする
というわけです。

コンパイラーをプラットフォームとして変形させることにより、
コードを対象にするようなツールあるいはアプリケーションを作成するための
障壁を劇的に下げることができます。
それにより、たとえばメタプログラミングやコード生成、コード変更、
C#やVBといった言語をインタラクティブに使用したり、
C#やVBをドメイン固有言語として組み込んだりといった、
様々な領域においてイノベーションが見込めます。

また、.NET コンパイラー プラットフォーム("Roslyn") SDK Previewには
コード生成や分析、リファクタリングにおける新しい言語オブジェクトモデルの
ドラフトが含まれています。
将来のプレビューでは、C#やVisual Basicをスクリプトあるいはインタラクティブに
使用できるようにするためのAPIドラフトも組み込むことが出来ればと考えています。
このドキュメントでは.NET コンパイラー プラットフォーム("Roslyn")の概要を紹介します。
各機能の詳細についてはSDK Previewに含まれるウォークスルーやサンプルを
参照してください。

## <a name="exposing_the_compiler_apis"></a>公開されているコンパイラーのAPI

### <a name="compiler_pipeline_functional_areas"></a>コンパイラーパイプラインの機能領域

### <a name="api_layers"></a>APIレイヤー

#### <a name="compiler_apis"></a>コンパイラーAPI

#### <a name="workspaces_apis"></a>ワークスペースAPI

## <a name="working_with_syntax"></a>シンタックスに対する処理

### <a name="syntax_trees"></a>シンタックスツリー

### <a name="syntax_nodes"></a>シンタックスノード

### <a name="syntax_tokens"></a>シンタックストークン

### <a name="syntax_trivia"></a>シンタックストリヴィア

### <a name="spans"></a>スパン

### <a name="kinds"></a>カインド

### <a name="errors"></a>エラー

## <a name="working_with_semantics"></a>セマンティクスに対する処理

### <a name="compilation"></a>コンパイル

### <a name="symbols"></a>シンボル

### <a name="semantic_model"></a>セマンティックモデル

## <a name="working_with_a_workspace"></a>ワークスペースに対する処理

### <a name="workspace"></a>ワークスペース

### <a name="solutions_projects_documents"></a>ソリューション、プロジェクト、ドキュメント

## <a name="summary"></a>まとめ
