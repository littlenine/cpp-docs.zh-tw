---
title: ISupportErrorInfoImpl 類別
ms.date: 11/04/2016
f1_keywords:
- ISupportErrorInfoImpl
- ATLCOM/ATL::ISupportErrorInfoImpl
- ATLCOM/ATL::ISupportErrorInfoImpl::InterfaceSupportsErrorInfo
helpviewer_keywords:
- ISupportErrorInfo ATL implementation
- ISupportErrorInfoImpl class
- error information, ATL
ms.assetid: e33a4b11-a123-41cf-bcea-7b19743902af
ms.openlocfilehash: f7e300e30ff0f14b56d2a1bae86b00e090674679
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62274759"
---
# <a name="isupporterrorinfoimpl-class"></a>ISupportErrorInfoImpl 類別

這個類別提供的預設實作[ISupportErrorInfo 介面](/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)方法，可以用於只有單一介面產生物件錯誤時。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
template<const IID* piid>
class ATL_NO_VTABLE ISupportErrorInfoImpl
   : public ISupportErrorInfo
```

#### <a name="parameters"></a>參數

*piid*<br/>
支援介面的 IID 的指標[IErrorInfo](/windows/desktop/api/oaidl/nn-oaidl-ierrorinfo)。

## <a name="members"></a>成員

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[ISupportErrorInfoImpl::InterfaceSupportsErrorInfo](#interfacesupportserrorinfo)|指出介面是否由識別`riid`支援[IErrorInfo](/windows/desktop/api/oaidl/nn-oaidl-ierrorinfo)介面。|

## <a name="remarks"></a>備註

[ISupportErrorInfo 介面](/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)可確保資訊時發生錯誤，可以傳回給用戶端。 物件，使用`IErrorInfo`必須實作`ISupportErrorInfo`。

類別`ISupportErrorInfoImpl`提供的預設實作`ISupportErrorInfo`方法，可以用於只有單一介面產生物件錯誤時。 例如：

[!code-cpp[NVC_ATL_COM#48](../../atl/codesnippet/cpp/isupporterrorinfoimpl-class_1.h)]

## <a name="inheritance-hierarchy"></a>繼承階層

`ISupportErrorInfo`

`ISupportErrorInfoImpl`

## <a name="requirements"></a>需求

**標頭：** atlcom.h

##  <a name="interfacesupportserrorinfo"></a>  ISupportErrorInfoImpl::InterfaceSupportsErrorInfo

指出介面是否由識別`riid`支援[IErrorInfo](/windows/desktop/api/oaidl/nn-oaidl-ierrorinfo)介面。

```
STDMETHOD(InterfaceSupportsErrorInfo)(REFIID riid);
```

### <a name="remarks"></a>備註

請參閱[ISupportErrorInfo::InterfaceSupportsErrorInfo](/windows/desktop/api/oaidl/nf-oaidl-isupporterrorinfo-interfacesupportserrorinfo) Windows SDK 中。

##  <a name="getsize"></a>  IThreadPoolConfig::GetSize

呼叫這個方法來取得集區中的執行緒數目。

```
STDMETHOD(GetSize)(int* pnNumThreads);
```

### <a name="parameters"></a>參數

*pnNumThreads*<br/>
[out]成功時，執行緒數目的集區中接收變數的位址。

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

### <a name="example"></a>範例

[!code-cpp[NVC_ATL_Utilities#134](../../atl/codesnippet/cpp/isupporterrorinfoimpl-class_2.cpp)]

##  <a name="gettimeout"></a>  IThreadPoolConfig::GetTimeout

呼叫這個方法，以取得最長的時間，以毫秒為單位，執行緒集區會等待關閉執行緒。

```
STDMETHOD(GetTimeout)(DWORD* pdwMaxWait);
```

### <a name="parameters"></a>參數

*pdwMaxWait*<br/>
[out]變數的位址，成功時，收到的最長時間的執行緒集區會關閉執行緒等候的毫秒數。

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

### <a name="example"></a>範例

請參閱[IThreadPoolConfig::GetSize](#getsize)。

##  <a name="setsize"></a>  IThreadPoolConfig::SetSize

呼叫此方法以設定集區中的執行緒數目。

```
STDMETHOD(SetSize)int nNumThreads);
```

### <a name="parameters"></a>參數

*nNumThreads*<br/>
執行緒集區中的要求的數目。

如果*nNumThreads*是負數，其絕對值將會乘以中取得的執行緒總數機器的處理器數目。

如果*nNumThreads*為零，若要取得的執行緒總數機器中的處理器數目將會乘以 ATLS_DEFAULT_THREADSPERPROC。

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

### <a name="example"></a>範例

請參閱[IThreadPoolConfig::GetSize](#getsize)。

##  <a name="settimeout"></a>  IThreadPoolConfig::SetTimeout

呼叫這個方法來設定以毫秒為單位，執行緒集區會等待執行緒關閉的時間上限。

```
STDMETHOD(SetTimeout)(DWORD dwMaxWait);
```

### <a name="parameters"></a>參數

*dwMaxWait*<br/>
以毫秒為單位，執行緒集區會等待關閉執行緒要求的最大時間。

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

### <a name="example"></a>範例

請參閱[IThreadPoolConfig::GetSize](#getsize)。

## <a name="see-also"></a>另請參閱

[類別概觀](../../atl/atl-class-overview.md)
