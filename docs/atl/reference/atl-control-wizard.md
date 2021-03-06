---
title: ATL コントロール ウィザード
ms.date: 11/04/2016
f1_keywords:
- vc.codewiz.class.atl.control.overview
helpviewer_keywords:
- ATL projects, adding controls
- controls [ATL], adding to projects
- ATL Control Wizard
ms.assetid: 991f8e72-ffbc-4382-a4ce-e255acfba5b6
ms.openlocfilehash: 58c3ebe4c2a15aa3f0d59191c37a7f2422a63ab5
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62261209"
---
# <a name="atl-control-wizard"></a>ATL コントロール ウィザード

ATL プロジェクト (または ATL サポートを MFC プロジェクト) への挿入、ATL コントロール。 このウィザードを使用して、3 種類のコントロールのいずれかを挿入することができます。

- 標準コントロール

- 複合コントロール

- DHTML コントロール

さらに、指定できます、最小限のコントロールからインターフェイスを削除する、[インターフェイス](../../atl/reference/interfaces-atl-control-wizard.md)一覧で、ほとんどのコンテナーで開くコントロールの既定値として提供されます。 内のコントロールをサポート インターフェイスを設定することができます、**インターフェイス**ウィザードのページ。

## <a name="remarks"></a>Remarks

このウィザードによって生成された登録スクリプトは、HKEY_LOCAL_MACHINE ではなく HKEY_CURRENT_USER の下には、その COM コンポーネントを登録します。 この動作を変更するには、設定、**コンポーネントをすべてのユーザー登録**ATL ウィザードのオプション。

## <a name="names"></a>名前

オブジェクト、インターフェイス、およびプロジェクトに追加するクラスの名前を指定します。 除く**短い名前**、他のすべてのボックス別に変更することができます。 テキストを変更する場合**短い名前**、このページの他のすべてのボックスの名前に変更が反映されます。 変更する場合、**コクラス**で名前 [COM] セクションで、変更が反映されて、**型**ボックスが、**インターフェイス**名と**ProgID**の操作を行います変更されません。 この名前付けの動作は、コントロールを開発するときに簡単に識別できるように、すべての名前に設計されています。

> [!NOTE]
>  **コクラス**は属性を持たないコントロールのみを編集します。 プロジェクトが考えられる場合は編集できません**コクラス**します。

### <a name="c"></a>C++

オブジェクトを実装するために作成された C++ クラスについて説明します。

- **短い名前**

   オブジェクトの省略名を設定します。 指定した名前は、クラスを決定します。 および**コクラス**ファイルの名前 (します。CPP とします。H) 名、インターフェイス名、および**型**名、フィールドを個別に変更しない限り、します。

- **Class**

   オブジェクトを実装するクラスの名前を設定します。 この名前がで指定した名前に基づいて**短い名前**'C'、クラス名の一般的なプレフィックスが付いた、します。

- **.h ファイル**

   新しいオブジェクトのクラスにヘッダー ファイルの名前を設定します。 既定では、この名前がで指定した名前に基づくは**短い名前**します。 選択した場所にファイル名を保存するには、あるいはクラス宣言を既存のファイルに追加するには、省略記号ボタンをクリックします。 既存のファイルを選択した場合、ウィザードに保存されません、選択した場所まで をクリックします**完了**します。

   ウィザードではファイルは上書きされません。 既存のファイルの名前を選択する場合、**[完了]** をクリックすると、ウィザードからクラス宣言をファイルのコンテンツに追加するかどうかを指定するように求められます。 ファイルを追加するには、**[はい]** をクリックします。ウィザードに戻り、別のファイル名を指定するには、**[いいえ]** をクリックします。

- **.cpp ファイル**

   新しいオブジェクトのクラスに実装ファイルの名前を設定します。 既定では、この名前がで指定した名前に基づくは**短い名前**します。 ファイル名を選択した場所に保存するには、省略記号ボタンをクリックします。 ファイルは、ウィザードで **[完了]** をクリックするまで選択した場所に保存されません。

   ウィザードではファイルは上書きされません。 既存のファイルの名前を選択する場合、**[完了]** をクリックすると、ウィザードからクラスの実装をファイルのコンテンツに追加するかどうかを指定するように求められます。 ファイルを追加するには、**[はい]** をクリックします。ウィザードに戻り、別のファイル名を指定するには、**[いいえ]** をクリックします。

- **属性付き**

   オブジェクトが属性を使用するかどうかを示します。 属性付き ATL プロジェクトにオブジェクトを追加する場合、このオプションが選択されて変更するのには使用できません。 つまり、属性付きオブジェクトのみを属性のサポートで作成されたプロジェクトに追加できます。

   属性付きオブジェクトは、属性を使用する ATL プロジェクトにのみ追加できます。 属性をサポートしていない ATL プロジェクトに対してこのオプションを選択した場合、ウィザードでは、属性のサポートをプロジェクトに追加するかどうかを指定するように求められます。

   既定で、このオプションを設定した後に追加するすべてのオブジェクトを属性として指定されます (チェック ボックスが選択されています)。 属性を使用しないオブジェクトを追加するには、このボックスをオフにすることができます。

   参照してください[アプリケーションの設定、ATL プロジェクト ウィザード](../../atl/reference/application-settings-atl-project-wizard.md)と[属性の基本的なしくみ](../../windows/basic-mechanics-of-attributes.md)詳細についてはします。

### <a name="com"></a>COM

オブジェクトの COM 機能に関する情報を提供します。

- **コクラス**

   オブジェクトによってサポートされるインターフェイスの一覧を含むコンポーネント クラスの名前を設定します。

   > [!NOTE]
   > 属性を使用してプロジェクトを作成するか、指定したこのウィザード ページで、コントロールが属性を使用する場合は、ATL が含まれていないために、このオプションを変更することはできません、**コクラス**属性。

- **Interface**

   オブジェクトのインターフェイスの名前を設定します。 既定では、インターフェイス名は"I"の先頭に追加されます。

- **Type**

   レジストリに表示されるオブジェクトの説明を設定します。

- **ProgID**

   コンテナーは、オブジェクトの CLSID の代わりに使用できる名前を設定します。 このフィールドは自動的に設定されません。 このフィールドを手動で設定しない場合、コントロールは他のツールで使用できません。 なしで生成される ActiveX コントロールなど、`ProgID`では使用できない、 **ActiveX コントロールの挿入** ダイアログ ボックス。 このダイアログ ボックスについて詳しくは、「[[ActiveX コントロールの挿入] ダイアログ ボックス](../../windows/insert-activex-control-dialog-box.md)」をご覧ください。

## <a name="see-also"></a>関連項目

[ATL コントロール](../../atl/reference/adding-an-atl-control.md)<br/>
[複合コントロールに機能を追加する](../../atl/adding-functionality-to-the-composite-control.md)<br/>
[ATL COM オブジェクトの基礎](../../atl/fundamentals-of-atl-com-objects.md)
