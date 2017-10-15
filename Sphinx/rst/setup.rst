==========================================
セットアップ方法
==========================================

PlartformIOはコマンドでインストールしていきます。Windows,Mac,LinuxどのOSにも対応しております。

大まかなステップ

・Python 環境を整える(2.7専用)

・pipを使ってPlatformIO環境をインストール

・コマンドの確認

以上

▼　Windowsの場合
--------------------------------------------------


・Python 2.7をインストール(3.xでは動きません涙)

https://www.python.org/downloads/release/python-2714/

この辺で、32bitの方は「Windows x86 MSI installer」 64bitの方は「Windows x86-64 MSI installer 」を。

全てOKで進めて行けば、今だとPATHまで自動で入ると思われるので、再起動後にコマンドプロントで「python -V」を入力します。

無事にコマンドが認識すればOK。

続いて pipコマンドを入れます。

・pipコマンドをインストール

https://bootstrap.pypa.io/get-pip.py 

より、ソースをダウンロードして、コマンドよりcdやdirを駆使して 「python get-pip.py」 を実行します。

無事に完了すると、コマンド pip が使用できるように成ります。

・pipを使ってPlatformIOをインストールする。

コマンドで「pip install platformio」で全自動でGCCやらヘッダーファイルやら何やら全部インストールが出来ます。

・インストールが終わったら、PlatformIO用のコマンドが動くか確認

PlatformIOのコマンドは２種類あり、

> platformio

と、

> pio

の２種類です。どちらも同じ動きをしますが、記述が面倒なので「pio」を主力として記述していきます。

もし、大きな力でpioが他のコマンドとかぶる際は、仕方がなくplatformioと全部書くようにしましょう。

以上でPlatformIOが使えるようになったと思います！（多分）


▼　Macの場合
--------------------------------------------------


