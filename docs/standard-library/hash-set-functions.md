---
title: '&lt;hash_set&gt; 関数'
ms.date: 11/04/2016
f1_keywords:
- hash_set/std::swap
- hash_set/std::swap (hash_multiset)
ms.assetid: 557a0162-3728-4537-97dc-f9f6cc7ece94
ms.openlocfilehash: 2fbc05c16ba6629397bbb07bab30cb9315a16e1f
ms.sourcegitcommit: 3e8fa01f323bc5043a48a0c18b855d38af3648d4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78883845"
---
# <a name="lthash_setgt-functions"></a>&lt;hash_set&gt; 関数

|||
|-|-|
|[スワップ](#swap)|[swap (hash_multiset)](#swap_hash_multiset)|

## <a name="swap"></a>  swap

> [!NOTE]
> この API は、互換性のために残されています。 代わりに、[unordered_set クラス](../standard-library/unordered-set-class.md)を使用してください。

2 つの hash_set の要素を交換します。

```cpp
void swap(
    hash_set <Key, Traits, Allocator>& left,
    hash_set <Key, Traits, Allocator>& right);
```

### <a name="parameters"></a>パラメーター

*右*\
交換する要素を提供する hash_set、または hash_set*左側*の要素と交換される要素を持つ hash_set。

*左*\
要素が hash_set*右側*の要素と交換される hash_set。

### <a name="remarks"></a>コメント

`swap` テンプレート関数は、コンテナークラス hash_set に特化したアルゴリズムであり、メンバー関数 `left.`[swap](../standard-library/hash-set-class.md#swap)(`right`) を実行します。 これは、コンパイラによる関数テンプレートの部分的な順序付けのインスタンスです。 テンプレートと関数呼び出しの照合が一意にならないようにテンプレート関数がオーバーロードされた場合、コンパイラは、最も特化したバージョンのテンプレート関数を選択します。 テンプレート関数の一般的なバージョン

**template \<class T> void swap(T&, T&),**

は、algorithm クラスにあり、代入によって機能し、処理は低速です。 各コンテナー内の特化バージョンのほうが、コンテナー クラスの内部表現で使用できるため大幅に高速になります。

### <a name="example"></a>例

[ のテンプレート バージョンの使用例については、メンバー クラス ](../standard-library/hash-set-class.md#swap)hash_set::swap`swap` のコード例をご覧ください。

## <a name="swap_hash_multiset"></a> swap (hash_multiset)

> [!NOTE]
> この API は、互換性のために残されています。 代わりに、[unordered_set クラス](../standard-library/unordered-set-class.md)を使用してください。

2 つの hash_multiset の要素を交換します。

```cpp
void swap(hash_multiset <Key, Traits, Allocator>& left, hash_multiset <Key, Traits, Allocator>& right);
```

### <a name="parameters"></a>パラメーター

*右*\
交換する要素を提供する hash_multiset、または hash_multiset*左側*の要素と交換される要素を持つ hash_multiset。

*左*\
要素が hash_multiset*右側*の要素と交換される hash_multiset。

### <a name="remarks"></a>コメント

`swap` テンプレート関数は、コンテナークラス hash_multiset に特化したアルゴリズムであり、メンバー関数 `left.`[swap](../standard-library/hash-multiset-class.md#swap)(`right`) を実行します。 これは、コンパイラによる関数テンプレートの部分的な順序付けのインスタンスです。 テンプレートと関数呼び出しの照合が一意にならないようにテンプレート関数がオーバーロードされた場合、コンパイラは、最も特化したバージョンのテンプレート関数を選択します。 テンプレート関数の一般的なバージョン

**template \<class T> void swap(T&, T&),**

は、algorithm クラスにあり、代入によって機能し、処理は低速です。 各コンテナー内の特化バージョンのほうが、コンテナー クラスの内部表現で使用できるため大幅に高速になります。

### <a name="example"></a>例

[ のテンプレート バージョンの使用例については、メンバー クラス ](../standard-library/hash-multiset-class.md#swap)hash_multiset::swap`swap` のコード例をご覧ください。

## <a name="see-also"></a>参照

[<hash_set>](../standard-library/hash-set.md)
