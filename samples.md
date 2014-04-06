# サンプル

原文：[Samples and Walkthroughs](http://roslyn.codeplex.com/wikipage?title=Samples)

以下のサンプルは[SDK Preview](http://go.microsoft.com/fwlink/?LinkId=394641)
パッケージのSamplesフォルダ以下にあります：

* **APISampleUnitTests** -
  様々なAPIの使用方法がわかる一連のユニットテストがあります。
  これらの多くは[FAQ](faq.md)内でも参照されています。
* **ConsoleClassifier** -
  ソースコードを色つきでコンソール上に表示する
  シンプルなコンソールアプリケーションです。
* **FormatSolution** -
  ソリューション内のC#およびVBのソースコードを整形する
  コンソールアプリケーションです。
* **MakeConst** -
  ローカル変数が定数に出来ることを示したり、簡単な変更で変数を定数に
  変換出来ることを示すような、
  (ユーザー定義のコンパイラー警告を出力する)診断ツールです。
  以下にある診断機能のウォークスルーでこのサンプルの詳細を紹介しています。
* **ConvertToAutoProperty** -
  自明なgetterやsetterを持ったプロパティを自動実装プロパティに変換する
  リファクタリングコードです。
* **ImplementNotifyPropertyChanged** -
  選択したクラスのプロパティがPropertyChangedイベントをサポートするように
  変換するリファクタリングコードです。
  エディタ上で対象のプロパティを選択してAlt+.を入力し、
  リファクタリング用のポップアップメニューを表示させた後、
  "Apply INotifyPropertyChanged pattern"を選択します。

コンパイラ層およびワークスペース層がAPIを使用する方法については
[ソースレポジトリ](https://roslyn.codeplex.com/SourceControl/latest)内を
探索してみてもよいでしょう：

* [レポジトリのDiagnosticsフォルダ](https://roslyn.codeplex.com/SourceControl/latest#Src/Diagnostics/)
  には実際の診断機能の例(ほとんどがFxCopのルールとして再実装されているもの)や、
  コード修正機能の例が数多く見つかります。
  CSharpあるいはVisualBasicというサブフォルダにある末端ノードのコードファイルを
  参照してみてください。

# ウォークスルー

以下のウォークスルーに進む前に、まずは[Roslynの概要](overview.md)に目を通して、
いくつか主要な概念を把握しておくことをおすすめします。

## はじめに

* [Getting Started - Semantic Analysis (CSharp).pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822179)
  または
  [Word docx](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822178)
* [Getting Started - Semantic Analysis (VB).pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822181)
  または
  [Word docx](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822180)
* [Getting Started - Syntax Analysis (CSharp).pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822183)
  または
  [Word docx](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822182)
* [Getting Started - Syntax Analysis (VB).pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822185)
  または
  [Word docx](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822184)
* [Getting Started - Syntax Transformation (CSharp).pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822187)
  または
  [Word docx](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822186)
* [Getting Started - Syntax Transformation (VB).pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822189)
  または
  [Word docx](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822188)

## 診断機能およびコード修正

* [How To Write a Diagnostic and Code Fix (CSharp).pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822458)
  または
  [Word docx](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822457)
* [How To Write a Diagnostic and Code Fix (VB).pdf](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822460)
  または
  [Word docx](http://www.codeplex.com/Download?ProjectName=roslyn&DownloadId=822459)
