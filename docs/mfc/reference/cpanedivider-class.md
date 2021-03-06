---
title: CPaneDivider クラス
ms.date: 11/04/2016
f1_keywords:
- CPaneDivider
- AFXPANEDIVIDER/CPaneDivider
- AFXPANEDIVIDER/CPaneDivider::CPaneDivider
- AFXPANEDIVIDER/CPaneDivider::AddPaneContainer
- AFXPANEDIVIDER/CPaneDivider::AddPane
- AFXPANEDIVIDER/CPaneDivider::AddRecentPane
- AFXPANEDIVIDER/CPaneDivider::CalcExpectedDockedRect
- AFXPANEDIVIDER/CPaneDivider::CalcFixedLayout
- AFXPANEDIVIDER/CPaneDivider::CheckVisibility
- AFXPANEDIVIDER/CPaneDivider::CreateEx
- AFXPANEDIVIDER/CPaneDivider::DoesAllowDynInsertBefore
- AFXPANEDIVIDER/CPaneDivider::DoesContainFloatingPane
- AFXPANEDIVIDER/CPaneDivider::FindPaneContainer
- AFXPANEDIVIDER/CPaneDivider::FindTabbedPane
- AFXPANEDIVIDER/CPaneDivider::GetDefaultWidth
- AFXPANEDIVIDER/CPaneDivider::GetFirstPane
- AFXPANEDIVIDER/CPaneDivider::GetPaneDividerStyle
- AFXPANEDIVIDER/CPaneDivider::GetRootContainerRect
- AFXPANEDIVIDER/CPaneDivider::GetWidth
- AFXPANEDIVIDER/CPaneDivider::Init
- AFXPANEDIVIDER/CPaneDivider::InsertPane
- AFXPANEDIVIDER/CPaneDivider::IsAutoHideMode
- AFXPANEDIVIDER/CPaneDivider::IsDefault
- AFXPANEDIVIDER/CPaneDivider::IsHorizontal
- AFXPANEDIVIDER/CPaneDivider::Move
- AFXPANEDIVIDER/CPaneDivider::NotifyAboutRelease
- AFXPANEDIVIDER/CPaneDivider::OnShowPane
- AFXPANEDIVIDER/CPaneDivider::ReleaseEmptyPaneContainers
- AFXPANEDIVIDER/CPaneDivider::RemovePane
- AFXPANEDIVIDER/CPaneDivider::ReplacePane
- AFXPANEDIVIDER/CPaneDivider::RepositionPanes
- AFXPANEDIVIDER/CPaneDivider::Serialize
- AFXPANEDIVIDER/CPaneDivider::SetAutoHideMode
- AFXPANEDIVIDER/CPaneDivider::SetPaneContainerManager
- AFXPANEDIVIDER/CPaneDivider::ShowWindow
- AFXPANEDIVIDER/CPaneDivider::StoreRecentDockSiteInfo
- AFXPANEDIVIDER/CPaneDivider::StoreRecentTabRelatedInfo
- AFXPANEDIVIDER/CPaneDivider::GetPanes
- AFXPANEDIVIDER/CPaneDivider::GetPaneDividers
- AFXPANEDIVIDER/CPaneDivider::m_nDefaultWidth
- AFXPANEDIVIDER/CPaneDivider::m_pSliderRTC
helpviewer_keywords:
- CPaneDivider [MFC], CPaneDivider
- CPaneDivider [MFC], AddPaneContainer
- CPaneDivider [MFC], AddPane
- CPaneDivider [MFC], AddRecentPane
- CPaneDivider [MFC], CalcExpectedDockedRect
- CPaneDivider [MFC], CalcFixedLayout
- CPaneDivider [MFC], CheckVisibility
- CPaneDivider [MFC], CreateEx
- CPaneDivider [MFC], DoesAllowDynInsertBefore
- CPaneDivider [MFC], DoesContainFloatingPane
- CPaneDivider [MFC], FindPaneContainer
- CPaneDivider [MFC], FindTabbedPane
- CPaneDivider [MFC], GetDefaultWidth
- CPaneDivider [MFC], GetFirstPane
- CPaneDivider [MFC], GetPaneDividerStyle
- CPaneDivider [MFC], GetRootContainerRect
- CPaneDivider [MFC], GetWidth
- CPaneDivider [MFC], Init
- CPaneDivider [MFC], InsertPane
- CPaneDivider [MFC], IsAutoHideMode
- CPaneDivider [MFC], IsDefault
- CPaneDivider [MFC], IsHorizontal
- CPaneDivider [MFC], Move
- CPaneDivider [MFC], NotifyAboutRelease
- CPaneDivider [MFC], OnShowPane
- CPaneDivider [MFC], ReleaseEmptyPaneContainers
- CPaneDivider [MFC], RemovePane
- CPaneDivider [MFC], ReplacePane
- CPaneDivider [MFC], RepositionPanes
- CPaneDivider [MFC], Serialize
- CPaneDivider [MFC], SetAutoHideMode
- CPaneDivider [MFC], SetPaneContainerManager
- CPaneDivider [MFC], ShowWindow
- CPaneDivider [MFC], StoreRecentDockSiteInfo
- CPaneDivider [MFC], StoreRecentTabRelatedInfo
- CPaneDivider [MFC], GetPanes
- CPaneDivider [MFC], GetPaneDividers
- CPaneDivider [MFC], m_nDefaultWidth
- CPaneDivider [MFC], m_pSliderRTC
ms.assetid: 8e828a5d-232f-4127-b8e3-7fa45a7a476e
ms.openlocfilehash: d4888fbf2a95652b0a38adc8ecd059a7515636cb
ms.sourcegitcommit: bd7ddc044f9083246614b602ef6a758775313214
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866114"
---
# <a name="cpanedivider-class"></a>CPaneDivider クラス

詳細については、Visual Studio のインストール**の\\VC atlmfc\\\\src mfc**フォルダーにあるソースコードを参照してください。

クラス`CPaneDivider`は、2つのペインを分割するか、ペインの2つのグループを分割するか、メインフレームウィンドウのクライアント領域からペインのグループを分離します。

## <a name="syntax"></a>構文

```
class CPaneDivider : public CBasePane
```

## <a name="members"></a>メンバー

### <a name="public-constructors"></a>パブリック コンストラクター

|名前|説明|
|----------|-----------------|
|[CPaneDivider:: CPaneDivider](#cpanedivider)||

### <a name="public-methods"></a>パブリック メソッド

|名前|説明|
|----------|-----------------|
|[CPaneDivider:: AddPaneContainer](#addpanecontainer)||
|[CPaneDivider:: AddPane](#addpane)||
|[CPaneDivider:: AddRecentPane](#addrecentpane)||
|[CPaneDivider:: CalcExpectedDockedRect](#calcexpecteddockedrect)||
|[CPaneDivider:: CalcFixedLayout](#calcfixedlayout)|( [Cbasepane:: CalcFixedLayout](../../mfc/reference/cbasepane-class.md#calcfixedlayout)をオーバーライドします)。|
|[CPaneDivider:: CheckVisibility](#checkvisibility)||
|[CPaneDivider:: CreateEx](#createex)|( [Cbasepane:: CreateEx](../../mfc/reference/cbasepane-class.md#createex)をオーバーライドします)。|
|[CPaneDivider::D oesAllowDynInsertBefore](#doesallowdyninsertbefore)|( [Cbasepane::D oesallowdyninsertbefore](../../mfc/reference/cbasepane-class.md#doesallowdyninsertbefore)をオーバーライドします)。|
|[CPaneDivider::D oesContainFloatingPane](#doescontainfloatingpane)||
|[CPaneDivider:: FindPaneContainer](#findpanecontainer)||
|[CPaneDivider:: FindTabbedPane](#findtabbedpane)||
|[CPaneDivider:: GetDefaultWidth](#getdefaultwidth)||
|[CPaneDivider:: GetFirstPane](#getfirstpane)||
|[CPaneDivider:: GetPaneDividerStyle](#getpanedividerstyle)||
|[CPaneDivider:: GetRootContainerRect](#getrootcontainerrect)||
|[CPaneDivider:: GetWidth](#getwidth)||
|[CPaneDivider:: Init](#init)||
|[CPaneDivider::InsertPane](#insertpane)||
|[CPaneDivider:: IsAutoHideMode](#isautohidemode)|( [Cbasepane:: IsAutoHideMode](../../mfc/reference/cbasepane-class.md#isautohidemode)をオーバーライドします)。|
|[CPaneDivider:: IsDefault](#isdefault)||
|[CPaneDivider:: IsHorizontal](#ishorizontal)|( [Cbasepane:: IsHorizontal](../../mfc/reference/cbasepane-class.md#ishorizontal)をオーバーライドします)。|
|[CPaneDivider:: Move](#move)||
|[CPaneDivider:: Notifyのリリース](#notifyaboutrelease)||
|[CPaneDivider:: OnShowPane](#onshowpane)||
|[CPaneDivider:: ReleaseEmptyPaneContainers](#releaseemptypanecontainers)||
|[CPaneDivider::RemovePane](#removepane)||
|[CPaneDivider:: ReplacePane](#replacepane)||
|[CPaneDivider:: RepositionPanes](#repositionpanes)||
|[CPaneDivider:: Serialize](#serialize)|( `CBasePane::Serialize`をオーバーライドします)。|
|[CPaneDivider:: SetAutoHideMode](#setautohidemode)||
|[CPaneDivider:: SetPaneContainerManager](#setpanecontainermanager)||
|[CPaneDivider:: ShowWindow](#showwindow)||
|[CPaneDivider:: StoreRecentDockSiteInfo](#storerecentdocksiteinfo)||
|[CPaneDivider:: StoreRecentTabRelatedInfo](#storerecenttabrelatedinfo)||

### <a name="public-methods"></a>パブリック メソッド

|名前|説明|
|----------|-----------------|
|[CPaneDivider:: GetPanes](#getpanes)|[Cpanecontainer クラス](../../mfc/reference/cpanecontainer-class.md)に存在するペインの一覧を返します。 このメソッドは、既定のペインの区分線に対してのみ呼び出す必要があります。|
|[Cpanedivider:: getpanedivitransport](#getpanedividers)|[Cpanecontainer クラス](../../mfc/reference/cpanecontainer-class.md)に存在するペインの区切り線の一覧を返します。 このメソッドは、既定のペインの区分線に対してのみ呼び出す必要があります。|

### <a name="data-members"></a>データ メンバー

|名前|説明|
|----------|-----------------|
|[CPaneDivider:: m_nDefaultWidth](#m_ndefaultwidth)|アプリケーションのすべてのペインの区切り線の既定の幅 (ピクセル単位) を指定します。|
|[CPaneDivider:: m_pSliderRTC](#m_psliderrtc)|派生オブジェクトに関する`CPaneDivider`ランタイムクラス情報へのポインターを保持します。|

## <a name="remarks"></a>Remarks

ペインがドッキング`CPaneDivider`されると、フレームワークによってオブジェクトが自動的に作成されます。

ペインの区切り線には、次の2種類があります。

- ペインのグループをメインフレームウィンドウの横にドッキングすると、既定のペインの区分線が作成されます。 既定のペインの区分線は、 [CPaneContainerManager クラス](../../mfc/reference/cpanecontainermanager-class.md)へのポインターを保持し、ペインのサイズを変更したり、他のウィンドウやコンテナーをドッキングしたりするなど、ウィンドウのグループに対するほとんどの操作をコンテナーマネージャーにリダイレクトします。 各ドッキングペインは、既定のペイン区分線へのポインターを保持します。

- 標準ペインの区切り線は、コンテナー内の2つのペインを分割するだけです。 詳細については、「 [Cpanecontainer クラス](../../mfc/reference/cpanecontainer-class.md)」を参照してください。

## <a name="example"></a>例

`CWorkspaceBar` オブジェクトから `CPaneDivider` オブジェクトを取得する方法を次の例に示します。 このコードスニペットは、 [MDI タブのデモサンプル](../../overview/visual-cpp-samples.md)に含まれています。

[!code-cpp[NVC_MFC_MDITabsDemo#5](../../mfc/reference/codesnippet/cpp/cpanedivider-class_1.cpp)]

## <a name="inheritance-hierarchy"></a>継承階層

[CObject](../../mfc/reference/cobject-class.md)\
└&nbsp;[CCmdTarget](../../mfc/reference/ccmdtarget-class.md)\
&nbsp;&nbsp;&nbsp;&nbsp;└&nbsp;[CWnd](../../mfc/reference/cwnd-class.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└&nbsp;[Cbasepane](../../mfc/reference/cbasepane-class.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└&nbsp;[Cpanedivider](../../mfc/reference/cpanedivider-class.md)

## <a name="requirements"></a>必要条件

**ヘッダー:** afxPaneDivider

##  <a name="setautohidemode"></a>CPaneDivider:: SetAutoHideMode

```
void SetAutoHideMode(BOOL bMode);
```

### <a name="parameters"></a>パラメーター

から*Bmode*<br/>

### <a name="remarks"></a>Remarks

##  <a name="setpanecontainermanager"></a>CPaneDivider:: SetPaneContainerManager

```
void SetPaneContainerManager(CPaneContainerManager* p);
```

### <a name="parameters"></a>パラメーター

から*p*<br/>

### <a name="remarks"></a>Remarks

##  <a name="addpane"></a>  CPaneDivider::AddPane

```
virtual void AddPane(CDockablePane* pBar);
```

### <a name="parameters"></a>パラメーター

から*Pbar*<br/>

### <a name="remarks"></a>Remarks

##  <a name="addpanecontainer"></a>  CPaneDivider::AddPaneContainer

```
virtual BOOL AddPaneContainer(
    CPaneContainerManager& barContainerManager,
    BOOL bOuterEdge);

virtual BOOL AddPaneContainer(
    CDockablePane* pTargetBar,
    CPaneContainerManager& barContainerManager,
    DWORD dwAlignment);
```

### <a name="parameters"></a>パラメーター

から*barContainerManager*<br/>
から*Bouteredge*<br/>
から*Ptargetbar*<br/>
から*dwAlignment*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="addrecentpane"></a>  CPaneDivider::AddRecentPane

```
virtual CDockablePane* AddRecentPane(CDockablePane* pBar);
```

### <a name="parameters"></a>パラメーター

から*Pbar*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="calcexpecteddockedrect"></a>CPaneDivider:: CalcExpectedDockedRect

```
virtual void CalcExpectedDockedRect(
    CWnd* pWndToDock,
    CPoint ptMouse,
    CRect& rectResult,
    BOOL& bDrawTab,
    CDockablePane** ppTargetBar);
```

### <a name="parameters"></a>パラメーター

から*pWndToDock*<br/>
から*Ptmouse*<br/>
から*rectResult*<br/>
から *[Bdrawtab タブ*<br/>
から*Pptargetbar*<br/>

### <a name="remarks"></a>Remarks

##  <a name="calcfixedlayout"></a>  CPaneDivider::CalcFixedLayout

```
virtual CSize CalcFixedLayout(
    BOOL bStretch,
    BOOL bHorz);
```

### <a name="parameters"></a>パラメーター

から*Bstretch*<br/>
から*bHorz*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="checkvisibility"></a>CPaneDivider:: CheckVisibility

```
virtual BOOL CheckVisibility();
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="cpanedivider"></a>CPaneDivider:: CPaneDivider

```
CPaneDivider();

CPaneDivider(
    BOOL bDefaultSlider,
    CWnd* pParent = NULL);
```

### <a name="parameters"></a>パラメーター

から*Bdefaultslider*<br/>
から*Pparent*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="createex"></a>CPaneDivider:: CreateEx

```
virtual BOOL CreateEx(
    DWORD dwStyleEx,
    DWORD dwStyle,
    const RECT& rect,
    CWnd* pParentWnd,
    UINT nID,
    CCreateContext* pContext);
```

### <a name="parameters"></a>パラメーター

から*Dwスタイル ex*<br/>
から*dwStyle*<br/>
から*rect*<br/>
から*pParentWnd*<br/>
から*nID*<br/>
から*pContext*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="doesallowdyninsertbefore"></a>  CPaneDivider::DoesAllowDynInsertBefore

```
virtual BOOL DoesAllowDynInsertBefore() const;
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="doescontainfloatingpane"></a>CPaneDivider::D oesContainFloatingPane

```
virtual BOOL DoesContainFloatingPane();
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="findpanecontainer"></a>  CPaneDivider::FindPaneContainer

```
CPaneContainer* FindPaneContainer(
    CDockablePane* pBar,
    BOOL& bLeftBar);
```

### <a name="parameters"></a>パラメーター

から*Pbar*<br/>
から*bLeftBar*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="findtabbedpane"></a>  CPaneDivider::FindTabbedPane

```
CDockablePane* FindTabbedPane(UINT nID);
```

### <a name="parameters"></a>パラメーター

から*nID*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="getdefaultwidth"></a>  CPaneDivider::GetDefaultWidth

```
static int __stdcall GetDefaultWidth();
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="getfirstpane"></a>  CPaneDivider::GetFirstPane

```
const CBasePane* GetFirstPane() const;
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="getpanedividers"></a>  CPaneDivider::GetPaneDividers

[Cpanecontainer クラス](../../mfc/reference/cpanecontainer-class.md)に存在するペインの区切り線の一覧を返します。 このメソッドは、既定のペインの区分線に対してのみ呼び出す必要があります。

```
void GetPaneDividers(CObList& lstSliders);
```

### <a name="parameters"></a>パラメーター

*lstSliders*<br/>
入出力ペインコンテナーに存在するペインの区分線の一覧が含まれています。

### <a name="remarks"></a>Remarks

このメソッドは、既定のペインの区分線に対してのみ呼び出す必要があります。 既定のペインの区分線は、ペイン全体のサイズを変更するための区分線です。

##  <a name="getpanedividerstyle"></a>CPaneDivider:: GetPaneDividerStyle

```
DWORD GetPaneDividerStyle() const;
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="getpanes"></a>  CPaneDivider::GetPanes

[Cpanecontainer クラス](../../mfc/reference/cpanecontainer-class.md)に存在するペインの一覧を返します。 このメソッドは、既定のペインの区切り線を取得するためにのみ呼び出す必要があります。

```
void GetPanes(CObList& lstBars);
```

### <a name="parameters"></a>パラメーター

*lstBars*<br/>
入出力ペインコンテナーに存在するペインの一覧が含まれます。

### <a name="remarks"></a>Remarks

このメソッドは、既定のペインの区分線に対してのみ呼び出す必要があります。 既定のペインの区分線は、ペイン全体のサイズを変更するための区分線です。

##  <a name="getrootcontainerrect"></a>  CPaneDivider::GetRootContainerRect

```
CRect GetRootContainerRect();
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="getwidth"></a>  CPaneDivider::GetWidth

```
int GetWidth() const;
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="init"></a>  CPaneDivider::Init

```
void Init(
    BOOL bDefaultSlider = FALSE,
    CWnd* pParent = NULL);
```

### <a name="parameters"></a>パラメーター

から*Bdefaultslider*<br/>
から*Pparent*<br/>

### <a name="remarks"></a>Remarks

##  <a name="insertpane"></a>  CPaneDivider::InsertPane

```
virtual BOOL InsertPane(
    CDockablePane* pBarToInsert,
    CDockablePane* pTargetBar,
    DWORD dwAlignment,
    LPCRECT lpRect = NULL);
```

### <a name="parameters"></a>パラメーター

から*pBarToInsert*<br/>
から*Ptargetbar*<br/>
から*dwAlignment*<br/>
から*lpRect*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="isautohidemode"></a>  CPaneDivider::IsAutoHideMode

```
BOOL IsAutoHideMode() const;
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="isdefault"></a>  CPaneDivider::IsDefault

```
BOOL IsDefault() const;
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="ishorizontal"></a>  CPaneDivider::IsHorizontal

```
BOOL IsHorizontal() const;
```

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="m_ndefaultwidth"></a>CPaneDivider:: m_nDefaultWidth

アプリケーション内のすべてのペインの区切り線の既定の幅をピクセル単位で指定します。

```
AFX_IMPORT_DATA static int m_nDefaultWidth;
```

##  <a name="move"></a>  CPaneDivider::Move

```
virtual void Move(
    CPoint& ptOffset,
    BOOL bAdjustLayout = TRUE);
```

### <a name="parameters"></a>パラメーター

から*ptOffset*<br/>
から*bAdjustLayout*<br/>

### <a name="remarks"></a>Remarks

##  <a name="m_psliderrtc"></a>CPaneDivider:: m_pSliderRTC

派生オブジェクトに関する`CPaneDivider`ランタイムクラス情報へのポインターを保持します。

```
AFX_IMPORT_DATA static CRuntimeClass* m_pSliderRTC;
```

### <a name="remarks"></a>Remarks

カスタムペインの区切り線を作成する場合は、このメンバー変数を設定します。 これにより、ペインが描画されたときにフレームワークがペインの区分線を作成できるようになります。

### <a name="example"></a>例

次の例では、メンバー変数`m_pSliderRTC`を設定する方法を示します。

```
class CMySplitter : public CPaneDivider
{
...
};

CPaneDivider::m_pSliderRTC = RUNTIME_CLASS(CMySpliter);
```

##  <a name="notifyaboutrelease"></a>CPaneDivider:: Notifyのリリース

```
virtual void NotifyAboutRelease();
```

### <a name="remarks"></a>Remarks

##  <a name="onshowpane"></a>  CPaneDivider::OnShowPane

```
virtual void OnShowPane(
    CDockablePane* pBar,
    BOOL bShow);
```

### <a name="parameters"></a>パラメーター

から*Pbar*<br/>
から*bShow*<br/>

### <a name="remarks"></a>Remarks

##  <a name="releaseemptypanecontainers"></a>  CPaneDivider::ReleaseEmptyPaneContainers

```
void ReleaseEmptyPaneContainers();
```

### <a name="remarks"></a>Remarks

##  <a name="removepane"></a>  CPaneDivider::RemovePane

```
virtual void RemovePane(CDockablePane* pBar);
```

### <a name="parameters"></a>パラメーター

から*Pbar*<br/>

### <a name="remarks"></a>Remarks

##  <a name="replacepane"></a>  CPaneDivider::ReplacePane

```
virtual BOOL ReplacePane(
    CDockablePane* pBarToReplace,
    CDockablePane* pBarToReplaceWith);
```

### <a name="parameters"></a>パラメーター

から*pBarToReplace*<br/>
から*pBarToReplaceWith*<br/>

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>Remarks

##  <a name="repositionpanes"></a>CPaneDivider:: RepositionPanes

```
virtual void RepositionPanes(
    CRect& rectNew,
    HDWP& hdwp);
```

### <a name="parameters"></a>パラメーター

から*rectNew*<br/>
から*hdwp*<br/>

### <a name="remarks"></a>Remarks

##  <a name="serialize"></a>CPaneDivider:: Serialize

```
void Serialize(CArchive& ar);
```

### <a name="parameters"></a>パラメーター

から*ar*<br/>

### <a name="remarks"></a>Remarks

##  <a name="showwindow"></a>CPaneDivider:: ShowWindow

```
void ShowWindow(int nCmdShow);
```

### <a name="parameters"></a>パラメーター

から*Ncmdshow*<br/>

### <a name="remarks"></a>Remarks

##  <a name="storerecentdocksiteinfo"></a>  CPaneDivider::StoreRecentDockSiteInfo

```
void StoreRecentDockSiteInfo(CDockablePane* pBar);
```

### <a name="parameters"></a>パラメーター

から*Pbar*<br/>

### <a name="remarks"></a>Remarks

##  <a name="storerecenttabrelatedinfo"></a>CPaneDivider:: StoreRecentTabRelatedInfo

```
void StoreRecentTabRelatedInfo(
    CDockablePane* pDockingBar,
    CDockablePane* pTabbedBar);
```

### <a name="parameters"></a>パラメーター

から*Pdocのボタン*<br/>
から*pTabbedBar*<br/>

### <a name="remarks"></a>Remarks

## <a name="see-also"></a>関連項目

[階層図](../../mfc/hierarchy-chart.md)<br/>
[クラス](../../mfc/reference/mfc-classes.md)<br/>
[CPaneContainerManager クラス](../../mfc/reference/cpanecontainermanager-class.md)<br/>
[CPaneContainer クラス](../../mfc/reference/cpanecontainer-class.md)<br/>
[CDockingManager クラス](../../mfc/reference/cdockingmanager-class.md)<br/>
[CBasePane クラス](../../mfc/reference/cbasepane-class.md)
