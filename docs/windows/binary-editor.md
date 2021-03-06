---
title: バイナリ エディター (C++)
ms.date: 02/14/2019
f1_keywords:
- vc.editors.binary.F1
- vc.editors.binary
helpviewer_keywords:
- editors, Binary
- resources [C++], editing
- resource editors [C++], Binary editor
- Binary editor
- binary data, editing
- resources [C++], opening for binary editing
- binary data
- hexadecimal bytes in binary data
- strings [C++], searching for
- file searches [C++]
- binary data, finding
- ASCII characters, finding in binary data
- custom resources [C++]
- data resources [C++]
- resources [C++], creating
ms.assetid: 2483c48b-1252-4dbc-826b-82e6c1a0e9cb
ms.openlocfilehash: 832dbf711307b81527bcaff0d1e1b8138f208e46
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62407048"
---
# <a name="binary-editor-c"></a>バイナリ エディター (C++)

> [!CAUTION]
> ダイアログ ボックス、画像、またはメニューなどのリソースの編集、**バイナリ エディター**は危険です。 編集方法が正しくないと、リソースを破損し、本来のエディターで読み取ることができなくなる場合があります。

**バイナリ エディター** 16 進形式または ASCII 形式でバイナリ レベルでリソースを編集することができます。 また、 [[検索] コマンド](/visualstudio/ide/reference/find-command) を使うと、ASCII 文字列や 16 進表現のバイト列を検索できます。 使用して、**バイナリ エディター**カスタム リソースやリソースの種類が Visual Studio 環境でサポートされていない変更を表示またはマイナー必要がある場合のみです。 **バイナリ エディター** Express エディションでは使用できません。

- 開くには、**バイナリ エディター**メニューに移動し、新しいファイルを**ファイル** > **新規** > **ファイル**の種類を選択します。ファイルを編集し、横にドロップダウン矢印を選択する、**オープン**ボタンをクリックし、選択**プログラムから開く** > **バイナリ エディター**します。

- 開くには、**バイナリ エディター**メニューに移動し、既存のファイル**ファイル** > **を開く** > **ファイル**を選択しますファイルを編集し、横にドロップダウン矢印を選択する、**オープン**ボタンをクリックし、選択**プログラムから開く** > **バイナリ エディター**します。

   ![バイナリ エディター](../mfc/media/vcbinaryeditor2.gif "vcBinaryEditor2")<br/>
   表示されるダイアログ ボックスのバイナリ データ、**バイナリ エディター**

特定の ASCII 値のみがで表される、**バイナリ エディター** (0x20 ~ 0x7E)。 拡張文字がピリオドの右側のパネルの ASCII 値セクションで表示されます、**バイナリ エディター**します。 印刷可能な文字は、ASCII 値 32 ~ 126 です。

> [!TIP]
> 使用しているときに、**バイナリ エディター**、多くの場合、リソース固有のコマンドのショートカット メニューを表示する右クリックすることができます。 使用できるコマンドは、ポインターの位置によって異なります。 たとえばをポイントした状態を右クリックして、**バイナリ エディター**で選択された 16 進値では、ショートカット メニューを示しています、**切り取り**、**コピー**、および**貼り付け**コマンド。

## <a name="how-to"></a>方法

**バイナリ エディター**できます。

### <a name="to-open-a-windows-desktop-resource-for-binary-editing"></a>バイナリ編集用に Windows デスクトップ リソースを開くには

1. [リソース ビュー](how-to-create-a-resource-script-file.md#create-resources)で、編集の対象となる特定のリソース ファイルを選択します。

1. リソースを右クリックして**バイナリ データを開く**します。

> [!NOTE]
> 使用する場合、**リソース ビュー** Visual Studio が認識されない書式のリソースを開くウィンドウ RCDATA やカスタム リソースなどのリソースが自動的にで開いたら、**バイナリ エディター**します。

### <a name="to-open-a-managed-resource-for-binary-editing"></a>バイナリ編集の対象となるマネージド リソースを開くには

1. **ソリューション エクスプ ローラー**、編集する特定のリソース ファイルを選択します。

1. リソースを右クリックして**プログラムから開く**します。

1. **[プログラムから開く]** ダイアログ ボックスで、 **バイナリ エディター**を選択します。

> [!NOTE]
> 使用することができます、[イメージ エディター](../windows/image-editor-for-icons.md)と**バイナリ エディター**マネージ プロジェクトのリソース ファイルを使用します。 編集の対象となるマネージド リソースは、リンク リソースである必要があります。 Visual Studio のリソース エディターでは、埋め込みリソースの編集はサポートしていません。

### <a name="to-edit-a-resource"></a>リソースを編集するには

使用する場合、**バイナリ エディター**別のエディター ウィンドウで既に編集中のリソースには、他のエディター ウィンドウをまず閉じています。

1. 編集するバイトを選択します。

   **タブ**キーは、16 進数のセクションでは ASCII とフォーカスを移動、**バイナリ エディター**します。 使用することができます、 **Pageup**と**Pagedown**一度にリソースの 1 つの画面を移動するキー。

1. 新しい値を入力します。

   値は 16 進数と ASCII セクションの両方ですぐに変更し、行の次の値にフォーカスを移動します。

> [!NOTE]
> **バイナリ エディター**エディターを閉じるときに自動的に変更を受け入れます。

### <a name="to-find-binary-data"></a>バイナリ データを検索するには

ASCII 文字列や 16 進数のバイトのいずれかを検索することができます。 たとえば、検索する*こんにちは*、文字列のどちらでも検索できます*こんにちは*または 16 進値、 *48 65 6C 6c 6F*します。

1. メニューに移動して**編集** > [検索](/visualstudio/ide/reference/find-command)します。

1. **検索**ボックス、ドロップダウン リストから、以前の検索文字列を選択または検索するデータを入力します。

1. いずれかの選択、**検索**オプションし、選択**次を検索**します。

### <a name="to-create-a-new-custom-or-data-resource"></a>新しいカスタム リソースやデータ リソースを作成するには

プロジェクトを右クリックして通常のリソース スクリプト (.rc) ファイルの構文を使用して別のファイルに、そのファイルをインクルードし、リソースを配置して、新しいカスタム リソースやデータ リソースを作成する**ソリューション エクスプ ローラー** の選択**リソース インクルード**します。

1. カスタム リソースやデータ リソースが格納される[.rc ファイルを作成します](../windows/how-to-create-a-resource-script-file.md) 。

   null で終わる引用符で囲まれた文字列として、または 10 進数、16 進数、または 8 進数形式の整数として.rc ファイルにカスタム データを入力することができます。

1. **ソリューション エクスプ ローラー**をプロジェクトの .rc ファイルを右クリックし、**リソース ファイルのインクルード**します。

1. **コンパイル時ディレクティブ**ボックスに、入力、`#include`ステートメントなど、カスタムのリソースを含むファイルの名前を指定します。

    ```cpp
    #include mydata.rc
    ```

   入力する構文とスペルが正しいことを確認します。 内容、**コンパイル時ディレクティブ**ボックスは、それらを入力したとおりにリソース スクリプト ファイルに挿入されます。

1. 選択**OK**変更内容を記録します。

カスタム リソースを作成することもできますが、カスタム リソースとしての外部のファイルをインポートしを参照してください、[方法。リソースの管理](../windows/how-to-import-and-export-resources.md)します。

> [!NOTE]
> 新しいカスタム リソースまたはデータ リソースを作成するには、Win32 が必要です。

## <a name="requirements"></a>必要条件

なし

## <a name="see-also"></a>関連項目

[リソース エディター](../windows/resource-editors.md)