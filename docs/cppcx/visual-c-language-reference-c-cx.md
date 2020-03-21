---
title: C++/CX 言語リファレンス
ms.date: 09/15/2017
ms.assetid: 3f6abf92-4e5e-4ed8-8e11-f9252380d30a
ms.openlocfilehash: ed8e2374daf862e99517fb113e869504b7c7aabc
ms.sourcegitcommit: 180f63704f6ddd07a4172a93b179cf0733fd952d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70740861"
---
# <a name="ccx-language-reference"></a>C++/CX 言語リファレンス

C++/CX は言語のC++一連の拡張機能であり、最新C++のものにできるだけ近い表現形式で Windows アプリと Windows ランタイムコンポーネントを作成できます。 C++/CX を使用して、Windows アプリとコンポーネントをネイティブコードで記述しC#ます。このコードは、Visual、Visual Basic、JavaScript など、Windows ランタイムをサポートするその他の言語と簡単にやり取りできます。 生の COM インターフェイスまたは非例外的コードへの直接アクセスを必要とするまれなケースでは、 [Windows ランタイムC++テンプレートライブラリ (wrl)](../windows/windows-runtime-cpp-template-library-wrl.md)を使用できます。

> [!NOTE]
> **/Cx の代替手段としてC++/WinRT をお勧めします。 [ C++](/windows/uwp/cpp-and-winrt-apis/index)** これは、バージョン1803以降の最新の Windows 10 SDK で使用できる Windows ランタイム API 向けの新しい標準 C++ 17 言語のプロジェクションです。 C++/WinRT は、完全にヘッダーファイルに実装され、最新の Windows API に対するファーストクラスのアクセスを提供するように設計されています。
>
> / C++WinRT では、標準に準拠した C++ 17 コンパイラを使用して Windows ランタイム API を使用し、作成することができます。 C++通常、WinRT は、Windows ランタイムの他の言語オプションよりもパフォーマンスが向上し、バイナリが小さくなります。 C++/CX と WRL は引き続きサポートされますが、新しいアプリケーションでは C++/WinRT を使用することを強くお勧めします。 詳細については、「[C++/WinRT](/windows/uwp/cpp-and-winrt-apis/index)」を参照してください。

C++/CX を使用すると、次のものを作成できます。

- C++XAML を使用してユーザーインターフェイスを定義し、ネイティブスタックを使用するユニバーサル Windows プラットフォーム (UWP) アプリ。 詳細については、「 [(UWP) でC++の "hello world" アプリの作成](/windows/uwp/get-started/create-a-basic-windows-10-app-in-cpp)」を参照してください。

- C++JavaScript ベースの Windows アプリで使用できるコンポーネントを Windows ランタイムします。 詳細については、「 [Creating Windows Runtime Components in C++](/windows/uwp/winrt-components/creating-windows-runtime-components-in-cpp)」を参照してください。

- Windows DirectX ゲームやグラフィックス処理の多いアプリ。 詳細については、「 [DirectX を使用した簡単な UWP ゲームの作成](/windows/uwp/gaming/tutorial--create-your-first-uwp-directx-game)」を参照してください。

## <a name="related-articles"></a>関連記事

|||
|-|-|
|[クイック リファレンス](../cppcx/quick-reference-c-cx.md)|/CxのC++キーワードと演算子の表|
|[型システム](../cppcx/type-system-c-cx.md)|/Cx のC++基本的な型とプログラミング構成要素についてC++説明します。また、/cx を使用して Windows ランタイム型を使用および作成する方法について説明します。|
|[アプリとライブラリのビルド](../cppcx/building-apps-and-libraries-c-cx.md)|IDE を使用してアプリを構築し、スタティックライブラリおよび Dll にリンクする方法について説明します。|
|[その他の言語との相互運用](../cppcx/interoperating-with-other-languages-c-cx.md)|/Cx を使用しC++て記述されたコンポーネントを、JavaScript、マネージ言語、または Windows ランタイムC++テンプレートライブラリで記述されたコンポーネントで使用する方法について説明します。|
|[スレッドとマーシャリング](../cppcx/threading-and-marshaling-c-cx.md)|作成するコンポーネントのスレッドとマーシャリングの動作を指定する方法について説明します。|
|[名前空間参照](../cppcx/namespaces-reference-c-cx.md)|既定の名前空間、Platform 名前空間、Platform::Collections、および関連する名前空間の参照ドキュメント。|
|[ユニバーサル Windows プラットフォーム アプリでサポートされていない CRT 関数](../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md)|Windows ランタイム アプリでは使用できない CRT 関数の一覧を示します。|
|[Windows 10 アプリを使ってみる](/windows/uwp/get-started/)|Windows 10 アプリについての全般的な概要と、詳細情報へのリンクがあります。|
|[C++/Cx パート 0/ \[n\]:概要](https://blogs.msdn.microsoft.com/vcblog/2012/08/29/ccx-part-0-of-n-an-introduction/)<br /><br />[C++/Cx パート 1/ \[n\]:単純なクラス](https://blogs.msdn.microsoft.com/vcblog/2012/09/05/ccx-part-1-of-n-a-simple-class/)<br /><br />[C++/Cx パート 2/ \[n\]:磨耗のある種類](https://blogs.msdn.microsoft.com/vcblog/2012/09/17/ccx-part-2-of-n-types-that-wear-hats/)<br /><br />[C++/Cx パート 3 ( \[n\]):構築中](https://blogs.msdn.microsoft.com/vcblog/2012/10/05/ccx-part-3-of-n-under-construction/)<br /><br />[C++/Cx パート 4/ \[n\]:静的メンバー関数](https://blogs.msdn.microsoft.com/vcblog/2012/10/19/ccx-part-4-of-n-static-member-functions/)|/CxのC++入門ブログシリーズです。|
