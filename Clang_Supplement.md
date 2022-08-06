








## 定数
`#define`はマクロ置換



`#define indentifer`

- [C言語のdefineについて](http://www.c-lang.org/define.html)


## 型修飾子
- const
- restrict
- volatile

### const
`const int a = 0;`は定数で、`a = 1;` とかするとコンパイルエラー


### volatile
- プログラムのコードで変数の値を変更しなくとも勝手に値が変わる
- 変数の値を変えようとすると、値が変わる以外の動作をする可能性がある
- 主に組み込みプログラミングで使われる
- 値がどうなるかコンパイラは知らない（がプログラマは知っている必要がある）


なぜそんなものが必要か？
- 組み込みプログラミングにはある特殊な変数があり、その変数はプログラムが動いているCPUとは別のデバイスの状態を表していて、そのデバイスの状態が変わるとその変数の値が変わる
- 普通の変数は変更しなければ変わらないので、その変数を用いている無駄な処理は除いて最適化する（例えば、その変数を条件式とした`if`文が下にあったとして、コンパイラはその`if`分を削除する）
- `volatile`で型修飾子した変数は変わりうるので、コンパイラはその変数を用いた（一見無駄な）処理は最適化されない




