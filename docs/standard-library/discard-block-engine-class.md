---
title: "discard_block_engine 類別 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: random/std::discard_block_engine
dev_langs: C++
helpviewer_keywords: discard_block_engine class
ms.assetid: aa84808e-38fe-4fa0-9f73-d5b9a653345b
caps.latest.revision: "18"
author: corob-msft
ms.author: corob
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: ca21ef820c4dfe713a5a9b0c969ac0b14e3efe01
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="discardblockengine-class"></a>discard_block_engine 類別
捨棄其基底引擎所傳回的值，以產生隨機序列。  
  
## <a name="syntax"></a>語法  
  
```  
template <class Engine, size_t P, size_t R>  
class discard_block_engine;  
```  
  
#### <a name="parameters"></a>參數  
 `Engine`  
 基底引擎類型。  
  
 `P`  
 **區塊大小**。 每個區塊中的值數目。  
  
 `R`  
 **已使用的區塊**。 每個區塊中使用的值數目。 其餘將會予以捨棄 ( `P` - `R`)。 **前置條件：**`0 < R ≤ P`  
  
## <a name="members"></a>成員  
  
||||  
|-|-|-|  
|`discard_block_engine::discard_block_engine`|`discard_block_engine::base`|`discard_block_engine::discard`|  
|`discard_block_engine::operator()`|`discard_block_engine::base_type`|`discard_block_engine::seed`|  
  
 如需引擎成員的詳細資訊，請參閱 [\<random>](../standard-library/random.md)。  
  
## <a name="remarks"></a>備註  
 此範本類別描述引擎配接器，其可透過捨棄其基底引擎所傳回的一些值來產生值。  
  
## <a name="requirements"></a>需求  
 **標頭：**\<random>  
  
 **命名空間：** std  
  
## <a name="see-also"></a>請參閱  
 [\<random>](../standard-library/random.md)
