---
title: main 関数に関する制約
ms.date: 11/04/2016
f1_keywords:
- Main
helpviewer_keywords:
- main function, restrictions on using
ms.assetid: 7b3df731-344b-44a8-850c-11cbcbfbfa83
ms.openlocfilehash: 9ccea987b05c7854e78ba1621fd6c0a065d73d5a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62301839"
---
# <a name="main-function-restrictions"></a>main 関数に関する制約

いくつかの制限が適用されます、**main**関数を他の C++ 関数には適用されません。 **main**関数。

- オーバー ロードできません (を参照してください[関数のオーバー ロード](function-overloading.md))。

- として宣言できません**inline**します。

- として宣言できません**static**します。

- そのアドレスを取得することはできません。

- 呼び出すことはできません。

## <a name="see-also"></a>関連項目

[main:プログラムの起動](../cpp/main-program-startup.md)