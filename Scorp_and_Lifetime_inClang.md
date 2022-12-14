
# 変数のスコープと記憶域期間

**変数 = オブジェクトに識別子をつけたもの**
- 識別子はソースコードのコンパイルまでに使われる静的なもの
- オブジェクトはプログラムの実行時に作られる動的なもの
- なので識別子の有効期間とオブジェクトの記憶域期間は別に考える必要がある


## スコープ:識別子の有効期間
- ブロックスコープ
- ファイルスコープ
- プロトタイプスコープ

ブロックスコープ
: - 宣言された位置からブロックの終了まで有効
  - 関数の定義の際の仮引数もこのスコープを持つ

ファイルスコープ
: - 宣言された位置からソースファイルの終了まで有効
  - 関数の外で宣言された識別子がこのスコープを持つ
  - ファイルスコープをもつ変数を一般にグローバル変数と呼ぶ<br>
    ↑ なんか違うかも？？？要訂正

プロトタイプスコープ
: 関数の宣言の際に記述する仮引数のスコープ（宣言の中に限定される）


- 同じスコープをもつ同じ名前の識別子の宣言はできない
- スコープが異なる場合は同じ名前の識別子の宣言ができ、スコープが重なった場合、内側のスコープを持つ識別子のみが参照できる



## 記憶域期間：オブジェクトの有効期間

記憶領域期間(生存期間)
: - オブジェクトがメモリ上に存在することが保証され、最後に記録した値が維持される期間 ＝ オブジェクトのメモリアドレスが有効である期間
  - そのオブジェクトのためのメモリ領域が確保されたときから始まり、そのメモリ領域を使わなくなったときに終了する

### 記憶領域期間の種類
- 自動記憶域期間
- 静的記憶域期間
- 動的（割り付け）記憶域期間

||自動記憶域領域|静的記憶域領域|動的記憶域領域|
|:---:|:---:|:----:|:----:|
|開始|オブジェクト定義時|プログラム実行開始時||
|終了|定義したブロックの終了時|プログラム終了時||
|配置されるメモリ域|スタック領域|静的領域<br>グローバル領域|ヒープ領域|

#### 自動記憶域期間

- 以下のように構築されたオブジェクト
  - ブロックスコープを持ち、`static`や`extern`キーワードが付加されていない変数
  - 仮引数
- オブジェクトが定義されたときに始まり、変数の定義を行ったブロックの終わりで終了する
- 関数に入るたびに作り直され、以前の値は引き継がれない
- `auto`を使用して宣言される（例：`auto int a = 0;`）
- とか言いつつも`auto`は省略可能（つまり普通に使ってる変数は自動記憶域期間を持つ）
- 生成しても自動的には初期化されない



#### 静的記憶域期間

- 以下のいずれかで構築されたオブジェクト
  - `static`キーワードを付加して定義した変数
  - 関数の外で定義した関数
- プログラムの実行開始直後に始まり、プログラムの実行が終わったときに終了する
- 静的変数（静的記憶領域を持つ変数）はプログラムの実行開始直後（`main`関数が始まるより前）にオブジェクトが構築される
- 生成時点で自動的に初期化される（初期値を与えればその値、そうでなければ型のデフォルトの値で初期化される）
- それぞれの方法で構築したオブジェクトの変数は、識別子のスコープは異なるが、生存期間も初期化されるタイミングも同じ
よって、
  ```
  void func(void) {
      static int b = 0;
      b++;
      printf("b = %d\n",b);
  }
  ```
  は、`func()`を呼び出すたびに`b`は(初期化されずに）+1 されていき、<br>呼び出すたびに1, 2, 3, ... を返す


#### 動的記憶域期間
- 任意のタイミングでメモリ上に置かれ、任意のタイミングで削除できるオブジェクト
- 


あとでかきまうす〜〜〜〜


### 参照
- [識別子のスコープとオブジェクトの寿命](https://ufcpp.net/study/csharp/start/st_scope/)
- [スコープと記憶域期間](https://programming-place.net/ppp/contents/c/022.html)