---
title: "Azure에서 앱 백업"
description: "Azure 앱 서비스에서 앱의 백업을 만드는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: cephalin
manager: wpickett
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
translationtype: Human Translation
ms.sourcegitcommit: b1a633a86bd1b5997d5cbf66b16ec351f1043901
ms.openlocfilehash: b00c320eeb1e8b30a0fad9634844ceeca60d1c29


---
# <a name="back-up-your-app-in-azure"></a>Azure에서 앱 백업
[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 의 백업 및 복원 기능을 사용하여 수동 또는 자동으로 앱 백업을 쉽게 만들 수 있습니다. 앱을 이전 상태로 복원하거나 원본 앱의 백업 중 하나를 기반으로 새 앱을 만들 수 있습니다. 

앱을 백업에서 복원하는 방법에 대한 자세한 내용은 [Azure에서 앱 복원](web-sites-restore.md)을 참조하세요.

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>백업 대상
앱 서비스는 다음 정보를 백업할 수 있습니다.

* 앱 구성
* 파일 콘텐츠
* 앱에 연결된 Azure SQL 데이터베이스 또는 Azure MySQL(ClearDB) 데이터베이스(백업에 포함할 대상을 선택할 수 있음)

이 정보는 지정한 Azure 저장소 계정 및 컨테이너로 백업됩니다. 

> [!NOTE]
> 각 백업은 증분 업데이트가 아니라 앱의 완전한 오프라인 복사본입니다.
> 
> 

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>요구 사항 및 제한 사항
* 백업 및 복원 기능을 사용하려면 앱 서비스 계획이 **표준** 계층 이상이어야 합니다. 더 높은 계층을 사용하도록 앱 서비스 계획을 확장하는 방법에 대한 자세한 내용은 [Azure에서 앱 확장](web-sites-scale.md)을 참조하세요. **프리미엄** 계층을 사용하면 **표준** 계층보다 더 많은 매일 백업이 수행됩니다.
* 백업하려는 앱과 동일한 구독에 Azure 저장소 계정 및 컨테이너가 필요합니다. Azure 저장소 계정에 대한 자세한 내용은 이 문서의 끝에 있는 [링크](#moreaboutstorage) 를 참조하십시오.
* 최대 10GB의 앱 및 데이터베이스 콘텐츠를 백업할 수 있습니다. 백업 크기가 이 제한을 초과하면 오류가 발생합니다. 

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>수동 백업 만들기
1. [Azure Portal](https://portal.azure.com)에서 앱의 블레이드로 이동한 후 **설정**을 선택하고 **백업**을 선택합니다. **백업** 블레이드가 표시됩니다.
   
    ![백업 페이지][ChooseBackupsPage]
   
   > [!NOTE]
   > 아래와 같은 메시지가 나타나면 백업을 계속 진행하기 전에 클릭하여 앱 서비스 계획을 업그레이드해야 합니다.
   > 자세한 내용은 [Azure에서 앱 확장](web-sites-scale.md) 을 참조하세요.  
   > ![저장소 계정 선택](./media/web-sites-backup/01UpgradePlan.png)
   > 
   > 
2. **백업** 블레이드에서 **저장소: 구성되지 않음**을 클릭하여 저장소 계정을 구성합니다.
   
    ![저장소 계정 선택][ChooseStorageAccount]
3. **저장소 계정** 및 **컨테이너**를 선택하여 백업 대상을 선택합니다. 저장소 계정은 백업할 앱이 있는 동일한 구독에 속해야 합니다. 필요한 경우 각 블레이드에서 새 저장소 계정이 나 새 컨테이너를 만들 수 있습니다. 완료되면 **선택**을 클릭합니다.
   
    ![저장소 계정 선택](./media/web-sites-backup/02ChooseStorageAccount1.png)
4. 왼쪽에 열여 있는 **백업 설정 구성** 블레이드에서 **데이터베이스 설정**을 클릭하고 백업에 포함할 데이터베이스(SQL Database 또는 MySQL)를 선택한 다음 **확인**을 클릭합니다.  
   
    ![저장소 계정 선택](./media/web-sites-backup/03ConfigureDatabase.png)
   
   > [!NOTE]
   > 이 목록에 표시될 데이터베이스의 경우 연결 문자열은 앱의 **응용 프로그램 설정** 블레이드에서 **연결 문자열** 섹션에 있어야 합니다.
   > 
   > 
5. **백업 설정 구성** 블레이드에서 **저장**을 클릭합니다.    
6. **백업** 블레이드 명령 모음에서 **지금 백업**을 클릭합니다.
   
    ![BackUpNow 단추][BackUpNow]
   
    백업 프로세스를 수행하는 동안 진행 메시지가 나타납니다.

백업에 대한 저장소 계정 및 컨테이너를 구성한 후에는 언제든지 수동 백업을 만들 수 있습니다.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>자동화된 백업 구성
1. **백업** 블레이드에서 **일정: 구성되지 않음**을 클릭합니다. 
   
    ![저장소 계정 선택](./media/web-sites-backup/05ScheduleBackup.png)
2. **백업 일정 설정** 블레이드에서 **예약된 백업**을 **켜기**로 설정하고 원하는 대로 백업 일정을 구성한 다음 **확인**을 클릭합니다.
   
    ![자동 백업 사용][SetAutomatedBackupOn]
3. 왼쪽에 열려 있는 **백업 설정 구성** 블레이드에서 **저장소 설정**을 클릭한 다음 **저장소 계정** 및 **컨테이너**를 선택하여 백업 대상을 선택합니다. 저장소 계정은 백업할 앱이 있는 동일한 구독에 속해야 합니다. 필요한 경우 각 블레이드에서 새 저장소 계정이 나 새 컨테이너를 만들 수 있습니다. 완료되면 **선택**을 클릭합니다.
   
    ![저장소 계정 선택](./media/web-sites-backup/02ChooseStorageAccount1.png)
4. **백업 설정 구성** 블레이드에서 **데이터베이스 설정**을 클릭하고 백업에 포함할 데이터베이스(SQL Database 또는 MySQL)를 선택한 다음 **확인**을 클릭합니다.  
   
    ![저장소 계정 선택](./media/web-sites-backup/03ConfigureDatabase.png)
   
   > [!NOTE]
   > 이 목록에 표시될 데이터베이스의 경우 연결 문자열은 앱의 **응용 프로그램 설정** 블레이드에서 **연결 문자열** 섹션에 있어야 합니다.
   > 
   > 
5. **백업 설정 구성** 블레이드에서 **저장**을 클릭합니다.    

<a name="partialbackups"></a>

## <a name="backup-just-part-of-your-app"></a>앱의 일부만 백업
앱의 모든 것을 백업하고 싶지 않을 때도 있습니다. 다음은 몇 가지 예입니다.

* 오래된 블로그 게시물이나 이미지처럼 변하지 않는 정적 콘텐츠가 포함된 앱의 [주별 백업을 설정](web-sites-backup.md#configure-automated-backups) 합니다.
* 앱에는 10GB 이상의 콘텐츠가 있습니다(한 번에 백업할 수 있는 최대 용량).
* 로그 파일은 백업하지 않아도 됩니다.

부분 백업을 사용하여 백업할 파일을 정확히 선택할 수 있습니다.

### <a name="exclude-files-from-your-backup"></a>백업에서 파일 제외
백업에서 파일 및 폴더를 제외하려면 앱의 D:\home\site\wwwroot 폴더에 `_backup.filter` 파일을 만들고 제외하려는 파일 및 폴더 목록을 지정합니다. 이 곳은 [Kudu 콘솔](https://github.com/projectkudu/kudu/wiki/Kudu-console)을 통해 쉽게 액세스할 수 있습니다. 

앱에 지난 몇 년 동안의 로그 파일과 정적 이미지가 포함되어 있다고 가정해 보겠습니다. 이러한 항목들은 앞으로도 변하지 않습니다. 여러분은 오래된 이미지가 포함된 앱을 이미 완벽히 백업해두었습니다. 이제 매일 앱을 백업하려고 하지만 변경되지 않는 정적 이미지 파일 또는 로그 파일을 저장하는 비용은 지불하고 싶지 않습니다.

![로그 폴더][LogsFolder]
![이미지 폴더][ImagesFolder]

다음 단계는 백업에서 이들 파일을 제외하는 방법을 보여줍니다.

1. `http://{yourapp}.scm.azurewebsites.net/DebugConsole` 로 이동하여 백업에서 제외하려는 폴더를 찾습니다. 이 예제에서는 해당 UI에 표시된 다음 파일 및 폴더를 제외하고자 합니다.
   
        D:\home\site\wwwroot\Logs
        D:\home\LogFiles
        D:\home\site\wwwroot\Images\2013
        D:\home\site\wwwroot\Images\2014
        D:\home\site\wwwroot\Images\brand.png
   
    [AZURE.NOTE] 마지막 줄은 개별 파일 및 폴더를 제외할 수 있음을 보여 줍니다.
2. `_backup.filter`라는 파일을 만들고 위 목록을 파일에 저장하지만 `D:\home`을 제거합니다. 줄당 하나의 디렉터리 또는 파일을 나열하세요. 파일의 내용은 다음과 같아야 합니다.
   
    \site\wwwroot\Logs  \LogFiles  \site\wwwroot\Images\2013  \site\wwwroot\Images\2014  \site\wwwroot\Images\brand.png
3. [ftp](web-sites-deploy.md#ftp) 또는 다른 방법을 사용하여 이 파일을 해당 사이트의 `D:\home\site\wwwroot\` 디렉터리에 업로드합니다. 필요한 경우 `http://{yourapp}.scm.azurewebsites.net/DebugConsole` 에서 직접 파일을 만들고 콘텐츠를 삽입할 수도 있습니다.
4. 이제 평소와 같이 [수동](#create-a-manual-backup) 또는 [자동](#configure-automated-backups)으로 백업을 실행합니다.

이제 `_backup.filter`에 지정된 모든 파일 및 폴더가 백업에서 제외됩니다. 이 예제에서는 로그 파일과 2013 및 2014 이미지 파일은 이제 더 이상 백업되지 않습니다. brand.png로 마찬가지입니다.

> [!NOTE]
> [정기 백업을 복원](web-sites-restore.md)할 때와 동일한 방법으로 사이트의 부분 백업을 복원합니다. 복원 프로세스는 올바른 일을 수행합니다.
> 
> 전체 백업이 복원되면 해당 사이트의 모든 콘텐츠가 백업에 있는 항목들로 대체됩니다. 파일이 사이트에 있지만 백업에 없는 경우 해당 파일은 삭제됩니다. 하지만 부분 백업이 복원되면 블랙 리스트 디렉터리에 위치한 모든 콘텐츠 또는 블랙 리스트에 포함된 모든 파일이 그대로 유지됩니다.
> 
> 

<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>백업 저장 방법
앱에 대해 하나 이상의 백업을 수행한 경우 앱뿐만 아니라 저장소 계정의 **컨테이너** 블레이드에도 백업이 표시됩니다. 저장소 계정에서, 각 백업은 백업 데이터가 포함된 .zip 파일과 그 .zip 파일 콘텐츠의 매니페스트가 포함된 .xml 파일로 구성되어 있습니다. 실제로 앱 복원을 수행하지 않고 백업에 액세스하고자 한다면 이들 파일의 압축을 풀고 찾아볼 수 있습니다.

앱에 대한 데이터베이스 백업이 .zip 파일의 루트에 저장됩니다. SQL 데이터베이스의 경우 이 파일은 BACPAC 파일(파일 확장명 없음)이며, 가져올 수 있습니다. BACPAC 내보내기를 기반으로 하여 새 SQL 데이터베이스를 만들려면 [BACPAC 파일을 가져와 새 사용자 데이터베이스 만들기](http://technet.microsoft.com/library/hh710052.aspx)를 참조하세요.

> [!WARNING]
> **websitebackups** 컨테이너에 있는 파일을 변경하면 백업이 잘못되어 복원할 수 없게 됩니다.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>다음 단계
앱을 백업에서 복원하는 방법에 대한 자세한 내용은 [Azure에서 앱 복원](web-sites-restore.md)을 참조하세요. 또한 REST API를 사용하여 앱 서비스 앱을 백업 및 복원할 수 있습니다( [REST를 사용하여 앱 서비스 앱 백업 및 복원](websites-csm-backup.md)참조).

> [!NOTE]
> Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png




<!--HONumber=Jan17_HO3-->


