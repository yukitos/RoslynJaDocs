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
多くのテストは既にUpdate 2 RCの環境で実行されていることもあり、
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

> 注意：`master`とreleases/build-preview`ではAPIが異なります。
  `master`をビルドした場合、変更をVisual Studio上で
  テストできなくなることに注意してください。

## Roslynバイナリに対する厳密名の検証を無効化して、
   Roslynの試験用VSハイヴの準備をする

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

1. 管理者権限で開発者コマンド プロンプト for VS2013を起動します。
  1. Windows 8.1の場合、スタートページを表示して`Visual Studio ツール`と入力します。
  2. 検索結果で表示されたフォルダを開きます。
  3. `開発者コマンド プロンプト for VS2013`を右クリックして
     [管理者として実行]を選択します。
2. 複製を作成したディレクトリに移動します。
   たとえば`cd /d C:\Code\Roslyn`のようにします。
   以下の手順ではこのディレクトリを<clone dir>として参照します。
3. スクリプトを実行します：
   `Src\Tools\Microsoft.CodeAnalysis.Toolset.Open\Scripts\Prepare.bat`

> 注意：Roslyn試験用VSハイヴを削除して厳密名の検証を復元したい場合には
  `**u**`を指定してこのコマンド実行します。

## NuGetパッケージのダウンロード


