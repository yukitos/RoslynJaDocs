# .NET Compiler Platform ("Roslyn") FAQ

原文：[.NET Compiler Platform (“Roslyn”) FAQ](http://roslyn.codeplex.com/wikipage?title=FAQ)

このFAQはよくある質問や、以前のRoslyn CTPから受け継いだすばらしい質疑応答だけでなく、
学習用および初心者向けの質問なども含まれています。
チームが介入せずにコミュニティーユーザー同士で
問題が解決されているようなものもあります。
すばらしいことです！
このページ内をキーワードまたはフレーズ検索すると
きっと手がかりとなるものが見つかることでしょう。

**多くの質問には関連するコードスニペットがあります。
サンプルコードおよびテストコードはチームからリリースされた
[SDK Preview](http://go.microsoft.com/fwlink/?LinkId=394641)の
`%installdir%\{CSharp|VisualBasic}\APISampleUnitTests\faq.{cs|vb}`
にあります。**
コードが利用できる質問に対しては、回答文に`FAQ(27)`というようなタグが
1つ以上付けられています。
ソースコードを開いて同じ名前のタグを検索すれば
コードが見つけられるようになっています。
このドキュメントにすべてのコードが記載されているわけではないので、
そのままでは動作しないコードもあることに注意してください。
samples/testプロジェクトには常に最新のAPIに対する変更が反映されています。


## コンテンツ

* [プロジェクト/横断的な質問](#project_cross_cutting_questions)
  * [Roslynにはどのようなドキュメントが用意されていますか？](#what_docs_are_available_on_roslyn)
  * [標準的なVisual Studio 2010 SP1あるいはVisual Studio 2012を使用してRoslynをSxSでインストールできますか？](#does_installing_roslyn_work_sxs_with_regular_vs_2010_sp1_or_vs_2012)
  * [コンパイラーパイプライン中のソースコードを変更できますか？](#can_i_rewrite_source_code_within_the_compiler_pipeline)
  * [RoslynのDLLを自分で作成したサンプルとともに配布したり、コードをブログに掲載してもいいですか？](#can_i_redistribute_the_roslyn_dlls_with_my_samples_or_code_on_my_blog)
  * [製品環境下でEnd User PreviewやSDKを使用できますか？「go-live」EULAはありますか？](#can_i_use_the_end_user_preview_or_sdk_for_my_production_code_does_it_have_a_go-live_eula)
  * [インストール後、あるいはRoslynのインストールを行わずにRoslynのEULAを確認できますか？](#where_can_i_see_the_roslyn_eula_after_installation_or_without_committing_to_install_roslyn)
  * [私の代わりにConnectにバグを登録してもらえますか？](#can_you_just_open_a_connect_bug_for_me)
