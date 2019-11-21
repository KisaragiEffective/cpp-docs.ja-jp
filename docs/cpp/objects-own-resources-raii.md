---
title: リソースを所有するオブジェクト (RAII)
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f86b484e-5a27-4c3b-a92a-dfaa5dd6d93a
ms.openlocfilehash: d100d4a9df5d829566e4856594c44dcf4057a329
ms.sourcegitcommit: 654aecaeb5d3e3fe6bc926bafd6d5ace0d20a80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74245591"
---
# <a name="objects-own-resources-raii"></a>リソースを所有するオブジェクト (RAII)

Make sure that objects own resources. This principle is also known as “resource acquisition is initialization” or “RAII.”

## <a name="example"></a>例

Pass every “new” object as a constructor argument to another named object that owns it (almost always unique_ptr).

```cpp
void f() {
    unique_ptr<widget> p( new widget() );
    my_class x( new widget() );
    // ...
} // automatic destruction and deallocation for both widget objects
  // automatic exception safety, as if "finally { p->dispose(); x.w.dispose(); }"
```

Always immediately pass any new resource to another object that owns it.

```cpp
void g() {
    other_class y( OpenFile() );
    // ...
} // automatic closing and release for file resource
  // automatic exception safety, as if "finally { y.file.dispose(); }"
```

## <a name="see-also"></a>関連項目

[Welcome back to C++](../cpp/welcome-back-to-cpp-modern-cpp.md)<br/>
[C++ 言語リファレンス](../cpp/cpp-language-reference.md)<br/>
[.NET 標準ライブラリ](../standard-library/cpp-standard-library-reference.md)
