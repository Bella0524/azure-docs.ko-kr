---
title: "VM 재시작 또는 크기 조정 문제 | Microsoft Docs"
description: "Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 Resource Manager 배포 문제 해결"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
translationtype: Human Translation
ms.sourcegitcommit: 0782000e87bed0d881be5238c1b91f89a970682c
ms.openlocfilehash: f237c5ffe9e95d538959e2d622bb643c9986f0d2


---
# <a name="troubleshoot-resource-manager-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a>Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 Resource Manager 배포 문제 해결
중지된 Azure 가상 컴퓨터(VM)를 시작하거나, 기존 Azure AM의 크기를 조정하려다 접하는 일반적인 오류는 할당 오류입니다. 이런 오류는 클러스터나 지역에 사용할 수 있는 리소스가 없거나 요청한 VM 크기를 지원할 수 없을 때 발생합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>활동 로그 수집
문제 해결을 시작하려면 문제와 관련된 오류를 파악하기 위해 활동 로그를 수집합니다. 다음 링크에는 프로세스에 대한 자세한 내용이 포함되어 있습니다.

[배포 작업 보기](../azure-resource-manager/resource-manager-deployment-operations.md)

[활동 로그를 보고 Azure 리소스 관리](../azure-resource-manager/resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>문제: 중지된 VM 시작 시 오류
중지된 VM을 시작하려는데 할당 오류가 발생했습니다.

### <a name="cause"></a>원인
중지된 VM을 시작하기 위한 요청은 클라우드 서비스를 호스트하는 원본 클러스터에서 시도되어야 합니다. 하지만, 클러스터에 요청을 수행하는 데 사용할 여유 공간이 없습니다.

### <a name="resolution"></a>해결 방법
* 가용성 집합의 VM을 모두 중지하고 각각의 VM을 다시 시작합니다.
  
  1. **리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.
  2. VM을 모두 중지한 후에, 중지된 각각의 VM을 선택하고 시작을 클릭합니다.
* 나중에 다시 시작 요청을 다시 시도합니다.

## <a name="issue-error-when-resizing-an-existing-vm"></a>문제: 기존 VM 재시작 시 오류
기존 VM의 크기를 조정하려는데 할당 오류가 발생했습니다.

### <a name="cause"></a>원인
VM 크기를 조정하기 위한 요청은 클라우드 서비스를 호스트하는 원본 클러스터에서 시도되어야 합니다. 하지만, 클러스터가 요청한 VM 크기를 지원하지 않습니다.

### <a name="resolution"></a>해결 방법
* 더 작은 VM 크기를 사용하여 요청을 다시 시도합니다.
* 요청한 VM의 크기를 변경할 수 없으면:
  
  1. 가용성 집합의 VM을 모두 중지합니다.
     
     * **리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.
  2. VM을 모두 중지한 후에, 원하는 VM을 더 크게 조정합니다.
  3. 크기가 조정된 VM을 선택하고 **시작**을 클릭한 다음 중지된 각각의 VM을 시작합니다.

## <a name="next-steps"></a>다음 단계
Azure에서 새 Linux VM을 만들 때 문제가 발생하면 [Azure에서 새 Linux 가상 컴퓨터 생성 관련 배포 문제 해결](virtual-machines-linux-troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.




<!--HONumber=Jan17_HO2-->


