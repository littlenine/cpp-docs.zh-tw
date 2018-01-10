---
title: "CDocObjectServer 類別 |Microsoft 文件"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- CDocObjectServer
- AFXDOCOB/CDocObjectServer
- AFXDOCOB/CDocObjectServer::CDocObjectServer
- AFXDOCOB/CDocObjectServer::ActivateDocObject
- AFXDOCOB/CDocObjectServer::OnActivateView
- AFXDOCOB/CDocObjectServer::OnApplyViewState
- AFXDOCOB/CDocObjectServer::OnSaveViewState
dev_langs: C++
helpviewer_keywords:
- CDocObjectServer [MFC], CDocObjectServer
- CDocObjectServer [MFC], ActivateDocObject
- CDocObjectServer [MFC], OnActivateView
- CDocObjectServer [MFC], OnApplyViewState
- CDocObjectServer [MFC], OnSaveViewState
ms.assetid: 18cd0dff-0616-4472-b8d9-66c081bc383a
caps.latest.revision: "23"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: 912262c4f1ba85c181bb30ee5d6f38a0defe5d5d
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="cdocobjectserver-class"></a>CDocObjectServer 類別
實作可讓一般 `COleDocument` 伺服器融入完整 DocObject 伺服器所需的其他 OLE 介面： `IOleDocument`、 `IOleDocumentView`、 `IOleCommandTarget`和 `IPrint`。  
  
## <a name="syntax"></a>語法  
  
```  
class CDocObjectServer : public CCmdTarget  
```  
  
## <a name="members"></a>成員  
  
### <a name="public-constructors"></a>公用建構函式  
  
|名稱|描述|  
|----------|-----------------|  
|[CDocObjectServer::CDocObjectServer](#cdocobjectserver)|建構 `CDocObjectServer` 物件。|  
  
### <a name="public-methods"></a>公用方法  
  
|名稱|描述|  
|----------|-----------------|  
|[CDocObjectServer::ActivateDocObject](#activatedocobject)|啟動文件物件的伺服器，但不會顯示。|  
  
### <a name="protected-methods"></a>保護方法  
  
|名稱|描述|  
|----------|-----------------|  
|[CDocObjectServer::OnActivateView](#onactivateview)|顯示 DocObject 檢視表。|  
|[CDocObjectServer::OnApplyViewState](#onapplyviewstate)|還原 DocObject 檢視表的狀態。|  
|[CDocObjectServer::OnSaveViewState](#onsaveviewstate)|儲存 DocObject 檢視表的狀態。|  
  
## <a name="remarks"></a>備註  
 `CDocObjectServer`衍生自`CCmdTarget`與密切合作及`COleServerDoc`来公開的介面。  
  
 DocObject 伺服器文件可以包含[CDocObjectServerItem](../../mfc/reference/cdocobjectserveritem-class.md) DocObject 項目代表伺服器介面的物件。  
  
 若要自訂 DocObject 伺服器，衍生您自己從`CDocObjectServer`並覆寫其檢視安裝函式， [OnActivateView](#onactivateview)， [OnApplyViewState](#onapplyviewstate)，和[OnSaveViewState](#onsaveviewstate). 您必須提供回應架構會呼叫您類別的新執行個體。  
  
 如需 DocObjects 的進一步資訊，請參閱[CDocObjectServerItem](../../mfc/reference/cdocobjectserveritem-class.md)和[COleCmdUI](../../mfc/reference/colecmdui-class.md)中*MFC 參考*。 另請參閱[網際網路第一個步驟： 主動式文件](../../mfc/active-documents-on-the-internet.md)和[主動式文件](../../mfc/active-documents-on-the-internet.md)。  
  
 另請參閱下列知識庫文件：  
  
-   Q247382: PRB: Server ActiveX 文件中的控制項的工具提示會顯示 ActiveX 文件容器  
  
## <a name="inheritance-hierarchy"></a>繼承階層  
 [CObject](../../mfc/reference/cobject-class.md)  
  
 [CCmdTarget](../../mfc/reference/ccmdtarget-class.md)  
  
 `CDocObjectServer`  
  
## <a name="requirements"></a>需求  
 **標頭：** afxdocob.h  
  
##  <a name="activatedocobject"></a>CDocObjectServer::ActivateDocObject  
 呼叫此函式可啟動 （但不是顯示） 的文件物件的伺服器。  
  
```  
void ActivateDocObject();
```  
  
### <a name="remarks"></a>備註  
 `ActivateDocObject`呼叫`IOleDocumentSite`的**ActivateMe**方法，但不會顯示檢視，因為它會等候如何設定及顯示檢視中，指定的呼叫中的特定指示[CDocObjectServer::OnActivateView](#onactivateview).  
  
 在一起，`ActivateDocObject`和`OnActivateView`啟動並顯示 DocObject 檢視表。 DocObject 啟用不同於其他類型的 OLE 就地啟用。 DocObject 啟動會略過顯示就地影線框線和物件裝飾時 （例如調整大小控點）、 略過物件延伸函式，以及繪製捲軸檢視矩形相對於繪製其外 （如同標準矩形內就地啟用）。  
  
##  <a name="cdocobjectserver"></a>CDocObjectServer::CDocObjectServer  
 建構並初始化 `CDocObjectServer` 物件。  
  
```  
explicit CDocObjectServer(
    COleServerDoc* pOwner,  
    LPOLEDOCUMENTSITE pDocSite = NULL);
```  
  
### <a name="parameters"></a>參數  
 *pOwner*  
 是 DocObject 伺服器的用戶端的用戶端站台文件指標。  
  
 `pDocSite`  
 指標`IOleDocumentSite`容器所實作的介面。  
  
### <a name="remarks"></a>備註  
 DocObject 作用中時，用戶端站台 OLE 介面 ( `IOleDocumentSite`) 就是允許 DocObject 伺服器通訊使用其用戶端 （容器）。 DocObject 伺服器啟動時，它會先檢查容器實作`IOleDocumentSite`介面。 如果是這樣， [COleServerDoc::GetDocObjectServer](../../mfc/reference/coleserverdoc-class.md#getdocobjectserver)稱為容器是否支援 DocObjects。 根據預設，`GetDocObjectServer`傳回**NULL**。 您必須覆寫`COleServerDoc::GetDocObjectServer`建構新`CDocObjectServer`物件或衍生您自己使用指標的物件`COleServerDoc`容器及其`IOleDocumentSite`做為建構函式的引數的介面。  
  
##  <a name="onactivateview"></a>CDocObjectServer::OnActivateView  
 呼叫此函式可顯示 DocObject 檢視表。  
  
```  
virtual HRESULT OnActivateView();
```  
  
### <a name="return-value"></a>傳回值  
 傳回錯誤或警告的值。 根據預設，會傳回**NOERROR**如果成功，否則**E_FAIL**。  
  
### <a name="remarks"></a>備註  
 此函式建立的就地框架視窗、 繪製捲軸檢視內、 設定伺服器以其容器的共用、 加入畫面格的控制項、 設定使用中的物件，則最後顯示的就地框架視窗和將焦點設定功能表。  
  
##  <a name="onapplyviewstate"></a>CDocObjectServer::OnApplyViewState  
 覆寫此函式以還原 DocObject 檢視表的狀態。  
  
```  
virtual void OnApplyViewState(CArchive& ar);
```  
  
### <a name="parameters"></a>參數  
 `ar`  
 A`CArchive`要序列化的檢視狀態的物件。  
  
### <a name="remarks"></a>備註  
 當它執行個體化之後第一次顯示的檢視時，會呼叫此函數。 `OnApplyViewState`指示檢視，以重新初始化本身的資料中根據`CArchive`與先前儲存的物件[OnSaveViewState](#onsaveviewstate)。 檢視必須驗證中的資料`CArchive`物件，因為容器不會嘗試解譯以任何方式的檢視狀態資料。  
  
 您可以使用`OnSaveViewState`來儲存您的檢視狀態的特定的持續性資訊。 如果您覆寫`OnSaveViewState`來儲存資訊，您會想要覆寫`OnApplyViewState`讀取該資訊，並將其套用至您的檢視，當新啟動。  
  
##  <a name="onsaveviewstate"></a>CDocObjectServer::OnSaveViewState  
 覆寫此函式可儲存 DocObject 檢視的額外狀態資訊。  
  
```  
virtual void OnSaveViewState(CArchive& ar);
```  
  
### <a name="parameters"></a>參數  
 `ar`  
 A`CArchive`序列化的檢視狀態的物件。  
  
### <a name="remarks"></a>備註  
 您的狀態可能包含屬性，例如檢視類型、 縮放因數、 插入和選取範圍點等等。 通常，容器會呼叫此函式之前停用檢視。 稍後可以透過還原已儲存的狀態[OnApplyViewState](#onapplyviewstate)。  
  
 您可以使用`OnSaveViewState`來儲存您的檢視狀態的特定的持續性資訊。 如果您覆寫`OnSaveViewState`來儲存資訊，您會想要覆寫`OnApplyViewState`讀取該資訊，並將其套用至您的檢視，當新啟動。  
  
## <a name="see-also"></a>請參閱  
 [CCmdTarget 類別](../../mfc/reference/ccmdtarget-class.md)   
 [階層架構圖表](../../mfc/hierarchy-chart.md)   
 [CDocObjectServerItem 類別](../../mfc/reference/cdocobjectserveritem-class.md)