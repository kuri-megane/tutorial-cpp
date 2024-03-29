# コンパイルとリンク

## コマンドによるビルド

C/C++で複数ソースからプログラムをビルドするとき、次のように作業する

1. オブジェクトファイル(.o)の生成

```sh
# src1.oを生成
g++ src1.cpp -c
# src2.oを生成
g++ src2.cpp -c
```

2. 生成したオブジェクトファイルのリンク

```sh
# src1.o, src2.o から実行ファイルprogram を生成
g++ src1.o src2.o -o program
```

ソースが多くなると次の問題が出てくる

- コマンド実行が面倒
- コンパイル時間が増大

    とくにこれが問題。いちいちすべてコンパイル、リンクし直すのが無駄

## ビルド自動化ツール

上記の問題を解消するようなビルド自動化するツールを使う

- GNU Make
- NMake (Windows?)
- Ninja? (Visual Studio?)

いいこと

- コンパイル、リンク作業の自動化

    `make`コマンドなどで一発

- 差分だけビルドする

    ファイルのタイムスタンプ確認して、更新されたファイルだけコンパイルし直してくれる

しかし、それぞれ別のツールで設定ファイルの書き方が違う

## CMake

いちいちビルドツール別に設定ファイルを用意するのが面倒なので、それを自動生成するツールがCMake

CMakeList.txtに設定書けば、各ビルドツールに応じた設定ファイルを生成してくれる

それを使って`make`すればビルドできる

- 完 -

```
g++ test.cpp -c -o test.o -I ../include
g++ HelloWorld.cpp -c -o HelloWorld.o -I ../include
g++ HelloWorld.o test.o -o HelloWorld
```