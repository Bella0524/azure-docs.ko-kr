---
title: "Azure Import/Export 서비스 REST API 사용 | Microsoft Docs"
description: "Azure Import/Export 서비스 REST API를 사용하는 방법을 알아봅니다"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
translationtype: Human Translation
ms.sourcegitcommit: 22e37e26fec913a7638c71b2547c38f5efacd10b
ms.openlocfilehash: 675aef8ec0f9344d2b3073021e83856c2fb34b7c


---
# <a name="using-the-azure-importexport-service-rest-api"></a>Azure Import/Export 서비스 REST API 사용

Microsoft Azure Import/Export 서비스는 내보내기/가져오기 작업을 프로그래밍 방식으로 제어하도록 설정하는 REST API를 노출합니다. REST API를 사용하여 [Azure Portal](https://portal.azure.com/)에서 수행할 수 있는 모든 가져오기/내보내기 작업을 수행할 수 있습니다. 또한 REST API를 사용하여 클래식 포털에서는 현재 사용할 수 없는 작업 완료 비율을 쿼리하는 등의 특정 세부적인 작업을 수행할 수 있습니다.

Import/Export 서비스에 대한 개요 및 클래식 포털을 사용하여 가져오기 및 내보내기 작업을 만들고 관리하는 방법을 보여 주는 자습서는 [Microsoft Azure Import/Export 서비스를 사용하여 데이터를 Blob Storage로 전송](storage-import-export-service.md)을 참조하세요.

## <a name="service-endpoints"></a>서비스 끝점

Azure Import/Export 서비스는 Azure Resource Manager의 리소스 공급자이며 가져오기/내보내기 작업을 관리하기 위해 다음 HTTPS 끝점에서 REST API 집합을 제공합니다.

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>버전 관리

Import/Export 서비스에 대한 요청은 `api-version` 매개 변수를 지정하고 해당 값을 `2016-11-01`로 설정해야 합니다.

## <a name="in-this-section"></a>섹션 내용

[가져오기 작업 만들기](storage-import-export-creating-an-import-job.md)

[내보내기 작업 만들기](storage-import-export-creating-an-export-job.md)

[작업에 대한 상태 정보 검색](storage-import-export-retrieving-state-info-for-a-job.md)

[작업 열거](storage-import-export-enumerating-jobs.md)

[작업 취소 및 삭제](storage-import-export-cancelling-and-deleting-jobs.md)

[드라이브 매니페스트 백업](storage-import-export-backing-up-drive-manifests.md)

[Import-Export 작업에 대한 진단 및 오류 복구](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="see-also"></a>참고 항목
 [저장소 Import/Export REST](/rest/api/storageimportexport)



<!--HONumber=Dec16_HO3-->


