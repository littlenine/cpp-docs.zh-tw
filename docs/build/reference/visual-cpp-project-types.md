---
title: Visual C++ 專案類型
ms.date: 11/29/2018
helpviewer_keywords:
- programs [C++], projects
- project templates [Visual Studio], C++
- TODO comments [C++]
- projects [C++], types
- templates [C++], projects
- applications [C++], projects
- C++ projects, types
ms.assetid: 7337987e-1e7b-4120-9a4b-94f0401f15e7
ms.openlocfilehash: dce96a221804e5538929d63fa3c125a27e7fc36d
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65217769"
---
# <a name="c-project-templates"></a>C++專案範本

Visual Studio 專案範本產生原始程式碼檔、 編譯器選項、 功能表、 工具列、 圖示、 參考和`#include`適用於您想要建立的專案類型之陳述式。 Visual Studio 包括各種類型的C++專案範本和精靈的許多提供它們，讓您可以自訂您的專案，當您建立它們。 在您建立專案之後，您就可以立即對其進行建置，並執行應用程式；在您開發應用程式時，間歇地進行建置是一個很好的做法。

> [!NOTE]
> 您可以使用 C++ 專案範本，來建立 C 語言專案。 在所產生的專案中，尋找副檔名為 .cpp 的檔案，並將其變更為 .c。 然後，在專案 (不適用於方案) 的 [專案屬性]  頁面上，展開 [組態屬性] 、[C/C++]  ，然後選取 [進階] 。 將 [編譯為]  設定變更為 [編譯為 C 程式碼 (/TC)] 。

## <a name="project-templates"></a>專案範本

Visual Studio 中包含的專案範本取決於您已安裝的產品版本和工作負載。 如果您已安裝的桌面開發使用C++工作負載，Visual Studio 有這些C++專案範本。

### <a name="windows-desktop"></a>Windows 桌面

|專案範本|描述|
|----------------------|-----------------------------|
|[Windows 主控台應用程式](../../windows/creating-a-console-application.md)|用於建立 Windows 主控台應用程式的專案。|
|[Windows 傳統型應用程式](../../windows/walkthrough-creating-windows-desktop-applications-cpp.md)|用於建立 Windows 傳統型 (Win32) 應用程式的專案。|
|[動態連結程式庫](../walkthrough-creating-and-using-a-dynamic-link-library-cpp.md)|用於建立動態連結程式庫 (DLL) 的專案。|
|[靜態程式庫](../../windows/walkthrough-creating-and-using-a-static-library-cpp.md)|用於建立靜態程式庫 (LIB) 的專案。|
|Windows 傳統式精靈|使用其他選項建立 Windows 傳統型應用程式和程式庫的精靈。|

### <a name="general"></a>一般

|專案範本|描述|
|----------------------|-----------------------------|
|空專案|用於建立應用程式、程式庫或 DLL 的空白專案。 您必須新增任何所需的程式碼或資源。|
|[Makefile 專案](creating-a-makefile-project.md)|在 Visual Studio 專案中包裝 Windows makefile 專案。 (若要開啟為以 makefile-在 Visual Studio 中，使用[開啟資料夾](../open-folder-projects-cpp.md)。|
|共用的項目專案|用來共用程式碼檔案或多個專案之間的資源檔的專案。 這種專案類型不會產生可執行檔。|

### <a name="atl"></a>ATL

|專案範本|描述|
|----------------------|-----------------------------|
|[ATL 專案](../../atl/reference/creating-an-atl-project.md)|使用 Active Template Library 的專案。|

### <a name="test"></a>測試

|專案範本|描述|
|----------------------|-----------------------------|
|[原生單元測試專案](/visualstudio/test/writing-unit-tests-for-c-cpp-with-the-microsoft-unit-testing-framework-for-cpp)|包含原生 C++ 單元測試的專案。|

### <a name="mfc"></a>MFC

如果您將 MFC 和 ATL 支援元件新增至 Visual Studio 安裝環境，這些專案範本就會新增至 Visual Studio。

|專案範本|描述|
|----------------------|-----------------------------|
|[MFC 應用程式](../../mfc/reference/creating-an-mfc-application.md)|用於建立使用 MFC 程式庫之應用程式的專案。|
|[MFC ActiveX 控制項](../../mfc/reference/creating-an-mfc-activex-control.md)|用於建立使用 MFC 程式庫之 ActiveX 控制項的專案。|
|[MFC DLL](../../mfc/reference/creating-an-mfc-dll-project.md)|用於建立使用 MFC 程式庫之動態連結程式庫的專案。|

### <a name="windows-universal-apps"></a>Windows 通用應用程式

如果您將 C++ Windows 通用平台工具元件新增至 Visual Studio 安裝環境，這些專案範本就會新增至 Visual Studio。

如需 C++ 的 Windows 通用應用程式的概觀，請參閱[通用 Windows 應用程式 (C++)](../../windows/universal-windows-apps-cpp.md)。

|專案範本|描述|
|----------------------|-----------------------------|
|空白應用程式|不具預先定義的控制項或配置之單一頁面通用 Windows 平台 (UWP) 應用程式的專案。|
|DirectX 11 應用程式|使用 DirectX 11 之通用 Windows 平台應用程式的專案。|
|DirectX 12 應用程式|使用 DirectX 12 之通用 Windows 平台應用程式的專案。|
|DirectX 11 和 XAML 應用程式|使用 DirectX 11 和 XAML 之通用 Windows 平台應用程式的專案。|
|單元測試應用程式|用於為通用 Windows 平台 (UWP) 應用程式建立單元測試應用程式的專案。|
|DLL|可供通用 Windows 平台應用程式或執行階段元件使用之原生動態連結程式庫 (DLL) 的專案。|
|靜態程式庫|可供通用 Windows 平台應用程式或執行階段元件使用之原生靜態連結程式庫 (LIB) 的專案。|
|Windows 執行階段元件|不論撰寫應用程式的程式設計語言為何，可供通用 Windows 平台應用程式使用之 Windows 執行階段元件的專案。|
|Windows 應用程式封裝專案|建立可讓傳統型應用程式透過 Microsoft Store 側載或散發之 UWP 套件的專案。|

## <a name="todo-comments"></a>TODO 註解

專案範本產生的許多檔案都包含 TODO 註解，以協助您識別您可以提供自己原始程式碼的位置。 如需如何新增程式碼的詳細資訊，請參閱[使用程式碼精靈新增功能](../../ide/adding-functionality-with-code-wizards-cpp.md)和[使用資源檔](../../windows/working-with-resource-files.md)。


