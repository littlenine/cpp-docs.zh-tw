---
title: /VERBOSE (列印進度訊息)
ms.date: 11/04/2016
f1_keywords:
- /verbose
- VC.Project.VCLinkerTool.ShowProgress
helpviewer_keywords:
- -VERBOSE linker option
- linking [C++], session progress information
- Print Progress Messages linker option
- linker [C++], output dependency information
- /VERBOSE linker option
- dependencies [C++], dependency information in linker output
- VERBOSE linker option
ms.assetid: 9c347d98-4c37-4724-a39e-0983934693ab
ms.openlocfilehash: 7aed1e17034b40ffdad4da4136fc5a64361b3d77
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62317298"
---
# <a name="verbose-print-progress-messages"></a>/VERBOSE (列印進度訊息)

```
/VERBOSE[:{ICF|INCR|LIB|REF|SAFESEH|UNUSEDLIBS}]
```

## <a name="remarks"></a>備註

連結器會傳送到連結的工作階段的進度資訊**輸出**視窗。 在命令列中，資訊會傳送至標準輸出，並可以重新導向至檔案。

|選項|描述|
|------------|-----------------|
|/VERBOSE|顯示關於連結的程序的詳細資料。|
|/VERBOSE:ICF|顯示使用產生的連結器活動的相關資訊[/opt: icf](opt-optimizations.md)。|
|/VERBOSE:INCR|顯示有關累加連結程序的資訊。|
|/VERBOSE:LIB|只顯示表示所搜尋之程式庫的進度訊息。<br /><br /> 顯示的資訊包括文件庫搜尋程序，並列出每個程式庫和物件名稱 （具有完整路徑），從程式庫，以及參考該符號的物件清單解析的符號。|
|/VERBOSE:REF|顯示使用產生的連結器活動的相關資訊[/opt: ref](opt-optimizations.md)。|
|/VERBOSE:SAFESEH|顯示與安全例外狀況時處理不相容的模組的相關資訊[/SAFESEH](safeseh-image-has-safe-exception-handlers.md)未指定。|
|/VERBOSE:UNUSEDLIBS|顯示建立映像時未使用的所有程式庫檔案的相關資訊。|

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個連結器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 依序展開**連結器**資料夾。

1. 選取 **命令列**屬性頁。

1. 新增選項，以**其他選項** 方塊中。

### <a name="to-set-this-linker-option-programmatically"></a>若要以程式設計方式設定這個連結器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.ShowProgress%2A>。

## <a name="see-also"></a>另請參閱

[MSVC 連結器參考](linking.md)<br/>
[MSVC 連結器選項](linker-options.md)
