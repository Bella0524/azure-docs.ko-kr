---
title: "Azure IaaS VM 디스크에 대한 질문과 대답(FAQ) | Microsoft Docs"
description: "Azure IaaS VM 디스크 및 프리미엄 디스크(관리 및 관리되지 않는 디스크)에 대한 질문과 대답"
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: ramankum
translationtype: Human Translation
ms.sourcegitcommit: 0746c954e669bd739b8ecfcddaf287cb5172877f
ms.openlocfilehash: 95b627738726f3c108fff38bfeda413303b2c718


---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Azure IaaS VM 디스크와 관리 및 관리되지 않는 프리미엄 디스크에 대한 질문과 대답

이 문서에서는 Managed Disks 및 Premium Storage에 대한 자주 묻는 질문과 대답 중 일부를 알아봅니다.

## <a name="managed-disks"></a>Managed Disks

**Azure Managed Disks란?**

Managed Disks는 저장소 계정 관리를 처리하여 Azure IaaS VM을 위한 디스크 관리를 간소화하는 기능입니다. 자세한 내용은 [Managed Disks 개요](storage-managed-disks-overview.md)를 참조하세요.

**크기가 80GB인 기존 VHD에서 표준 관리 디스크를 만들 경우 비용은 얼마나 드나요?**

80GB VHD로 만든 표준 관리 디스크는 그 다음 프리미엄 디스크 크기인 S10으로 취급됩니다. S10 디스크 가격 책정에 따라 대금이 청구됩니다. 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)를 확인하세요.

**표준 관리 디스크에 대한 트랜잭션 비용이 있나요?**

예, 각 트랜잭션에 대해 요금이 부과됩니다. 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)를 확인하세요.

**표준 관리 디스크에 대한 요금은 디스크에 있는 데이터의 실제 크기에 대해 부과되나요? 아니면 디스크의 프로비전된 용량에 대해 부과되나요?**

디스크의 프로비전된 용량에 따라 청구됩니다. 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)를 확인하세요.

**프리미엄 관리 디스크의 가격은 관리되지 않는 디스크와 어떻게 다르게 책정되나요?**

프리미엄 관리 디스크의 가격은 관리되지 않는 프리미엄 디스크와 같습니다.

**내 관리 디스크의 저장소 계정 유형(표준/프리미엄)을 내가 변경할 수 있나요?**

예. Azure Portal, PowerShell 또는 Azure CLI를 사용하여 관리 디스크의 저장소 계정 유형을 변경할 수 있습니다.

**개인 저장소 계정에 관리 디스크를 복사하거나 내보낼 수 있는 방법이 있나요?**

예, Azure Portal, PowerShell 또는 Azure CLI를 사용하여 관리 디스크를 내보낼 수 있습니다.

**Azure Storage 계정에서 VHD 파일을 사용하여 다른 구독에 관리 디스크를 만들 수 있나요?**

아니요.

**Azure Storage 계정에서 VHD 파일을 사용하여 다른 지역에 관리 디스크를 만들 수 있나요?**

아니요.

**고객이 관리 디스크를 사용하기 위한 규모 제한이 있나요?**

Managed Disks는 저장소 계정과 관련된 한도를 없앱니다. 그러나 구독당 관리 디스크의 수는 기본적으로 2000개로 제한됩니다. 이 제한은 지원 부서에 문의하여 늘릴 수 있습니다.

**관리 디스크의 증분 스냅숏을 가져올 수 있나요?**

아니요. 현재 스냅숏 기능은 관리 디스크의 전체 복사본을 만듭니다. 그러나 나중에는 증분 스냅숏을 지원하도록 할 계획입니다.

**가용성 집합에서 VM을 관리 및 관리되지 않는 디스크로 혼합 구성할 수 있나요?**

아니요, 가용성 집합에 있는 VM은 모두 관리 디스크를 사용하거나 모두 관리되지 않는 디스크를 사용해야 합니다. 가용성 집합을 만들 때 사용할 디스크 유형을 사용자가 선택할 수 있습니다.

**Managed Disks가 Azure Portal에서 기본 옵션인가요?**

현재는 아니지만 나중에는 기본 옵션으로 사용될 예정입니다.

**내가 빈 관리 디스크를 만들 수 있나요?**

예, 사용자가 빈 디스크를 만들 수 있습니다. 관리 디스크는 VM에 독립적으로 즉, VM에 연결하지 않고 만들 수 있습니다.

**Managed Disks를 사용하는 가용성 집합에 대해 지원되는 장애 도메인 수는 몇 개인가요?**

위치한 지역에 따라 Managed Disks를 사용하는 관리 디스크에 대해 지원되는 장애 도메인 수는 2개 또는 3개입니다.

**진단을 위한 표준 저장소 계정은 어떤 방식으로 설정되나요?**

VM 진단을 위한 개인 저장소 계정을 설정할 수 있습니다. 향후에는 진단 역시 Managed Disks로 전환할 계획입니다.

**Managed Disks에 대해 어떤 종류의 RBAC 지원이 제공되나요?**

Managed Disks에서는 세 가지 주요 기본 역할을 지원합니다.

1.  소유자: 액세스를 포함한 모든 것을 관리할 수 있습니다.

2.  참여자: 액세스를 제외한 모든 것을 관리할 수 있습니다.

3.  읽기 권한자: 모든 항목을 볼 수 있지만 변경할 수는 없습니다.

**개인 저장소 계정에 관리 디스크를 복사하거나 내보낼 수 있는 방법이 있나요?**

관리 디스크에 대한 읽기 전용 공유 액세스 서명(SAS) URI를 가져온 후 이를 사용하여 개인 저장소 계정 또는 온-프레미스 저장소에 콘텐츠를 복사할 수 있습니다.

**내 관리 디스크의 복사본을 만들 수 있나요?**

사용자는 관리 디스크의 스냅숏을 만든 후 이 스냅숏을 사용하여 다른 관리 디스크를 만들 수 있습니다.

**관리되지 않는 디스크도 계속 지원되나요?**

예, 관리 및 관리되지 않는 디스크가 모두 지원됩니다. 그러나, 새 워크로드에 대해서는 관리 디스크를 사용하여 시작하고 현재 워크로드를 Managed Disks로 마이그레이션하는 것이 좋습니다.

**크기가 128GB인 디스크를 만든 후 130GB로 크기를 증가시키려는 경우 다음 디스크 크기(512GB)에 대한 요금이 부과되나요?**

예.

**내가 LRS, GRS 및 ZRS Managed Disks를 만들 수 있나요?**

Azure Managed Disks에서는 현재 로컬 중복 저장소(LRS)만 지원됩니다.

## <a name="premium-disks--both-managed-and-unmanaged"></a>프리미엄 디스크 - 관리 및 관리되지 않는 디스크

**VM에서 DSv2와 같이 Premium Storage를 지원하는 크기를 사용하는 경우 프리미엄 및 표준 데이터 디스크를 모두 연결할 수 있나요?** 

예.

**프리미엄 및 표준 데이터 디스크를 모두 D, Dv2, G 또는 F 시리즈와 같이 Premium Storage를 지원하지 않는 크기에 연결할 수 있나요?**

아니요. Premium Storage를 지원하는 크기를 사용하지 않는 VM에는 표준 데이터 디스크만 연결할 수 있습니다.

**크기가 80GB인 기존 VHD로 프리미엄 데이터 디스크를 만들 경우 비용은 얼마가 드나요?**

80GB VHD로 만든 프리미엄 데이터 디스크는 그 다음 프리미엄 디스크 크기인 P10으로 취급됩니다. P10 디스크 가격 책정에 따라 대금이 청구될 것입니다.

**Premium Storage를 사용할 때 발생하는 트랜잭션 비용이 있나요?**

특정 한도의 IOPS 및 처리량이 프로비전되는 디스크 크기마다 고정 비용이 있습니다. 기타 비용은 아웃바운드 대역폭 및 스냅숏 용량입니다(해당하는 경우). 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)를 확인하세요.

**디스크 캐시에서 가져올 수 있는 IOPS 및 처리량 한도는 얼마나 되나요?**

DS 시리즈의 캐시 및 로컬 SSD에 대한 결합 제한은 코어당 4000 IOPS 및 코어당 초당 33MB입니다. GS 시리즈는 코어당 5000 IOPS 및 코어당 초당 50MB를 제공합니다.

**Managed Disks VM에 대해 로컬 SSD가 지원되나요?**

로컬 SSD는 Managed Disks VM에 포함되어 있는 임시 저장소입니다. 이 임시 저장소에 대한 추가 비용은 없습니다. 이 로컬 SSD는 Azure Blob Storage에 보존되지 않으므로 응용 프로그램 데이터를 저장하는 용도로 사용하지 않는 것이 좋습니다.

## <a name="what-if-my-question-isnt-answered-here"></a>여기서 내 질문에 대답하지 않으면 어떻게 하나요?

질문하려는 내용이 아래 목록에 나와 있지 않으면 알려 주세요. 대답을 확인하는 방법을 알려 드리겠습니다. 이 문서의 끝에서 주석이나 MSDN [Azure Storage 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)에 질문을 게시하여 Azure Storage 팀 및 다른 커뮤니티 회원과 이 문서에 대해 논의할 수 있습니다.

기능을 요청하려면 요청 내용과 아이디어를 [Azure Storage 피드백 포럼](https://feedback.azure.com/forums/217298-storage)으로 제출해 주세요.


<!--HONumber=Feb17_HO2-->


