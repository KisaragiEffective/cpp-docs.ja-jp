---
title: parallel_policy クラス
ms.date: 04/18/2019
f1_keywords:
- execution/std::execution::parallel_policy
ms.openlocfilehash: 7bb2b095a50e664dfc585e0bd4aaa608a6ad8e95
ms.sourcegitcommit: 3590dc146525807500c0477d6c9c17a4a8a2d658
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68268964"
---
# <a name="parallelpolicy-class"></a>parallel_policy クラス

並列アルゴリズムのオーバー ロードあいまいさを解消し、並列アルゴリズムの実行を並列化することがあることを示す一意の型として使用されます。

## <a name="syntax"></a>構文

```cpp
class execution::parallel_policy;
```

## <a name="remarks"></a>Remarks

使用の並列アルゴリズムの実行中に、 `execution::parallel_policy` 、キャッチされない例外を使用して、要素アクセス関数の呼び出しが終了した場合、ポリシー`terminate()`呼び出されます。
