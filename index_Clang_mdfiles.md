# 私にはC言語がわからない

- [苦C](./kuruC.md)

- [ビルドの仕組みとライブラリ](./about_Build_Library_inClang.md)
- [スコープと生存期間](./Scorp_and_Lifetime_inClang.md)
- [ファイル](./Clang_file.md)
- [ポインタ](./Clang_Pointer.md)




## 用語集


### 宣言と定義の違い
宣言（declaration）
: コンパイラが参照を解消するために必要な構成要素

定義（defintion）
: リンカが参照をリンクさせるのに必要な構文要素<br>
    つまり

要補足

#### 参考
- [宣言と定義の違い](https://ja.stackoverflow.com/questions/12941/宣言と定義の明確な違いはなんですか)


### メインルーチン・サブルーチン
- サブルーチン：再利用目的の関数
- メインルーチン：そのプログラムを開始するための関数



### オブジェクト （not オブジェクト指向）

オブジェクト
: - メモリ上で **値を表現** and **型を持つ** and **寿命がある** もの
  - メモリ上にある ＝ ポインタによって存在を表せる
  - 名前の有無は問題ではないので、オブジェクト＝変数ではない

変数
: オブジェクトに識別子をつけたもの<br>
  変数を定義すると、メモリ上にオブジェクトが作られ、以降、識別子を用いてそのオブジェクトを参照する

#### オブジェクトの寿命

記憶域期間
- 自動記憶域期間
- 静的記憶域期間
- 動的記憶域期間
- 



#### 　おまけ
##### アラインメント
アラインメント
: ある型のオブジェクトが配置されるメモリアドレスに制約をかける整数値


- オブジェクトはメモリアドレスがその型のアラインメントの倍数になるように配置される
- 各型に設定されているアラインメントの値は処理系定義
- 構造体では各メンバの型のアラインメントを保つためにメンバ間、構造体の末尾にパディングが追加される


パディング：
: それ自体が意味を持たないデータ、もしくはそうしたデータを追加する処理

###### アラインメントとバディングの例
以下のような構造体`S`を宣言する
```
struct S {
    long long a;
    char b;
    short c;
}
```
この`S`について、
- long long のアラインメントが 8
- char のアラインメントが 1
- short のアラインメントが 2
- `S` のアラインメントが8

の時、
1. `S`型の変数`s`を定義すると、`S`のアラインメントは8なので、8の倍数のアドレスのメモリに配置される（例えば1000）
2. データメンバ`a`はlong long型で、`S`型と同じくアラインメントが8なので問題は生じない<br>（構造体変数のメモリアドレスと先頭のデータメンバのメモリアドレスは同じものを指すため）
3. データメンバ`b`はchar型でアラインメントが1なので、どこに配置してもOK<br>
    - `s`と`a`のアドレスは1000
    - そこから8アドレス分格納されるので末端のアドレスは1007
    - `b`はその続きから配置されるので、アドレスは10008
3. データメンバ`c`はshort型でアラインメントが2
    - `b`の続きに配置されるならアドレスは1009となる
    - しかしアラインメントが2 = 2の倍数のアドレスのメモリに格納される必要があるので、`c`はアドレス1009のメモリには配置できない
    - よって1バイト分のパディングを挟み、アドレスが1010のメモリに配置する

よって構造体Sを定義した場合、1000~1011の範囲のメモリを占有する

###### 注意

配列は


#### 参考
- [メモリとオブジェクト](https://programming-place.net/ppp/contents/cpp2/main/memory.html)



## tmp
Local

教育訓練給付制度ってなに？返済義務なしの超お得な制度とは？ | manabi &
https://manabi-and.com/archives/59

NULL | Programming Place Plus　Ｃ言語編　標準ライブラリのリファレンス
https://programming-place.net/ppp/contents/c/appendix/reference/NULL.html

分割の定石 - 苦しんで覚えるC言語
https://9cguide.appspot.com/20-02.html

配列と構造体の動的確保 - 東京大学工学部 精密工学科 プログラミング応用 I・II
http://www.den.t.u-tokyo.ac.jp/ad_prog/struct/

【C言語】realloc関数｜正しい使い方と注意点 メモリ断片化など | MaryCore
https://marycore.jp/prog/c-lang/realloc/

C言語のdefineについて
http://www.c-lang.org/define.html

C言語のプリプロセッサにおけるマクロと演算子の一覧
https://segakuin.com/c/preprocessor.html

C/C++のビルドの仕組みとライブラリ - かみのメモ
https://kamino.hatenablog.com/entry/c%2B%2B-principle-of-build-library

一週間で身につくC言語の基本|第７日目：複雑なファイル分割
https://c-lang.sevendays-study.com/ex-day7.html

一週間で身につくC言語の基本|第３日目：ポインタと配列
https://c-lang.sevendays-study.com/ex-day3_pointer_pointer.html

C言語のexternの悪魔的で危ない誘惑【＊ご利用は自己責任で】 - なるぽのブログ
https://yu-nix.com/archives/c-extern/

C初心者が知っておきたいヘッダーファイルとリンクの基礎知識：目指せ！ Cプログラマ（終）（2/4 ページ） - ＠IT
https://atmarkit.itmedia.co.jp/ait/articles/1404/11/news045_2.html

識別子 - Wikipedia
https://ja.wikipedia.org/wiki/%E8%AD%98%E5%88%A5%E5%AD%90

外部リンケージ | Microsoft Docs
https://docs.microsoft.com/ja-jp/cpp/c-language/external-linkage?view=msvc-170

Cにおける識別子の有効範囲と変数の生存期間：目指せ！ Cプログラマ（9）（1/2 ページ） - ＠IT
https://atmarkit.itmedia.co.jp/ait/articles/1104/26/news107.html

関数プロトタイプ - Wikipedia
https://ja.wikipedia.org/wiki/%E9%96%A2%E6%95%B0%E3%83%97%E3%83%AD%E3%83%88%E3%82%BF%E3%82%A4%E3%83%97

メモリとオブジェクト | Programming Place Plus　新C++編
https://programming-place.net/ppp/contents/cpp2/main/memory.html#alignment

トップページ | Programming Place Plus　Ｃ言語編
https://programming-place.net/ppp/contents/c/index.html#language

値型と参照型
http://wisdom.sakura.ne.jp/programming/cs/cs20.html

落穂拾い:スタティックリンクとダイナミックリンク
http://www.cc.kyoto-su.ac.jp/~kbys/kiso/cpu/dynamic-link.html

リンカ
https://tanakamura.github.io/pllp/docs/linker.html

コンパイラの構造を解説 | Shinta's Site
https://www.gadgety.net/shin/tips/unix/compiler.html

そもそもコンパイラの中ってどうなっているの？：Javaでコンパイラの基礎を理解する（1）（2/2 ページ） - ＠IT
https://atmarkit.itmedia.co.jp/ait/articles/0612/02/news016_2.html

[雑記] 識別子のスコープとオブジェクトの寿命 - C# によるプログラミング入門 | ++C++; // 未確認飛行 C
https://ufcpp.net/study/csharp/start/st_scope/?p=2

データ・オブジェクトの概要 - IBM Documentation
https://www.ibm.com/docs/ja/zos/2.3.0?topic=odod-overview-data-objects

ポインタ⑤（動的メモリ割り当て） | Programming Place Plus　Ｃ言語編　第３５章
https://programming-place.net/ppp/contents/c/035.html#allocated_storage_duration

