---
title: WINVER と _WIN32_WINNT の更新
ms.date: 09/04/2017
helpviewer_keywords:
- WINVER in an upgraded Visual Studio C++ project
- _WIN32_WINNT in an upgraded Visual Studio C++ project
ms.assetid: 6a1f1d66-ae0e-48a7-81c3-524d8e8f3447
ms.openlocfilehash: 0cfdb3d065a85bd02ef21de9c4c5282cf54fcb2a
ms.sourcegitcommit: 0cfc43f90a6cc8b97b24c42efcf5fb9c18762a42
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73627256"
---
# <a name="update-winver-and-_win32_winnt"></a>WINVER と _WIN32_WINNT の更新

Visual C++ では、Windows 95、Windows 98、Windows ME、Windows NT、および Windows 2000 がサポート対象外になりました。 **WINVER** マクロまたは **_WIN32_WINNT** マクロをこれらのいずれかのバージョンの Windows に割り当てている場合は、そのマクロを修正する必要があります。 Visual C++ の以前のバージョンを使用して作成したプロジェクトをアップグレードすると、 **WINVER** マクロまたは **_WIN32_WINNT** マクロがサポート対象外になった Windows のバージョンに割り当てられている場合には、そのマクロに関連するコンパイル エラーが発生することがあります。

## <a name="remarks"></a>Remarks

マクロを変更するには、ヘッダー ファイル (たとえば、Windows を対象とするプロジェクトを作成するときに含まれる targetver.h) で、以下の行を追加します。

```C
#define WINVER 0x0A00
#define _WIN32_WINNT 0x0A00
```

これは、Windows 10 オペレーティング システムを対象としています。 これらの値は、各 Windows バージョンのマクロを定義する Windows ヘッダー ファイル SDKDDKVer.h にもリストされています。 SDKDDKVer.h を含める前に、#define ステートメントを追加する必要があります。 Windows の各バージョンの値をエンコードする、SDKDDKVer.h の Windows 10 バージョンの行を次に示します。

```C
//
// _WIN32_WINNT version constants
//
#define _WIN32_WINNT_NT4                    0x0400 // Windows NT 4.0
#define _WIN32_WINNT_WIN2K                  0x0500 // Windows 2000
#define _WIN32_WINNT_WINXP                  0x0501 // Windows XP
#define _WIN32_WINNT_WS03                   0x0502 // Windows Server 2003
#define _WIN32_WINNT_WIN6                   0x0600 // Windows Vista
#define _WIN32_WINNT_VISTA                  0x0600 // Windows Vista
#define _WIN32_WINNT_WS08                   0x0600 // Windows Server 2008
#define _WIN32_WINNT_LONGHORN               0x0600 // Windows Vista
#define _WIN32_WINNT_WIN7                   0x0601 // Windows 7
#define _WIN32_WINNT_WIN8                   0x0602 // Windows 8
#define _WIN32_WINNT_WINBLUE                0x0603 // Windows 8.1
#define _WIN32_WINNT_WINTHRESHOLD           0x0A00 // Windows 10
#define _WIN32_WINNT_WIN10                  0x0A00 // Windows 10
```

表示している SDKDDKVer.h のコピーに Windows のすべてのバージョンがリストされていない場合、古いバージョンの Windows SDK を使用している可能性があります。 既定では、Visual Studio 2017 の Win32 プロジェクトは Windows 10 SDK を使用します。

> [!NOTE]
> アプリケーションに内部 MFC ヘッダーを含めた場合には、値が動作する保証はありません。

`/D` コンパイラ オプションを使用して、このマクロを定義することもできます。 詳細については、「[/D (プリプロセッサの定義)](../build/reference/d-preprocessor-definitions.md)」を参照してください。

これらのマクロの意味について詳しくは、「 [Windows ヘッダーの使用](/windows/win32/WinProg/using-the-windows-headers)」をご覧ください。

## <a name="see-also"></a>関連項目

[Visual C++ の変更履歴](../porting/visual-cpp-change-history-2003-2015.md)
