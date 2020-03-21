---
title: Visual C++ 2003 ～ 2015 の新機能
ms.date: 07/02/2019
ms.assetid: c4afde6f-3d75-40bf-986f-be57e3818e26
ms.openlocfilehash: 6a3db2c9af2bcd9201f696756053cedb0788571a
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69510300"
---
# <a name="visual-c-what39s-new-2003-through-2015"></a>Visual C++ 2003 ～ 2015 の新機能

このページは、Visual Studio 2003 から 2015 までのすべてのバージョンの Visual C++ の "新機能" をまとめたものです。 この情報は、以前のバージョンの Visual Studio からアップグレードする場合に有用な情報として提供されます。

> [!NOTE]
> 現行版の Visual Studio の詳細については、「[What's new for Visual C++ in Visual Studio](../overview/what-s-new-for-visual-cpp-in-visual-studio.md)」(Visual Studio の Visual C++ の新機能)、「[Conformance Improvements in Visual C++ in Visual Studio](../overview/cpp-conformance-improvements.md)」(Visual Studio の C++ 準拠の強化) を参照してください。

## <a name="whats-new-for-c-in-visual-studio-2015"></a>Visual Studio 2015 の C++ の新機能

Visual Studio 2015 以降では、コンパイラの準拠に関する継続的な強化によって、コンパイラが既存のソース コードを認識する方法が変わる可能性があります。 このような場合、以前にビルドして問題なく実行できていたコードでも、ビルド時に新しいエラーや異なるエラーが発生したり、動作が変わったりする可能性があります。

幸いなことに、これらの変更はほとんどのソース コードにほとんど、またはまったく影響がありません。また、変更に対応するためにソース コードやその他の変更が必要な場合でも、通常は軽微で簡単な変更で済みます。 以前は問題がなかったソース コードで、変更が必要な *(修正前の)* コード例と、正しい *(修正後の)* コード例を多数紹介します。

これらの変更点はソース コードや他のビルド成果物に影響はあっても、Visual C++ の異なるバージョン間のバイナリの互換性には影響がありません。 より重大な変更で、*互換性に影響する変更*の場合、バイナリの互換性に影響が及ぶ可能性がありますが、このようなバイナリの互換性に影響する変更は、Visual C++ のメジャーバージョンが異なる場合にのみ発生します。 たとえば、Visual C++ 2013 と Visual C++ 2015 間などです。 Visual C++ 2013 と Visual C++ 2015 の間の互換性に影響する変更点については、「[Visual C++ 2003 ～ 2015 の変更履歴](../porting/visual-cpp-change-history-2003-2015.md)」を参照してください。

- [Visual Studio 2015 の準拠の強化](#VS_RTM)

- [Visual Studio 2015 Update 1 の準拠の強化](#VS_Update1)

- [Visual Studio 2015 Update 2 の準拠の強化](#VS_Update2)

- [Visual Studio 2015 Update 3 の準拠の強化](#VS_Update3)

### <a name="VS_RTM"></a> Visual Studio 2015 の準拠の強化

- **/Zc:forScope- オプション**

   コンパイラ オプション `/Zc:forScope-` は非推奨となりました。今後のリリースからは削除されます。

   ```output
    Command line warning  D9035: option 'Zc:forScope-' has been deprecated and will be removed in a future release
   ```

   このオプションは通常、標準ではスコープから外れるポイントの後のループ変数を使用する、非標準のコードを許可するために使用されていました。 これは `/Za` オプションを使ってコンパイルするときにのみ必要でした。`/Za` がない場合は、ループの後でも常に for ループ変数が使用できるからです。 標準への準拠を考慮しない場合 (たとえば、コードを他のコンパイラに移植しない場合)、`/Za` オプションをオフにする (または、 **[言語拡張機能の無効化]** プロパティを **[いいえ]** に設定する) こともできます。 移植可能で標準に準拠したコードの記述を考慮する場合、標準に準拠するようコードを再記述する必要があります。そのためには、変数の宣言をループの外側に移動します。

   ```cpp
    // zc_forScope.cpp
    // compile with: /Zc:forScope- /Za
    // C2065 expected
    int main() {
       // Uncomment the following line to resolve.
       // int i;
       for (int i =0; i < 1; i++)
          ;
       i = 20;   // i has already gone out of scope under /Za
    }
   ```

- **Zg コンパイラ オプション。**

   `/Zg` コンパイラ オプション (関数プロトタイプの生成) は使用できなくなりました。 前バージョンで、このコンパイラ オプションは非推奨とされました。

- mstest.exe のコマンド ラインから C++/CLI で単体テストを実行できなくなりました。 代わりに、vstest.console.exe を使います

- **mutable キーワード。**

   **mutable** ストレージ クラス指定子は、エラーなしで以前コンパイルされていた場所で使用できなくなりました。 現在、コンパイラによってエラー C2071 (無効なストレージ クラス) が出されます。 標準では、変更可能な指定子はクラスのデータ メンバーの名前にのみ適用でき、const または static として宣言された名前には適用できません。また、参照メンバーにも適用できません。

   次に例を示します。

   ```cpp
    struct S {
        mutable int &r;
    };
   ```

   以前のバージョンの Microsoft C++ コンパイラはこれを受け入れていましたが、現在のコンパイラでは次のエラーが示されます。

   ```Output
    error C2071: 'S::r': illegal storage class
   ```

   エラーを修正するには、冗長な **mutable** キーワードを削除するだけです。

- **char16_t と char32_t**

   `char16_t` または `char32_t` を typedef の別名として使用できなくなりました。これらの型は現在、組み込みとして扱われているからです。 ユーザーやライブラリ作成者は、`char16_t` および `char32_t` を `uint16_t` および `uint32_t` の別名として定義するのが一般的でした。

   ```cpp
    #include <cstdint>

    typedef uint16_t char16_t; //C2628
    typedef uint32_t char32_t; //C2628

    int main(int argc, char* argv[])
    {
    uint16_t x = 1; uint32_t y = 2;
    char16_t a = x;
    char32_t b = y;
    return 0;
    }
   ```

   コードを更新するには、**typedef** 宣言を削除してこれらの名前と競合するその他の ID の名前を変更します。

- **非型テンプレート パラメーター**

   非型テンプレート パラメーターを含む特定のコードは現在、明示的なテンプレート引数を指定すると、型の互換性について正しくチェックされます。 たとえば、次のコードは、以前のバージョンの Visual C++ でエラーなしでコンパイルしたものです。

   ```cpp
    struct S1
    {
        void f(int);
        void f(int, int);
    };

    struct S2
    {
        template <class C, void (C::*Function)(int) const> void f() {}
    };

    void f()
    {
        S2 s2;
        s2.f<S1, &S1::f>();
    }
   ```

   現在のコンパイラは、正しくエラーを出します。テンプレート パラメーターの型がテンプレートの引数と一致しないからです (パラメーターは const メンバーへのポインターですが、関数 f は非 const です)。

   ```Output
    error C2893: Failed to specialize function template 'void S2::f(void)'note: With the following template arguments:note: 'C=S1'note: 'Function=S1::f'
   ```

   コードのこのエラーに対処するには、使用するテンプレート引数の型が、テンプレート パラメーターの宣言された型と一致することを確認してください。

- **__declspec(align)**

   コンパイラは関数で `__declspec(align)` を受け入れなくなりました。 これは常に無視されていましたが、コンパイラ エラーを生成するようになりました。

   ```cpp
    error C3323: 'alignas' and '__declspec(align)' are not allowed on function declarations
   ```

   この問題を修正するには、関数の宣言から `__declspec(align)` を削除してください。 これは影響がなかったため、削除しても何も変わりません。

- **例外処理**

   例外処理への変更がいくつかあります。 まず、例外オブジェクトはコピー可能または移動可能にする必要があります。 次のコードは、Visual Studio 2013 ではコンパイルされますが、Visual Studio 2015 ではコンパイルされません。

   ```cpp
    struct S {
    public:
        S();
    private:
        S(const S &);
    };

    int main()
    {
        throw S(); // error
    }
   ```

   問題は、コピー コンストラクターはプライベートであるために通常の例外処理とは異なりオブジェクトをコピーできないことです。 コピー コンストラクターが **explicit** として宣言されている場合も同じことが当てはまります。

   ```cpp
    struct S {
        S();
        explicit S(const S &);
    };

    int main()
    {
        throw S(); // error
    }
   ```

   コードを更新するには、例外オブジェクトのコピー コンストラクターがパブリックであり、**explicit** とマークされていないことを確認します。

   値によって例外をキャッチする場合も、例外オブジェクトをコピー可能にする必要があります。 次のコードは、Visual Studio 2013 ではコンパイルされますが、Visual Studio 2015 ではコンパイルされません。

   ```cpp
    struct B {
    public:
        B();
    private:
        B(const B &);
    };

    struct D : public B {
    };

    int main()
    {
        try
        {
        }
        catch (D d) // error
        {
        }
    }
   ```

   この問題を解決するには、**catch** のパラメーターの型を参照に変更します。

   ```cpp
    catch(D& d)
    {
    }
   ```

- **マクロに続く文字列リテラル**

   このバージョンでは、コンパイラはユーザー定義リテラルをサポートするようになりました。 その結果、空白文字の介入がないマクロに続く文字列リテラルはユーザー定義のリテラルとして解釈されます。これにより、エラーまたは予期しない結果が起こる可能性があります。 たとえば、以前のコンパイラでは次のコードが正常にコンパイルされていました。

   ```cpp
    #define _x "there"
    char* func() {
        return "hello"_x;
    }
    int main()
    {
        char * p = func();
        return 0;
    }
   ```

   コンパイラはこれを、マクロに続く "hello" というリテラル文字列として解釈していました。これは "there" に拡張され、2 つの文字列リテラルが 1 つに連結されていました。 Visual Studio 2015 では、コンパイラはこれをユーザー定義リテラルと解釈しますが、一致するユーザー定義リテラル _x が定義されていないため、エラーになります。

   ```cpp
    error C3688: invalid literal suffix '_x'; literal operator or literal operator template 'operator ""_x' not found
    note: Did you forget a space between the string literal and the prefix of the following string literal?

   ```

   この問題を解決するには、文字列リテラルとマクロの間に空白に追加します。

- **隣接する文字列リテラル**

   以前と同様、文字列の解析に関連する変更のため、空白なしの隣接する文字列リテラル (ワイド文字列リテラルまたはナロー文字列リテラルのいずれか) は、以前のバージョンの Visual C++ では、単一の連結文字列と解釈されていました。 Visual Studio 2015 では、2 つの文字列間に空白を追加する必要があります。 たとえば、次のコードを変更する必要があります。

   ```cpp
    char * str = "abc""def";
   ```

   単に 2 つの文字列間に空白を追加します。

   ```cpp
    char * str = "abc" "def";
   ```

- **placement new と delete**

   C++14 標準に準拠させるために **delete** 演算子に対して変更が加えられました。 標準の変更について詳しくは、「 [C++ サイズの割り当て解除](https://isocpp.org/files/papers/n3778.html)」をご覧ください。 変更により、size パラメーターを取るグローバルな **delete** 演算子のフォームが追加されます。 互換性に影響する変更は、(**placement new** 演算子と一致させるために) 以前同じシグネチャで **delete** 演算子を使用していた場合、コンパイラ エラーを受け取ります (これは C2956 というエラーで、**placement new** が使用されるポイントで発生します。それは、一致する適切な **delete** 演算子の識別をコンパイラが試行するコードの場所だからです)。

   関数 `void operator delete(void *, size_t)` は、C++11 の **placement new** 関数 `void * operator new(size_t, size_t)` に対応する **placement delete** 演算子でした。 現在、C++14 サイズの割り当て解除では、この **delete** 関数は "*通常の解放関数*" (グローバルな **delete** 演算子) です。 標準では、**placement new** の使用で対応する **delete** 関数を検索し、通常の解放関数を見つけた場合、プログラムの形式が不適切である必要があります。

   たとえば、コードで **placement new** と **placement delete** の両方を定義するとします。

   ```cpp
    void * operator new(std::size_t, std::size_t);
    void operator delete(void*, std::size_t) noexcept;
   ```

   この問題は、定義した **placement delete** 演算子と新しいグローバル サイズの **delete** 演算子の間の関数シグネチャの一致により発生します。 **placement new** 演算子および **delete** 演算子で `size_t` とは異なる型を使用できるかどうかを検討してください。  `size_t` **typedef** の型はコンパイラによって異なります。これは Visual C++ の **unsigned int** の **typedef** です。 適切なソリューションでは、次のように列挙型を使用します。

   ```cpp
    enum class my_type : size_t {};
   ```

   次に、placement **new** と **delete** の定義を変更し、`size_t` の代わりにこの型を 2 番目の引数として使用します。 **placement new** の呼び出しを更新して新しい型を渡したり (たとえば、`static_cast<my_type>` を使用することにより整数値から変換する)、**new** と **delete** の定義を更新して整数型にキャスト バックしたりする必要もあります。 これに対して **enum** を使用する必要はありません。`size_t` メンバーを持つクラス型も機能します。

   代わりの方法として、**placement new** を完全に除去することもできます。 コードで **placement new** を使用してメモリ プールを実装する場合 (placement 引数が割り振られるまたは削除されるオブジェクトのサイズである)、独自のカスタム メモリ プール コードをサイズ割り当て解除機能で置き換えるほうが良い可能性があります。配置関数を削除でき、配置関数の代わりに独自の 2 つの引数 **delete** 演算子だけを使用することができます。

   コードを即時に更新しない場合は、コンパイラ オプション `/Zc:sizedDealloc-` を使用して、従来の動作に戻すことができます。 このオプションを使用すると、2 つの引数を持つ **delete** 関数が存在せず、**placement delete** 演算子との競合は発生しません。

- **共用体データ メンバー**

   共用体データ メンバーで参照型を使用することはできなくなりました。 次のコードは Visual Studio 2013 では正常にコンパイルされますが、Visual Studio 2015 ではエラーになります。

   ```cpp
    union U1 {
        const int i;
    };
    union U2 {
       int &i;
    };
    union U3 {
        struct {int &i;};
    };
   ```

   上のコードを実行すると、次のエラーが生成されます。

   ```Output
    test.cpp(67): error C2625: 'U2::i': illegal union member; type 'int &' is reference type
    test.cpp(70): error C2625: 'U3::i': illegal union member; type 'int &' is reference type
   ```

   この問題に対処するには、参照型をポインターか値に変更します。 ポインターに型を変更する場合、共用体フィールドを使用するコードでの変更が必要です。 コードを値に変更すると、共用体に格納されているデータが変更されます。これは、他のフィールドに影響を与えます。共用体型のフィールドは同じメモリを共有するからです。 値のサイズによっては、共用体のサイズも変更される場合があります。

- **匿名共用体**

   の標準への適合が改善されました。 以前のバージョンのコンパイラでは、匿名共用体に対して明示的なコンストラクターとデストラクターが生成されていました。 これらは Visual Studio 2015 で削除されています。

   ```cpp
   struct S {
      S();
   };

   union {
      struct {
         S s;
      };
   } u; // C2280
   ```

   上のコードを実行すると、Visual Studio 2015 で次のエラーが生成されます。

   ```cpp
    error C2280: '<unnamed-type-u>::<unnamed-type-u>(void)': attempting to reference a deleted function
    note: compiler has generated '<unnamed-type-u>::<unnamed-type-u>' here
   ```

   この問題を解決するには、コンストラクターおよび/またはデストラクターの独自の定義を提供してください。

   ```cpp
    struct S {
       // Provide a default constructor by adding an empty function body.
       S() {}
    };

    union {
       struct {
          S s;
       };
    } u;
   ```

- **匿名構造体を持つ共用体**

   標準と準拠させるために、共用体の匿名構造体メンバーのランタイムの動作が変更されました。 共用体の匿名構造体のメンバーのコンストラクターは、そのような共用体の作成時に暗黙的に呼び出されなくなりました。 また、共用体の匿名構造体のメンバーのデストラクターも、共用体がスコープから外れたときに暗黙的に呼び出されなくなりました。 次のコードを検討します。共用体 U に匿名構造体が含まれています。この匿名構造体には、名前付き構造体 S のメンバーが含まれており、その構造体にはデストラクターが含まれています。

   ```cpp
    #include <stdio.h>
    struct S {
        S() { printf("Creating S\n"); }
        ~S(){ printf("Destroying S\n"); }
    };
    union U {
        struct {
        S s;
    };
        U() {}
        ~U(){}
    };

    void f()
    {
        U u;
        // Destructor implicitly called here.
    }

    int main()
    {
        f();

        char s[1024];
        printf("Press any key.\n");
        gets_s(s);
        return 0;
    }
   ```

   Visual Studio 2013 では、S のコンストラクターは共用体の作成時に呼び出され、S のデストラクターは関数 f のスタックがクリーンアップされるときに呼び出されます。 しかし、Visual Studio 2015 では、コンストラクターとデストラクターは呼び出されません。 コンパイラによって、この動作の変更に関する警告が出されます。

   ```Output
    warning C4587: 'U::s': behavior change: constructor is no longer implicitly calledwarning C4588: 'U::s': behavior change: destructor is no longer implicitly called
   ```

   元の動作を復元するには、匿名構造体に名前を付けます。 非匿名構造体の実行時の動作は、コンパイラのバージョンに関係なく、同じです。

   ```cpp
    #include <stdio.h>

    struct S {
        S() { printf("Creating S.\n"); }
        ~S() { printf("Destroying S\n"); }
    };
    union U {
        struct {
            S s;
        } namedStruct;
        U() {}
        ~U() {}
    };

    void f()
    {
        U u;
    }

    int main()
    {
        f();

        char s[1024];
        printf("Press any key.\n");
        gets_s(s);
        return 0;
    }
   ```

   別の方法として、新しい関数にコンストラクターとデストラクターのコードを移動し、共用体のコンストラクターおよびデストラクターからこれらの関数の呼び出しを追加します。

   ```cpp
    #include <stdio.h>

    struct S {
        void Create() { printf("Creating S.\n"); }
        void Destroy() { printf("Destroying S\n"); }
    };
    union U {
        struct {
            S s;
        };
        U() { s.Create();  }
        ~U() { s.Destroy(); }
    };

    void f()
    {
        U u;
    }

    int main()
    {
        f();

    char s[1024];
    printf("Press any key.\n");
    gets_s(s);
    return 0;
    }
   ```

- **テンプレートの解決**

   テンプレートの名前解決に変更が加えられています。 C++ では、名前解決の候補を検討する場合、一致の可能性として検討されている 1 つ以上の名前により、無効なテンプレート インスタンス化が生成される可能性があります。 これらの無効なインスタンス化は通常、それ自体はコンパイラ エラーの原因にはなりません。これは SFINAE (Substitution Failure Is Not An Error: 置き換えの失敗はエラーではない) と呼ばれます。

   SFINAE のコンパイラがクラス テンプレートの特殊化のインスタンス化を必要とする場合は、この処理中に発生したエラーはコンパイラ エラーです。 以前のバージョンでは、コンパイラはこのようなエラーを無視していました。 次に例を示します。

   ```cpp
    #include <type_traits>

    template<typename T>
    struct S
    {
    S() = default;
    S(const S&);
    S(S&&);

    template<typename U, typename = typename std::enable_if<std::is_base_of<T, U>::value>::type>
    S(S<U>&&);
    };

    struct D;

    void f1()
    {
    S<D> s1;
        S<D> s2(s1);
    }

    struct B
    {
    };

    struct D : public B
    {
    };

    void f2()
    {
    S<D> s1;
        S<D> s2(s1);
    }
   ```

   現在のコンパイラでコンパイルすると、次のエラーが表示されます。

   ```Output
    type_traits(1110): error C2139: 'D': an undefined class is not allowed as an argument to compiler intrinsic type trait '__is_base_of'
    ..\t331.cpp(14): note: see declaration of 'D'
    ..\t331.cpp(10): note: see reference to class template instantiation 'std::is_base_of<T,U>' being compiled
            with
            [
                T=D,
                U=D
            ]
   ```

   これは、is_base_of の最初の呼び出しの時点でクラス 'D' がまだ定義されていないためです。

   この場合の修正は、クラスが定義されるまでそのような型の特徴を使用しないことです。 B と D の定義をコード ファイルの先頭に移動すると、エラーが解決されます。 定義がヘッダー ファイルにある場合、ヘッダー ファイルの include ステートメントの順序を確認し、問題のあるテンプレートが使用される前にクラス定義がコンパイルされるようにしてください。

- **コピー コンストラクター**

   Visual Studio 2013 と Visual Studio 2015 の両方において、コンパイラは、クラスにユーザー定義の移動コンストラクターがあり、ユーザー定義のコピー コンストラクターはない場合に、そのクラスのコピー コンストラクターを生成します。 Dev14 では、この暗黙的に生成されたコピー コンストラクターは "= delete" とマークされています。

### <a name="VS_Update1"></a> Visual Studio 2015 Update 1 の準拠の強化

- **プライベートの仮想基底クラスと間接継承**

   以前のバージョンのコンパイラでは、派生クラスは*間接的に派生した*`private virtual`基底クラスのメンバー関数を呼び出すことができました。 この従来の動作は正しい動作ではなく、C++ 標準に準拠していません。 コンパイラはこの方法で記述されたコードを受け入れなくなりました。その結果、コンパイラ エラー C2280 を発行します。

   ```Output
    error C2280: 'void *S3::__delDtor(unsigned int)': attempting to reference a deleted function
   ```

   例 (変更前)

   ```cpp
    class base
    {
    protected:
        base();
        ~base();
    };

    class middle: private virtual base {};class top: public virtual middle {};

    void destroy(top *p)
    {
        delete p;  //
    }
   ```

   例 (変更後)

   ```cpp
    class base;  // as above

    class middle: protected virtual base {};
    class top: public virtual middle {};

    void destroy(top *p)
    {
        delete p;
    }
   ```

  \- または -

   ```cpp
    class base;  // as above

    class middle: private virtual base {};
    class top: public virtual middle, private virtual bottom {};

    void destroy(top *p)
    {
        delete p;
    }
   ```

- **オーバーロードされた operator new と operator delete**

   以前のバージョンのコンパイラでは、メンバー以外の **operator new** とメンバー以外の **operator delete** を static として宣言することや、グローバル名前空間以外の名前空間で宣言することが許可されていました。  この従来の動作のせいで、プログラマが意図した **new** または **delete** 演算子の実装がプログラムによって呼び出されないという危険性が生じ、結果として、問題のあるランタイム動作が警告なしに生じていました。 コンパイラはこの方法で記述されたコードを受け入れなくなりました。代わりにコンパイラ エラー C2323 を発行します。

   ```Output
    error C2323: 'operator new': non-member operator new or delete functions may not be declared static or in a namespace other than the global namespace.
   ```

   例 (変更前)

   ```cpp
    static inline void * __cdecl operator new(size_t cb, const std::nothrow_t&)  // error C2323
   ```

   例 (変更後)

   ```cpp
    void * __cdecl operator new(size_t cb, const std::nothrow_t&)  // removed 'static inline'
   ```

   また、コンパイラは特定の診断を行いませんが、インラインの operator new の形式は不適切であると見なされます。

- **非クラス型で 'operator *type*()' (ユーザー定義の変換) を呼び出す** 以前のバージョンのコンパイラでは 'operator *type*()' を非クラス型で呼び出すことが許可されていましたが、それは何の警告もなく無視されていました。 この従来の動作のせいで、問題のあるコードが警告なしに生成される危険性が生じ、結果として、予期しないランタイム動作の原因となっていました。 コンパイラはこの方法で記述されたコードを受け入れなくなりました。代わりにコンパイラ エラー C2228 を発行します。

   ```Output
    error C2228: left of '.operator type' must have class/struct/union
   ```

   例 (変更前)

   ```cpp
    typedef int index_t;

    void bounds_check(index_t index);

    void login(int column)
    {
        bounds_check(column.operator index_t());  // error C2228
    }
   ```

   例 (変更後)

   ```cpp
    typedef int index_t;

    void bounds_check(index_t index);

    void login(int column)
    {
         bounds_check(column);  // removed cast to 'index_t', 'index_t' is an alias of 'int'
    }
   ```

- **詳細な型指定子の冗長な typename** 以前のバージョンのコンパイラでは、詳細な型指定子内で **typename** を指定できました。この方法で記述されたコードは意味的に正しくありません。 コンパイラはこの方法で記述されたコードを受け入れなくなりました。代わりにコンパイラ エラー C3406 を発行します。

   ```Output
    error C3406: 'typename' cannot be used in an elaborated type specifier
   ```

   例 (変更前)

   ```cpp
    template <typename class T>
    class container;
   ```

   例 (変更後)

   ```cpp
    template <class T>  // alternatively, could be 'template <typename T>'; 'typename' is not elaborating a type specifier in this case
    class container;
   ```

- **初期化子リストからの配列の型推論** 以前のバージョンのコンパイラでは、初期化子リストからの配列の型推論はサポートされていませんでした。 コンパイラでこの形式の型推論がサポートされるようになりました。その結果、初期化子リストを使用した関数テンプレートへの呼び出しがあいまいになったり、以前のバージョンのコンパイラとは異なるオーバーロードが選ばれたりする可能性があります。 これらの問題を解決するには、プログラマの意図したオーバーロードをプログラムが明示的に指定する必要があります。

   この新しい動作により、オーバーロードの解決で過去の候補と同程度に優れた追加候補が検討されると、呼び出しはあいまいになり、結果としてコンパイラはコンパイラ エラー C2668 を発行します。

   ```Output
    error C2668: 'function' : ambiguous call to overloaded function.
   ```

   例 1: オーバーロード関数のあいまいな呼び出し (変更前)

   ```cpp
    // In previous versions of the compiler, code written in this way would unambiguously call f(int, Args...)
    template <typename... Args>
    void f(int, Args...);  //

    template <int N, typename... Args>
    void f(const int (&)[N], Args...);

    int main()
    {
        // The compiler now considers this call ambiguous, and issues a compiler error
        f({3});  error C2668: 'f' ambiguous call to overloaded function
    }
   ```

   例 1: オーバーロード関数のあいまいな呼び出し (変更後)

   ```cpp
    template <typename... Args>
    void f(int, Args...);  //

    template <int N, typename... Args>
    void f(const int (&)[N], Args...);

    int main()
    {
        // To call f(int, Args...) when there is just one expression in the initializer list, remove the braces from it.
        f(3);
    }
   ```

   この新しい動作により、オーバーロードの解決で過去の候補よりも適合度の高い追加候補が検討されると、呼び出しはあいまいにならずに新しい候補に解決され、プログラムの動作は変化します。これはプログラマの意図した動作とは異なる場合があります。

   例 2: オーバーロードの解決の変更 (変更前)

   ```cpp
    // In previous versions of the compiler, code written in this way would unambiguously call f(S, Args...)
    struct S
    {
        int i;
        int j;
    };

    template <typename... Args>
    void f(S, Args...);

    template <int N, typename... Args>
    void f(const int *&)[N], Args...);

    int main()
    {
        // The compiler now resolves this call to f(const int (&)[N], Args...) instead
        f({1, 2});
    }
   ```

   例 2: オーバーロードの解決の変更 (変更後)

   ```cpp
    struct S;  // as before

    template <typename... Args>
    void f(S, Args...);

    template <int N, typename... Args>
    void f(const int *&)[N], Args...);

    int main()
    {
        // To call f(S, Args...), perform an explicit cast to S on the initializer list.
        f(S{1, 2});
    }
   ```

- **switch ステートメントの警告の復元**

   前のバージョンのコンパイラで、**switch** ステートメント関連の、以前から存在していた警告が削除されました。今ではこれらの警告は復元されています。 コンパイラは復元された警告を発行するようになり、特定の case (既定の case を含む) に関連する警告が、switch ステートメントの最後の行ではなく、問題のある case を含む行で発行されるようになりました。 この結果、以前とは異なる行でそれらの警告が発行されるようになり、以前は `#pragma warning(disable:####)` を使用して抑制できていた警告も、意図どおりに抑制できなくなる可能性があります。 意図どおりにこれらの警告を抑制するには、問題がある可能性のある最初の case の上の行まで `#pragma warning(disable:####)` ディレクティブを移動しなければならない場合があります。 復元された警告を次に示します。

   ```Output
    warning C4060: switch statement contains no 'case' or 'default' labels
   ```

   ```Output
    warning C4061: enumerator 'bit1' in switch of enum 'flags' is not explicitly handled by a case label
   ```

   ```Output
    warning C4062: enumerator 'bit1' in switch of enum 'flags' is not handled
   ```

   ```Output
    warning C4063: case 'bit32' is not a valid value for switch of enum 'flags'
   ```

   ```Output
    warning C4064: switch of incomplete enum 'flags'
   ```

   ```Output
    warning C4065: switch statement contains 'default' but no 'case' labels
   ```

   ```Output
    warning C4808: case 'value' is not a valid value for switch condition of type 'bool'
   ```

   ```Output
    Warning C4809: switch statement has redundant 'default' label; all possible 'case' labels are given
   ```

   C4063 の例 (変更前)

   ```cpp
    class settings
    {
    public:
        enum flags
        {
            bit0 = 0x1,
            bit1 = 0x2,
            ...
        };
        ...
    };

    int main()
    {
        auto val = settings::bit1;

        switch (val)
        {
        case settings::bit0:
            break;

        case settings::bit1:
            break;

        case settings::bit0 | settings::bit1:  // warning C4063
            break;
        }
    };
   ```

   C4063 の例 (変更後)

   ```cpp
    class settings {...};  // as above

    int main()
    {
        // since C++11, use std::underlying_type to determine the underlying type of an enum
        typedef std::underlying_type<settings::flags>::type flags_t;

        auto val = settings::bit1;

        switch (static_cast<flags_t>(val))
        {
        case settings::bit0:
            break;

        case settings::bit1:
            break;

        case settings::bit0 | settings::bit1:  // ok
            break;
        }
    };
   ```

   その他の復元の警告の例については、それらのドキュメントをご覧ください。

- **#include: パス名で親ディレクトリの指定子 '..' を使用する** (`/Wall` `/WX` にのみ影響)

   以前のバージョンのコンパイラでは、親ディレクトリの指定子の使用が検出されませんでした '… ' パス名で  `#include` ディレクティブです。 この方法で記述されたコードは通常、プロジェクトの相対パスが正しく使用されていないためにプロジェクトの外部に存在するヘッダーをインクルードすることを目的としています。 この従来の動作のせいで、プログラマが意図したものとは異なるソース ファイルをインクルードしてプログラムがコンパイルされる危険性や、これらの相対パスを他のビルド環境に移植できない危険性が生じました。 コンパイラは、この方法で書かれたコードを検出してプログラマに通知し、有効な場合にはオプションのコンパイラ警告 C4464 を発行するようになりました。

   ```Output
    warning C4464: relative include path contains '..'
   ```

   例 (変更前)

   ```cpp
    #include "..\headers\C4426.h"  // emits warning C4464
   ```

   例 (変更後)

   ```cpp
    #include "C4426.h"  // add absolute path to 'headers\' to your project's include directories
   ```

   さらに、コンパイラは特定の診断を示しませんが、プロジェクトのインクルード ディレクトリを指定する場合、親ディレクトリの指定子".." を使用することもお勧めします。

- **#pragma optimize() がヘッダー ファイルの終わりを超える** (`/Wall` `/WX` にのみ影響)

   以前のバージョンのコンパイラでは、翻訳単位内に含まれるヘッダー ファイルをエスケープする最適化フラグの設定の変更は検出されませんでした。 コンパイラは、この方法で書かれたコードを検出してプログラマに通知し、有効な場合には、問題のある `#include`の位置でオプションのコンパイラ警告 C4426 を発行するようになりました。 この警告が発行されるのは、この変更が、コンパイラに対するコマンドライン引数によって設定された最適化フラグと競合する場合のみです。

   ```Output
    warning C4426: optimization flags changed after including header, may be due to #pragma optimize()
   ```

   例 (変更前)

   ```cpp
    // C4426.h
    #pragma optimize("g", off)
    ...
    // C4426.h ends

    // C4426.cpp
    #include "C4426.h"  // warning C4426
   ```

   例 (変更後)

   ```cpp
    // C4426.h
    #pragma optimize("g", off)
    ...
    #pragma optimize("", on)  // restores optimization flags set via command-line arguments
    // C4426.h ends

    // C4426.cpp
    #include "C4426.h"
   ```

- **#pragma warning(push)** と **#pragma warning(pop) の不一致** (`/Wall` `/WX` にのみ影響)

   以前のバージョンのコンパイラでは、`#pragma warning(push)` の状態の変更が、異なるソース ファイルの `#pragma warning(pop)` 状態の変更とペアになっていても (故意であることはまれですが)、それを検出しませんでした。 この従来の動作のせいで、プログラマの意図と異なる一連の警告が有効な状態でプログラムがコンパイルされる危険性が生じ、結果として、問題のあるランタイム動作が警告なしに発生する原因となっていました。 コンパイラは、この方法で書かれたコードを検出してプログラマに通知し、有効な場合には、一致する `#pragma warning(pop)` の位置でオプションのコンパイラの警告 C5031 を発行するようになりました。 この警告には、対応する `#pragma warning(push)` の場所を参照するメモが含まれます。

   ```Output
    warning C5031: #pragma warning(pop): likely mismatch, popping warning state pushed in different file
   ```

   例 (変更前)

   ```cpp
    // C5031_part1.h
    #pragma warning(push)
    #pragma warning(disable:####)
    ...
    // C5031_part1.h ends without #pragma warning(pop)

    // C5031_part2.h
    ...
    #pragma warning(pop)  // pops a warning state not pushed in this source file
    ...
    // C5031_part1.h ends

    // C5031.cpp
    #include "C5031_part1.h" // leaves #pragma warning(push) 'dangling'
    ...
    #include "C5031_part2.h" // matches 'dangling' #pragma warning(push), resulting in warning C5031
    ...
   ```

   例 (変更後)

   ```cpp
    // C5031_part1.h
    #pragma warning(push)
    #pragma warning(disable:####)
    ...
    #pragma warning(pop)  // pops the warning state pushed in this source file
    // C5031_part1.h ends without #pragma warning(pop)

    // C5031_part2.h
    #pragma warning(push)  // pushes the warning state pushed in this source file
    #pragma warning(disable:####)
    ...
    #pragma warning(pop)
    // C5031_part1.h ends

    // C5031.cpp
    #include "C5031_part1.h" // #pragma warning state changes are self-contained and independent of other source files or their #include order.
    ...
    #include "C5031_part2.h"
    ...
   ```

   一般的ではありませんが、意図的にこの方法でコードを記述する場合があります。 この方法で記述されたコードは `#include` の順序の変更の影響を受けます。可能な場合は、自己完結型の方法を使用してソース コード ファイルで警告状態を管理することをお勧めします。

- **一致していない #pragma warning(push)** (`/Wall` `/WX` にのみ影響)

   以前のバージョンのコンパイラでは、翻訳単位の末尾で一致していない `#pragma warning(push)` の状態の変更は検出されませんでした。 コンパイラは、この方法で書かれたコードを検出してプログラマに通知し、有効な場合には、一致していない `#pragma warning(push)` の位置でオプションのコンパイラ警告 C5032 を発行するようになりました。 この警告が発行されるのは、翻訳単位にコンパイル エラーがない場合のみです。

   ```Output
    warning C5032: detected #pragma warning(push) with no corresponding #pragma warning(pop)
   ```

   例 (変更前)

   ```cpp
    // C5032.h
    #pragma warning(push)
    #pragma warning(disable:####)
    ...
    // C5032.h ends without #pragma warning(pop)

    // C5032.cpp
    #include "C5032.h"
    ...
    // C5032.cpp ends -- the translation unit is completed without #pragma warning(pop), resulting in warning C5032 on line 1 of C5032.h
   ```

   例 (変更後)

   ```cpp
    // C5032.h
    #pragma warning(push)
    #pragma warning(disable:####)
    ...
    #pragma warning(pop) // matches #pragma warning (push) on line 1
    // C5032.h ends

    // C5032.cpp
    #include "C5032.h"
    ...
    // C5032.cpp ends -- the translation unit is completed without unmatched #pragma warning(push)
   ```

- **#pragma 警告状態の追跡が強化された結果、追加の警告が発行される場合があります。**

   以前のバージョンのコンパイラでは、`#pragma warning` 状態の変化の追跡が不十分なため、すべての意図された警告を発行できませんでした。 この動作により、プログラマの意図したものとは異なる状況で、事実上、特定の警告が抑制される危険性がありました。 コンパイラにより `#pragma warning` 状態がより確実に追跡されるようになりました (特にテンプレート内部での `#pragma warning` 状態の変化に関連するもの)。また `#pragma warning(push)` と `#pragma warning(pop)`の意図しない使用をプログラマが特定する助けになるように、新しい警告 C5031 と C5032 を必要に応じて発行されるようになりました。

   `#pragma warning` 状態の変更の追跡が強化された結果、以前は誤って抑制されていた警告、または以前は誤って診断されていた問題に関連する警告が発行されるようになる場合があります。

- **制御が渡らないコードの識別の強化**

   C++ 標準ライブラリが変更されたり、以前のバージョンのコンパイラよりも関数呼び出しのインライン化機能が強化されたりしたため、コンパイラは特定のコードに制御が渡らないことを示せるようになりました。 この新しい動作の結果、警告 C4720 のインスタンスが新しく、あるいはより頻繁に発行される可能性があります。

   ```Output
    warning C4720: unreachable code
   ```

   多くの場合、この警告が発行されるのは、最適化を有効にしてコンパイルするときだけです。最適化により、より多くの関数呼び出しがインライン化されたり、冗長なコードが削除されたり、コードに制御が渡っていないことを他の方法で判別できるようになったりするためです。 警告 C4720 の新しいインスタンスが **try/catch** ブロックで頻繁に発生 (特に [std::find](assetId:///std::find?qualifyHint=False&autoUpgrade=True) の使用に関連して) していることが確認されています。

   例 (変更前)

   ```cpp
    try
    {
        auto iter = std::find(v.begin(), v.end(), 5);
    }
    catch(...)
    {
        do_something();  // ok
    }
   ```

   例 (変更後)

   ```cpp
    try
    {
        auto iter = std::find(v.begin(), v.end(), 5);
    }
    catch(...)
    {
        do_something();  // warning C4702: unreachable code
    }
   ```

### <a name="VS_Update2"></a> Visual Studio 2015 Update 2 の準拠の強化

- **SFINAE 式の部分的なサポートの結果として、追加の警告とエラーが発行される場合がある**

   以前のバージョンのコンパイラは、SFINAE 式のサポートがなかったため、**decltype** 指定子内の特定の種類の式を解析しませんでした。 この従来の動作は正しい動作ではなく、C++ 標準に準拠していません。 コンパイラは、継続的な適合性の向上により、これらの式を解析し、SFINAE 式を部分的にサポートするようになりました。 その結果、コンパイラは、以前のバージョンのコンパイラが解析しなかった式で検出された警告とエラーを発行します。

   この新しい動作が、まだ宣言されていない型を含む **decltype** 式を解析するとき、コンパイラは結果としてコンパイラ エラー C2039 を発行します。

   ```Output
    error C2039: 'type': is not a member of '`global namespace''
   ```

   例 1: 宣言されていない型の使用 (変更前)

   ```cpp
    struct s1
    {
      template <typename T>
      auto f() -> decltype(s2<T>::type::f());  // error C2039

      template<typename>
      struct s2 {};
    }
   ```

   例 1 (変更後)

   ```cpp
    struct s1
    {
      template <typename>  // forward declare s2struct s2;

      template <typename T>
      auto f() -> decltype(s2<T>::type::f());

      template<typename>
      struct s2 {};
    }
   ```

   依存名が型であることを指定するために必要な **typename** キーワードが欠落している **decltype** 式がこの新しい動作によって解析されると、コンパイラは、コンパイラ エラー C2923 と共にコンパイラの警告 C4346 を発行します。

   ```Output
    warning C4346: 'S2<T>::Type': dependent name is not a type
   ```

   ```Output
    error C2923: 's1': 'S2<T>::Type' is not a valid template type argument for parameter 'T'
   ```

   例 2: 依存名が型ではない (変更前)

   ```cpp
    template <typename T>
    struct s1
    {
      typedef T type;
    };

    template <typename T>
    struct s2
    {
      typedef T type;
    };

    template <typename T>
    T declval();

    struct s
    {
      template <typename T>
      auto f(T t) -> decltype(t(declval<S1<S2<T>::type>::type>()));  // warning C4346, error C2923
    };
   ```

   例 2 (変更後)

   ```cpp
    template <typename T> struct s1 {...};  // as above
    template <typename T> struct s2 {...};  // as above

    template <typename T>
    T declval();

    struct s
    {
      template <typename T>
      auto f(T t) -> decltype(t(declval<S1<typename S2<T>::type>::type>()));
    };
   ```

- **`volatile` メンバー変数が、暗黙的に定義されたコンストラクターと代入演算子を防止する** 以前のバージョンのコンパイラは、**volatile** メンバー変数を持つクラスが、自動的に生成された既定のコピー/移動コンストラクターと既定のコピー/移動代入演算子を持つことを許可していました。 この従来の動作は正しい動作ではなく、C++ 標準に準拠していません。 コンパイラは、揮発性のメンバー変数を持つクラスが、非単純コンストラクションと代入演算子を持つとみなすようになりました。それにより、これらの演算子の既定の実装が自動的に生成されることを防止します。 そのようなクラスが共用体 (またはクラス内の無名共用体) のメンバーである場合は、共用体のコピー/移動コンストラクターとコピー/移動代入演算子 (または無名共用体を含むクラス) は、暗黙的に削除済みとして定義されます。 明示的に定義することなく、共用体 (または無名共用体を含むクラス) を構築またはコピーしようとするとエラーとなり、結果として、コンパイラはコンパイラ エラー C2280 を発行します。

   ```Output
    error C2280: 'B::B(const B &)': attempting to reference a deleted function
   ```

   例 (変更前)

   ```cpp
    struct A
    {
      volatile int i;
      volatile int j;
    };

    extern A* pa;

    struct B
    {
      union
      {
        A a;
        int i;
      };
    };

    B b1 {*pa};
    B b2 (b1);  // error C2280
   ```

   例 (変更後)

   ```cpp
    struct A
    {
      int i;int j;
    };

    extern volatile A* pa;

    A getA()  // returns an A instance copied from contents of pa
    {
      A a;
      a.i = pa->i;
      a.j = pa->j;
      return a;
    }

    struct B;  // as above

    B b1 {GetA()};
    B b2 (b1);  // error C2280
   ```

- **静的メンバー関数は、CV 修飾子をサポートしていません。**

   以前のバージョンの Visual C++ 2015 は、静的メンバー関数が CV 修飾子を持つことを許可していました。 この動作は、Visual C++ 2015 および Visual C++ 2015 Update 1 での回帰が原因です。Visual C++ 2013 および Visual C++ の以前のバージョンは、この方法で記述されたコードを拒否します。 Visual C++ 2015 および Visual C++ 2015 Update 1 の動作は正しいものではなく、C++ 標準に準拠していません。  Visual Studio 2015 Update 2 は、この方法で記述されたコードを拒否し、コンパイラ エラー C2511 を代わりに発行します。

   ```Output
    error C2511: 'void A::func(void) const': overloaded member function not found in 'A'
   ```

   例 (変更前)

   ```cpp
    struct A
    {
      static void func();
    };

    void A::func() const {}  // C2511
   ```

   例 (変更後)

   ```cpp
    struct A
    {
      static void func();
    };

    void A::func() {}  // removed const
   ```

- **列挙型の事前宣言は、WinRT コードでは許可されていません** (`/ZW` にのみ影響)

   マネージド C++ コードが `/clr` コンパイラ スイッチを使用して .Net Framework 用にコンパイルされる場合と同様に、Windows ランタイム (WinRT) 用にコンパイルされたコードは、**enum** 型が事前に宣言されることを許可しません。 この動作により、列挙型のサイズが常にわかり、WinRT 型システムに正しくプロジェクションを実行することができます。 コンパイラは、この方法で記述されたコードを拒否し、コンパイラ エラー C3197 と共にコンパイラ エラー C2599 を発行します。

   ```Output
    error C2599: 'CustomEnum': the forward declaration of a WinRT enum is not allowed
   ```

   ```Output
    error C3197: 'public': can only be used in definitions
   ```

   例 (変更前)

   ```cpp
    namespace A {
      public enum class CustomEnum: int32;  // forward declaration; error C2599, error C3197
    }

    namespace A {
      public enum class CustomEnum: int32
      {
        Value1
      };
    }

    public ref class Component sealed
    {
    public:
      CustomEnum f()
      {
        return CustomEnum::Value1;
      }
    };
   ```

   例 (変更後)

   ```cpp
              // forward declaration of CustomEnum removed
    namespace A {
      public enum class CustomEnum: int32
      {
        Value1
      };
    }

    public ref class Component sealed
    {
    public:
      CustomEnum f()
      {
        return CustomEnum::Value1;
      }
    };
   ```

- **オーバーロードされた非メンバー operator new と operator delete をインラインで宣言できない** (レベル 1 (`/W1`) 既定で有効)

   以前のバージョンのコンパイラは、非メンバー **operator new** と **operator delete** 関数がインラインで宣言されるときに警告を発行しません。 この方法で記述されたコードは、形式が正しくなく (診断は必要なし)、new 演算子と delete 演算子の不一致 (特に、サイズ割り当て解除と共に使用された場合) から生じるメモリの問題を引き起こす可能性があります。この問題を診断するのは難しい場合があります。 コンパイラは警告 C4595 を発行するようになったので、この方法で記述されたコードを識別しやすくなりました。

   ```Output
    warning C4595: 'operator new': non-member operator new or delete functions may not be declared inline
   ```

   例 (変更前)

   ```cpp
    inline void* operator new(size_t sz)  // warning C4595
    {
      ...
    }
   ```

   例 (変更後)

   ```cpp
    void* operator new(size_t sz)  // removed inline
    {
      ...
    }
   ```

   この方法で記述されたコードを修正するには、演算子の定義をヘッダー ファイルから対応するソース ファイルに移動することが必要な場合があります。

### <a name="VS_Update3"></a> Visual Studio 2015 Update 3 の準拠の強化

- **std::is_convertable が self-assignment を検出するようになった** (標準ライブラリ) 以前のバージョンの `std::is_convertable` type-trait は、コピー コンストラクターが削除済みまたはプライベートの場合、クラス型の自己代入を正しく検出していませんでした。 コピー コンストラクターが削除済みまたはプライベートの場合でも、クラス型の自己代入時にも `std::is_convertable<>::value` が正しく **false** に設定されるようになりました。

   この変更に関連するコンパイラの診断はありません。

   例

   ```cpp
    #include <type_traits>

    class X1
    {
    public:
        X1(const X1&) = delete;
    };

    class X2
    {
    private:
        X2(const X2&);
    };

    static_assert(std::is_convertible<X1&, X1>::value, "BOOM");static_assert(std::is_convertible<X2&, X2>::value, "BOOM");
   ```

   以前のバージョンの Visual C++ では、`std::is_convertable<>::value` が不適切に **true** に設定されているため、この例の一番下にある静的なアサーションは成功します。 新しいバージョンでは、`std::is_convertable<>::value` は正しく **false** に設定され、静的なアサーションが失敗するようになりました。

- **既定値にされた、または削除された単純なコピー コンストラクターと移動コンストラクターのアクセス指定子の尊重**

   以前のバージョンのコンパイラは、既定値にされた、または削除された単純なコピー コンストラクターと移動コンストラクターを呼び出し前に確認していませんでした。 この従来の動作は正しい動作ではなく、C++ 標準に準拠していません。 場合によっては、この従来の動作のせいで、問題のあるコードが警告なしに生成される危険性が生じ、結果として、予期しないランタイム動作の原因となっていました。 コンパイラは、既定値に指定された、または削除された単純なコピー コンストラクターと移動コンストラクターをチェックし、呼び出し可能かどうかを判断し、呼び出し不能と判断した場合に、コンパイラの警告 C2248 を結果として返します。

   ```Output
    error C2248: 'S::S' cannot access private member declared in class 'S'
   ```

   例 (変更前)

   ```cpp
    class S {
    public:
       S() = default;
    private:
        S(const S&) = default;
    };

    void f(S);  // pass S by value

    int main()
    {
        S s;
        f(s);  // error C2248, can't invoke private copy constructor
    }
   ```

   例 (変更後)

   ```cpp
    class S {
    public:
       S() = default;
    private:
        S(const S&) = default;
    };

    void f(const S&);  // pass S by reference

    int main()
    {
        S s;
        f(s);
    }
   ```

- **属性が指定された ATL コードのサポートの非推奨化** (デフォルトでレベル 1 (`/W1`))

   以前のバージョンのコンパイラは、属性が指定された ATL コードをサポートしていました。 [Visual C++ 2008 から始まった](#whats-new-for-c-in-visual-studio-2008)、属性が指定された ATL コードのサポートを停止する次のフェーズとして、属性が指定された ATL コードは非推奨とされました。 コンパイラは、非推奨になったこの種類のコードを特定するために、コンパイラの警告 C4467 を発行するようになりました。

   ```Output
    warning C4467: Usage of ATL attributes is deprecated
   ```

   コンパイラからサポートが削除されるまで、属性が指定された ATL コードを今後も使い続ける場合は、`/Wv:18` または `/wd4467` コマンド ライン引数をコンパイラに渡すことで、またはソース コードに `#pragma warning(disable:4467)` を追加することで、この警告を無効にすることができます。

   例 1 (変更前)

   ```cpp
              [uuid("594382D9-44B0-461A-8DE3-E06A3E73C5EB")]
    class A {};
   ```

   例 1 (変更後)

   ```cpp
    __declspec(uuid("594382D9-44B0-461A-8DE3-E06A3E73C5EB")) A {};
   ```

   非推奨になった ATL 属性の使用を防ぐために、次のコード例のように、IDL ファイルを作成する場合があります

   例 2 (変更後)

   ```cpp
    [emitidl];
    [module(name="Foo")];

    [object, local, uuid("9e66a290-4365-11d2-a997-00c04fa37ddb")]
    __interface ICustom {
        HRESULT Custom([in] long l, [out, retval] long *pLong);
        [local] HRESULT CustomLocal([in] long l, [out, retval] long *pLong);
    };

    [coclass, appobject, uuid("9e66a294-4365-11d2-a997-00c04fa37ddb")]
    class CFoo : public ICustom
    {
        // ...
    };
   ```

   まず、*.idl ファイルを作成します。vc140.idl で生成されるファイルを使用して、インターフェイスと注釈を含む \*.idl ファイルを取得することができます。

   次に、MIDL 手順をビルドに追加し、C++ インターフェイス定義が生成されるようにします。

   例 2 IDL (変更後)

   ```cpp
    import "docobj.idl";

    [
        object,local,uuid(9e66a290-4365-11d2-a997-00c04fa37ddb)
    ]

    interface ICustom : IUnknown {
        HRESULT  Custom([in] long l, [out,retval] long *pLong);
        [local] HRESULT  CustomLocal([in] long l, [out,retval] long *pLong);
    };

    [ version(1.0), uuid(29079a2c-5f3f-3325-99a1-3ec9c40988bb) ]
    library Foo
    {
        importlib("stdole2.tlb");
        importlib("olepro32.dll");
            [
                version(1.0),
                appobject,uuid(9e66a294-4365-11d2-a997-00c04fa37ddb)
            ]

        coclass CFoo {
            interface ICustom;
        };
    }
   ```

   次に、以下のコード例のように、実装ファイルで ATL を直接使用します。

   例 2 実装 (変更後)

   ```cpp
    #include <idl.header.h>
    #include <atlbase.h>

    class ATL_NO_VTABLE CFooImpl :
        public ICustom,
        public ATL::CComObjectRootEx<CComMultiThreadModel>
    {
    public:
        BEGIN_COM_MAP(CFooImpl)
        COM_INTERFACE_ENTRY(ICustom)
        END_COM_MAP()
    };
   ```

- **プリコンパイル済みヘッダー (PCH) ファイルと一致しない #include ディレクティブ** (`/Wall` `/WX` にのみ影響)

   以前のバージョンのコンパイラは、プリコンパイル済みヘッダー (PCH) ファイルの使用時に、`-Yc` と `-Yu` のコンパイル間のソース ファイルの `#include` ディレクティブ一致しない場合でも、受け入れていました。 この方法で記述されたコードは、コンパイラで処理できなくなります。 コンパイラは、PCH ファイルの使用時に `#include` ディレクティブの不一致を特定できるようにコンパイラの警告 CC4598 を発行するようになりました。

   ```Output
    warning C4598: 'b.h': included header file specified for Ycc.h at position 2 does not match Yuc.h at that position
   ```

   例 (変更前):

   X.cpp (-Ycc.h)

   ```cpp
    #include "a.h"
    #include "b.h"
    #include "c.h"
   ```

   Z.cpp (-Yuc.h)

   ```cpp
    #include "b.h"
    #include "a.h"  // mismatched order relative to X.cpp
    #include "c.h"
   ```

   例 (変更後)

   X.cpp (-Ycc.h)

   ```cpp
    #include "a.h"
    #include "b.h"
    #include "c.h"
   ```

   Z.cpp (-Yuc.h)

   ```cpp
    #include "a.h"
    #include "b.h" // matched order relative to X.cpp
    #include "c.h"
   ```

- **プリコンパイル済みヘッダー (PCH) ファイルと一致しない #include ディレクトリ** (`/Wall` `/WX` にのみ影響)

   プリコンパイル済みヘッダー (PCH) ファイルの使用時に、以前のバージョンのコンパイラは、コンパイラ `-Yc` と `-Yu` のコンパイルで一致しない include ディレクトリ (`-I`) コマンド ライン引数を受け入れていました。 この方法で記述されたコードは、コンパイラで処理できなくなります。   コンパイラは、PCH ファイルの使用時に include ディレクトリ (`-I`) コマンド ライン引数を特定できるコンパイラの警告 CC4599 を発行するようになりました。

   ```Output
    warning C4599: '-I..' : specified for Ycc.h at position 1 does not match Yuc.h at that position
   ```

   例 (変更前)

   ```ms-dos
    cl /c /Wall /Ycc.h -I.. X.cpp
    cl /c /Wall /Yuc.h Z.cpp
   ```

   例 (変更後)

   ```ms-dos
    cl /c /Wall /Ycc.h -I.. X.cpp
    cl /c /Wall /Yuc.h -I.. Z.cpp
   ```

## <a name="whats-new-for-c-in-visual-studio-2013"></a>Visual Studio 2013 での C++ の新機能

### <a name="improved-iso-cc-standards-support"></a>ISO C/C++ 標準のサポートの強化

#### <a name="compiler"></a>コンパイラ

MSVC では次の ISO C++11 の言語機能がサポートされています。

- 関数テンプレートに関する既定のテンプレート引数。
- コンストラクターのデリゲート
- 明示的な変換演算子。
- 初期化子リストと均一な初期化。
- 未加工の文字列リテラル。
- 可変値引数テンプレート。
- エイリアスのテンプレート。
- 削除指定関数。
- 非静的データ メンバーの初期化子 (NSDMI)
- 既定化関数。 \*
- サポートされる ISO C99 機能:
- _Bool
- 複合リテラル。
- 初期化子の指定。
- コードによる宣言の混合。
- 文字列リテラルから変更可能な値への変換は、新しいコンパイラ オプション `/Zc:strictStrings` を使用して無効にすることができます。 C++98 では、文字列リテラルから `char*` (およびワイド文字列リテラル `wchar_t*`) への変換は非推奨とされます。 C++11 では、変換は完全に削除されました。 コンパイラを標準に厳密に準拠させることもできますが、そうではなく、変換を制御できるように `/Zc:strictStrings` のオプションが用意されています。 既定では、このオプションはオフです。 デバッグ モードでこのオプションを使用すると、STL はコンパイルされません。
- rvalue/lvalue の参照キャスト。 C++11 では、右辺値参照を使用して、左辺値と右辺値を明確に区別できます。 以前は、コンパイラは、具体的なキャストのシナリオでこれを実現できませんでした。 新しいコンパイラ オプションである `/Zc:rvalueCast` が追加され、コンパイラが C++ Language Working Paper (C++ 言語報告書) (セクション 5.4 [expr.cast]/1 を参照) に準拠するようになりました。 このオプションを指定しない場合の既定の動作は、Visual Studio 2012 の動作と同じです。

> [!NOTE]
> 既定化関数では、=default を使用したメンバー関数の移動コンストラクターと移動代入演算子の要求はサポートされていません。

### <a name="c99-libraries"></a>C99 ライブラリ

複数のヘッダーで、不足していた関数の宣言と実装が追加されます (math.h、ctype.h、wctype.h、stdio.h、stdlib.h、wchar.h)。 また新しいヘッダーとして complex.h、stdbool.h、fenv.h、inttypes.h が追加され、これらのヘッダーで宣言されたすべての関数が実装されます。 新しい C++ のラッパー ヘッダー (ccomplex、cfenv、cinttypes、ctgmath) が追加され、複数のヘッダーが更新されます (ccomplex、cctype、clocale、cmath、cstdint、cstdio、cstring、cwchar、cwctype)。

### <a name="standard-template-library"></a>標準テンプレート ライブラリ

C++11 の明示的な変換演算子、初期化子リスト、スコープ指定の列挙型、および可変個引数テンプレートがサポートされています。
すべてのコンテナーは、C++11 の詳細な要素要件をサポートするようになりました。
次の C++14 機能のサポート。

- "透過的な演算子のファンクター" less<>、greater<>、plus<>、multiplies<> など。
- make_unique<T>(args...)、make_unique<T[]>(n)
- cbegin()/cend()、rbegin()/rend()、crbegin()/crend() の各非メンバー関数。
- \<atomic> で多数のパフォーマンス向上を実現しました。
- \<type_traits> で安定性の大幅向上とコード修正を行いました。

### <a name="breaking-changes"></a>互換性に影響する変更点

この ISO C/C++ 標準のサポート強化に伴って、既存のコードに変更を加える必要が生じる可能性があります。その結果、コードは C++11 に準拠し、Visual Studio 2013 の Visual C++ で正しくコンパイルできるようになります。

### <a name="visual-c-library-enhancements"></a>Visual C++ ライブラリの強化

- C++ REST SDK を追加しました。 この中には、REST サービスに関する C++ の最新の実装があります。
- C++ AMP テクスチャのサポートが強化されました。 この中には、ミップマップと新しいサンプリング モードのサポートが含まれます。
- PPL タスクは複数のスケジューリング テクノロジおよび非同期デバッグをサポートします。 新しい API により、通常の結果と例外条件の両方を対象とする PPL タスクを作成できます。

### <a name="c-application-performance"></a>C++ アプリケーションのパフォーマンス

- 自動ベクター化は、より多くの C++ のパターンを認識および最適化し、コードをいっそう高速に実行できるようになりました。
- ARM プラットフォームと Atom マイクロアーキテクチャ コードの品質が向上しました。
- 呼び出し規約 __vectorcall が追加されました。 ベクター レジスタを使用するための呼び出し規約 __vectorcall を使用して、ベクター型の引数を渡します。
- 新しいリンカー オプション。 `/Gw` (コンパイラ) と `/Gy` (アセンブラー) スイッチにより、より効率的なバイナリを生成するためのリンカー最適化が有効になります。
- C++ AMP の共有メモリのサポート。これにより、CPU と GPU との間でのデータ コピーが減少するか、不要になります。

### <a name="profile-guided-optimization-pgo-enhancements"></a>ガイド付き最適化のプロファイル (Profile Guided Optimization、PGO) が次のように強化されました

- PGO を使用して最適化されたアプリケーションのワーキング セットの縮小を通じてパフォーマンスを向上させました。
- Windows ランタイム アプリ開発用の新しい PGO。

### <a name="windows-runtime-app-development-support"></a>Windows ランタイム アプリ開発のサポート

- **Value 構造体の中でのボックス化された値のサポート。**

   null にすることができるフィールドを使用して、値の型を定義できます。たとえば、**int** ではなく、`IBox<int>^` です。つまり、これらのフィールドは値を持つことも、または **nullptr** に等しくすることもできます。

- **よりリッチな例外情報。**

   C++/CX は新しい Windows エラー モデルをサポートし、アプリケーション バイナリ インターフェイス (ABI) を通じたリッチな例外情報の伝達とキャプチャを可能にします。その中には、呼び出し履歴とカスタム メッセージ文字列が含まれます。

- **Object::ToString () は、仮想メソッドになりました。**

   ユーザー定義の Windows ランタイムの参照型の中で、ToString をオーバーライドできるようになりました。

- **非推奨の API のサポート。**

   Public Windows ランタイム API は、"非推奨" というマークを付けられ、ビルドの警告として表示されるカスタム メッセージを付与され、移行のガイドラインが提供されるようになりました。

- **デバッガーの強化。**

   ネイティブ/JavaScript ネの相互運用機能デバッグ、Windows ランタイムの例外診断、非同期コードのデバッグ (Windows ランタイムと PPL の両方) をサポートします。

> [!NOTE]
> ここで説明する C++ 固有の機能と拡張機能に加えて、Visual Studio 内の他の拡張機能も、より適切な Windows ランタイム アプリの開発に役立ちます。

### <a name="diagnostics-enhancements"></a>診断の強化

- デバッガーの強化。 非同期デバッグとマイ コードのみのデバッグのサポート。
- コード分析カテゴリ。 これで、コード アナライザーからの出力を分類して表示し、コードの欠陥を検出して修正することができます。
- XAML 診断。 XAML 内での UI の応答性やバッテリ使用の問題を診断できるようになりました。
- グラフィックスと GPU のデバッグの強化。
- 実際のデバイス上でのリモート キャプチャと再生。
- AMP C++ と CPU の同時デバッグ。
- C++ AMP ランタイム診断の強化。
- HLSL 計算シェーダー トレースのデバッグ。

### <a name="3-d-graphics-enhancements"></a>3-D グラフィックスの強化

- イメージ コンテンツ パイプラインによる、プリマルチプライされたアルファ DDS 形式のサポート。
- イメージ エディターは、内部でプリマルチプライされたアルファを使用してレンダリングを行い、その結果、濃いにじみのようなレンダリングの副産物を回避できます。
- イメージ エディターとモデル エディター。 イメージ エディターとモデル エディターのシェーダー デザイナー モードで、ユーザー定義フィルターの作成がサポートされるようになりました。

### <a name="ide-and-productivity"></a>IDE と生産性

**強化されたコード形式**。 C++ コードに、さらに多くの書式設定を適用できます。 これらの設定を使用することにより、中かっことキーワードに関連する改行位置、インデント、スペース入力、および行の折り返しを制御できます。 ステートメントとブロックを完了させたとき、およびファイルにコードを貼り付けたときに、コードが自動的に書式設定されます。

**中かっこの補完。** C++ コードで、これらの開始文字に対応する終了文字が自動補完されるようになりました。

- { (中かっこ)
- [ (角かっこ)
- ( (かっこ)
- ' (単一引用符)
- " (二重引用符)

**追加の C++ オート コンプリート機能。**

- クラス型を表すセミコロンを追加します。
- 未加工リテラル文字列のかっこを補完します。
- 複数行コメント (/\* \*/) を補完します

**[すべての参照の検索]** は、一致するテキストの一覧を表示した後、参照の解決とフィルター処理をバックグラウンドで自動的に実行するようになりました。

**コンテキスト ベースのメンバー一覧のフィルター処理。** アクセス不可能なメンバーは、IntelliSense のメンバー一覧から除外されます。 たとえば、プライベート メンバーは、型を実装するコードを変更しない限り、メンバー一覧の中に表示されません。 メンバーの一覧が開いている間、**Ctrl** + **J** キーを押してフィルター処理を 1 レベル削除することもできます (現在のメンバーの一覧ウィンドウにのみ適用されます)。 もう一度 **Ctrl** + **J** キーを押してテキストのフィルター処理を解除し、すべてのメンバーを表示することもできます。

**パラメーター ヘルプのスクロール。** 任意のシグネチャを表示するだけの動作や、現在のコンテキストに基づいてシグネチャを更新しない動作以外に、パラメーター ヘルプのツールヒントの中に表示される関数シグネチャが、実際に入力したパラメーターの数に基づいて変化するようになりました。 パラメーター ヘルプの表示が、入れ子になった関数に対しても正しく機能するようになりました。

**ヘッダー/コード ファイルの切り替え。** ショートカット メニューのコマンドまたはキーボード ショートカットを使用して、ヘッダー ファイルとそれに対応するコード ファイルの間で切り替えを実行できるようになりました。

**サイズ変更可能な C++ プロジェクトのプロパティ ウィンドウ**

**C++/CX および C++/CLI 内でのイベント ハンドラー コードの自動生成。**  C++/CX または C++/CLI コード ファイル内で、イベント ハンドラーを追加するためにコードを入力しているときに、エディターでデリゲート インスタンスとイベント ハンドラー定義を自動的に生成できます。 イベント ハンドラー コードが自動生成できる場合に、ツールヒント ウィンドウが表示されます。

**DPI 対応の拡張。** アプリケーション マニフェスト ファイルに対する DPI 対応設定は、[モニターごとの高い DPI 認識] をサポートするようになりました。

**構成の高速切り替え。** 大規模なアプリケーションでは、構成の切り替え、特に後続の切り替え操作がより迅速に実行されるようになりました。

**ビルド時間の効率。** 多数の最適化と、マルチコアの活用により、特に大規模プロジェクトで、ビルドがさらに高速になりました。 C++ の WinMD を参照している C++ アプリケーションのインクリメンタル ビルドも非常に高速になりました。

## <a name="whats-new-for-c-in-visual-studio-2012"></a>Visual Studio 2012 での C++ の新機能

### <a name="improved-c11-standards-support"></a>C++11 標準のサポートの向上

#### <a name="standard-template-library"></a>標準テンプレート ライブラリ

- 新しい STL ヘッダーのサポート: \<atomic>、\<chrono>、\<condition_variable>、\<filesystem>、\<future>、\<mutex>, \<ratio>、\<thread>。
- メモリ リソースの使用率を最適化するため、コンテナーが以前より小さくなりました。 たとえば、既定の設定の x86 リリース モードの場合、`std::vector` は Visual Studio 2010 での 16 バイトから Visual Studio 2012 では 12 バイトに、`std::map` は Visual Studio 2010 での 16 バイトから Visual Studio 2012 では 8 バイトに、それぞれ小さくなりました。
- C++11 標準に従って、必須ではなく許容として SCARY 反復子が実装されました。

#### <a name="other-c11-enhancements"></a>C++11 に関する他の機能強化

- 範囲ベースの for ループ。 for (for 範囲宣言 : 式) の形式で配列、STL コンテナー、Windows ランタイムのコレクションに対して使用できる、より信頼性の高いループを記述できます。 これは、コア言語サポートの一部です。
- ステートレスのラムダとは空のラムダ導入子 [] で始まるコード ブロックで、ローカル変数をキャプチャしません。標準 C++11 で必須要件とされたことから、ステートレスのラムダから関数ポインターへの暗黙的な変換ができるようになりました。
- スコープ付きの列挙型のサポート。 C++ の enum class 列挙キーがサポートされるようになりました。 次のコードでは、この列挙キーが以前の enum の動作とどのように異なるかを示します。

   ```cpp
  enum class Element { Hydrogen, Helium, Lithium, Beryllium };
  void func1(Element e);
  func1(Hydrogen); // error C2065: 'Hydrogen' : undeclared identifier
  func1(Element::Helium); // OK
   ```

### <a name="windows-runtime-app-development-support"></a>Windows ランタイム アプリ開発のサポート

- **ネイティブな XAML ベースの UI モデル**。 Windows ランタイム アプリでは、新しいネイティブな XAML ベースの UI モデルを使用できます。
- **Visual C++ コンポーネントの拡張機能**。 これらの拡張機能は Windows ランタイム アプリの必要な部分である Windows ランタイム オブジェクトの使用を簡略化します。 詳しくは、「[Roadmap for Windows Runtime apps using C++](../cppcx/universal-windows-apps-cpp.md)」(C++ を使った Windows ランタイム アプリのためのロードマップ) および「[Visual C++ language reference (C++/CX)](../cppcx/visual-c-language-reference-c-cx.md)」(Visual C++ の言語リファレンス (C++/CX)) をご覧ください
- **DirectX ゲーム**。 Windows ランタイム アプリに対する DirectX の新しいサポートを使って、魅力的なゲームを作成できます。
- **XAML/DirectX の相互運用**。 XAML と DirectX の両方を使う Windows ランタイム アプリの相互運用が効率よくなりました。
- **Windows ランタイム コンポーネント DLL の開発**。 コンポーネント DLL の開発により、Windows ランタイムの環境が拡張可能になります。

### <a name="compiler-and-linker"></a>コンパイラとリンカー

- **自動ベクター化**。 コンパイラはコード内のループを解析し、可能であれば、ベクター レジスタを使用する命令や最新のプロセッサのすべてに存在する命令を出力します。 これによりループがより速くなります (プロセッサの命令はストリーミング SIMD 拡張命令 (SSE) と呼ばれます)。 この最適化は自動的に適用されるため、最適化を有効化または要求する必要はありません。
- **自動並行化**。 コンパイラは、コードのループを分析し、複数のコアまたはプロセッサに計算を広げる命令を生成できます。 これにより、ループの実行速度が向上します。 既定では有効にならないので、この最適化を要求する必要があります。 多くの場合、並行化するループの直前のコードに `#pragma loop(hint_parallel(N))` を含めると役に立ちます。
- 自動ベクター化と自動並行化が連携することで、複数のコアで計算を実行し、各コアのコードでベクター レジスタを使うことができます。

### <a name="new-in-visual-studio-2012-update-1"></a>Visual Studio 2012 Update 1 の新機能

C++ コードをビルドするときに、Windows XP を対象にします。
Microsoft C++ のコンパイラとライブラリを使って、Windows XP および Windows Server 2003 を対象にすることができます。

#### <a name="parallel-programming-support"></a>並列プログラミングのサポート

##### <a name="c-accelerated-massive-parallelism-amp"></a>C++ Accelerated Massive Parallelism (AMP)

C++ AMP は、通常は個々のグラフィックス カードに GPU として存在するデータ並列ハードウェアを活用して、C++ コードの実行を高速化します。 C++ AMP のプログラミング モデルには、多次元配列、インデックス作成、メモリ転送、タイル、数学関数ライブラリが含まれています。 C++ AMP の言語拡張機能とコンパイラの制限を使うことにより、データが CPU から GPU またはその逆に移動される方法を制御できます。

**デバッグ。** C++ AMP を使って GPU を対象とするアプリのデバッグ エクスペリエンスは、他の C++ アプリのデバッグと同じです。 これには、前述した新しい並列デバッグの追加が含まれます。

**プロファイリング。** C++ AMP および他の Direct3D ベースのプログラミング モデルに基づく GPU アクティビティのプロファイリングがサポートされるようになりました。

#### <a name="general-parallel-programming-enhancements"></a>全般的な並列プログラミングの機能強化

マルチコアおよびメニーコア アーキテクチャに移行するハードウェアでは、開発者はシングルコアの上がり続けるクロック速度に依存することはできなくなりました。 コンカレンシー ランタイムでの並列プログラミングのサポートにより、開発者はこれらの新しいアーキテクチャを利用できます。
Visual Studio 2010 では、並列パターン ライブラリなどの強力な C++ 並列化ライブラリが、高度なデータフロー パイプラインを表すことによってコンカレンシーを利用するための機能と共に導入されました。 Visual Studio 2012 では、これらのライブラリが、よりよいパフォーマンス、よりきめ細かい制御、開発者が最も必要とする並列パターンの豊富なサポートを提供するように拡張されています。 次のような広範な機能が含まれます。

- 非同期性と継続性をサポートするリッチなタスク ベースのプログラミング モデル。
- fork と join の並列実行をサポートする並列アルゴリズム (parallel_for、parallel_for with affinity、parallel_for_each、parallel_sort、parallel_reduce、parallel_transform)。
- priority_queue、queue、vector、map などの std データ構造のスレッドセーフ バージョンを提供するコンカレンシー セーフなコンテナー。
- 必然的に同時実行の単位に分解するデータフロー パイプラインを表すために開発者が使用できる非同期エージェント ライブラリ。
- この一覧内のパターンの円滑な構成を容易にするカスタマイズ可能なスケジューラおよびリソース マネージャー。

##### <a name="general-parallel-debugging-enhancements"></a>全般的な並列デバッグの機能強化

**[並列タスク]** ウィンドウと **[並列スタック]** ウィンドウに加えて、Visual Studio 2012 では、すべてのスレッドおよびプロセスで式の値を調べて、結果の並べ替えとフィルター処理を実行できる、新しい **[並列ウォッチ]** ウィンドウが提供されています。 また、独自のビジュアライザーを使ってウィンドウを拡張したり、すべてのツール ウィンドウで新しいマルチプロセスのサポートを利用したりすることもできます。

### <a name="ide"></a>IDE

**Visual Studio テンプレートのサポート。** Visual Studio テンプレート テクノロジを使って、C++ プロジェクトや項目テンプレートを作成できます。

**ソリューションの非同期読み込み**。 ソリューションの重要な部分を最初にしてプロジェクトが非同期的に読み込まれるようになり、作業を速く開始できます。

**リモート デバッグの自動配置。** Visual C++ でのリモート デバッグ用のファイルの配置が簡素化されています。 プロジェクト コンテキスト メニューの **[配置]** オプションは、デバッグ構成プロパティで指定されているファイルをリモート コンピューターに自動的にコピーします。 リモート コンピューターにファイルを手動でコピーする必要はなくなりました。

**C++/CLI の IntelliSense。** C++/CLI で IntelliSense が完全にサポートされるようになりました。 クイック ヒント、パラメーター ヘルプ、メンバーの一覧、オート コンプリートなどの IntelliSense の機能が、C++/CLI で動作するようになりました。 さらに、このドキュメントで説明されている IntelliSense および IDE の他の拡張機能も、C++/CLI で動作します。

**高度な IntelliSense ツールヒント。** C++ IntelliSense のクイック ツールヒントで、より詳細な XML ドキュメント コメント スタイルの情報が表示されるようになりました。 XML ドキュメント コメントのある C++ AMP などのライブラリから API を使っている場合、IntelliSense のツールヒントに単なる宣言以上の情報が表示されます。 また、コードに XML ドキュメント コメントがある場合、IntelliSense のツールヒントは詳細な情報を表示します。

**C++ コードの構築。** [メンバーの一覧] ドロップダウン リストでは、スイッチ、if-else、for ループ、その他の基本的なコード構造のスケルトン コードを利用できます。 一覧からコードの断片を選択し、コードに挿入して、必要なロジックを入力します。 独自のカスタム コードを作成してエディターで使うこともできます。

**[メンバーの一覧] の機能強化。** コード エディターにコードを入力すると、 **[メンバーの一覧]** ドロップダウン リストが自動的に表示されます。 結果はフィルター処理されるので、入力に合わせて関連するメンバーだけが表示されます。 **[オプション]** ダイアログ ボックスの **[テキスト エディター]**  >  **[C/C++]**  >  **[詳細設定]** で、[メンバーの一覧] で使われるフィルター処理のロジックの種類を制御できます。

**セマンティクスの色づけ。** 型、列挙、マクロ、その他の C++ トークンが、既定で色づけされるようになりました。

**参照の強調表示。** シンボルを選ぶと、現在のファイル内にあるそのシンボルのすべてのインスタンスが強調表示されます。 強調表示された参照間を移動するには、**Ctrl** + **Shift** + **上向き矢印**キーまたは **Ctrl** + **Shift** + **下向き矢印**キーを押します。 **[オプション]** ダイアログ ボックスの **[テキスト エディター]**  >  **[C/C++]**  >  **[詳細設定]** で、この機能をオフにできます。

### <a name="application-lifecycle-management-tools"></a>アプリケーション ライフサイクル管理ツール

#### <a name="static-code-analysis"></a>スタティック コード分析

C++ のスタティック分析が、より詳細なエラー コンテキスト情報、より多くの分析ルール、よりよい分析結果を提供するように更新されました。 新しい [コード分析] ウィンドウでは、キーワード、プロジェクト、重大度によってメッセージをフィルター処理できます。 ウィンドウでメッセージを選ぶと、そのメッセージがトリガーされたコード行がコード エディターで強調表示されます。 C++ の特定の警告に対するメッセージでは、警告の原因になった実行パスを示すソース行が一覧表示されます。その特定のパスを取得することになった判断ポイントと理由が強調表示されます。
コード分析は、Visual Studio 2012 のほとんどのエディションに付属しています。 Professional、Premium、Ultimate エディションには、すべてのルールが含まれます。 Windows 8 および Windows Phone 用の Express エディションには、最も重大な警告だけが含まれています。 Web 用の Express エディションにはコード分析は含まれません。
コード分析では他に次のような機能強化が行われています。

- 新しいコンカレンシーの警告は、マルチスレッド C/C++ プログラムで正しいロック規範を使っていることを確認することにより、コンカレンシーのバグの回避に役立ちます。 アナライザーは、潜在的な競合状態、ロック順序の逆転、呼び出し元/呼び出し先のロック コントラクト違反、一致しない同期操作、その他のコンカレンシーのバグを検出します。
- 規則セットを使うことにより、コード分析の実行に適用する C++ の規則を指定できます。
- **[コード分析]** ウィンドウでは、選んだ警告を抑制するプラグマをソース コードに挿入できます。
- Microsoft ソース コード注釈言語 (SAL) の新しいバージョンを使って、関数がパラメーターを使う方法、関数がパラメーターについて行う想定、終了するときに行う保証を記述することにより、スタティック コード分析の精度と完全性を高めることができます。
- 64 ビット C++ プロジェクトのサポート。

#### <a name="updated-unit-test-framework"></a>更新された単体テスト フレームワーク

Visual Studio の新しい C++ 単体テスト フレームワークを使って、C++ の単体テストを記述します。 [新しいプロジェクト] ダイアログ ボックスの Visual C++ カテゴリで C++ 単体テスト プロジェクト テンプレートを探して、新しい単体テスト プロジェクトを既存の C++ ソリューションに追加します。 Unittest1.cpp ファイルに生成された TEST_METHOD コード スタブに、単体テストを記述します。 テスト コードを記述したら、ソリューションをビルドします。 テストを実行するときは、 **[表示]**  >  **[その他のウィンドウ]**  >  **[単体テスト エクスプローラー]** を選んで **[単体テスト エクスプローラー]** ウィンドウを開いた後、目的のテスト ケースのショートカット メニューで **[選択したテストの実行]** を選びます。 テストの実行が終了した後は、テスト結果と追加のスタック トレース情報を同じウィンドウに表示することができます。

#### <a name="architecture-dependency-graphs"></a>アーキテクチャの依存関係グラフ

コードをより深く理解するため、ソリューションのバイナリ、クラス、名前空間、インクルード ファイルの依存関係グラフを生成できるようになりました。 メニュー バーで **[アーキテクチャ]**  >  **[依存関係グラフの生成]** の順に選び、 **[ソリューション対象]** または **[インクルード ファイルの場合]** を選んで依存関係グラフを生成します。 グラフの生成が完了すると、各ノードを展開して調査し、ノード間を移動して依存関係を理解し、ノードのショートカット メニューの **[コンテンツの表示]** を選んでソース コードを参照することができます。 インクルード ファイルの依存関係グラフを生成するには、\*.cpp ソース コード ファイルまたは \*.h ヘッダー ファイルのショートカット メニューで、 **[インクルード ファイルのグラフを生成]** を選びます。

#### <a name="architecture-explorer"></a>アーキテクチャ エクスプローラー

**アーキテクチャ エクスプローラー**を使うと、C++ のソリューション、プロジェクト、またはファイル内のアセットを調べることができます。 メニュー バーから **[アーキテクチャ]**  >  **[Windows]**  >  **[アーキテクチャ エクスプローラー]** の順に選びます。 関心があるノードを選びます ( **[クラス ビュー]** など)。 この場合、ツール ウィンドウの右側に名前空間の一覧が展開されます。 名前空間を選ぶと、新しい列にその名前空間のクラス、構造体、列挙型の一覧が表示されます。 これらのアセットの調査を続けることも、左端の列に戻って別のクエリを始めることもできます。 「**アーキテクチャ エクスプローラーを使用したコードの検索**」をご覧ください。

#### <a name="code-coverage"></a>コード カバレッジ

実行時にバイナリを動的にインストルメント化するように、コード カバレッジが更新されました。 これにより、構成のオーバーヘッドが減り、パフォーマンスが向上します。 また、C++ アプリの単体テストからコード カバレッジ データを収集することもできます。 C++ の単体テストを作成してある場合は、**単体テスト エクスプローラー**を使ってソリューション内のテストを検出できます。 単体テストを実行し、そのコード カバレッジ データを収集するには、**単体テスト エクスプローラー**で **[コード カバレッジの分析]** を選びます。 **[コード カバレッジの結果]** ウィンドウでコード カバレッジの結果を調べることができます。メニュー バーで、 **[テスト]**  >  **[Windows]**  >  **[コード カバレッジの結果]** を選びます。

## <a name="whats-new-for-c-in-visual-studio-2010"></a>Visual Studio 2010 での C++ の新機能

### <a name="c-compiler-and-linker"></a>C++ のコンパイラとリンカー

**auto キーワード** **auto** キーワードには、新しい用途が追加されています。 **auto** キーワードの既定の意味を使って、変数の宣言の中の初期化式から推測される型の変数を宣言します。 `/Zc:auto` コンパイラ オプションでは、**auto** キーワードの新しい意味または以前の意味のどちらかが呼び出されます。

**decltype 型指定子。** **decltype** 型指定子は、指定された式の型を返します。 **decltype** 型指定子を **auto** キーワードと組み合わせて使い、複雑な型またはそのコンパイラのみで認識される型を宣言できます。 たとえば、この組み合わせを使って、テンプレート引数の型に応じた戻り値の型を持つテンプレート関数を宣言します。 または、別の関数を呼び出し、呼び出した関数の戻り値の型を返すテンプレート関数を宣言できます。

**ラムダ式。** ラムダ関数には、関数本体があるだけで名前はありません。 ラムダ関数は、関数ポインターと関数オブジェクトの最も良い部分を組み合わせています。 ラムダ関数は、それ自体を関数オブジェクトの代わりにテンプレート関数のパラメーターとして使うか、または型がラムダの変数を宣言するために **auto** キーワードと一緒に使います。

**rvalue 参照。** rvalue 参照宣言子 (&&) では、rvalue への参照を宣言します。 rvalue 参照を使うと、移動セマンティクスおよび完全転送を使って、より効率的なコンストラクター、関数、テンプレートを記述できます。

**static_assert 宣言。** **static_assert** 宣言は、実行時にテストするその他のアサーションのしくみと異なり、コンパイル時にソフトウェアのアサーションをテストします。 アサーションが失敗した場合は、コンパイルはエラーになり、指定されたエラー メッセージが発行されます。

**nullptr キーワードと __nullptr キーワード。** MSVC では、**nullptr** キーワードをネイティブ コードまたはマネージド コードと共に使うことができます。 **nullptr** キーワードは、オブジェクト ハンドル、内部ポインター、またはネイティブ ポインターの型がオブジェクトを指していない状態を示します。 **nullptr** は、`/clr` コンパイラ オプションが指定された場合はマネージド コード、`/clr` オプションが指定されていない場合はネイティブ コードとして解釈されます。
Microsoft 固有の **__nullptr** キーワードは **nullptr** と同じ意味ですが、ネイティブ コードに対してのみ適用されます。 ネイティブ C/C++ コードを `/clr` コンパイラ オプションを使ってコンパイルする場合、コンパイラでは、**nullptr** キーワードがネイティブかマネージドかを判断できません。 コンパイラに意図を明確に伝えるため、マネージド コードを指定するには nullptr キーワードを使い、ネイティブ コードを指定するには **__nullptr** キーワードを使います。

**/Zc:trigraphs コンパイラ オプション。** 既定では、トライグラフのサポートは無効です。 トライグラフのサポートを有効にするには、`/Zc:trigraphs` コンパイラ オプションを使用します。
トライグラフは、2 つの連続する疑問符 (??) と、一意の 3 番目の文字で構成されます。 コンパイラはトライグラフを対応する区切り文字に置き換えます。 たとえば、コンパイラは ??= というトライグラフを # 文字 (シャープ記号) で置き換えます。 トライグラフは、特定の区切り文字を含まない文字セットを使う C ソース ファイルで使います。

**新しいガイド付き最適化のプロファイル オプション。** PogoSafeMode はガイド付き最適化のプロファイルの新しいオプションであり、アプリケーションを最適化するときに、セーフ モードと高速モードのどちらにするかを指定できます。 セーフ モードはスレッド セーフですが、高速モードより低速になります。 高速モードが既定の動作です。

**新しい共通言語ランタイム (CLR) オプション /clr:nostdlib。** `/clr` (共通言語ランタイムのコンパイル) 用に新しいオプションが追加されました。 同じライブラリの異なるバージョンが含まれている場合は、コンパイル エラーが発生します。 新しいオプションでは、指定したバージョンをプログラムで使用できるように、既定の CLR ライブラリを除外できます。

**新しいプラグマ ディレクティブ detect_mistmatch。** プラグマ ディレクティブ detect_mismatch により、同じ名前の他のタグと比較されるタグをファイルに配置できます。 同じ名前の複数の値がある場合、リンカーはエラーを生成します。

**XOP 組み込み、FMA4 組み込み、LWP 組み込み。** Visual Studio 2010 SP1 用に追加された XOP 組み込み 、Visual Studio 2010 SP1 用に追加された FMA4 組み込み、Visual Studio 2010 SP1 プロセッサ技術用に追加された LWP 組み込みをサポートするために、新しい組み込み関数が追加されました。 __cpuid、__cpuidex を使うと、特定のコンピューターにどのコプロセッサ技術がサポートされるかを確認できます。

### <a name="visual-studio-c-projects-and-the-build-system"></a>Visual Studio C++ プロジェクトとビルド システム

**MSBuild。** Visual C++ ソリューションおよびプロジェクトは、VCBuild.exe に代わる MSBuild.exe を使ってビルドするようになりました。 MSBuild は、柔軟で拡張性のある XML ベースのビルド ツールであり、他の Visual Studio 言語やプロジェクトの種類でも使われます。 この変更により、Visual Studio C++ プロジェクト ファイルは XML ファイル形式になり、ファイル名拡張子は .vcxproj になります。 以前のバージョンの Visual Studio からの Visual Studio C++ プロジェクト ファイルは、新しいファイル形式に自動的に変換されます。

**VC++ ディレクトリ。** VC++ ディレクトリの設定が、2 つの場所になりました。 VC++ ディレクトリのプロジェクトごとの値を設定するには、プロジェクトのプロパティ ページを使います。 VC++ ディレクトリの、グローバルな構成ごとの値を設定するには、**プロパティ マネージャー**およびプロパティ シートを使います。

**プロジェクト間の依存関係。** 以前のリリースでは、定義されたプロジェクト間の依存関係はソリューション ファイルに格納されていました。 これらのソリューションが新しいプロジェクト ファイル形式に変換されると、依存関係は、プロジェクト間参照に変換されます。 ソリューションの依存関係の概念とプロジェクト間参照の概念は異なるため、この変更によってアプリケーションに影響が生じることがあります。

**マクロと環境変数。** 新しい _ITERATOR_DEBUG_LEVEL マクロは、反復子に対するデバッグのサポートを呼び出します。 このマクロは、以前の _SECURE_SCL マクロおよび _HAS_ITERATOR_DEBUGGING マクロの代わりに使います。

### <a name="visual-c-libraries"></a>Visual C++ のライブラリ

**コンカレンシー ランタイム ライブラリ。** コンカレンシー ランタイム フレームワークは、同時に実行されるアプリケーションやコンポーネントをサポートし、Visual C++ でコンカレンシーアプリケーションをプログラミングするためのフレームワークとなっています。 並列パターン ライブラリ (PPL) では、同時実行アプリケーション プログラミングをサポートするために、粒度の細かい並列化を実行するための汎用目的コンテナーおよびアルゴリズムが用意されています。 非同期エージェント ライブラリは、アクターベースのプログラミング モデルと、粒度の粗いデータ フローおよびパイプライン処理タスクのメッセージ パッシング インターフェイスの役割も果たします。

**標準 C++ ライブラリ。** 次のリストは、標準 C++ ライブラリに対して行われた変更の一部を示しています。

- 新しい rvalue 参照 C++ 言語機能は、標準テンプレート ライブラリの多くの関数で移動セマンティクスおよび完全転送を実装するために使われています。 移動セマンティクスと完全転送は、変数またはパラメーターの割り当て操作のパフォーマンスを大幅に向上させます。
- rvalue 参照はまた、新しい `unique_ptr` クラスを実装するためにも使用されています。これは `auto_ptr` クラスより安全なスマート ポインター型です。 `unique_ptr` クラスは、移動可能ですがコピー可能ではなく、安全性に影響を及ぼさずに厳密な所有権セマンティクスを実装し、rvalue 参照を認識するコンテナーに適しています。 `auto_ptr` クラスの使用は非推奨とされます。
- 15 個の新しい関数、たとえば `find_if_not`、`copy_if`、`is_sorted` が、\<algorithm> ヘッダーに追加されました。
- \<memory> ヘッダーの新しい make_shared 関数は、オブジェクトの作成時に、そのオブジェクトに共有ポインターを作成するための便利で堅牢かつ効率的な方法です。
- シングル リンク リストは \<forward_list> ヘッダーによってサポートされています。
- 新しい `cbegin`、`cend`、`crbegin`、`crend` の各メンバー関数には、コンテナーで前方または後方に移動する `const_iterator` が用意されています。
- \<system_error> ヘッダーおよび関連テンプレートは、低レベルのシステム エラーの処理をサポートします。 `exception_ptr` クラスのメンバーは、スレッド間で例外を転送するために使うことができます。
- \<codecvt> ヘッダーは、Unicode 文字のさまざまなエンコードから他のエンコードへの変換をサポートします。
- \<allocators> ヘッダーは、ノード ベース コンテナーのためにメモリ ブロックの割り当てと解放を行うための各種テンプレートを定義します。
- \<random> ヘッダーにはさまざまな更新があります。

### <a name="microsoft-foundation-class-mfc-library"></a>Microsoft Foundation Class (MFC) ライブラリ

**Windows 7 の機能。** MFC は Windows 7 の多くの機能をサポートしています。たとえば、リボン ユーザー インターフェイス (UI)、タスク バー、ジャンプ リスト、タブ化されたサムネイル、サムネイルのプレビュー、プログレス バー、アイコン オーバーレイ、検索インデックス作成などがあります。 MFC は Windows 7 の多くの機能を自動的にサポートしているため、既存のアプリケーションを変更する必要がない場合があります。 新しいアプリケーションで他の機能をサポートするには、MFC アプリケーション ウィザードを使って、使う機能を指定します。

**マルチタッチ認識。** MFC はマルチタッチ ユーザー インターフェイスを持つアプリケーションをサポートしています。これには、Microsoft Surface オペレーティング システム用に書かれたアプリケーションが含まれます。 マルチタッチ アプリケーションは、Windows のタッチ メッセージおよびタッチ メッセージの組み合わせであるジェスチャ メッセージを処理できます。 タッチおよびジェスチャのイベントを扱うようアプリケーションを登録しておくと、オペレーティング システムがマルチタッチ イベントをイベント ハンドラーにルーティングします。

**高 DPI の認識。** MFC アプリケーションは、既定で高 DPI 認識になりました。 アプリケーションが高 DPI (High Dots Per Inch) 認識の場合、オペレーティング システムでは、ウィンドウ、テキスト、その他の UI 要素を現在の画面の解像度にスケーリングできます。 つまり、スケーリングされたイメージは正しいレイアウトで表示され、切り取られたり粗くなったりすることはありません。

**再起動マネージャー。** 再起動マネージャーは、アプリケーションが予期せず終了または再起動した場合に、ドキュメントを自動的に保存してアプリケーションを再起動します。 たとえば、自動更新によってアプリケーションが終了した後に、再起動マネージャーを使ってアプリケーションを起動できます。 再起動マネージャーを使うためのアプリケーションの構成方法について詳しくは、「**方法: 再起動マネージャーのサポートを追加する**」をご覧ください。

**CTaskDialog。** `CTaskDialog` クラスは、標準の `AfxMessageBox` の代わりに使用できます。 `CTaskDialog` クラスでは、標準のメッセージ ボックスよりも多くの情報を表示して収集できます。

#### <a name="safeint-library"></a>SafeInt ライブラリ

新しい SafeInt ライブラリは、整数のオーバーフローの原因となる算術演算を安全に実行します。 このライブラリは、異なる種類の整数も比較します。

#### <a name="new-active-template-library-atl-macros"></a>新しい ATL (Active Template Library) マクロ

新しいマクロが ATL に追加され、PROP_ENTRY_TYPE および PROP_ENTRY_TYPE_EX の機能が拡張されました。 PROP_ENTRY_INTERFACE および PROP_ENTRY_INTERFACE_EX では、有効な CLSID のリストを追加できます。 PROP_ENTRY_INTERFACE_CALLBACK および PROP_ENTRY_INTERFACE_CALLBACK_EX では、コールバック関数を指定して、CLSID が有効かどうかを判断できます。

#### <a name="analyze-warnings"></a>/analyze の警告

`/analyze` (Enterprise コード分析) のほとんどの警告が、CRT (C ランタイム) ライブラリ、MFC ライブラリ、ATL ライブラリから削除されました。

#### <a name="animation-and-d2d-support"></a>アニメーションおよび D2D のサポート

MFC でアニメーションと Direct2D グラフィックスがサポートされるようになりました。 MFC ライブラリには、この機能をサポートするための複数の新しい MFC クラスと関数があります。 また、2 つの新しいチュートリアルで、D2D オブジェクトおよびアニメーション オブジェクトをプロジェクトに追加する方法が説明されています。 これらのチュートリアルは、「**チュートリアル: MFC プロジェクトへの D2D オブジェクトの追加**」と「**チュートリアル: MFC プロジェクトへのアニメーションの追加**」です。

### <a name="ide"></a>IDE

**強化された IntelliSense。** Visual C++ の IntelliSense の設計が刷新され、スピードと正確さが増し、より大きいプロジェクトを処理できるようになりました。 IDE はこれを実現するために、開発者がソース コードを表示して変更する方法と、IDE がソリューションを構築するためにソース コードとプロジェクト設定を使う方法を使い分けています。
この役割分担のおかげで、**クラス ビュー**や新しい **[移動]** ダイアログ ボックスなどの参照機能は、以前のコンパイルされないブラウザー (.ncb) ファイルに代わる新しい SQL Server デスクトップ データベース (.sdf) ファイルに基づいたシステムによって処理されます。 クイック ヒント、オート コンプリート、パラメーター ヘルプなどの IntelliSense 機能は、必要な場合にのみ翻訳単位を解析します。 新しい **[呼び出し階層]** ウィンドウなどのハイブリッド機能は、参照機能と IntelliSense 機能の組み合わせを使います。
IntelliSense はその時点で必要な情報のみを処理するため、IDE の反応はより迅速です。 また、より新しい情報を使うため、IDE のビューとウィンドウもさらに正確です。 最後に、IDE インフラストラクチャの組織、機能、スケーラビリティが優れているため、より大きなプロジェクトを処理できます。

**強化された IntelliSense エラー。** IDE では、IntelliSense の障害を引き起こす可能性があるエラーの検出機能が強化され、エラーには赤色の波線が表示されます。 また、IDE により IntelliSense エラーが **[エラー一覧]** ウィンドウにレポートされます。 問題の原因となっているコードを表示するには、 **[エラー一覧]** ウィンドウでエラーをダブルクリックします。

**#include オートコンプリート機能。** IDE では、`#include` キーワードのオートコンプリートがサポートされます。 「`#include`」と入力すると、IDE によって有効なヘッダー ファイルのドロップダウン リスト ボックスが作成されます。 ファイル名の入力を続けると、入力内容に基づいてリストが IDE によりフィルター処理されます。 含めるファイルはリストからいつでも選択できます。 これにより、正確なファイル名を知らなくても、ファイルを簡単に含めることができます。

**移動。** **[移動]** ダイアログ ボックスでは、指定した文字列と一致するすべてのシンボルやファイルをプロジェクト内で検索できます。 検索文字列に追加の文字を入力していくと、検索結果が瞬時に更新されます。 **[結果]** フィードバック フィールドでは、見つかった項目の数が表示され、検索を絞り込む必要性を判断するのに役立ちます。 **[種類/スコープ]** 、 **[位置]** 、および **[プレビュー]** の各フィードバック フィールドは、似た名前の項目を識別するのに役立ちます。 また、この機能を拡張して、他のプログラミング言語をサポートすることもできます。

**並列デバッグとプロファイリング。** Visual Studio デバッガーはコンカレンシー ランタイムを認識し、並列処理アプリケーションのトラブルシューティングに役立ちます。 新しいコンカレンシープロファイラー ツールを使って、アプリケーションの全体的な動作を視覚化できます。 さらに、新しいツール ウィンドウを使って、タスクの状態とその呼び出し履歴も視覚化できます。

**リボン デザイナー。** **リボン デザイナー**とは、MFC リボン UI の作成と変更を行うためのグラフィカル エディターです。 最終的なリボン UI は、XML ベースのリソース ファイル (.mfcribbon-ms) によって表されます。 既存のアプリケーションの場合、何行かのコードを一時的に追加し、**リボン デザイナー**を呼び出すことによって、現在のリボン UI を取り込むことができます。 リボン リソース ファイルが作成された後、手書きのリボン UI コードを、リボン リソースを読み込む少数のステートメントに置き換えることができます。

**呼び出し階層。** **[呼び出し階層]** ウィンドウでは、特定の関数によって呼び出されるすべての関数、または特定の関数を呼び出すすべての関数に移動できます。

### <a name="tools"></a>ツール

**MFC クラス ウィザード。** Visual C++ 2010 では、評価の高かった MFC クラス ウィザード ツールが復活しています。 MFC クラス ウィザードを使うと、ソース ファイルのセットを手作業で変更せずに、クラス、メッセージ、変数を簡単にプロジェクトに追加できます。

**ATL コントロール ウィザード。** ATL コントロール ウィザードでは、`ProgID` フィールドが自動的に設定されなくなりました。 ATL コントロールに `ProgID` がない場合、他のツールを使用できないことがあります。 コントロールに `ProgID` があることを必要とするツールの例としては、 **[Active コントロールの挿入]** ダイアログ ボックスがあります。 このダイアログ ボックスについて詳しくは、「 **[ActiveX コントロールの挿入] ダイアログ ボックス**」をご覧ください。

### <a name="microsoft-macro-assembler-reference"></a>Microsoft Macro Assembler リファレンス

YMMWORD データ型の追加では、Intel Advanced Vector Extensions (AVX) 命令に含まれている、256 ビットのマルチメディア オペランドがサポートされます。

## <a name="whats-new-for-c-in-visual-studio-2008"></a>Visual Studio 2008 での C++ の新機能

### <a name="visual-c-integrated-development-environment-ide"></a>Visual C++ 統合開発環境 (IDE: Integrated Development Environment)

- ATL、MFC、Win32 の各アプリケーション内に作成されたダイアログ ボックスが、Windows Vista スタイル ガイドラインに準拠するようになりました。 Visual Studio 2008 を使って新しいプロジェクトを作成すると、アプリケーション内に挿入したダイアログ ボックスはすべて、Windows Vista スタイル ガイドラインに準拠します。 旧バージョンの Visual Studio で作成したプロジェクトを再コンパイルした場合、既存のダイアログ ボックスは以前と同じ外観になります。 アプリケーションにダイアログ ボックスを挿入する方法について詳しくは、「**ダイアログ エディター**」をご覧ください。

- **ATL プロジェクト** ウィザードに、すべてのユーザーについてコンポーネントを登録するオプションが追加されました。 Visual Studio 2008 以降では、**ATL プロジェクト** ウィザードで作成された COM コンポーネントとタイプ ライブラリは、 **[すべてのユーザーについてコンポーネントを登録]** を選択した場合を除いて、レジストリの HKEY_CURRENT_USER ノードに登録されます。
- **ATL プロジェクト** ウィザードから、属性付き ATL プロジェクトを作成するオプションがなくなりました。 Visual Studio 2008 以降の **ATL プロジェクト** ウィザードには、新しいプロジェクトの属性付きステータスを変更するオプションがありません。 ウィザードで作成される新しい ATL プロジェクトはすべて属性なしになります。
- レジストリへの書き込みをリダイレクトできるようになりました。 Windows Vista の導入に伴い、レジストリの一部の領域への書き込みの際に、プログラムをシステム特権のあるモードで実行することが必要になりました。 Visual Studio を常にシステム特権のあるモードで実行することは望ましくありません。 ユーザーごとのリダイレクトにより、プログラミングを変更せずに、レジストリへの書き込みを HKEY_CLASSES_ROOT から HKEY_CURRENT_USER に自動的にリダイレクトできます。
- **クラス デザイナー**で、ネイティブ C++ コードが限定的にサポートされるようになりました。 以前のバージョンの Visual Studio では、**クラス デザイナー**は Visual C# と Visual Basic でしか使用できませんでした。 C++ ユーザーも、読み取り専用モードだけですが、**クラス デザイナー**を使うことができるようになりました。 C++ で**クラス デザイナー**を使う方法について詳しくは、「**クラス デザイナーにおける Visual C++ コードの使用**」をご覧ください。
- プロジェクト ウィザードに、C++ SQL Server プロジェクトを作成するオプションがなくなりました。 Visual Studio 2008 以降、新しいプロジェクト ウィザードでは C++ SQL Server プロジェクトを作成するオプションがなくなりました。 以前のバージョンの Visual Studio を使用して作成した SQL Server プロジェクトは、今後も適切にコンパイルされ、動作します。

### <a name="visual-c-libraries"></a>Visual C++ のライブラリ

#### <a name="general"></a>全般

- アプリケーションを特定のバージョンの Visual C++ ライブラリにバインドできるようになりました。 アプリケーションが、Visual C++ ライブラリのリリース後に行われた更新に依存している場合があります。 その場合、以前のバージョンのライブラリが存在するコンピューターでアプリケーションを実行すると、予期しない動作が発生する可能性があります。 以前のバージョンのライブラリが存在するコンピューターでアプリケーションが実行されないように、アプリケーションを特定バージョンのライブラリにバインドできるようになりました。

#### <a name="stlclr-library"></a>STL/CLR ライブラリ

- Visual C++ に STL/CLR ライブラリが追加されました。 STL/CLR ライブラリは、標準 C++ ライブラリのサブセットである標準テンプレート ライブラリ (STL: Standard Template Library) のパッケージであり、C++ と .NET Framework の共通言語ランタイム (CLR: Common Language Runtime) で使用します。 STL/CLR を使うと、マネージド環境で STL のすべてのコンテナー、反復子、アルゴリズムを利用できるようになりました。

#### <a name="mfc-library"></a>MFC ライブラリ

- Windows Vista でコモン コントロールがサポートされるようになりました。 Windows Vista の機能のサポートまたは現在の MFC クラスの機能向上のために、18 の新規または既存のクラスに 150 以上のメソッドが追加されました。
- 新しい `CNetAddressCtrl` クラスを使うと、IPv4 アドレス、IPv6 アドレス、または DNS 名を入力して検証できます。
- 新しい `CPagerCtrl` クラスを使うと、Windows のページャー コントロールを簡単に使うことができます。
- また、新しい `CSplitButton` クラスを使うと、Windows の分割ボタン コントロールを簡単に使って、既定またはオプションのアクションを選択できます。

#### <a name="c-support-library"></a>C++ のサポート ライブラリ

- C++ にマーシャリング ライブラリが導入されました。 マーシャリング ライブラリを使うと、最適化された簡単な方法で、ネイティブ環境とマネージド環境との間でデータのマーシャリングを行うことができます。 このライブラリは、PInvoke を使用するような、より複雑で非効率的な方法の代わりになります。 詳しくは、「**C++ におけるマーシャリングの概要**」をご覧ください。

#### <a name="atl-server"></a>ATL Server

- ATL Server が共有ソース プロジェクトとしてリリースされるようになりました。
- ATL サーバーのほとんどのコード ベースは CodePlex 上で共有ソース プロジェクトとしてリリースされており、Visual Studio 2008 の一部としてはインストールされません。 ATL サーバーに関連する一部のファイルは、Visual Studio に含まれなくなりました。 削除されたファイルの一覧については、「**削除された ATL Server ファイル**」をご覧ください。
- atlenc.h の関数とユーティリティ関数のデータ エンコード/デコード クラス、および atlutil.h と atlpath.h のクラスが ATL ライブラリに追加されました。
- Microsoft は、以前のリリースの Visual Studio に含まれていたバージョンの ATL Server を、そのバージョンの Visual Studio がサポートされている間は引き続きサポートします。 CodePlex は ATL Server コードの開発をコミュニティ プロジェクトとして続行します。 Microsoft は CodePlex バージョンの ATL Server をサポートしません。

### <a name="visual-c-compiler-and-linker"></a>Visual C++ のコンパイラとリンカー

#### <a name="compiler-changes"></a>コンパイラに関する変更点

- コンパイラでマネージド インクリメンタル ビルドがサポートされるようになりました。 このオプションを指定した場合、コンパイラは参照アセンブリが変更されたときにコードを再コンパイルしません。 代わりに、インクリメンタル ビルドを実行します。 ファイルの再コンパイルは、変更が依存コードに影響する場合にのみ実行されます。
- ATL Server 関連の属性はサポートされなくなりました。 コンパイラで、ATL Server に直接関連付けられていたいくつかの属性がサポートされなくなりました。 削除された属性の一覧については、「互換性に影響する変更点」をご覧ください。
- コンパイラで Intel Core Microarchitecture がサポートされるようになりました。 コンパイラで、コード生成中に Intel Core Microarchitecture 用の調整が行われます。 この調整は既定で実行され、Pentium 4 およびその他のプロセッサにも役立つため無効にはできません。
- 組み込み命令で AMD および Intel の新しいプロセッサがサポートされるようになりました。 いくつかの新しい組み込み命令で、AMD および Intel の新しいプロセッサの高度な機能がサポートされています。 新しい組み込み命令について詳しくは、「**Supplemental Streaming SIMD Extensions 3 Instructions**」(追加のストリーミング SIMD Extensions 3 命令)、「**Streaming SIMD Extensions 4 Instructions**」(ストリーミング SIMD Extensions 4 命令)、「**SSE4A and Advanced Bit Manipulation Intrinsics**」(SSE4A と高度なビット操作命令)、**AES 組み込み命令**、 **_mm_clmulepi64_si128**、_ **_rdtscp** をご覧ください。
- `__cpuid` 関数が更新されました。 `__cpuid` および `__cpuidex` 関数で、最新バージョンの AMD および Intel のプロセッサの複数の新機能がサポートされるようになりました。 新しい `__cpuidex` 組み込み関数を使うと、最新のプロセッサについてより詳細な情報を収集できます。
- `/MP` コンパイラ オプションにより、合計ビルド時間が短縮されます。 `/MP` オプションを使うと、ファイルを同時にコンパイルするいくつかのプロセスを作成することにより、複数のソース ファイルをコンパイルする合計時間を大幅に短縮できます。 このオプションは、ハイパースレッド、複数のプロセッサ、または複数のコアをサポートするコンピューターで特に便利です。
- `/Wp64` コンパイラ オプションおよび **__w64** キーワードは非推奨とされます。 64 ビット移植性の問題を検出する `/Wp64` コンパイラ オプションと **__w64** キーワードは非推奨となり、コンパイラの将来のバージョンでは削除される予定です。 このコンパイラ オプションとキーワードの代わりに、64 ビット プラットフォームが対象の MSVC を使用します。
- `/Qfast_transcendentals` 超越関数のインライン コードを生成します。
- `/Qimprecise_fwaits` は、`/fp:except` コンパイラ オプションの使用時に、try ブロック内部の fwait コマンドを削除します。

### <a name="linker-changes"></a>リンカーに関する変更点

- Visual C++ リンカー (link.exe) で、実行可能ファイルのマニフェスト ファイルにユーザー アカウント制御情報が組み込まれるようになりました。 この機能は、既定で有効になっています。 この機能を無効にする方法および既定の動作を変更する方法については、「`/MANIFESTUAC` (UAC 情報をマニフェストに組み込む)」をご覧ください。
- Windows Vista の Address Space Layout Randomization 機能を有効にする `/DYNAMICBASE` オプションがリンカーに追加されました。 このオプションは、ロード時にアプリケーションをランダムにリベースするかどうかを示すように実行可能ファイルのヘッダーを変更します。

## <a name="whats-new-for-c-in-visual-studio-2005"></a>Visual Studio 2005 での C++ の新機能

Visual C++ 2005 Service Pack 1 での新機能は以下のとおりです。

### <a name="intrinsics-for-x86-and-x64"></a>x86 と x64 用の組み込み関数

- __halt
- __lidt
- __nop
- __readcr8
- __sidt
- __svm_clgi
- __svm_invlpga
- __svm_skinit
- __svm_stgi
- __svm_vmload
- __svm_vmrun
- __svm_vmsave
- __ud2
- __vmx_off
- __vmx_vmptrst
- __writecr8

### <a name="intrinsics-for-x64-only"></a>x64 のみ用の組み込み関数

- __vmx_on
- __vmx_vmclear
- __vmx_vmlaunch
- __vmx_vmptrld
- __vmx_vmread
- __vmx_vmresume
- __vmx_vmwrite

### <a name="new-language-keywords"></a>新しい言語キーワード

__sptr、__uptr

### <a name="new-compiler-features"></a>新しいコンパイラ機能

このリリースのコンパイラには重大な変更があります。

- 64 ビットのネイティブ コンパイラとクロス コンパイラ。
- `/analyze` (エンタープライズ コード分析) コンパイラ オプションが追加されました。
- `/bigobj` コンパイラ オプションが追加されました。
- `/clr:pure`、`/clr:safe`、`/clr:oldSyntax` が追加されました。 (のちに、Visual Studio 2015 で非推奨になり、Visual Studio 2017 で削除されました。)
- 非推奨のコンパイラ オプション: このリリースでは、多くのコンパイラ オプションが使われなくなりました。詳しくは、「**Deprecated Compiler Options**」(非推奨のコンパイラ オプション) をご覧ください。
- `/clr` コードのダブル サンキングが減りました。詳しくは、「**ダブル サンキング (C++)** 」をご覧ください。
- `/EH` (例外処理モデル) または `/EHs` は、スロー以外の手段で発生した例外のキャッチに使用できなくなりました。`/EHa` を使用してください。
- `/errorReport` (内部コンパイラ エラーの報告) コンパイラ オプションが追加されました。
- `/favor` (64 用の最適化) コンパイラ オプションが追加されました。
- `/FA`、`/Fa` (リスティング ファイル) コンパイラ オプションが追加されました。
- `/FC` (診断時のソース コード ファイルの完全パス) コンパイラ オプションが追加されました。
- `/fp` (浮動小数点の動作の指定) コンパイラ オプションが追加されました。
- `/G` (プロセッサの最適化) コンパイラ オプションが追加されました。
- `/G` (プロセッサの最適化) コンパイラ オプションが追加されました。
- `/G3`、`/G4`、`/G5`、`/G6`、`/G7`、`/GB` コンパイラ オプションが削除されました。 コンパイラは、すべてのアーキテクチャに対して最適な出力ファイルの作成を試みる "ブレンド モデル" を使うようになりました。
- `/Gf` が削除されました。 代わりに `/GF` (同一文字列の削除) を使います。
- `/GL` (プログラム全体の最適化) が `/CLRHEADER` と互換性を持つようになりました。
- `/GR` が既定でオンになるようになりました。
- `/GS` (バッファーのセキュリティ チェック) が、脆弱なポインター パラメーターをセキュリティで保護するようになりました。 `/GS` が既定でオンになるようになりました。 `/GS` が、`/clr` (共通言語ランタイムのコンパイル) で MSIL に対してコンパイルされた関数で動作するようになりました。
- `/homeparams` (レジスタ パラメーターのスタックへのコピー) コンパイラ オプションが追加されました。
- `/hotpatch` (ホットパッチ可能なイメージの作成) コンパイラ オプションが追加されました。
- インライン関数のヒューリスティックが更新されました。詳しくは、**inline**、 **__inline**、 **__forceinline**、**inline_depth** をご覧ください。
- 多くの新しい組み込み関数が追加され、以前はドキュメントに記載されていなかった多くの組み込み関数が記載されるようになりました。
- 既定で、失敗した新規の呼び出しが例外をスローするようになります。
- `/ML` および `/MLd` コンパイラ オプションが削除されました。 Visual C++ は、シングルスレッドの静的にリンクされた CRT ライブラリをサポートしなくなりました。
- コンパイラは、名前付き戻り値の最適化を実装するようになりました。この機能は、`/O1`、`/O2` (サイズの最小化、実行速度の最大化)、`/Og` (グローバルの最適化)、`/Ox` (最大限の最適化) を指定してコンパイルすると有効になります。
- `/Oa` コンパイラ オプションは削除されましたが、何の警告もなく無視されます。コンパイラのエイリアス方法を指定するには、`noalias` または `restrict__declspec` 修飾子を使います。
- `/Op` コンパイラ オプションが削除されました。 代わりに `/fp` (浮動小数点の動作の指定) を使います。
- OpenMP が Visual C++ でサポートされるようになりました。
- `/openmp` (OpenMP 2.0 サポートの有効化) コンパイラ オプションが追加されました。
- `/Ow` コンパイラ オプションは削除されましたが、何の警告もなく無視されます。 コンパイラのエイリアス方法を指定するには、`noalias` または `restrict__declspec` 修飾子を使います。

### <a name="profile-guided-optimizations"></a>ガイド付き最適化のプロファイル

- `/QI0f` が削除されました。
- `/QIfdiv` が削除されました。
- `/QIPF_B` (B CPU ステップ実行のエラー) コンパイラ オプションが追加されました。
- `/QIPF_C` (C CPU ステップ実行のエラー) コンパイラ オプションが追加されました。
- `/QIPF_fr32` (上位 96 ビットの浮動小数点レジスタの使用の禁止) コンパイラ オプションが追加されました。
- `/QIPF_noPIC` (位置に依存するコードの生成) コンパイラ オプションが追加されました。
- `/QIPF_restrict_plabels` (実行時に関数が作成されないものと仮定) コンパイラ オプションが追加されました。

### <a name="unicode-support-in-the-compiler-and-linker"></a>コンパイラおよびリンカーでの Unicode のサポート

- `/vd` (ディスプレイスメントの無効化) で、構築中 (/vd2) のオブジェクトに対して dynamic_cast 演算子を使用できるようになりました
- `/YX` コンパイラ オプションが削除されました。 代わりに、`/Yc` (プリコンパイル済みヘッダー ファイルの作成) または `/Yu` (プリコンパイル済みヘッダー ファイルの使用) を使います。 ビルド構成から `/YX` を削除し、代わりに何も指定しないと、ビルドが高速になります。
- `/Zc:forScope` が既定でオンになるようになりました。
- `/Zc:wchar_t` が既定でオンになるようになりました。
- `/Zd` コンパイラ オプションが削除されました。 行番号のみのデバッグ情報がサポートされなくなりました。 代わりに `/Zi` を使います (詳しくは、「 **/Z7、/Zi、/ZI (デバッグ情報の形式)** 」をご覧ください)。
- `/Zg` は C ソース コード ファイルでのみ有効になり、C++ ソース コード ファイルでは有効ではなくなりました。
- `/Zx` (デバッグ最適化された Itanium コード) コンパイラ オプションが追加されました。

### <a name="new-language-features"></a>新しい言語機能

- attributeattribute は非推奨となりました。
- `appdomain__declspec` 修飾子が追加されました。
- `__clrcall` 呼び出し規則が追加されました。
- deprecated (C++) **declspec** 修飾子を使って、ユーザーが非推奨のクラスまたは関数にアクセスしようとするとコンパイル時に表示される文字列を指定できるようになりました。
- **dynamic_cast** 演算子で、重大な変更がありました。
- ネイティブ列挙型で、基になる型を指定できるようになりました。
- `jitintrinsicdeclspec` 修飾子が追加されました。
- `noaliasdeclspec` 修飾子が追加されました。
- `process__declspec` 修飾子が追加されました。
- **abstract**、**override**、**sealed** がネイティブ コンパイルで有効になりました。
- **__restrict** キーワードが追加されました。
- `restrictdeclspec` 修飾子が追加されました。
- **__thiscall** がキーワードになりました。
- **__unaligned** キーワードがドキュメントに記載されるようになりました。
- **volatile** (C++) の最適化に関する動作が更新されました。

### <a name="new-preprocessor-features"></a>新しいプリプロセッサ機能

- __CLR_VER 定義済みマクロが追加されました。
- comment (C/C++) プラグマが、リンカー コメントとして `/MANIFESTDEPENDENCY` を受け付けるようになりました。 comment に対する exestr オプションが非推奨となりました。
- `embedded_idl` 属性 (`#import` ディレクティブ) がオプションのパラメーターを受け取るようになりました。
- `fenv_access` プラグマ
- `float_control` プラグマ
- `fp_contract` プラグマ
- グローバル変数がプラグマ マネージド、プラグマ アンマネージド、アンマネージドの各セクションにある場合、グローバル変数は宣言されている順序で初期化されません。 これは、たとえば、アンマネージド グローバル変数がマネージド グローバル変数で初期化され、完全に構築されたマネージド オブジェクトが必要な場合などに、互換性に影響する変更になる可能性があります。
- init_seg で指定されたセクションは、以前のバージョンでは読み取り/書き込みでしたが、読み取り専用になりました。
- inline_depth の既定値が 16 になりました。 既定値 16 は、Visual C++ .NET 2003 でも有効でした。
- _INTEGRAL_MAX_BITS 定義済みマクロが追加されました。「定義済みマクロ」をご覧ください。
- _M_CEE、_M_CEE_PURE、_M_CEE_SAFE 定義済みマクロが追加されました。「定義済みマクロ」をご覧ください。
- _M_IX86_FP 定義済みマクロが追加されました。
- _M_X64 定義済みマクロが追加されました。
- `make_public` プラグマ
- `managed`、`unmanaged` プラグマの構文が更新されました (`push` と `pop` を持つようになりました)
- mscorlib.dll が、すべての `/clr` コンパイルの `#using` ディレクティブによって暗黙的に参照されるようになりました。
- _OPENMP 定義済みマクロが追加されました。
- optimize プラグマが更新され、a と w は有効なパラメーターではなくなりました。
- no_registry#import 属性が追加されました。
- `region`、`endregion` プラグマが追加されました
- _VC_NODEFAULTLIB 定義済みマクロが追加されました。
- 可変個引数マクロが実装されるようになりました。
- `vtordisp` が非推奨となりました。今後の Visual C++ バージョンからは削除されます。
- `warning` プラグマに suppress 指定子が追加されました。

### <a name="new-linker-features"></a>リンカーの新機能

- モジュール (非アセンブリ MSIL 出力ファイル) が、リンカーへの入力として許可されるようになりました。
- `/ALLOWISOLATION` (マニフェスト検索) リンカー オプションが追加されました。
- `/ASSEMBLYRESOURCE` (マネージド リソースの埋め込み) が更新され、アセンブリ内のリソース名の指定、およびリソースがアセンブリ内でプライベートであることの指定ができるようになりました。
- `/CLRIMAGETYPE` (CLR イメージのタイプの指定) リンカー オプションが追加されました。
- `/CLRSUPPORTLASTERROR` (PInvoke 呼び出しの最終エラー コードの保持) リンカー オプションが追加されました。
- `/CLRTHREADATTRIBUTE` (CLR スレッド属性の設定) リンカー オプションが追加されました。
- `/CLRUNMANAGEDCODECHECK` (SuppressUnmanagedCodeSecurityAttribute の追加) リンカー オプションが追加されました。
- `/ERRORREPORT` (内部リンカー エラーの報告) リンカー オプションが追加されました。
- `/EXETYPE` リンカー オプションが削除されました。 リンカーは、Windows 95 および Windows 98 のデバイス ドライバーの作成をサポートしなくなりました。 これらのデバイス ドライバーを作成するには、適切な DDK を使います。 EXETYPE キーワードが、モジュール定義ファイルに対して有効ではなくなりました。
- `/FUNCTIONPADMIN` (ホットパッチ可能なイメージの作成) リンカー オプションが追加されました。
- `/LTCG` リンカー オプションが、`/clr` でコンパイルされたモジュールでサポートされるようになりました。 また、`/LTCG` はガイド付き最適化のプロファイルをサポートするように更新されました。
- `/MANIFEST` (side-by-side アセンブリ マニフェストを作成する) リンカー オプションが追加されました。
- `/MANIFESTDEPENDENCY` (マニフェストの依存関係を指定する) リンカー オプションが追加されました。
- `/MANIFESTFILE` (マニフェスト ファイルに名前を付ける) リンカー オプションが追加されました。
- `/MAPINFO:LINES` リンカー オプションが削除されました。
- `/NXCOMPAT` (データ実行防止との互換性) リンカー オプションが追加されました。
- `/PGD` (ガイド付き最適化のプロファイル用データベースの指定) リンカー オプションが追加されました。
- `/PROFILE` (パフォーマンス ツール プロファイラー) リンカー オプションが追加されました。
- `/SECTION` (セクション属性の指定) リンカー オプションが、属性の否定をサポートするようになり、L または D (VxD 関連) 属性をサポートしなくなりました。
- コンパイラおよびリンカーでの Unicode のサポート
- `/VERBOSE` (進行状況メッセージの出力) リンカー オプションが、ICF および REF も受け付けるようになりました。
- `/VXD` リンカー オプションが削除されました。 リンカーは、Windows 95 および Windows 98 のデバイス ドライバーの作成をサポートしなくなりました。 これらのデバイス ドライバーを作成するには、適切な DDK を使います。 VXD キーワードが、モジュール定義ファイルに対して有効ではなくなりました。
- `/WS` リンカー オプションが削除されました。 `/WS` は、Windows NT 4.0 を対象とするイメージの変更に使われていました。 `/WS` の代わりに、IMAGECFG.exe -R <ファイル名> を使うことができます。 IMAGECFG.exe は、Windows NT 4.0 CD-ROM の SUPPORT\DEBUG\I386\IMAGECFG.EXE にあります。
- `/WX` (リンカー警告をエラーとして扱う) リンカー オプションがドキュメントに記載されるようになりました。

### <a name="new-linker-utility-features"></a>リンカー ユーティリティの新機能

- `/ALLOWISOLATION` editbin オプションが追加されました
- DESCRIPTION モジュール定義ファイル ステートメントが削除されました。 リンカーは、仮想デバイス ドライバーのビルドをサポートしなくなりました。
- `/ERRORREPORT` オプションが、bscmake.exe、dumpbin.exe、editbin.exe、lib.exe に追加されました。
- `/LTCG` lib オプションが追加されました。
- `/NXCOMPAT` editbin オプションが追加されました。
- `/RANGE` dumpbin オプションが追加されました。
- `/TLS` dumpbin オプションが追加されました。
- `/WS` editbin オプションが削除されました。 `/WS` は、Windows NT 4.0 を対象とするイメージの変更に使われていました。 `/WS` の代わりに、IMAGECFG.exe -R <ファイル名> を使うことができます。 IMAGECFG.exe は、Windows NT 4.0 CD-ROM の SUPPORT\DEBUG\I386\IMAGECFG.EXE にあります。
- /WX[:NO] lib オプションが追加されました。

### <a name="new-nmake-features"></a>NMAKE の新機能

- `/ERRORREPORT` が追加されました。
- `/G` が追加されました。
- 定義済みのルールが更新されました。
- 「再帰マクロ」に記載されている $(MAKE) マクロが、nmake.exe への完全なパスを提供するようになりました。

### <a name="new-masm-features"></a>MASM の新機能

- MASM の式が 64 ビット値になりました。 以前のバージョンの MASM 式は 32 ビット値でした。
- 命令 __asm int 3 により、関数がネイティブにコンパイルされるようになりました。
- ALIAS (MASM) がドキュメントに記載されるようになりました。
- `/ERRORREPORT` ml.exe and ml64.exe オプションが追加されました。
- .FPO がドキュメントに記載されるようになりました。
- H2INC.exe は Visual C++ 2005 では出荷されません。 引き続き H2INC を使う必要がある場合は、以前のバージョンの Visual C++ の H2INC.exe をお使いください。
- 演算子 IMAGEREL が追加されました。
- 演算子 HIGH32 が追加されました。
- 演算子 LOW32 が追加されました。
- ml64.exe は、x64 アーキテクチャ用の MASM のバージョンです。 x64 .asm ファイルを x64 オブジェクト ファイルにアセンブルします。 インライン アセンブリ言語が x64 コンパイラでサポートされなくなりました。 以下の MASM ディレクティブが ml64.exe (x64) に追加されました。
- .ALLOCSTACK
- .ENDPROLOG
- .PUSHFRAME
- .PUSHREG
- .SAVEREG
- .SAVEXMM128
- .SETFRAME さらに、PROC ディレクティブが x64 専用構文で更新されました。
- MMWORD ディレクティブが追加されました
- `/omf` (ML.exe コマンド ライン オプション) が `/c` を意味するようになりました。 ML.exe が OMF 形式オブジェクトのリンクをサポートしなくなりました。
- SEGMENT ディレクティブが追加属性をサポートするようになりました。
- 演算子 SECTIONREL が追加されました。
- XMMWORD ディレクティブが追加されました

### <a name="new-crt-features"></a>CRT の新機能

- いくつかの関数のセキュリティで保護されたバージョンが追加されました。 これらの関数はより優れた方法でエラーを処理し、より厳密にバッファーを制御して、一般的なセキュリティ侵害を回避するのに役立ちます。 新しいセキュリティで保護されたバージョンは、 **_s** サフィックスによって識別されます。
- 既存の安全性の低いバージョンの関数の多くは非推奨とされました。 廃止の警告を無効にするには、_CRT_SECURE_NO_WARNINGS を定義します。
- 既存の関数の多くは、パラメーターを検証し、無効なパラメーターが渡されたときは無効パラメーター ハンドラーを呼び出します。
- 多くの既存関数は、以前は設定しなかった場所で `errno` を設定するようになりました。
- 整数型の typedef `errno_t` が追加されました。 関数の戻り値の型またはパラメーターが `errno` からのエラー コードを処理するたびに、`errno_t` が使われます。 `errcode` が `errno_t` に置き換えられます。
- ロケールに依存する関数に、現在のロケールを使うのではなく、ロケールをパラメーターとして受け取るバージョンができました。 これらの新しい関数には、 **_l** というサフィックスが付いています。 ロケール オブジェクトを処理するために複数の新しい関数が追加されました。 新しい関数は、`_get_current_locale`、`_create_locale`、`_free_locale` などです。
- ファイル ハンドルのロックおよびロック解除をサポートするために、新しい関数が追加されました。
- `_spawn` ファミリの関数は、以前のバージョンでは成功時に errno をゼロにリセットしていましたが、リセットしなくなりました。
- 引数の使用順序を指定できるバージョンの `printf` 関数ファミリが、使用できるようになりました。
- Unicode がテキスト形式としてサポートされるようになりました。 関数 `_open` が、_O_TEXTW、_O_UTF8、_O_UTF16 の各属性をサポートするようになりました。 `fopen` 関数が、"ccs=ENCODING" で Unicode 形式を指定する方法をサポートするようになりました。
- マネージド コード (MSIL) でビルドされた CRT ライブラリの新しいバージョンが使用できるようになり、`/clr` (共通言語ランタイムのコンパイル) オプションでコンパイルするときに使われます。
- _fileinfo が削除されました。
- `time_t` の既定のサイズが 64 ビットになり、`time_t` および複数の時間関数の範囲が 3000 年まで拡張されました。
- CRT が、スレッド単位でのロケール設定をサポートするようになりました。 この機能をサポートするために、関数 `_configthreadlocale` が追加されました。
- x87 と SSE2 両方の浮動小数点プロセッサで浮動小数点制御ワードにアクセスして制御できるように、`_statusfp2` 関数と `__control87_2` 関数が追加されました。
- 時刻 (tm 構造体) のグリニッジ標準時 (GMT) への変換をサポートするために、`_mkgmtime` 関数と `_mkgmtime64` 関数が追加されました。
- 標準への準拠を向上させるため、`swprintf` と `vswprintf` が変更されました。
- 新しいヘッダー ファイル INTRIN.H で、一部の組み込み関数のプロトタイプが提供されるようになりました。
- `fopen` 関数に N 属性が追加されました。
- `_open` 関数に _O_NOINHERIT 属性が追加されました。
- `atoi` 関数が、オーバーフロー時に INT_MAX を返して `errno` を ERANGE に設定するようになりました。 以前のバージョンでは、オーバーフロー時の動作が定義されていませんでした。
- 関数の `printf` ファミリが、形式種類指定子 %a と %A を使用する ANSI C99 標準に従って実装された 16 進浮動小数点数出力をサポートするようになりました。
- `printf` ファミリが、"ll" (long long) サイズ プレフィックスをサポートするようになりました。
- `_controlfp` 関数が、パフォーマンス向上のために最適化されました。
- 複数の関数のデバッグ バージョンが追加されました。
- `_chgsignl` および `_cpysignl` (long double バージョン) が追加されました。
- `_locale_t` 型が型テーブルに追加されました。
- 配列の要素数の計算用に、新しいマクロ `_countof` が追加されました。
- 各関数のトピックに、等価な .NET Framework のセクションが追加されました。
- 複数の文字列関数に、出力バッファーが小さすぎる場合に失敗するのではなく文字列を切り捨てるオプションが追加されました。 **_TRUNCATE** をご覧ください。
- `_set_se_translator` に対し、`/EHa` コンパイラ オプションの使用が必要になりました。
- `/Za` (C コード用) および __STDC__ が手動に設定されている場合 (C++ コード用) の `fpos_t` が、 **__int64** になりました。 以前は **struct** でした。
- _CRT_DISABLE_PERFCRIT_LOCKS を指定すると、シングルスレッド プログラムの I/O パフォーマンスが向上します。
- POSIX 名が非推奨とされ、ISO C++ に準拠する名前が使われるようになりました (たとえば、`getch` ではなく `_getch` を使います)。
- 新しいリンク オプションの .obj ファイルが、ピュア モードに使用できるようになりました
- `_recalloc` は、`realloc` と `calloc` の機能を結合します。

## <a name="whats-new-for-c-in-visual-studio-2003"></a>Visual Studio 2003 での C++ の新機能

### <a name="compiler"></a>コンパイラ

- 現在のバージョンのコンパイラでビルドされた Managed Extensions for C++ アプリケーションを以前のバージョンのランタイムで実行する方法についての情報。
- Managed Extensions for C++ に関してよく寄せられる質問。
- C++ マネージ拡張を使用する既存のネイティブ アプリケーションを移植する方法を示すチュートリアルが追加されました。チュートリアル: .NET Framework コンポーネントと相互運用する既存のネイティブ C++ アプリケーションを移植します。
- 値の型のメソッドへのデリゲートを作成できるようになりました。
- C++ 標準へのコンパイラの準拠が、Visual C++ .NET 2003 で大幅に強化されました。
- `/arch` コンパイラ オプションが追加されました。
- `/Gf` が非推奨とされ、次のバージョンの Visual C++ では削除されます。
- `/G7` コンパイラ オプションが追加されました。
- 直接バッファー オーバーランからローカル変数を保護するように、`/GS` コンパイラ オプションが強化されました。
- `/noBool` コンパイラ オプションが削除されました。 コンパイラが、C++ ソース コード ファイルのキーワードとしてのみ **bool** の使用を許可するようになりました (識別子としては使用できません)。
- **long long** 型が **__int64** の **typedef** として使用できるようになりました。CRT での **long long** のサポートはまだないことに注意してください。
- `/Zm` コンパイラ オプションが、プリコンパイル済みヘッダーのメモリ割り当て制限を指定するようになりました。
- _InterlockedCompareExchange 組み込み関数がドキュメントに記載されるようになりました。
- _InterlockedDecrement 組み込み関数がドキュメントに記載されるようになりました。
- _InterlockedExchange 組み込み関数がドキュメントに記載されるようになりました。
- _InterlockedExchangeAdd 組み込み関数がドキュメントに記載されるようになりました。
- _InterlockedIncrement 組み込み関数がドキュメントに記載されるようになりました。
- _ReadWriteBarrier 組み込み関数が追加されました。

### <a name="attributes"></a>属性

- `implements` 属性がドキュメントに記載されるようになりました。

### <a name="linker-features"></a>リンカーの機能

次のリンカー スイッチが追加されました。

- /ASSEMBLYDEBUG
- /ASSEMBLYLINKRESOURCE
- DELAYSIGN
- /KEYFILE
- /KEYCONTAINER
- /SAFESEH

### <a name="masm"></a>MASM

.SAFESEH ディレクティブと `/safeseh` ml.exe オプションが追加されました。

## <a name="see-also"></a>関連項目

[Visual C++ 移植とアップグレードのガイド](visual-cpp-porting-and-upgrading-guide.md)
