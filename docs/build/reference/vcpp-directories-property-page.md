---
title: VC++ 目錄屬性頁
ms.date: 10/09/2018
f1_keywords:
- VC.Project.VCDirectories.IncludePath
- VC.Project.VCDirectories.ReferencePath
- VC.Project.VCDirectories.SourcePath
- VC.Project.VCDirectories.LibraryWPath
- VC.Project.VCDirectories.ExecutablePath
- VC.Project.VCDirectories.LibraryPath
- VS.ToolsOptionsPages.Projects.VCDirectories
- VC.Project.VCDirectories.ExcludePath
helpviewer_keywords:
- VC++ Directories Property Page
ms.assetid: 428eeef6-f127-4271-b3ea-0ae6f2c3d624
ms.openlocfilehash: e739ea99df424f44dc43a28e3dc01c3529bb0c1a
ms.sourcegitcommit: 28eae422049ac3381c6b1206664455dbb56cbfb6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66450711"
---
# <a name="vc-directories-property-page-windows"></a>VC++ 目錄屬性頁 (Windows)

使用此屬性頁指示 Visual Studio 要用來建置目前所選專案的目錄。 若要在方案中設定多個專案的目錄，使用自訂的屬性工作表中所述[共用或 resuse Visual StudioC++專案設定](../create-reusable-property-configurations.md)。

若是此頁面的 Linux 版本，請參閱 [VC++ 目錄 (Linux C++)](../../linux/prop-pages/directories-linux.md)。

若要存取 [VC++ 目錄]  屬性頁：

1. 如果看不到 [方案總管]  視窗，請在主要功能表上，選擇 [檢視]   > [方案總管]  。
1. 以滑鼠右鍵按一下專案節點 (而不是最上層方案)，然後選擇 [屬性]  。
1. 在 [屬性頁]  對話方塊的左窗格中，選取 [組態屬性]   > [VC++ 目錄]  。

VC++ 目錄屬性會套用至專案，而不是最上層方案節點。 如果在 [組態屬性]  下看不到 [VC++ 目錄]  ，請在 [方案總管]  視窗中選取 C++ 專案節點：

![選取專案節點](../media/vcppdir.png "選取專案節點以查看 VC++ 目錄屬性")

請注意，跨平台專案的 [VC++ 目錄]  屬性頁看起來不太一樣。 如需 Linux C++ 專案特定的資訊，請參閱 [VC++ 目錄 (Linux C++)](../../linux/prop-pages/directories-linux.md)。

如果您不熟悉*專案屬性*在 Visual Studio 中，您可能會覺得很有幫助第一次讀取[設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。

[VC++ 目錄]  屬性的預設設定取決於專案類型。 若是桌面專案，則會包含特定平台工具組的 C++ 工具位置及 Windows SDK 位置。 您可以在 [組態屬性]   > [一般]  頁面上，變更 [平台工具組]  和 [Windows SDK 版本]  。

若要檢視任何目錄的值：

1. 在 [VC++ 目錄]  頁面中，選取其中一個屬性。 例如，選擇 [程式庫目錄]  。
1. 選擇屬性值欄位結尾的向下箭號按鈕。
1. 在下拉式功能表中，選擇 [編輯]  。

![編輯程式庫目錄](../media/vcppdir_libdir_edit.png "編輯程式庫路徑的對話方塊")

您會看到類似如下的對話方塊：

![顯示程式庫目錄](../media/vcppdir_libdir.png "新增或移除程式庫路徑的對話方塊")

使用此對話方塊可檢視目前的目錄。 不過，如果您想要變更或新增目錄，最好使用 [屬性管理員]  建立屬性工作表，或修改預設使用者屬性工作表。 如需詳細資訊，請參閱 <<c0> [ 共用或 resuse Visual StudioC++專案設定](../create-reusable-property-configurations.md)。</c0>

如上所示，許多繼承的路徑已指定為巨集。  若要檢查巨集的目前值，請選擇對話方塊右下角的 [巨集]  按鈕。 請注意，許多巨集取決於組態類型。 偵錯組建中的巨集可能會評估為與發行組建中相同巨集不同的路徑。

您可以在編輯方塊中搜尋部分或完全符合的項目。 下圖顯示包含字串 "WindowsSDK" 的所有巨集，並顯示巨集評估的目前路徑：

![查看巨集值](../media/vcppdir_libdir_macros.png "編輯巨集的對話方塊")

注意:當您輸入時，會填入此清單。 請勿按 **Enter** 鍵。

如需有關巨集和為什麼您應該而不是硬式編碼路徑，請盡可能使用它們的詳細資訊，請參閱[設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。

如需常用的巨集的清單，請參閱 <<c0> [ 的一般巨集建置命令和屬性](common-macros-for-build-commands-and-properties.md)。

您可以透過兩種方式來定義自己的巨集：

- 在開發人員命令提示字元中設定環境變數。 所有環境變數會視為 MSBuild 屬性/巨集。

- 在 .props 檔案中定義使用者巨集。 如需詳細資訊，請參閱[屬性頁巨集](../working-with-project-properties.md)。

如需詳細資訊，請參閱這些部落格文章：[VC + + 目錄](https://blogs.msdn.com/b/vsproject/archive/2009/07/07/vc-directories.aspx)，[繼承屬性和屬性工作表](https://blogs.msdn.com/b/vsproject/archive/2009/06/23/inherited-properties-and-property-sheets.aspx)，以及[Visual Studio 2010C++專案升級指南](https://devblogs.microsoft.com/cppblog/visual-studio-2010-c-project-upgrade-guide/)。

## <a name="directory-types"></a>目錄類型

您也可以指定其他目錄，如下所示。

**可執行檔目錄**<br/>
要在其中搜尋可執行檔的目錄。 對應至 **PATH** 環境變數。

**Include 目錄**<br/>
要在其中搜尋原始程式碼中所參考之 Include 檔案的目錄。 對應至 **INCLUDE** 環境變數。

**參考目錄**<br/>
要在其中搜尋組件和模組 (中繼資料) 檔的目錄，原始程式碼是使用 [#using](../../preprocessor/hash-using-directive-cpp.md) 指示詞參考這些檔案。 對應至 **LIBPATH** 環境變數。

**程式庫目錄**<br/>
要在其中搜尋程式庫 (.lib) 檔案的目錄；包括執行階段程式庫。 對應至 **LIB** 環境變數。 此設定不適用於 .obj 檔案；若要連結至 .obj 檔案，請在 [組態屬性]   > [連結器]   > [一般]  屬性頁上，選取 [其他程式庫相依性]  ，然後指定檔案的相對路徑。 如需詳細資訊，請參閱[連結器屬性頁](linker-property-pages.md)。

**WinRT 程式庫目錄**<br/>
要搜尋用於通用 Windows 平台 (UWP) 應用程式之 WinRT 程式庫檔案的目錄。

**來源目錄**<br/>
要在其中搜尋用於 IntelliSense 之來源檔的目錄。

**排除目錄**<br/>
每次編譯之前，Visual Studio 都會查詢所有檔案上的時間戳記，以判斷自上次編譯以來是否已做了任何修改。 如果您的專案具有大型穩定的程式庫，您可以透過從時間戳記檢查排除這些目錄，來盡可能加速建置時間。

## <a name="sharing-the-settings"></a>共用設定

您可以與其他使用者或多部電腦共用專案屬性。 如需詳細資料，請參閱[在 Visual Studio 中設定 C ++ 編譯器和組建屬性](../working-with-project-properties.md)。
