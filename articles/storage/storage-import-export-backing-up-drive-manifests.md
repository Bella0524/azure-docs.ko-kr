---
title: "Azure Import/Export 드라이브 매니페스트 백업 | Microsoft Docs"
description: "Microsoft Azure Import/Export 서비스에 대한 드라이브 매니페스트를가 자동으로 백업하도록 하는 방법을 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
translationtype: Human Translation
ms.sourcegitcommit: 22e37e26fec913a7638c71b2547c38f5efacd10b
ms.openlocfilehash: 3d3abfb93ba09aa9f09258743ef6d4c1fc932ae5


---

# <a name="backing-up-drive-manifests"></a>드라이브 매니페스트 백업
드라이브 매니페스트는 [작업 배치](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 또는 [작업 속성 업데이트](/rest/api/storageimportexport/jobs#Jobs_Update) 작업에서 `BackupDriveManifest` 속성을 `true`로 설정하여 자동으로 Blob에 백업될 수 있습니다. 기본적으로 드라이브 매니페스트는 백업되지 않습니다. 드라이브 매니페스트 백업은 작업과 연결된 저장소 계정 내의 컨테이너에 블록 blob으로 저장됩니다. 기본적으로 컨테이너 이름은 `waimportexport`이지만 `Put Job` 또는 `Update Job Properties` 작업을 호출할 때 `DiagnosticsPath` 속성에서 다른 이름을 지정할 수 있습니다. 백업 매니페스트 blob은 다음과 같은 형식으로 이름이 지정됩니다: `waies/jobname_driveid_timestamp_manifest.xml`.

 [작업 가져오기](/rest/api/storageimportexport/jobs#Jobs_Get) 작업을 호출하여 작업의 백업 드라이브 매니페스트 URI를 검색할 수 있습니다. Blob URI는 각 드라이브에 대한 `ManifestUri` 속성으로 반환됩니다.

## <a name="see-also"></a>참고 항목
 [Import/Export 서비스 REST API 사용](storage-import-export-using-the-rest-api.md)



<!--HONumber=Dec16_HO3-->


