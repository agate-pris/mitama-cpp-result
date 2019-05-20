# mitama::Result 101

正常値と異常値のどちらかの状態を取りうるエラーハンドリング専用の直和型.

## Motivation

C++の持つエラーハンドリングの機能にはいくつかの問題がある.

手軽に正常値と異常値を両方扱える型が必要である.

問題点を確認するため、各言語のエラーハンドリングの典型的なパターンを見てみる.


### 言語ごとのエラーハンドリングと最近の動向

言語ごとのよく見られるエラーの扱いかた。
主に標準ライブラリなどのエラーの扱いを調べている。


| Lang    | 例外    | 多値返却 | Null許容型 | 代数的データ型 | パターンマッチ |
| ------- | ------- | -------- | ---------- | -------------- | -------------- |
| C++     | Yes     | Yes      | Yes        | No             | No             |
| Java    | Yes     | No       | Yes        | No             | No             |
| Go      | No      | Yes      | Yes        | No             | Partial        |
| Rust    | Partial | No       | Yes        | Yes            | Yes            |
| Haskell | Yes     | No       | Yes        | Yes            | Yes            |
| Scala   | Yes     | Yes      | Yes        | Yes            | Yes            |

最近の言語になると、代数的データ型とパターンマッチによるハンドリングができるものが多い。



### 伝統的なアプローチ

伝統的なC言語のアプローチではエラー値を戻り値とし、
返り値を引数として書き換える.

（C言語にはboolがないのでint型を返すことが多いが、C++にはboolがある.
また、C言語に参照はないがC++には参照がある.）


```cpp
bool f(int &a/* return value */){
  /// implementation
  if(...)
    return false; // error
  else
    return true;
}

int a;
if(!f(a)) {
  // error handling ...
}

```

この方法は戻り値を受け取るため予め変数を用意しなければならず、
また副作用により変数を書き換えるためコードの見通しが悪くなる.

### 例外というアプローチ

C++には例外という機能がある.

```cpp
int f(){
  /// implementation
  if(...)
    throw std::runtime_error("error");
  else
    return 42;
}

try {
  int v = f();
}
catch (std::runtime_error const& e) {
  // error handling ...
}

```

例外の問題は、例外テーブルによりランタイムにオーバーヘッドが大きいことがある.

例外はキャッチに失敗するとterminate()を呼びプログラムを終了させる.

プログラムの進行が不可能なエラーを扱うには最適であるが、
ちょっとした計算の失敗やファイルの読み込みの失敗などの
巻き戻しが可能なエラーを扱うにはオーバーヘッドが少々気になる.

これと同様のアプローチは多くの言語が採用している。
特にオブジェクト指向言語。

C++、Java、C#、Pythonなどは例外を主なエラーハンドリング機能として備えている。


### 多値返却というアプローチ

Goは例外を備えていない。

Goは関数が複数の戻り値を返すことができるため、2つめの戻り値でerror型を返すようになっている.


```go
func f(first string, family string) (string, error) {
    if (first == "") || (family == "" ) {
        return nil, errors.New("error: empty name")
    }
    return strings.ToUpper(first) + strings.toLower(family)), nil
}

if name, err := f("", "Joi"); err {
  /// error handling
}

```

C++17では同じようなことができる.


```cpp
auto f(int a){
  using std::literals::string_literals;
  if(a < 0)
    return std::tuple{ 0, false };
  else
    return std::tuple{ 1, true };
}

if (auto [value, err] = f(); !err) {
  // error handling ...
}
else {
  // ok
  // ...
}
```

tuple likeな機能を有している言語でこのアプローチを採用することができる。

しかし、この方法はエラー値を無視して捨てることができるので、これ一本でエラーハンドリングを行うのはいいアイデアとは言えないだろう.

実際、Go2のドラフトで修正案が出ている.

C++の標準ライブラリも例外を使うまでもないという場合において、このアプローチを用いる。
例えば、mapのemplaceは挿入位置のイテレータと挿入に成功したかを表すbool値のpairを返り値としている。



### 無効値を表す特別な型（Null許容型）というアプローチ

Nullという状態を許容し、エラーを表すという方法。

非Null許容型とNull許容型を区別できる機能や、Optionalによる。

C#、Kotlin、SwiftなどはNull許容型を使う。
C++、Java、RustなどはOptionalを使う。

HaskellはMaybeを使う。
Haskellはこの後の代数的データ型で解説する。

このアプローチの良いところは、成功と失敗を一つの変数（型）で表すことができるということだ。

このアプローチの欠点はエラーということしかわからず、エラー原因が全くわからずデバッグが困難ということである。

### 代数的データ型というアプローチ

C++のbool型で成功と失敗を表したとき、int型がboolに変換できてしまう。

エラーと関係ないint値を返却してもboolに変換されてコンパイルが通ってしまい、おかしな動きをするという事故を起こす可能性がある。

Haskellでは`Bool`は**代数的データ型**である。

```haskell
data Bool = True | False
```


BoolはTrueかFalse以外の値を取り得ない。

代数的データ型は事故を型レベルで防ぐ。

Haskellにおける無効値を表すMaybeも代数的データ型である。

```haskell
data Maybe a = Nothing | Just a
```


多くの言語でenum（列挙型）と呼ばれる機能でなんだかんだ頑張れば実現可能。


ところで、Rustではenumは代数的データ型である.


```rust

enum V {
   A,
   B,
}

```

のようにするとVは、AかBの型を取りうる代数的データ型型になる.


Resultの定義を見てみよう.

```rust

enum Result<T, E> {
   Ok(T),
   Err(E),
}

```

これはジェネリクスであり、`Ok(T)`, `Err(E)`はコンストラクタである.

`Result<T, E>`は`Ok(T)`か`Err(E)`のどちらかの状態を持つ.

Resultを受け取り値を取り出すには`unwrap`を呼び出す必要がある.

Errの状態のResultでunwrapを呼び出すとpanic（例外のようなもの）になる。

異常値と正常値を統合的に扱えている.
値を取り出して使うしかないため、エラー状態を無視してエラー値を捨てることはできない.

実行時オーバーヘッドは少なく、プログラムの巻き戻しやエラーメッセージの運搬に気軽に使うことができる.

`map`, `map_err`, `and_then`, `or_else`などの便利な関数群もある.

正常値を持つ状態と異常値を持つ状態をシームレスに扱える、かつエラーメッセージも運搬できる。

このアプローチをC++でも採用したい.


## Result<T, E> for C++

実用に耐えるように2つの型の直和型としての機能を実装した.

`std::variant`では`Result<int, int>`のような同じ型に正常・異常という2つの意味をもたせるためには型を`

```cpp
std::variant<Ok<int>, Err<int>>
```

のようにラップする必要がある.
Resultの内部実装はこのようになっており、ヘルパー型として`Ok<T>`と`Err<E>`というクラステンプレートを用いる.

## Basic Usage

単純なif文を置き換えるような使い方が考えられる.

Resultの良いところは、
どの時点でエラーになったかをメッセージ含めることができることである.

これにより、バグの追跡が容易になるし、エラーメッセージも親切になる.

```cpp
  auto even = [](uint32_t u) -> Result<uint32_t, std::string> {
    if (u % 2 == 0)
      return Ok(u); // implicit convert to Result<uint32_t, std::string>
    else
      return Err("odd"s); // implicit convert to Result<uint32_t, std::string>
  };

  auto func = [](auto u) -> Result<uint32_t, std::string> {
    if(u%3==0) return Ok(1u); // implicit convert to Result<uint32_t, std::string>
  else
    return Err("error"s); // implicit convert to Result<uint32_t, std::string>
  };


  auto res = even(2)
      .and_then(func) // if even(2) is ok, and then call func ( returns Err );

  if (res.is_err()) {
    std::string mesasge = res.unwrap_err(); // get error message
  }
  uint32_t value = res.unwrap(); // get result value

  // ...
```