---
title: Opf クラス
description: ビルドC++インサイト SDK のクラス参照。
ms.date: 02/12/2020
helpviewer_keywords:
- C++ Build Insights
- C++ Build Insights SDK
- OptICF
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: b7594d573a0e4eaf2e19f306b8a109923ba235dc
ms.sourcegitcommit: 3e8fa01f323bc5043a48a0c18b855d38af3648d4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2020
ms.locfileid: "78334644"
---
# <a name="opticf-class"></a>Opf クラス

::: moniker range="<=vs-2015"

Build C++ Insights SDK は、Visual Studio 2017 以降と互換性があります。 これらのバージョンのドキュメントを表示するには、この記事の Visual Studio バージョンセレクターコントロールを Visual Studio 2017 または Visual Studio 2019 に設定します。

::: moniker-end
::: moniker range=">=vs-2017"

`OptICF` クラスは、 [Matchevent](../functions/match-event.md)、 [matcheventinmemberfunction](../functions/match-event-in-member-function.md)、 [Matcheventstack](../functions/match-event-stack.md)、および[matcheventstackinmemberfunction](../functions/match-event-stack-in-member-function.md)関数と共に使用されます。 [OPT_ICF](../event-table.md#opt-icf)イベントと一致させるには、これを使用します。

## <a name="syntax"></a>構文

```cpp
class OptICF : public Activity
{
public:
    OptICF(const RawEvent& event);
};
```

## <a name="members"></a>メンバー

[アクティビティ](activity.md)基本クラスから継承されたメンバーと共に、`OptICF` クラスには次のメンバーが含まれます。

### <a name="constructors"></a>コンストラクター

[Opf](#opt-icf)

## <a name="opt-icf"></a>Opf

```cpp
OptICF(const RawEvent& event);
```

### <a name="parameters"></a>パラメーター

*event*\
[OPT_ICF](../event-table.md#opt-icf)イベントです。

::: moniker-end
