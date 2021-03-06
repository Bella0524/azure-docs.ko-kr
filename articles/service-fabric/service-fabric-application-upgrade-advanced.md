---
title: "고급 응용 프로그램 업그레이드 항목 | Microsoft Docs"
description: "이 문서에서는 서비스 패브릭 응용 프로그램 업그레이드와 관련된 고급 항목을 다룹니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: subramar
translationtype: Human Translation
ms.sourcegitcommit: f1e035b50b415f68ce567fe1db3a3fe93c2a1394
ms.openlocfilehash: 63d7ca0224c1989618c474181b02fa79eb69c966


---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>서비스 패브릭 응용 프로그램 업그레이드: 고급 항목
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>응용 프로그램을 업그레이드하는 동안 서비스 추가 또는 제거
새 서비스가 이미 배포된 응용 프로그램에 추가되고 업그레이드로 게시되면 새 서비스는 배포된 응용 프로그램에 추가됩니다.  이러한 업그레이드는 응용 프로그램에 이미 속하는 서비스에는 영향을 주지 않습니다. 하지만 새 서비스가 활성화( `New-ServiceFabricService` cmdlet 사용)되려면 추가된 서비스 인스턴스가 시작되어야 합니다.

업그레이드의 일부로 응용 프로그램에서 서비스를 제거할 수도 있습니다. 그러나 업그레이드를 계속하기 전에 삭제하려는 서비스의 모든 현재 인스턴스를 중지해야 합니다( `Remove-ServiceFabricService` cmdlet 사용).

## <a name="manual-upgrade-mode"></a>수동 업그레이드 모드
> [!NOTE]
> 모니터링되지 않는 수동 모드는 업그레이드가 실패 또는 일시 중단된 경우에만 고려해야 합니다. 서비스 패브릭 응용 프로그램에 권장되는 업그레이드 모드는 모니터링 모드입니다.
>
>

Azure 서비스 패브릭은 개발 및 프로덕션 클러스터를 지원하는 여러 업그레이드 모드를 제공합니다. 선택한 배포 옵션은 환경마다 다를 수 있습니다.

모니터링되는 롤링 응용 프로그램 업그레이드는 프로덕션 환경에서 가장 많이 사용되는 업그레이드입니다. 업그레이드 정책이 지정되면 서비스 패브릭에서는 응용 프로그램이 정상인지 확인한 후 업그레이드를 계속 진행합니다.

 응용 프로그램 관리자는 수동 롤링 응용 프로그램 업그레이드 모드를 사용하여 여러 업그레이드 도메인의 모든 업그레이드 진행 상황을 제어할 수 있습니다. 이 모드는 응용 프로그램의 데이터가 이미 손실된 경우처럼 사용자 지정 또는 복잡한 상태 평가 정책이 필요하거나 일반적이지 않은 업그레이드가 수행될 때 유용합니다.

마지막으로 자동화된 롤링 응용 프로그램 업그레이드는 서비스를 개발하는 동안 개발 또는 테스트 환경에서 빠른 반복 주기를 제공하는 데  유용합니다.

## <a name="change-to-manual-upgrade-mode"></a>수동 업그레이드 모드로 변경
**수동**--현재 UD에서 응용 프로그램 업그레이드를 중지하고 업그레이드 모드를 모니터링되지 않은 수동 모드로 변경합니다. 관리자가 수동으로 **MoveNextApplicationUpgradeDomainAsync** 를 호출하고 새 업그레이드를 초기화하여 업그레이드를 진행하거나 롤백을 트리거해야 합니다. 업그레이드가 수동 모드로 전환되면 새 업그레이드가 초기화될 때까지 수동 모드가 유지됩니다. **GetApplicationUpgradeProgressAsync** 명령은 FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING을 반환합니다.

## <a name="upgrade-with-a-diff-package"></a>diff 패키지로 업그레이드
완전한 자체 포함 응용 프로그램 패키지로 프로비전하여 서비스 패브릭 응용 프로그램을 업그레이드할 수 있습니다. 또한 업데이트된 응용 프로그램 파일과 업데이트된 응용 프로그램 매니페스트 및 서비스 매니페스트 파일만 포함하는 diff 패키지를 사용하여 응용 프로그램을 업그레이드할 수도 있습니다.

전체 응용 프로그램 패키지에는 서비스 패브릭 응용 프로그램을 시작 및 실행하는 데 필요한 모든 파일이 포함되어 있습니다. diff 패키지는 마지막 프로비전과 현재 업그레이드 사이에 변경된 파일과 전체 응용 프로그램 매니페스트 및 서비스 매니페스트 파일만 포함합니다. 빌드 레이아웃에서 찾을 수 없는 응용 프로그램 매니페스트 또는 서비스 매니페스트의 모든 참조는 이미지 저장소에서 검색됩니다.

전체 응용 프로그램 패키지는 클러스터에 응용 프로그램을 처음으로 설치할 때 필요합니다. 후속 업데이트는 전체 응용 프로그램 패키지도 가능하고 diff 패키지도 가능합니다.

다음과 같은 경우에는 diff 패키지를 사용하는 것이 좋습니다.

* 여러 서비스 매니페스트 파일 및/또는 여러 코드 패키지, config 패키지 또는 데이터 패키지를 참조하는 대형 응용 프로그램 패키지가 있는 경우에는 diff 패키지가 좋습니다.
* 응용 프로그램 빌드 프로세스에서 직접 빌드 레이아웃을 생성하는 배포 시스템을 사용하는 경우에는 diff 패키지가 좋습니다. 이 경우 코드가 변경되지 않았더라도 새로 빌드된 어셈블리는 다른 체크섬을 갖습니다. 전체 응용 프로그램 패키지를 사용하려면 모든 코드 패키지의 버전을 업데이트해야 합니다. diff 패키지를 사용하면 변경된 파일과 버전이 변경된 매니페스트 파일만 제공하면 됩니다.

Visual Studio를 사용하여 응용 프로그램이 업그레이드되는 경우 diff 패키지가 자동으로 게시됩니다. diff 패키지를 수동으로 만들려면 응용 프로그램 매니페스트 및 서비스 매니페스트를 업데이트해야 하지만 변경된 패키지만 최종 응용 프로그램 패키지에 포함되어야 합니다.

예를 들어 다음 응용 프로그램을 시작하겠습니다(이해하기 쉽도록 버전 번호 제공).

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

이제 PowerShell을 사용하여 diff 패키지로 service1의 코드 패키지만 업데이트하려고 한다고 가정해 보겠습니다. 이제 업데이트된 응용 프로그램은 다음과 같은 폴더 구조를 갖습니다.

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

이 경우 응용 프로그램 매니페스트를 2.0.0으로 업데이트하고 service1에 대한 서비스 매니페스트가 코드 패키지 업데이트를 반영하도록 업데이트합니다. 응용 프로그램 패키지에 대한 폴더 구조는 다음과 같습니다.

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>다음 단계
[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.

[데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)사용 방법을 익혀 응용 프로그램 업그레이드와 호환되도록 만듭니다.

[응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)의 단계를 참조하여 응용 프로그램 업그레이드 중 발생하는 일반적인 문제를 해결합니다.



<!--HONumber=Jan17_HO1-->


