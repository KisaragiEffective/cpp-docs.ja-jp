---
title: naked 関数の規則と制限
ms.date: 11/04/2016
helpviewer_keywords:
- naked functions [C++]
ms.assetid: ff203858-2dd3-4a76-8a57-d0d06817adef
ms.openlocfilehash: c813b97b85469165aae892b0a4cce888112e3dc5
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62267377"
---
# <a name="rules-and-limitations-for-naked-functions"></a>naked 関数の規則と制限

## <a name="microsoft-specific"></a>Microsoft 固有の仕様

次の規則と制約が naked 関数に適用されます。

- **return**ステートメントは許可されていません。

- 構造化例外処理コンストラクトと C++ の例外処理コンストラクトは、スタック フレームを越えてアンワインドする必要があるため許可されていません。

- 同じ理由で、`setjmp` の形式は禁止されています。

- `_alloca` 関数の使用は禁止されています。

- プロローグ シーケンスの前にローカル変数の初期化コードが出現しないように、初期化されたローカル変数は関数のスコープ内では許可されません。 特に、C++ オブジェクトの宣言は関数のスコープでは許可されません。 ただし、入れ子になったスコープ内には初期化されたデータが含まれる場合があります。

- フレーム ポインター最適化 (/Oy コンパイラ オプション) は推奨されていませんが、naked 関数に対しては自動的に抑制されます。

- 関数の構文スコープでは C++ クラス オブジェクトを宣言できません。 ただし、入れ子になったブロックではオブジェクトを宣言できます。

- **Naked**でコンパイルするときに、キーワードは無視されます[/clr](../build/reference/clr-common-language-runtime-compilation.md)します。

- [_ _Fastcall](../cpp/fastcall.md) C での参照があるたびに、naked 関数/C++コード プロローグ コードにレジスタ引数のいずれか、その変数のスタックの場所にそのレジスタの値を格納する必要があります。 例:

```cpp
// nkdfastcl.cpp
// compile with: /c
// processor: x86
__declspec(naked) int __fastcall  power(int i, int j) {
   // calculates i^j, assumes that j >= 0

   // prolog
   __asm {
      push ebp
      mov ebp, esp
      sub esp, __LOCAL_SIZE
     // store ECX and EDX into stack locations allocated for i and j
     mov i, ecx
     mov j, edx
   }

   {
      int k = 1;   // return value
      while (j-- > 0)
         k *= i;
      __asm {
         mov eax, k
      };
   }

   // epilog
   __asm {
      mov esp, ebp
      pop ebp
      ret
   }
}
```

**Microsoft 固有の仕様はここまで**

## <a name="see-also"></a>関連項目

[naked 関数呼び出し](../cpp/naked-function-calls.md)