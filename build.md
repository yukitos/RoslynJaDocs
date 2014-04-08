# ビルド、テスト、デバッグ

原文：[Building, Testing, and Debugging](http://roslyn.codeplex.com/wikipage?title=Building%2c%20Testing%20and%20Debugging)

## 必須のソフトウェア

### Visual Studio 2013 Professional

現在、RoslynのソースコードはVisual Studio 2013を対象にしています。
Visual Studioを拡張するためにコードの一部でVS SDKを使用しているので、
Professional以上のバージョンのVisual Studioが必要です。

### Visual Studio 2013 SDK

Visual Studio 2013を拡張するためにVisual Studio SDKを使用しています。
SDKは
[無料でダウンロード](http://www.microsoft.com/en-us/download/details.aspx?id=40758)
して簡単にインストールできますが、Visual Studio 2013 Professional
(以上のバージョン)が必要です。

### .NET Compiler Platform ("Roslyn") End User Preview

変更をVisual Studio内でテストするためには、
End User PreviewをインストールしてVisual Studioの
試験用インスタンス(以下を参照)を構成する必要があります。

また、Roslynのソースコードでは言語の新機能をいくつか使用しています。
これらの新機能をVisual Studio IDEが把握できるようにするためにも、
[End User Preview](http://go.microsoft.com/fwlink/?LinkId=394641)
をインストールしておく必要があります。
End User Previewをインストールしなかった場合にはそれらしいエラーが
エラーリストに表示されることになるでしょう。

### NuGetパッケージマネージャ

依存するパッケージを復元するために[NuGet]()を使用しています。
NuGet Package Managerの一部のバージョンではパッケージの復元機能に問題があったため、
最低限NuGet 2.8.1がインストールされていることを確認しておくことを推奨します。
[ツール]-[拡張機能と更新プログラム]を開いて、[更新プログラム]のタブをクリックして
最新の状態になっているかどうかチェックするとよいでしょう。

### Visual Studio 2013 Update 2 RC (推奨)

VS2013の以前のビルドを使用した場合の問題点については今のところ把握していませんが、
多くのテストが既にUpdate 2 RCの環境で実行されていることもあり、
Update 2 RCのインストールを推奨します。

## コードを取得する

1. ブラウザ上で http://roslyn.codeplex.com/SourceControl/latest を開きます
2. [Clone]のリンクをクリックしてURLをコピーします。
3. Visual Studio チーム エクスプローラーウィンドウを開きます
   ([表示]-[チーム エクスプローラー])。
4. 既に別のプロジェクトに接続している場合は[チームプロジェクトへの接続]を
   選択します。
   (訳注：チーム エクスプローラ上部にある電源プラグのようなアイコン)
5. [ローカル Git リポジトリ]の下にある[複製]をクリックします。
6. 手順2でコピーしたURLを入力します。
7. コードを保存しておくためのローカルマシン上の場所を指定します。
8. [複製]ボタンをクリックします。
9. 分岐を`releases/build-preview`に切り替えます。
  1. チーム エクスプローラー上で[分岐]ビューを選択します。
  2. [新しい分岐]のリンクをクリックします。
  3. 分岐の名前を`releases/build-preview`にします。
     (訳注：手順4を先に行うと分岐の名前が自動的に入力されます)
  4. ドロップダウンから`origin/releases/build-preview`を選択します。
  5. [分岐のチェックアウト]にチェックがあることを確認します。
  6. [分岐の作成]をクリックします。

> 注意：`master`と`releases/build-preview`ではAPIが異なります。
  `master`をビルドした場合、変更をVisual Studio上で
  テストできなくなることに注意してください。

## Roslynバイナリに対する厳密名の検証無効化およびRoslynの試験用VSハイヴの準備

RoslynバイナリはMicrosoftの厳密名キーを使用して遅延署名されるように構成されています。
プライベートキーを使用することはできないため、
これらの遅延署名されたバイナリをロードしようとすると通常はエラーになります。
したがって、これらのバイナリをテストしたり、
ローカルビルドバージョンを実行したりするためには
厳密名の検証を無効化する必要があります。

また、通常の開発環境に影響を与えずにVisual Studio上で
変更をテスト出来るようにするために、
コマンドラインオプション`rootSuffix`を指定して
隔離されたレジストリハイブおよびAppDataディレクトリが使用されるようにします。

ソースコード内には厳密名の検証を無効化して、"Roslyn"の試験用Visual Studioハイヴを
設定するためのスクリプトも含まれています。

このスクリプトは以下の手順で実行できます：

1. `開発者コマンド プロンプト for VS2013`を管理者として実行します。
  1. Windows 8.1の場合、スタートページを表示して`Visual Studio ツール`と入力します。
  2. 検索結果で表示されたフォルダを開きます。
  3. `開発者コマンド プロンプト for VS2013`を右クリックして
     [管理者として実行]を選択します。
2. 複製を作成したディレクトリに移動します。
   たとえば`cd /d C:\Code\Roslyn`のようにします。
   以下の手順ではこのディレクトリを`<clone dir>`として参照します。
3. スクリプトを実行します：
   `Src\Tools\Microsoft.CodeAnalysis.Toolset.Open\Scripts\Prepare.bat`

> 注意：Roslyn試験用VSハイヴを削除して厳密名の検証を復帰させる場合には
  **`u`**を指定してこのコマンド実行します。

## NuGetパッケージのダウンロード

コマンドプロンプトで`<clone dir>`ディレクトリに移動した後、
`Src\.nuget\nuget restore Src\Roslyn.sln` を実行します。

これにより、Roslynのビルドに必要なすべての参照およびツールがマシン上に揃えられます。
ツールセットパッケージを使用しているため、ソリューションファイルを開く前に
このコマンドを実行しておくことが重要です。

## コマンドラインコンパイラのビルド

コマンドラインコンパイラをビルドするには、git cloneで作成したディレクトリ内にある
`Src\Roslyn.sln`のファイルを開くだけです。
あるいはコマンドラインから`msbuild Src\Roslyn.sln`を実行して
ビルドすることもできます。
C#コンパイラーをデバッグしたい場合は`Compilers\CSharp\rcsc`プロジェクトを
スタートアッププロジェクトに設定します。
Visual Basicのコンパイラーの場合は`Compilers\VisualBasic\rvbc`
プロジェクトになります。

たいていの場合、パフォーマンス的な理由からrcscやrvbc経由でコンパイラが
呼び出されることは**無い**ものの、それが一番簡単なデバッグ方法であることに
注意してください。
エントリポイントとしては以下があります：

1. rcsc2.exeおよびrvbc2.exe。
   これらは非常に小さな実行ファイルで、VBCSCompiler.exeのプロセスを
   起動する、あるいはこのプロセスに接続して、コマンドライン引数を渡すだけのものです。
   このようにすることによって、VBCSCompiler.exeが複数のプロジェクト間でデータを
   再利用することが出来るようになります。
2. MSBuildタスク。
   `Compilers\Core\MSBuildTasks`プロジェクト内には同じくVBCSCompiler.exeに接続して
   引数を渡すためのMSBuildタスクが定義されています。

3. 独自に作成したAPIのホスト。
   これにはコンパイラを呼び出す試験用Visual Studio IDEや、SDKを使用して作成された
   その他のアプリケーションなどが含まれます。
   Visual Studioを使用してバイナリをデバッグする方法については以下で説明します。

> 注意：デフォルトではVBCSCompiler.exeは起動してから3時間動作します。
  もしも頻繁に変更およびリビルドする場合には
  `Src\Compilers\Core\VBCSCompiler\App.config`
  を編集してタイムアウトの値を変更できます。

## 変更をVisual Studioに反映する

Roslyn試験用ハイヴを作成する前に変更をビルドした場合、
Visual Studioはその変更を認識しません。
その場合、上で説明したPrepareスクリプトを実行した後、
(メニューから[ビルド]-[ソリューションのリビルド]を選択して)
ソリューションをリビルドすると変更がテスト用Visual Studioに反映されます。

### Visual Studioによるデバッグ

1. ソリューション エクスプローラーで`Compilers\CompilerPackage`を右クリックして
   [スタートアップ プロジェクトに設定]を選択します。
2. [デバッグ]-[デバッグ開始]を選択します
   (あるいはショートカットキー`F5`を押します)。

これで変更済みのコードをデバッグすることが出来るはずです。
なおコンパイラーのすべての機能がVisual Studioのプロセス内で
実行されるわけではないため、すべてのブレークポイントにヒットするとは限らない
ことに注意してください。
Visual StudioはビルドしたバイナリのAPIを多数呼び出して機能を実現しようとしますが、
対象のVisual Studio内でビルドを実行すると新しいVBCSCompiler.exeのインスタンスが
起動されます。

## ユニットテストの実行

ユニットテストは以下の手順で実行できます：

1. Visual Studioでソリューションを閉じます。(ファイルのロックを避けるためです)
2. 開発者用コマンドプロンプトを起動します。
   (既にPrepareスクリプトを実行してある場合には管理者権限は不要です)
3. 複製したルートディレクトリに移動します。
4. `msbuild /m BuildAndTest.proj`を実行します。

このコマンドではまず最初にすべてのソースコードがビルドされて、
次に
[xUnit 2.0 runners NuGet Package](https://www.nuget.org/packages/xunit.runners/2.0.0-alpha-build2576)
にあるmsbuildランナーを使用してすべてのユニットテストが実行されます。
結果は`<clone dir>\UnitTestResults.html`という名前のファイルに出力されます。
まだ修正されていないバグに対するユニットテストを追加しておいてスキップするという
ポリシーを採用しているため、いくつかの警告が表示されるのは意図的なものです。

### ユニットテストの失敗をデバッグする

ユニットテストプロジェクトは先のパッケージに同梱されている
`xunit.console.x86.exe`を使用してデバッグすることが出来ます：

1. デバッグしたいテストを含むユニットテストプロジェクトのプロパティを開きます。
2. [デバッグ]タブを選択します。
3. [開始動作]を[外部プログラムの開始]に変更します。
4. プログラムのパスを
   `<clone directory>\Src\packages\xunit.runners.2.0.0-alpha-build2576\tools\xunit.console.x86.exe`
   に設定します。
5. [コマンドライン引数]のテキストボックスに
   ユニットテストアセンブリの名前を入力します。
6. 実行したいテストの本体にブレークポイントを設定します。
7. (F5キーで)デバッグを開始します。

## 貢献方法

コードの変更に関する貢献方法の詳細については
[貢献方法について](how_to_contribute.md)を参照してください。

## アンインストール

### "Roslyn"試験用Visual Studioハイヴの削除および厳密名の検証の復帰

管理者として実行している開発者コマンド プロンプト for VS2013で
次のコマンドを実行します：
`rc\Tools\Microsoft.CodeAnalysis.Toolset.Open\Scripts\Prepare.bat u`

### コードの削除

1. タスクマネージャを起動して、すべての「VBCSCompiler.exe」プロセスを終了させます。
2. ローカルにgit cloneされたディレクトリを削除します。

### End User Previewのアンインストール(省略可)

End User Previewを使用し続けて、新しい言語およびIDEの機能に対するフィードバッグを
是非行って欲しいところですが、アンインストールする場合には
以下の手順を実行してください：

1. タスクマネージャを起動して、すべての「VBCSCompiler.exe」プロセスを終了させます。
2. Visual Studioを起動します。
3. [ツール]-[拡張機能と更新プログラム]を開きます。
4. 「Roslyn Preview」を選択して[アンインストール]をクリックします。
