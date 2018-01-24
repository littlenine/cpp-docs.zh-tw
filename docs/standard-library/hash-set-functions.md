---
title: "&lt;hash_set&gt; 函式 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- hash_set/std::swap
- hash_set/std::swap (hash_multiset)
ms.assetid: 557a0162-3728-4537-97dc-f9f6cc7ece94
caps.latest.revision: "7"
manager: ghogen
ms.openlocfilehash: 4fcd6f0d72d31823a0d35108f087f2ad680e2f48
ms.sourcegitcommit: ca2f94dfd015e0098a6eaf5c793ec532f1c97de1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2017
---
# <a name="lthashsetgt-functions"></a>&lt;hash_set&gt; 函式
|||  
|-|-|  
|[swap](#swap)|[swap (hash_multiset)](#swap_hash_multiset)|  
  
##  <a name="swap"></a>  swap  
  
> [!NOTE]
>  這個 API 已過時。 替代方案是 [unordered_set 類別](../standard-library/unordered-set-class.md)。  
  
 交換兩個 hash_set 的元素。  
  
```
void swap(
    hash_set <Key, Traits, Allocator>& left,
    hash_set <Key, Traits, Allocator>& right);
```  
  
### <a name="parameters"></a>參數  
 `right`  
 提供要交換之元素的 hash_set，或要與 hash_set `left` 交換元素的 hash_set。  
  
 `left`  
 要與 hash_set `right` 交換元素的 hash_set。  
  
### <a name="remarks"></a>備註  
 `swap` 範本函式是在容器類別 hash_set 特製化的演算法，用來執行成員函式 `left.`[swap](../standard-library/hash-set-class.md#swap)( `right`)。 這是編譯器所執行之函式樣板的部分排序執行個體。 若因樣板函式多載而導致樣板與函式呼叫的比對不是唯一，則編譯器就會選取特製化程度最高的樣板函式版本。 演算法類別中範本函式的一般版本  
  
 **template \<class T> void swap(T&, T&)**  
  
 會依指派運作而作業緩慢。 每個容器中的特製化版本運作速度會更快，因為它可以與容器類別的內部表示法一起運作。  
  
   
  
### <a name="example"></a>範例  
  如需使用 `swap` 之範本版本的範例，請參閱成員函式 [hash_set::swap](../standard-library/hash-set-class.md#swap) 的程式碼範例。  
  
##  <a name="swap_hash_multiset"></a>  swap (hash_multiset)  
  
> [!NOTE]
>  這個 API 已過時。 替代方案是 [unordered_set 類別](../standard-library/unordered-set-class.md)。  
  
 交換兩個 hash_multiset 的元素。  
  
```
void swap(hash_multiset <Key, Traits, Allocator>& left, hash_multiset <Key, Traits, Allocator>& right);
```  
  
### <a name="parameters"></a>參數  
 `right`  
 提供要交換之元素的 hash_multiset，或要與 hash_multiset `left` 交換元素的 hash_multiset。  
  
 `left`  
 要與 hash_multiset `right` 交換元素的 hash_multiset。  
  
### <a name="remarks"></a>備註  
 `swap` 範本函式是在容器類別 hash_multiset 特製化的演算法，用來執行成員函式 `left.`[swap](../standard-library/hash-multiset-class.md#swap)( `right`)。 這是編譯器所執行之函式樣板的部分排序執行個體。 若因樣板函式多載而導致樣板與函式呼叫的比對不是唯一，則編譯器就會選取特製化程度最高的樣板函式版本。 演算法類別中範本函式的一般版本  
  
 **template \<class T> void swap(T&, T&)**  
  
 會依指派運作而作業緩慢。 每個容器中的特製化版本運作速度會更快，因為它可以與容器類別的內部表示法一起運作。  
  
   
  
### <a name="example"></a>範例  
  如需使用 `swap` 之範本版本的範例，請參閱成員函式 [hash_multiset::swap](../standard-library/hash-multiset-class.md#swap) 的程式碼範例。  
  
## <a name="see-also"></a>請參閱  
 [<hash_set>](../standard-library/hash-set.md)


