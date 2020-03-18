---
title: '&lt;scoped_allocator&gt; 演算子'
ms.date: 11/04/2016
f1_keywords:
- scoped_allocator/std::operator!=
- scoped_allocator/std::operator==
ms.assetid: 4dfe0805-cc6e-479f-887f-a1c164f73837
ms.openlocfilehash: 071fc3b73cd3378b110d6d412bb7575e35a77478
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79425173"
---
# <a name="ltscoped_allocatorgt-operators"></a>&lt;scoped_allocator&gt; 演算子

|||
|-|-|
|[operator!=](#op_neq)|[operator==](#op_eq_eq)|

## <a name="op_neq"></a>  operator!=

2 つの `scoped_allocator_adaptor` オブジェクトが等しくないかどうかをテストします。

```cpp
template <class Outer, class... Inner>
bool operator!=(
    const scoped_allocator_adaptor<Outer, Inner...>& left,
    const scoped_allocator_adaptor<Outer, Inner...>& right) noexcept;
```

### <a name="parameters"></a>パラメーター

*左*\
左側の `scoped_allocator_adaptor` オブジェクト。

*右*\
右側の `scoped_allocator_adaptor` オブジェクト。

### <a name="return-value"></a>戻り値

`!(left == right)`

## <a name="op_eq_eq"></a>  operator==

2 つの `scoped_allocator_adaptor` オブジェクトが等しいかどうかをテストします。

```cpp
template <class Outer, class... Inner>
bool operator==(
    const scoped_allocator_adaptor<Outer, Inner...>& left,
    const scoped_allocator_adaptor<Outer, Inner...>& right) noexcept;
```

### <a name="parameters"></a>パラメーター

*左*\
左側の `scoped_allocator_adaptor` オブジェクト。

*右*\
右側の `scoped_allocator_adaptor` オブジェクト。

### <a name="return-value"></a>戻り値

`left.outer_allocator() == right.outer_allocator() && left.inner_allocator() == right.inner_allocator()`

## <a name="see-also"></a>参照

[<scoped_allocator>](../standard-library/scoped-allocator.md)
