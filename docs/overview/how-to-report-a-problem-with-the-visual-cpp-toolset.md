---
title: 如何回報 Visual C++ 工具組問題
ms.date: 06/21/2018
ms.technology: cpp-ide
author: corob-msft
ms.author: corob
ms.openlocfilehash: da703d6649cb430b572d4d0db44adcfdef8ed8c4
ms.sourcegitcommit: 28eae422049ac3381c6b1206664455dbb56cbfb6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66451158"
---
# <a name="how-to-report-a-problem-with-the-visual-c-toolset-or-documentation"></a>如何回報 Visual C++ 工具組或文件的問題

如果發生 Microsoft C++ 編譯器、連結器或其他工具和程式庫的問題，請告知我們。 如果問題是出自文件，也請告知我們。

## <a name="how-to-report-a-c-toolset-issue"></a>如何回報 C++ 工具組問題

讓我們知道問題的最佳方式是將一份內含下列資訊的報表傳送給我們：所遇到問題的描述、如何建置程式的詳細資料、「重現」  ，以及可用來在我們自己的電腦上重現問題的完整測試案例。 這項資訊可讓我們快速驗證問題存在於程式碼中而且不在環境本機、判斷是否影響其他版本的編譯器，以及診斷其原因。

在下節中，您將了解如何建立良好的報表、如何針對您所發現的問題類型產生報表，以及如何將報表傳送給產品小組。 您的報表對我們和您這類其他開發人員而言十分重要。 感謝您協助我們改善 Visual C++！

## <a name="how-to-prepare-your-report"></a>如何準備報表

因為沒有完整資訊很難在我們自己的電腦上重現您所遇到的問題，所以建立高品質報表十分重要。 您的報表越好，我們就越能更有效率地重新建立並診斷問題。

您的報表最少應該包含：

- 所使用工具組的完整版本資訊。

- 用來建置您程式碼的完整 cl.exe 命令列。

- 所遇到問題的詳細描述。

- 重現：可示範問題的完整、簡化、獨立原始程式碼範例。

請閱讀以深入了解我們需要的特定資訊、可找到它的位置，以及如何建立良好重現。

### <a name="the-toolset-version"></a>工具組版本

我們需要完整版本資訊以及造成問題之工具組的目標架構，讓我們能夠在我們的電腦上針對相同的工具組測試您的重現。 如果我們可以重現問題，這項資訊也會提供一個起點，讓我們調查哪些其他版本的工具組展示相同的問題。

#### <a name="to-report-the-full-version-of-the-compiler-youre-using"></a>回報所使用編譯器的完整版本

1. 開啟**開發人員命令提示字元**，以符合用來建置專案的 Visual Studio 版本和組態架構。 例如，如果您是針對 x64 目標使用 Visual Studio 2017 on x64 進行建置，則請選擇 [x64 Native Tools Command Prompt for VS 2017] (適用於 VS 2017 的 x64 Native Tools 命令提示字元)  。 如需詳細資訊，請參閱[開發人員命令提示字元捷徑](../build/building-on-the-command-line.md#developer_command_prompt_shortcuts)。

1. 在開發人員命令提示字元主控台視窗中，輸入 **cl /Bv** 命令。

輸出應該如下：

```Output
C:\Users\username\Source>cl /Bv
Microsoft (R) C/C++ Optimizing Compiler Version 19.14.26428.1 for x86
Copyright (C) Microsoft Corporation.  All rights reserved.

Compiler Passes:
 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\VC\Tools\MSVC\14.14.26428\bin\HostX86\x86\cl.exe:        Version 19.14.26428.1
 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\VC\Tools\MSVC\14.14.26428\bin\HostX86\x86\c1.dll:        Version 19.14.26428.1
 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\VC\Tools\MSVC\14.14.26428\bin\HostX86\x86\c1xx.dll:      Version 19.14.26428.1
 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\VC\Tools\MSVC\14.14.26428\bin\HostX86\x86\c2.dll:        Version 19.14.26428.1
 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\VC\Tools\MSVC\14.14.26428\bin\HostX86\x86\link.exe:      Version 14.14.26428.1
 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\VC\Tools\MSVC\14.14.26428\bin\HostX86\x86\mspdb140.dll:  Version 14.14.26428.1
 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\VC\Tools\MSVC\14.14.26428\bin\HostX86\x86\1033\clui.dll: Version 19.14.26428.1

cl : Command line error D8003 : missing source filename
```

複製整個輸出，並將其貼入您的報表。

### <a name="the-command-line"></a>命令列

我們需要用來建置您程式碼的確切命令列 (cl.exe 和其所有引數)，以在我們的電腦上以完全相同的方式進行建置。 因為只有在使用特定引數或引數組合進行建置時才會發生您遇到的問題，所以這十分重要。

找到這項資訊的最佳位置是在遇到問題之後那時的組建記錄檔。 這確保命令列包含可能造成問題的完全相同引數。

#### <a name="to-report-the-contents-of-the-command-line"></a>回報命令列內容

1. 找到並開啟 **CL.command.1.tlog** 檔案。 根據預設，這個檔案位於 Documents 資料夾的 \\Visual Studio *version*\\Projects\\*SolutionName*\\*ProjectName*\\*Configuration*\\*ProjectName*.tlog\\CL.command.1.tlog 中，或 User 資料夾的 \\Source\\Repos\\*SolutionName*\\*ProjectName*\\*Configuration*\\*ProjectName*.tlog\\CL.command.1.tlog 下方。 如果您使用另一個建置系統，或已經變更您專案的預設位置，則它可能是在不同的位置。

   在此檔案內，您可以找到後接用來編譯原始程式碼檔之命令列引數的原始程式碼檔名稱，而且一行一個引數。

1. 找到包含發生問題之原始程式碼檔名稱的那一行；該行下面的那一行會包含對應的 cl.exe 命令引數。

複製整個命令列，並將其貼入您的報表。

### <a name="a-description-of-the-problem"></a>問題描述

我們需要您所遇到問題的詳細描述，以確認看到您電腦上的相同效果；它有時也可讓我們知道您嘗試完成的作業以及預期發生的情況。

請提供工具組所提供的**確切錯誤訊息**，或您看到的確切執行階段行為。 我們需要這項資訊來驗證我們已正確地重現問題。 請包含**所有**編譯器輸出，而不只是最後一個錯誤訊息。 我們需要查看導致您所回報問題的所有項目。 如果您可以使用命令列編譯器來複製問題，則會偏好使用該編譯器輸出；IDE 和其他組建系統可以篩選您看到的錯誤訊息，或只擷取錯誤訊息的第一行。

如果問題是編譯器接受無效的程式碼，而且未產生診斷，則請在報表中注意這一點。

若要報告執行階段行為問題，請包含程式所印出的**確切複本**，以及您預期看到的確切複本。 在理想情況下，這會內嵌在輸出陳述式本身中，例如，`printf("This should be 5: %d\n", actual_result);`。 如果您的程式當機或停止回應，則也會提及該問題。

新增可能有助於診斷所發生問題的任何其他詳細資料，例如您可能已找到的任何因應措施。 請避免在報表的其他位置出現找到的重複資訊。

### <a name="the-repro"></a>重現

重現是完整且獨立的原始程式碼範例，以重現方式示範您所遇到的問題 (因此顯示名稱)。 我們需要重現，才能在電腦上重現錯誤。 程式碼本身應該就足以建立可編譯和執行的簡單可執行檔，或將在不適用於您所發現問題時編譯和執行的簡單可執行檔。 重現不是程式碼片段；它應該有完整的函式和類別，而且包含所有必要 #include 指示詞，即使針對標準標頭也是一樣。

#### <a name="what-makes-a-good-repro"></a>如何建立良好的重現

良好的重現為：

- **最少**。 重現應該越小越好，但仍然確切地示範您所遇到的問題。 重現不需要複雜或實際；它們只需要顯示符合 Standard 或所記載編譯器實作的程式碼；或者，如果診斷遺失，則會顯示不一致的程式碼。 包含剛好足夠的程式碼來示範問題的簡單該點重現最適合。 如果您可以排除或簡化程式碼並保持一致，同時將問題保持不變，則請這麼做。 您不需要包含適用的相反範例程式碼。

- **獨立。** 重現應該避免不必要的相依性。 如果您可以重現問題，而不需要協力廠商程式庫，則請這樣做。 如果您除了簡單輸出陳述式 (例如，`puts("this shouldn't compile");`、`std::cout << value;` 和 `printf("%d\n", value);`) 之外，不需要任何程式庫程式碼即可重現問題，則請這麼做。 如果範例可以壓縮成單一原始程式碼檔，而未參考任何使用者標頭，則它十分適合。 減少視為可能造成問題的程式碼數量十分有幫助。

- **針對最新編譯器版本。** 重現應該使用工具組最新版本的更新，或下一個更新或下一個主要版本的最新發行前版本 (只要可能的話)。 在新版本中，通常已修正舊版工具組中所遇到的問題。 只有在例外狀況下，修正程式才會往回移植到較舊的版本。

- **針對其他編譯器檢查** (如果相關)。 涉及可攜式 C++ 程式碼的報表應該確認其他編譯器行為 (可能的話)。 Standard 最終會判斷程式正確性，並且沒有編譯器是完美的，但 Clang 和 GCC 接受沒有診斷的程式碼而 MSVC 不接受時，您可能會在我們的編譯器中看到 Bug (其他可能性包含 Unix 和 Windows 行為的差異，或不同層級的 C++ Standard 實作等等)。相反地，如果所有編譯器都拒絕您的程式碼，則您的程式碼可能不正確。 查看不同的錯誤訊息可以協助您自行診斷問題。

   您可以在 ISO C++ 網站的[線上 C++ 編譯器](https://isocpp.org/blog/2013/01/online-c-compilers)中，或 GitHub 上這個策劃的[線上 C++ 編譯器清單](https://arnemertz.github.io/online-compilers/)，尋找線上編譯器清單來測試您的程式碼。 某些特定範例包含 [Wandbox](https://wandbox.org/)、[編譯器總管](https://godbolt.org/)和 [Coliru](https://coliru.stacked-crooked.com/)。

   > [!NOTE]
   > 線上編譯器網站未與 Microsoft 建立關聯。 許多線上編譯器網站都會執行為個人專案；而且，在您閱讀這篇文章時，其中一些網站可能無法使用，但搜尋應該會發現其他您可使用的網站。

編譯器、連結器和程式庫中的問題，傾向於以特定方式予以顯示。 您所遇到問題的類型將決定應該包含在報表中的重現類型。 如果沒有適當的重現，我們就無法進行調查。 以下是您可能會看到的數種問題，以及產生您應該用來回報每種問題之重現類型的指示。

#### <a name="frontend-parser-crash"></a>前端 (剖析器) 損毀

前端損毀是在編譯器的剖析階段期間發生。 編譯器通常會發出[嚴重錯誤 C1001](../error-messages/compiler-errors-1/fatal-error-c1001.md)，並參考發生錯誤的原始程式碼檔和行號；它通常會提及 msc1.cpp 檔案，但您可以忽略此詳細資料。

針對這種損毀，請提供[前置處理過的重現](#preprocessed-repros)。

以下是這種損毀的範例編譯器輸出︰

```Output
SandBoxHost.cpp
d:\o\dev\search\foundation\common\tools\sandbox\managed\managed.h(929):
        fatal error C1001: An internal error has occurred in the compiler.
(compiler file 'msc1.cpp', line 1369)
To work around this problem, try simplifying or changing the program near the
        locations listed above.
Please choose the Technical Support command on the Visual C++
Help menu, or open the Technical Support help file for more information
d:\o\dev\search\foundation\common\tools\sandbox\managed\managed.h(929):
        note: This diagnostic occurred in the compiler generated function
        'void Microsoft::Ceres::Common::Tools::Sandbox::SandBoxedProcess::Dispose(bool)'
Internal Compiler Error in d:\o\dev\otools\bin\x64\cl.exe.  You will be prompted
        to send an error report to Microsoft later.
INTERNAL COMPILER ERROR in 'd:\o\dev\otools\bin\x64\cl.exe'
    Please choose the Technical Support command on the Visual C++
    Help menu, or open the Technical Support help file for more information
```

#### <a name="backend-code-generation-crash"></a>後端 (程式碼產生) 損毀

後端損毀是在編譯器的程式碼產生階段期間發生。 編譯器通常會發出[嚴重錯誤 C1001](../error-messages/compiler-errors-1/fatal-error-c1001.md)，但可能未參考與問題建立關聯的原始程式碼檔和行號；它通常會提及 compiler\\utc\\src\\p2\\main.c 檔案，但您可以忽略此詳細資料。

針對這種損毀，如果您要使用由 cl.exe 的 **/GL** 命令列引數所啟用的連結時產生程式碼 (LTCG)，請提供[連結重現](#link-repros)。 否則，請改成提供[前置處理過的重現](#preprocessed-repros)。

以下是未使用 LTCG 這種後端損毀的範例編譯器輸出。 如果您的編譯器輸出看起來像這樣，則應該提供[前置處理過的重現](#preprocessed-repros)。

```Output
repro.cpp
\\officefile\public\tadg\vc14\comperror\repro.cpp(13) : fatal error C1001:
        An internal error has occurred in the compiler.
(compiler file 'f:\dd\vctools\compiler\utc\src\p2\main.c', line 230)
To work around this problem, try simplifying or changing the program near the
        locations listed above.
Please choose the Technical Support command on the Visual C++
Help menu, or open the Technical Support help file for more information
INTERNAL COMPILER ERROR in
        'C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\BIN\cl.exe'
    Please choose the Technical Support command on the Visual C++
    Help menu, or open the Technical Support help file for more information
```

如果開頭為**內部編譯器錯誤**的行提及 link.exe，而非 cl.exe，則已啟用 LTCG，而且您應該提供[連結重現](#link-repros)。 如果無法從編譯器錯誤訊息中了解是否已啟用 LTCG，您可能需要檢查從前一個步驟中 **/GL** 命令列引數之組建記錄複製的命令列引數。

#### <a name="linker-crash"></a>連結器損毀

連結器損毀是在執行編譯器後的連結階段期間發生。 連結器通常會發出[連結器工具錯誤 LNK1000](../error-messages/tool-errors/linker-tools-error-lnk1000.md)。

> [!NOTE]
> 如果輸出提及 C1001，或涉及連結時產生程式碼，請參閱[後端 (程式碼產生) 損毀](#backend-code-generation-crash)，而非詳細資訊。

針對這種損毀，請提供[連結重現](#link-repros)。

以下是這種損毀的範例編譯器輸出。

```Output
z:\foo.obj : error LNK1000: Internal error during IMAGE::Pass2

  Version 14.00.22816.0

  ExceptionCode            = C0000005
  ExceptionFlags           = 00000000
  ExceptionAddress         = 00007FF73C9ED0E6 (00007FF73C9E0000)
        "z:\tools\bin\x64\link.exe"
  NumberParameters         = 00000002
  ExceptionInformation[ 0] = 0000000000000000
  ExceptionInformation[ 1] = FFFFFFFFFFFFFFFF

CONTEXT:

  Rax    = 0000000000000400  R8     = 0000000000000000
  Rbx    = 000000655DF82580  R9     = 00007FF840D2E490
  Rcx    = 005C006B006F006F  R10    = 000000655F97E690
  Rdx    = 000000655F97E270  R11    = 0000000000000400
  Rsp    = 000000655F97E248  R12    = 0000000000000000
  Rbp    = 000000655F97EFB0  E13    = 0000000000000000
  Rsi    = 000000655DF82580  R14    = 000000655F97F390
  Rdi    = 0000000000000000  R15    = 0000000000000000
  Rip    = 00007FF73C9ED0E6  EFlags = 0000000000010206
  SegCs  = 0000000000000033  SegDs  = 000000000000002B
  SegSs  = 000000000000002B  SegEs  = 000000000000002B
  SegFs  = 0000000000000053  SegGs  = 000000000000002B
  Dr0    = 0000000000000000  Dr3    = 0000000000000000
  Dr1    = 0000000000000000  Dr6    = 0000000000000000
  Dr2    = 0000000000000000  Dr7    = 0000000000000000
```

如果已啟用累加連結，並且只有在成功初始連結之後才會發生損毀 (也就是，只有在後續累加連結所依據的第一個完整連結之後)，也請提供物件 (.obj) 和程式庫 (.lib) 檔案的複本，這些檔案必須對應到初始連結完成後經過修改的原始程式檔。

#### <a name="bad-code-generation"></a>產生錯誤的程式碼

產生錯誤的程式碼十分罕見，但發生時機是編譯器錯誤地產生不正確程式碼讓您的應用程式在執行階段損毀，而不是在編譯時期偵測此問題。 如果您認為所遇到的問題會導致產生錯誤的程式碼，請使用與[後端 (程式碼產生) 損毀](#backend-code-generation-crash)相同的方式來處理報表。

針對這種損毀，如果您要使用由 cl.exe 的 **/GL** 命令列引數所啟用的連結時產生程式碼 (LTCG)，請提供[連結重現](#link-repros)。 否則，請提供[前置處理過的重現](#preprocessed-repros)。

## <a name="how-to-generate-a-repro"></a>如何產生重現

為了協助追蹤問題來源，[良好重現](#what-makes-a-good-repro)十分重要。 執行下面針對特定重現類型所述的任何步驟之前，請嘗試盡可能緊縮示範問題的程式碼。 嘗試刪除或最小化相依性、必要標頭和程式庫，並盡可能限制使用的編譯器選項和前置處理器定義。

以下是產生用來回報不同問題類型之各種重現類型的指示。

### <a name="preprocessed-repros"></a>前置處理過的重現

「前置處理過的重現」  是可示範問題的單一原始程式檔，而單一原始程式檔是使用原始重現原始程式檔上的 **/P** 編譯器選項以從 C 前置處理器輸出所產生。 這會內嵌包含的標頭來移除與其他來源和標頭檔的相依性，也會解析巨集、#ifdefs 以及其他取決於本機環境的前置處理器命令。

> [!NOTE]
> 因為我們通常會想要替代最新進行中的實作，以查看我們是否已修正問題，所以對於可能是標準程式庫實作中 Bug 所造成的問題，前置處理過的重現不實用。 在此情況下，請不要前置處理重現，而且如果您無法將問題減少為單一原始程式檔，則請將程式碼封裝為 .zip 檔案或類似檔案，或考慮使用 IDE 專案重現。 如需詳細資訊，請參閱[其他重現](#other-repros)。

#### <a name="to-preprocess-a-source-code-file"></a>前置處理原始程式碼檔

1. 擷取用來建置重現的命令列引數，如[回報命令列內容](#to-report-the-contents-of-the-command-line)所述。

1. 開啟**開發人員命令提示字元**，以符合用來建置專案的 Visual Studio 版本和組態架構。

1. 切換至包含重現專案的目錄。

1. 在開發人員命令提示字元主控台視窗中，輸入命令 **cl /P** *arguments* *filename.cpp*，其中 *arguments* 是上面所擷取的引數清單，而 *filename.cpp* 是重現原始程式檔的名稱。 此命令會複寫用於重現的命令列，但在前置處理器通過時停止編譯，並將前置處理過的原始程式碼輸出至 *filename*.i。

如果您要前置處理 C++/CX 原始程式碼檔案，或者要使用 C++ 模組功能，則需要執行一些其他步驟。 如需詳細資訊，請參閱以下節。

產生前置處理過的檔案之後，最好確定仍然可以使用前置處理過的檔案重現問題。

#### <a name="to-confirm-that-the-error-still-repros-with-the-preprocessed-file"></a>確認仍然可以使用前置處理過的檔案重現錯誤

1. 在開發人員命令提示字元主控台視窗中，輸入 **cl** *arguments* **/TP** *filename*.i 命令，以告訴 cl.exe 將前置處理過的檔案編譯為 C++ 原始程式檔，其中 *arguments* 是上面所擷取的引數清單，但移除任何 **/D** 和 **/I** 引數 (因為它們已包含在前置處理過的檔案中)；而 *filename*.i 是前置處理過的檔案的名稱。

1. 請確認已重現問題。

最後，將前置處理過的重現 *filename*.i 附加到報表中。

### <a name="preprocessed-ccx-winrtuwp-code-repros"></a>前置處理過的 C++/CX WinRT/UWP 程式碼重現

如果您要使用 C++/CX 來建置可執行檔，必須執行一些額外步驟，才能建立和驗證前置處理過的重現。

#### <a name="to-preprocess-ccx-source-code"></a>前置處理 C++/CX 原始程式碼

1. 建立前置處理過的原始程式檔，如[前置處理原始程式碼檔案](#to-preprocess-a-source-code-file)中所述。

1. 搜尋產生的 _filename_.i 檔案中是否有 **#using** 指示詞。

1. 製作所有參考檔案的清單。 請排除任何 Windows\*.winmd 檔案、platform.winmd 檔案和 mscorlib.dll。

若要準備驗證前置處理過的檔案仍會重現問題，請：

1. 為前置處理過的檔案建立新目錄，並將它複製到新目錄。

1. 將 **#using** 清單中的.winmd 檔案複製到新目錄。

1. 在新目錄中建立空白的 vccorlib.h 檔案。

1. 編輯前置處理過的檔案，以移除 mscorlib.dll 的任何 **#using** 指示詞。

1. 編輯前置處理過的檔案，將所有絕對路徑變更為複製之 .winmd 檔案的純檔名。

確認前置處理過的檔案仍會重現問題，如上所述。

### <a name="preprocessed-c-modules-repros"></a>前置處理過的 C++ 模組重現

如果您要使用 C++ 編譯器的模組功能，必須執行一些不同的步驟，才能建立和驗證前置處理過的重現。

#### <a name="to-preprocess-a-source-code-file-that-uses-a-module"></a>前置處理使用模組的原始程式碼檔案

1. 擷取用來建置重現的命令列引數，如[回報命令列內容](#to-report-the-contents-of-the-command-line)所述。

1. 開啟**開發人員命令提示字元**，以符合用來建置專案的 Visual Studio 版本和組態架構。

1. 切換至包含重現專案的目錄。

1. 在開發人員命令提示字元主控台視窗中，輸入 **cl /P** *arguments* *filename.cpp* 命令，其中 *arguments* 是上面所擷取的引數清單，而 *filename.cpp* 是取用模組之原始程式檔的名稱。

1. 切換至包含建置模組介面 ( .ifc 輸出) 所使用之重現專案的目錄。

1. 擷取用來建置模組介面的命令列引數。

1. 在開發人員命令提示字元主控台視窗中，輸入 **cl /P** *arguments* *modulename.ixx* 命令，其中 *arguments* 是上面所擷取的引數清單，而 *modulename.ixx* 是建立模組介面之檔案的名稱。

產生前置處理過的檔案之後，最好確定仍然可以使用前置處理過的檔案重現問題。

#### <a name="to-confirm-that-the-error-still-repros-with-the-preprocessed-file"></a>確認仍然可以使用前置處理過的檔案重現錯誤

1. 在開發人員主控台視窗中，切換回包含您重現專案的目錄。

1. 如上所述輸入 **cl** *arguments* **/TP** *filename*.i 命令，以編譯前置處理過的檔案，就像它是 C++ 原始程式檔一樣。

1. 確認前置處理過的檔案仍會重現該問題。

最後，將前置處理過的重現檔案 (*filename*.i 和 *modulename*.i) 以及 .ifc 輸出附加到您的報表。

### <a name="link-repros"></a>連結重現

「連結重現」  是由連結器所產生且由 **link\_repro** 環境變數所指定之目錄的內容。 它包含的組建成品可以統一示範在連結時發生的問題，例如涉及連結時產生程式碼 (LTCG) 的後端損毀或是連結器損毀。 這些組建成品是連結器輸入所需的項目，因此可以重現問題。 使用這個環境變數啟用連結器的內建重現產生功能，即可輕鬆地建立連結重現。

#### <a name="to-generate-a-link-repro"></a>產生連結重現

1. 擷取用來建置重現的命令列引數，如[回報命令列內容](#to-report-the-contents-of-the-command-line)所述。

1. 開啟**開發人員命令提示字元**，以符合用來建置專案的 Visual Studio 版本和組態架構。

1. 在開發人員命令提示字元主控台視窗中，切換至包含您重現專案的目錄。

1. 輸入 **mkdir linkrepro**，以建立連結重現的目錄。

1. 輸入 **set link\_repro=linkrepro** 命令，以將 **link\_repro** 環境變數設為您剛剛建立的目錄。 如果您的組建從不同的目錄執行 (這在較複雜的專案時常發生)，請改將 **link\_repro** 設為 linkrepro 目錄的完整路徑。

1. 若要在 Visual Studio 中建置重現專案，請在開發人員命令提示字元主控台視窗中輸入 **devenv** 命令。 這確保 Visual Studio 可以看到 **link\_repro** 環境變數的值。 若要在命令列中建置專案，請使用上述擷取的命令列引數來複製重現組建。

1. 建置重現專案，並確認發生預期的問題。

1. 如果您已使用 Visual Studio 來執行建置，則請予以關閉。

1. 在開發人員命令提示字元主控台視窗中，輸入 **set link\_repro=** 命令，以清除 **link\_repro** 環境變數。

最後，將整個 linkrepro 目錄壓縮成 .zip 檔案或類似檔案來封裝重現，並將它附加到報表。

### <a name="other-repros"></a>其他重現

如果您無法將問題減少為單一原始程式檔或前置處理過的重現，而且問題不需要連結重現，則我們可以調查 IDE 專案。 所有如何建立良好重現的指引仍然適用；程式碼應該最少且獨立、我們的最新工具中應該會發生問題，而且如果相關，則問題應該不會出現在其他編譯器中。

將重現建立為最少 IDE 專案，然後將整個目錄結構壓縮成 .zip 檔案或類似檔案以進行封裝，並將其附加至報表。

## <a name="ways-to-send-your-report"></a>報表的傳送方式

有幾種不錯的方法可將您的報表送給我們。 您可以使用 Visual Studio 的內建[回報問題工具](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)，或 [Visual Studio 開發人員社群](https://developercommunity.visualstudio.com/)頁面。 您也可以選擇此頁面底部的 [產品意見反應]  按鈕，直接前往我們的開發人員社群頁面。 此選擇取決於您是否想要在開發人員社群頁面中使用 IDE 內建工具來擷取螢幕擷取畫面和組織要張貼的報表，或者您是否想要直接使用此網站。

> [!NOTE]
> 不論您如何提交報表，Microsoft 都會尊重您的隱私權。 Microsoft 致力於遵循所有資料的隱私權法律和規定。 如需我們如何處理您所傳送之資料的相關資訊，請參閱 [Microsoft 隱私權聲明](https://privacy.microsoft.com/privacystatement)。

### <a name="use-the-report-a-problem-tool"></a>使用回報問題工具

Visual Studio 中的 [回報問題]  工具是 Visual Studio 使用者用來回報各種問題的方式，只要按幾下就可回報問題。 它提供簡單的表單以用來指定您所遇到問題的詳細資訊，然後提交報表，而不需要離開 IDE。

從 IDE 透過 [回報問題]  工具回報問題簡單又方便。 您可以選擇 [快速啟動]  搜尋方塊旁的**傳送意見反應**圖示從標題列存取這項工具，也可以在功能表列上的 [協助]   > [傳送意見反應]   > [回報問題]  中找到該工具。

當您選擇回報問題時，請先在開發人員社群中搜尋是否有類似問題。 如果其他人之前回報過相關問題，請附議主題並新增留言，提出具體細節。 如果您找不到類似問題，請選擇 Visual Studio 意見反應對話方塊底部的 [回報新問題]  按鈕，然後遵循這些步驟回報問題。

### <a name="use-the-visual-studio-developer-community-pages"></a>使用 Visual Studio 開發人員社群頁面

Visual Studio 開發人員社群頁面提供另一種方便的途徑，讓您回報 Visual Studio 和 C++ 編譯器、工具和程式庫的問題和尋找其解決方案。 [Visual Studio](https://developercommunity.visualstudio.com/spaces/8/index.html)、[Visual Studio for Mac](https://developercommunity.visualstudio.com/spaces/41/index.html)、[.NET](https://developercommunity.visualstudio.com/spaces/61/index.html)、[C++](https://developercommunity.visualstudio.com/spaces/62/index.html)、[Azure DevOps](https://developercommunity.visualstudio.com/spaces/21/index.html) 和 [TFS](https://developercommunity.visualstudio.com/spaces/22/index.html) 有特定的開發人員社群頁面。 在這些標籤下方，靠近每個頁面頂端的橫幅為搜尋方塊，您可用來尋找回報類似您問題的文章或主題。 您也許可以找到與您問題相關的解決方案或其他有用資訊。 如果其他人已回報過相同的問題，請附議該主題並留言，而非建立新的問題回報。 若要留言、投票或回報新問題，系統可能會要求您登入 Visual Studio 帳戶，並同意將您設定檔的存取權授與開發人員社群應用程式。

若要回報 C++ 編譯器、連結器，以及其他工具和程式庫的相關問題，則請使用 [C++](https://developercommunity.visualstudio.com/spaces/62/index.html) 頁面。 如果其他人未回報過您搜尋的問題，請選擇頁面頂端搜尋方塊旁的 [回報問題]  按鈕。 您可以包含您重新產生的程式碼和命令列、螢幕擷取畫面、相關討論的連結，及其他您認為相關且有用的任何資訊。

> [!TIP]
> 針對在 Visual Studio 中可能遇到與 C++工具組無關的其他類型問題 (例如 UI 問題、損壞的 IDE 功能或常見當機)，請使用 IDE 中的 [回報問題]  工具。 這是最佳選擇，因為該工具有螢幕擷取畫面功能，並且能夠記錄導致您遇到問題的 UI 動作。 您也可以在[開發人員社群](https://developercommunity.visualstudio.com/)網站上尋找這類錯誤。 如需詳細資訊，請參閱[如何回報 Visual Studio 的問題](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)。

### <a name="reports-and-privacy"></a>報表和隱私權

根據預設，**報表中的所有資訊以及任何留言和回覆都是公開顯示**。 一般來說，這是一項優點，因為它可讓整個社群查看問題、解決方案和其他使用者找到的因應措施。 不過，如果您基於隱私權或智慧財產權理由擔心會讓您的資料或身分公開，則可使用其他選項。

如果您擔心揭露您的身分，請[建立新的 Microsoft 帳戶](https://signup.live.com/)，這不會揭露關於您的任何詳細資料。 使用此帳戶來建立您的報表。

**請不要在公開的初始報表標題或內容中放置您想要保持私用的任何項目。** 相反地，請注意您會在個別的留言中私下傳送詳細資料。 為了確定您的報表會導向至適當的人員，請在問題報表的主題清單中包含 **cppcompiler**。 建立問題報表後，現在就能夠指定誰可以查看您的回覆和附件。

#### <a name="to-create-a-problem-report-for-private-information"></a>建立私人資訊的問題報表

1. 在建立的報表中，選擇 [新增留言]  來建立您對問題的私人描述。

1. 在回覆編輯器中，使用 [送出]  和 [取消]  按鈕下方的下拉式控制項來指定回覆的對象。 只有您指定的人員才能看到這些私人回覆以及其中包含的任何影像、連結或程式碼。 選擇 [可供仲裁者和原始貼文者檢視]  來限制 Microsoft 員工和您自己的可見性。

1. 新增描述，以及重現所需的任何其他資訊、影像和檔案附件。 選擇 [送出]  按鈕以私下傳送這些資訊。

   請注意，附加的檔案有 2GB 的限制，最多 10 個檔案。 對於任何較大的上傳項目，請在您的私用留言中要求一個上傳 URL。

這個留言底下的所有回覆都具有您指定的相同受限可見性。 即使回覆的下拉式控制項未正確顯示受限可見性狀態也是如此。

若要維護您的隱私權，並讓機密資訊不要公開檢視，請小心地將所有與 Microsoft 的互動保持在這個受限留言下回覆。 對其他留言的回覆可能會導致您不小心公開機密資訊。

## <a name="how-to-report-a-c-documentation-issue"></a>如何回報 C++ 文件問題

我們使用 GitHub 問題來追蹤文件中所回報的問題。 您現在可以直接從內容頁建立 GitHub 問題，這可讓您以更豐富的方式與作者和產品小組互動。 如果您發現文件問題、錯誤的程式碼範例、造成混淆的說明、嚴重遺漏，或甚至只是錯字，，都可以輕鬆地通知我們。 請捲動至頁面底部，並選取 [登入以提供文件應見反應]  。 如果您還沒有 GitHub 帳戶，則必須建立一個 GitHub 帳戶，但是一旦完成，您就可以查看所有文件問題及其狀態，並在您所回報的問題有所變更時收到通知。 如需詳細資訊，請參閱[即將在 docs.microsoft.com 推出新的意見反應系統](/teamblog/a-new-feedback-system-is-coming-to-docs)。

當您使用 [文件意見反應] 按鈕在 GitHub 上建立文件問題時，該問題會自動填入有關建立問題來源頁面的一些資訊，以便讓我們知道問題所在位置。 請不要編輯此資訊。 只需要附加有關錯誤的詳細資料，如有必要，還可以提供建議的修正程式。 [我們的文件是開放原始碼](https://github.com/MicrosoftDocs/cpp-docs/)，因此如果您想要實際進行修正並自行提出建議，就可以這樣做。 如需您可以如何參與文件的詳細資訊，請參閱我們在 GitHub 上的[參與指南](https://github.com/MicrosoftDocs/cpp-docs/blob/master/CONTRIBUTING.md) (英文)。
