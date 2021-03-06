---
title: "로컬 실행 및 Azure Data Lake U-SQL SDK를 사용하여 U-SQL 작업 테스트 및 디버그 | Microsoft Docs"
description: "Azure Data Lake Tools for Visual Studio 및 Azure Data Lake U-SQL SDK를 사용하여 로컬 워크스테이션에서 U-SQL 작업을 테스트하고 디버그하는 방법에 대해 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: jgao
translationtype: Human Translation
ms.sourcegitcommit: c43fb7b513136bb3ea964419d68f58585bba48fd
ms.openlocfilehash: 348971e07169ae9c155753c7943124e96e6e9597


---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a>로컬 실행 및 Azure Data Lake U-SQL SDK를 사용하여 U-SQL 작업 테스트 및 디버그

Azure Data Lake 서비스의 경우처럼 Visual Studio와 Azure Data Lake U-SQL SDK에 대해 Azure Data Lake 도구를 사용하여 워크스테이션에서 U-SQL 작업을 실행할 수 있습니다. 이들 두 가지 로컬 실행 기능으로 U-SQL 작업을 테스트하고 디버그하는 시간을 절약할 수 있습니다.

필수 조건:

- Azure Data Lake Analytics 계정 - [Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md) 참조
- Visual Studio용 Azure Data Lake 도구입니다. [Data Lake Tools for Visual Studio로 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md) 참조
- U-SQL 스크립트 개발 환경 - [Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md) 참조


## <a name="understand-the-data-root-folder-and-the-file-path"></a>데이터 루트 폴더 및 파일 경로 이해

로컬 실행 및 U-SQL SDK에는 모두 데이터 루트 폴더가 필요합니다. 데이터 루트 폴더는 로컬 계산 계정의 "로컬 저장소"입니다. 이는 Data Lake Analytics 계정의 Azure Data Lake Store 계정과 동일합니다. 다른 데이터 루트 폴더로 전환하는 것은 다른 저장소 계정으로 전환하는 것과 같습니다. 다른 데이터 루트 폴더와 공유된 데이터에 액세스하려는 경우 스크립트에서 절대 경로를 사용해야 합니다. 또는 데이터 루트 폴더 아래에 파일 시스템 심볼 링크를 만들어 공유 데이터를 가리키도록 합니다(예, NTFS의 **mklink**).

데이터 루트 폴더는 다음 용도로 사용됩니다.

- 데이터베이스, 테이블, TVF(테이블 반환 함수), 어셈블리 등의 메타데이터를 저장합니다.
- U-SQL에서 상대 경로로 정의된 입력 및 출력 경로 조회 - 상대 경로를 사용하면 U-SQL 프로젝트를 Azure에 보다 쉽게 배포할 수 있습니다.

U-SQL 스크립트의 상대 경로 및 로컬 절대 경로를 사용할 수 있습니다. 상대 경로는 지정된 데이터-루트 폴더 경로 기준으로 하는 것입니다. 스크립트를 서버 쪽과 호환되게 하려면 경로 구분 기호로 "/"를 사용하는 것이 좋습니다. 다음은 상대 경로 및 이와 대등한 절대 경로의 몇 가지 예입니다. 이 예에서 C:\LocalRunDataRoot는 데이터 루트 폴더입니다.

|상대 경로|절대 경로|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Visual Studio에서 로컬 실행 사용

Data Lake Tools for Visual Studio는 Visual Studio에서 U-SQL 로컬 실행 환경을 제공합니다. 이 기능을 사용하면 다음을 수행할 수 있습니다.

- C# 어셈블리와 함께 U-SQL 스크립트를 로컬로 실행합니다.
- C# 어셈블리를 로컬로 디버그합니다.
- [서버 탐색기]에서 U-SQL 카탈로그(로컬 데이터베이스, 어셈블리, 스키마 및 테이블)를 만들고, 보고, 삭제합니다. 또 서버 탐색기에서 로컬 카탈로그도 찾을 수 있습니다.

    ![Data Lake Tools for Visual Studio의 로컬 카탈로그 로컬 실행](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

Data Lake Tools 설치 관리자는 기본 데이터 루트 폴더로 사용할 C:\LocalRunRoot 폴더를 만듭니다. 기본 병렬 처리 로컬 실행은 1입니다.

### <a name="to-configure-local-run-in-visual-studio"></a>Visual Studio에서 로컬 실행을 구성하려면

1. Visual Studio를 엽니다.
2. **서버 탐색기**를 엽니다.
3. **Azure** > **Data Lake Analytics**를 차례로 확장합니다.
4. **Data Lake** 메뉴, **옵션 및 설정**을 차례로 클릭합니다.
5. 왼쪽 트리에서 **Azure Data Lake**, **일반**을 차례로 확장합니다.

    ![Data Lake Tools for Visual Studio의 로컬 실행 구성 설정](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

로컬 실행을 수행하려면 Visual Studio U-SQL 프로젝트가 필요합니다. 이 점이 Azure에서 실행하는 U-SQL 스크립트와 다릅니다.

### <a name="to-run-a-u-sql-script-locally"></a>로컬로 U-SQL 스크립트를 실행하려면
1. Visual Studio에서 U-SQL 프로젝트를 엽니다.   
2. [솔루션 탐색기]에서 U-SQL 스크립트를 마우스 오른쪽 단추로 클릭한 다음 **스크립트 제출**을 클릭합니다.
3. 로컬로 스크립트를 실행하려면 분석 계정을 **(로컬)**로 선택합니다.
또는 스크립트 창 위쪽에서 **(로컬)** 계정을 클릭한 다음 **제출**을 클릭하거나 Ctrl+F5 바로 가기를 사용할 수도 있습니다.

    ![Data Lake Tools for Visual Studio의 로컬 실행 작업 제출](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)



## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a>Data Lake U-SQL SDK에서 로컬 실행 사용

Visual Studio를 사용하여 U-SQL 스크립트를 로컬로 실행하는 것 외에도 Azure Data Lake U-SQL SDK를 사용하여 명령줄 및 프로그래밍 인터페이스로 U-SQL 스크립트를 로컬로 실행할 수 있습니다. 이를 통해 U-SQL 로컬 테스트를 확장할 수 있습니다.

### <a name="install-the-sdk"></a>SDK 설치

Data Lake U-SQL SDK에는 다음과 같은 종속성이 필요합니다.

- [Microsoft .NET Framework 4.6 이상](https://www.microsoft.com/en-us/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 및 Windows SDK 10.0.10240.0 이상 - 이를 수행하는 방법에는 두 가지입니다.

    - [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou)을 설치합니다. 프로그램 파일 폴더 아래에 \Windows Kits\10 폴더가 생성됩니다(예: C:\Program Files (x86)\Windows Kits\10)\. 또한 \Windows Kits\10\Lib 아래에서 Windows 10 SDK 버전을 찾습니다. 이들 폴더가 보이지 않으면 Visual Studio를 다시 설치하고 설치하는 동중 Windows 10 SDK를 선택해야 합니다. U-SQL 로컬 컴파일러 스크립트는 이러한 종속성을 자동으로 찾습니다.

    ![Data Lake Tools for Visual Studio의 Windows 10 SDK 로컬 실행](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - [Visual Studio용 Data Lake 도구](http://aka.ms/adltoolsvs)를 설치합니다. 미리 패키지된 Visual C++ 및 Windows SDK 파일은 C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK에서 찾을 수 있습니다. 이 경우 U-SQL 로컬 컴파일러는 이러한 종속성을 자동으로 찾을 수 없습니다. 이에 대한 CppSDK 경로를 지정해야 합니다. 파일을 다른 위치로 복사하거나 그대로 사용할 수 있습니다. 그런 다음 **SCOPE_CPP_SDK** 환경 변수를 디렉터리에 설정하거나 로컬 실행 도우미 응용 프로그램의 명령줄에서 이 디렉터리와 함께 **-CppSDK** 인수를 지정하도록 선택할 수 있습니다.

SDK를 설치한 후에는 다음 구성 단계를 수행해야 합니다.

- **SCOPE_CPP_SDK** 환경 변수를 설정합니다.

    Data Lake Tools for Visual Studio를 설치하여 Microsoft Visual C++ 및 Windows SDK를 가져온 경우 다음 폴더가 있는지 확인합니다.

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    이 디렉터리를 가리키도록 **SCOPE_CPP_SDK**라는 새로운 환경 변수를 정의합니다. 또는 다른 위치에 폴더를 복사하고 **SCOPE_CPP_SDK**를 지정합니다.

    환경 변수를 설정하는 것 외에도 명령줄을 사용할 때 **-CppSDK** 인수를 지정할 수도 있습니다. 이 인수는 기본 CppSDK 환경 변수를 덮어씁니다.

- **LOCALRUN_DATAROOT** 환경 변수를 설정합니다.

    데이터 루트를 가리키는 **LOCALRUN_DATAROOT**라는 새로운 환경 변수를 정의합니다.

    환경 변수를 설정하는 것 외에도 명령줄을 사용할 때 데이터 루트 경로로 **-DataRoot** 인수를 지정할 수 있습니다. 이 인수는 기본 데이터 루트 환경 변수를 덮어씁니다. 모든 작업에 대해 기본 데이터 루트 환경 변수를 덮어 쓸 수 있도록 실행 중인 모든 명령줄에 이 인수를 추가해야 합니다.

### <a name="use-the-sdk-from-the-command-line"></a>명령줄에서 SDK 사용

#### <a name="command-line-interface-of-the-helper-application"></a>도우미 응용 프로그램의 명령줄 인터페이스

SDK에서 LocalRunHelper.exe는 일반적으로 사용되는 대부분의 로컬 실행 기능에 대한 인터페이스를 제공하는 명령줄 도우미 응용 프로그램입니다. 명령 및 인수 스위치는 모두 대소문자를 구분합니다. 도우미를 호출하려면 다음 명령을 사용합니다.

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

인수를 사용하지 않거나 다음과 같이 **help** 스위치와 함께 LocalRunHelper.exe를 실행하여 도움말 정보를 표시합니다.

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

도움말 정보에서 다음과 같이 구성됩니다.

-  **Command**: 명령의 이름을 제공합니다.  
-  **Required Argument**: 제공해야 하는 인수를 나열합니다.  
-  **Optional Argument**: 선택적이며 기본값을 갖는 인수를 나열합니다.  선택적 부울 인수에는 매개 변수가 없으며, 이 매개 변수의 출현은 기본값에 부정적이라는 것을 의미합니다.

#### <a name="return-value-and-logging"></a>반환 값 및 로깅

도우미 응용 프로그램은 성공한 경우 **0**을, 실패한 경우 **-1**을 반환합니다. 기본적으로 도우미는 모든 메시지를 현재 콘솔로 보냅니다. 그러나 대부분의 명령은 출력을 로그 파일로 리디렉션하는 **-MessageOut path_to_log_file** 선택적 인수를 지원합니다.


### <a name="sdk-usage-samples"></a>SDK 사용 샘플

#### <a name="compile-and-run"></a>컴파일 및 실행

**run** 명령은 스크립트를 컴파일한 다음 컴파일 결과를 실행하는 데 사용됩니다. 명령줄 인수는 **compile**과 **run**의 조합입니다.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

예를 들면 다음과 같습니다.

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

**compile**과 **run**을 조합하는 것 외에도 컴파일된 실행 파일을 개별적으로 컴파일하고 실행할 수 있습니다.

#### <a name="compile-a-u-sql-script"></a>U-SQL 스크립트 컴파일

**compile** 명령은 U-SQL 스크립트를 실행 파일로 컴파일하는 데 사용됩니다.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

다음은 컴파일용 선택적 인수입니다.

|인수|설명|
|--------|-----------|
|-CppSDK [기본값 '']|CppSDK 디렉터리입니다.|
|-DataRoot [기본값 '']|데이터 및 메타데이터의 루트 데이터입니다. **LOCALRUN_DATAROOT** 환경 변수로 기본 설정합니다.|
|-MessageOut [기본값 '']|콘솔의 메시지를 파일에 덤프합니다.|
|-Shallow [기본값 'False']|단순 컴파일입니다. 스크립트의 구문 검사 및 반환만 수행합니다.|
|-WorkDir [기본값 'D:\localrun\t\ScopeWorkDir']|컴파일러 사용 및 출력을 위한 디렉터리입니다. 자세한 내용은 부록의 "작업 디렉터리"를 참조하세요.|

다음은 어셈블리 및 코드 숨김을 위한 선택적 인수입니다.

|인수|설명|
|--------|-----------|
|-CodeBehind [기본값 'False']|스크립트가 .cs 코드 숨김을 포함하고 있는 표시기로, 자동으로 UDO(사용자 정의 개체)로 컴파일되고 등록됩니다.|
|-References [기본값 '']|';'으로 구분된 코드 참조의 추가 참조 어셈블리 또는 데이터 파일의 경로 목록입니다.|
|-UseDatabase [기본값 'master']|코드 숨김 임시 어셈블리 등록에 사용할 데이터베이스입니다.|
|-UdoRedirect [기본값 'False']|UDO가 호출될 때 먼저 컴파일된 출력 디렉터리에서 종속 어셈블리를 검사하도록 .NET 런타임에 지시하는 UDO 어셈블리 리디렉션 구성입니다.|

몇 가지 사용 예제는 다음과 같습니다.

U-SQL 스크립트를 컴파일합니다.

    LocalRunHelper compile -Script d:\test\test1.usql

U-SQL 스크립트를 컴파일하고 데이터 루트 폴더를 설정합니다. 이는 환경 변수 설정을 덮어 씁니다.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

U-SQL 스크립트를 컴파일하고 작업 디렉터리, 참조 어셈블리 및 데이터베이스를 설정합니다.

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>컴파일된 결과 실행

**execute** 명령은 컴파일된 결과를 실행하는 데 사용됩니다.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

다음은 선택적 인수입니다.

|인수|설명|
|--------|-----------|
|-DataRoot [기본값 '']|메타데이터 실행을 위한 루트 데이터입니다. **LOCALRUN_DATAROOT** 환경 변수로 기본 설정합니다.|
|-MessageOut [기본값 '']|콘솔의 메시지를 파일에 덤프합니다.|
|-Parallel [기본값 '1']|지정된 병렬 처리 수준으로 생성된 로컬 실행 단계를 실행하는 표시기입니다.|
|-Verbose [기본값 'False']|런타임의 자세한 출력을 보여주는 표시기입니다.|

사용 예는 다음과 같습니다.

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5

## <a name="use-the-sdk-with-programming-interfaces"></a>프로그래밍 인터페이스와 함께 SDK 사용

프로그래밍 인터페이스는 모두 Microsoft.Analytics.LocalRun 어셈블리에 있습니다. 이 인터페이스를 사용하여 U-SQL SDK 및 C# 테스트 프레임워크의 기능을 통합하여 U-SQL 스크립트 로컬 테스트의 크기를 조정할 수 있습니다. 인터페이스에 대한 자세한 정보는 부록을 참조하세요.

## <a name="appendix"></a>부록

### <a name="working-directory"></a>작업 디렉터리

U-SQL 스크립트를 로컬로 실행하면 컴파일 중에 작업 디렉터리가 만들어집니다. 컴파일 결과 외에도 로컬 실행에 필요한 런타임 파일이 이 작업 디렉터리에 섀도 복사됩니다. 명령줄에서 **-WorkDir** 인수를 지정하지 않으면 ScopeWorkDir 기본 작업 디렉터리가 현재 디렉터리 아래에 만들어집니다. 작업 디렉터리에 있는 파일은 다음과 같습니다.

|디렉터리/파일|정의|설명|
|--------------|----------|-----------|
|ScopeWorkDir|작업 디렉터리|루트 폴더|
|C6A101DDCB470506|런타임 버전의 해시 문자열|로컬 실행에 필요한 런타임 파일의 섀도 복사본|
|\.\Script_66AE4909AA0ED06C|스크립트 경로의 스크립트 이름 + 해시 문자열|컴파일 출력 및 실행 단계 로깅|
|\.\.\\_\_script\_\_.abr|컴파일러 출력|대수 파일|
|\.\.\\_\_ScopeCodeGen\_\_.*|컴파일러 출력|생성된 관리 코드|
|\.\.\\_\_ScopeCodeGenEngine\_\_.*|컴파일러 출력|생성된 네이티브 코드|
|\.\.\referenced_assemblies|어셈블리 참조|참조 어셈블리 파일|
|\.\.\deployed_resources|리소스 배포|리소스 배포 파일|
|\.\.\xxxxxxxx.xxx[1..n]_*.*|실행 로그|실행 단계에 대한 로그|

### <a name="programming-interfaces-for-the-azure-data-lake-u-sql-sdk"></a>Azure Data Lake U-SQL SDK용 프로그래밍 인터페이스

프로그래밍 인터페이스는 모두 Microsoft.Analytics.LocalRun 어셈블리에 있습니다.

#### <a name="microsoftanalyticslocalrunconfiguration"></a>Microsoft.Analytics.LocalRun.Configuration
Microsoft.Analytics.LocalRun.Configuration은 컴파일 구성 매개 변수 클래스입니다.

**생성자**

public Configuration(string rootPath)

|매개 변수|형식|설명|
|---------|----|-----------|
|rootPath|System.String|작업 중인 컨텍스트의 현재 디렉터리 경로입니다. WorkingDirectory가 설정되지 않은 경우 기본 작업 디렉터리는 rootPath + ScopeWorkDir입니다.|

**속성**

|이름|설명|
|----|-----------|
|CppSDK|시스템 기본 구성이 아닌 경우 CppSDK의 위치입니다. |
|DataDirectory|테이블, 어셈블리 및 입/출력 데이터가 저장된 위치입니다. 기본값은 ScopeWorkDir\DataDir입니다. |
|GenerateUdoRedirect|어셈블리 로딩 리디렉션 오버라이드 구성을 생성할지 여부를 나타내는 표시기입니다.|
|WorkingDirectory|컴파일러의 작업 디렉터리입니다. 기본값은 ScopeWorkDir입니다.|


#### <a name="microsoftanalyticslocalrunlocalcompiler"></a>Microsoft.Analytics.LocalRun.LocalCompiler
Microsoft.Analytics.LocalRun.LocalCompiler는 U-SQL 로컬 컴파일러 클래스입니다.

**생성자**

public LocalCompiler(Configuration configuration)

|매개 변수|형식|설명|
|---------|----|-----------|
|구성|Microsoft.Analytics.LocalRun.Configuration||

**메서드**

public bool Compile( string script, string filePath, bool shallow, out CommonCompileResult result )

|매개 변수|형식|설명|
|---------|----|-----------|
|script|System.String|입력 스크립트의 문자열입니다.|
|filePath|System.String|스크립트 파일의 경로입니다. null로 설정하여 기본값을 사용합니다.|
|shallow|System.Boolean|단순 컴파일(구문 확인만) 또는 전체 컴파일을 나타냅니다.|
|result|Microsoft.Cosmos.ClientTools.Shared.CommonCompileResult|자세한 컴파일 결과입니다.|
|Return Value|System.Boolean|True: 컴파일에서 심각한 오류가 없습니다. <br>False: 컴파일에서 심각한 오류가 있습니다.|

#### <a name="microsoftanalyticslocalrunlocalrunner--idisposable"></a>Microsoft.Analytics.LocalRun.LocalRunner : IDisposable
Microsoft.Analytics.LocalRun.LocalRunner : IDisposable은 U-SQL 로컬 runner 클래스입니다.

**생성자**

public LocalRunner( string algebraFilePath, string dataRoot, Action<string> postMessage = null )

|매개 변수|형식|설명|
|---------|----|-----------|
|algebraFilePath|System.String|대수 파일의 경로입니다.|
|dataRoot|System.String|DataRoot의 경로입니다.|
|postMessage(선택 사항)|System.Action<String>|진행률에 대한 로깅 처리기입니다.|

public LocalRunner( string algebraFilePath, string dataRoot, string cachePath, string runtimePath, string tempPath, string logPath, Action<Object, ExecutionStatusBase. ExecutionEventArgs> execEventHandler, Object eventContext, Action<string> postMessage = null )

|매개 변수|형식|설명|
|---------|----|-----------|
|algebraFilePath|System.String|대수 파일의 경로입니다.|
|dataRoot|System.String|DataRoot의 경로입니다.|
|cachePath|System.String|컴파일 결과의 디렉터리 경로입니다. null로 설정하여 대수 파일이 있는 기본값을 사용합니다.|
|runtimePath|System.String|섀도 복사 런타임의 디렉터리 경로입니다. null로 설정하여 cachePath의 부모 디렉터리가 있는 기본값을 사용합니다.|
|tempPath|System.String|임시 저장소 경로로, 내부 전용입니다. null로 설정합니다.|
|logPath|System.String|실행 로그를 쓸 위치 경로입니다. null로 설정하여 cachePath를 기본값으로 사용합니다.|
|execEventHandler|System. Action<Object, ExecutionStatusBase.ExecutionEventArgs>|실행 상태 변경을 위한 이벤트 알림 처리기입니다.|
|eventContext|System. Object|이벤트 처리기에 대한 컨텍스트입니다.|
|postMessage(선택 사항)|System.Action<String>|진행률에 대한 로깅 처리기입니다.|

**속성**

|이름|설명|
|----|-----------|
|AlgebraPath|대수 파일의 경로입니다.|
|CachePath|생성된 바이너리가 있는 컴파일러 결과 캐시 경로입니다.|
|CompletedSteps|완료된 단계의 수입니다.|
|DataRoot|메타데이터의 DataRoot입니다.|
|LastErrorMessage|(ExecutionStatusBase에서 상속됨)|
|LogPath|로깅 파일 저장 위치입니다. 이 위치가 없는 경우 Setter가 디렉터리를 만듭니다. 이전에 만든 로그 경로는 지워지지 않습니다.|
|OutputHeader|텍스트 출력에서 스키마 헤더를 덤프합니다.|
|병렬 처리|병렬 처리입니다. 논리 프로세서: 1로 기본 설정합니다. 시작 후 이를 변경하면 예외가 발생합니다.|
|진행|0-100% 비율의 실행 진행률입니다.|
|RuntimePath|런타임 파일의 위치입니다. 컴파일러에 의한 섀도 복사본인 경우 디렉터리 한 개가 CachePath 위에 있어야 합니다.|
|가동 상태|실행 상태입니다. <br><br>enum ExecutionStatusBase.ExecutionStatus <br>{ <br>Initialized, // Initialized. <br>Running,     // It is running.  이 상태에서는 WaitOne만 이벤트를 확인합니다. <br>Success,     // It finished successfully. <br>Error,       // It failed. <br>}|
|TotalSteps|실행할 총 단계 수입니다. 꼭짓점 DAG를 작성한 후에만 유효한 값을 사용할 수 있습니다.|
|자세한 정보 표시|실행 중에 표시되는 자세한 정보입니다.|

**메서드**

|메서드|설명|
|------|-----------|
|Cancel()|실행 중인 대수를 취소합니다. <br><br>반환 값 형식은 부울입니다. <br><br>false: 오류로 인해 취소하지 못했습니다라는 값이 반환됩니다. 자세한 내용은 LastErrorMessage를 확인합니다.|
|Start()|대수 실행을 시작합니다. <br><br>반환 값 형식은 부울입니다. <br><br>false: 오류로 인해 시작하지 못했습니다라는 값이 반환됩니다. 자세한 내용은 LastErrorMessage를 확인합니다.|
|WaitOne() <br>WaitOne(Int32) <br>WaitOne(TimeSpan) <br>WaitOne(Int32, Boolean) <br>WaitOne(TimeSpan, Boolean)|완료될 때까지 기다립니다. WaitHandle.WaitOne를 참조하세요.|
|Dispose()||


## <a name="next-steps"></a>다음 단계

* Data Lake Analytics에 대한 개요를 보려면 [Azure Data Lake Analytics 개요](data-lake-analytics-overview.md)를 참조하세요.
* U-SQL 응용 프로그램 개발을 시작하려면 [Visual Studio용 Data Lake 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.
* U-SQL을 알아보려면 [Azure Data Lake Analytics U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)을 참조하세요.
* 관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.
* 진단 정보를 기록하려면 [Azure Data Lake Analytics에 대한 진단 로그에 액세스](data-lake-analytics-diagnostic-logs.md)를 참조하세요.
* 더 복잡한 쿼리를 보려면 [Azure Data Lake Analytics을 사용하여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)을 참조하세요.
* 작업 세부 정보를 보려면, [Azure Data lake Analytics 작업에 대한 작업 브라우저 및 작업 보기 사용하기](data-lake-analytics-data-lake-tools-view-jobs.md)를 참조하세요.
* 꼭짓점 실행 보기를 사용하려면 [Data Lake Tools for Visual Studio에서 Vertex Execution View 사용](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)을 참조하세요.



<!--HONumber=Dec16_HO1-->


