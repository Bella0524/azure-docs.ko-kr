---
title: "Azure의 Windows VM 배포 모델 간 마이그레이션 | Microsoft Docs"
description: "이 문서에서는 플랫폼 지원 방식으로 클래식에서 Azure Resource Manager로 리소스를 마이그레이션하는 과정의 기술적 측면을 설명합니다."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ee40d32-a5e8-42a2-97d0-3232fd3cbb98
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: kasing
translationtype: Human Translation
ms.sourcegitcommit: d835d5825268a4ec0fa5b761f9b5714e3236b0ce
ms.openlocfilehash: 2dd35a65d1b5b6db1401cdf5737b5355aa6d564b


---
# <a name="technical-deep-dive-on-platform-supported-migration-from-classic-to-azure-resource-manager"></a>클래식에서 Azure Resource Manager로의 플랫폼 지원 마이그레이션에 대한 기술 정보
Azure 클래식 배포 모델에서 Azure Resource Manager 배포 모델로 마이그레이션하는 방법을 자세하게 살펴보겠습니다. Azure 플랫폼에서 두 가지 배포 모델 간에 리소스를 마이그레이션하는 방법을 더욱 잘 이해할 수 있도록 리소스 및 기능 수준에서 리소스를 검토합니다. 자세한 내용은 서비스 발표 문서 [클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션](virtual-machines-windows-migration-classic-resource-manager.md)을 읽어보세요.

## <a name="detailed-guidance-on-migration"></a>마이그레이션에 대한 자세한 지침
다음 표에서 클래식 및 Resource Manager에서 리소스를 표현하는 방식을 확인할 수 있습니다. 다른 기능 및 리소스는 현재 지원되지 않습니다.

| 클래식 표현 | Resource Manager 표현 | 자세한 정보 |
| --- | --- | --- |
| 클라우드 서비스 이름 |DNS 이름 |마이그레이션하는 동안 명명 패턴 `<cloudservicename>-migrated`를 사용하여 모든 클라우드 서비스에 대한 새 리소스 그룹을 만듭니다. 이 리소스 그룹에는 모든 리소스가 포함됩니다. 클라우드 서비스 이름은 공용 IP 주소와 연결된 DNS 이름이 됩니다. |
| 가상 컴퓨터 |가상 컴퓨터 |VM 관련 속성은 변경되지 않고 마이그레이션됩니다. 클래식 배포 모델에서는 컴퓨터 이름 등의 특정 osProfile 정보가 저장되지 않으므로 마이그레이션 후 빈 상태로 유지됩니다. |
| VM에 연결된 디스크 리소스 |VM에 연결된 암시적 디스크 |Resource Manager 배포 모델에서는 디스크가 최상위 리소스로 모델링되지 않습니다. VM에서 암시적 디스크로 마이그레이션됩니다. 현재 VM에 연결되어 있는 디스크만 지원됩니다. Resource Manager VM은 이제 클래식 저장소 계정을 사용할 수 있습니다. 이를 통해 업데이트하지 않고도 디스크를 쉽게 마이그레이션할 수 있습니다. |
| VM 확장 |VM 확장 |클래식 배포 모델에서는 XML 확장을 제외한 모든 리소스 확장이 마이그레이션됩니다. |
| 가상 컴퓨터 인증서 |Azure 키 자격 증명 모음의 인증서 |클라우드 서비스에 서비스 인증서가 포함된 경우 클라우드 서비스당 새 Azure 주요 자격 증명 모음이 생성되고 주요 자격 증명 모음으로 인증서가 이동됩니다. VM이 업데이트되면서 주요 자격 증명 모음의 인증서를 참조합니다. <br><br> **참고:** VM이 실패한 상태로 전환될 수 있으므로 keyvault를 삭제하지 않습니다. Key Vaults을 안전하게 삭제하거나 VM과 함께 새 구독으로 이동할 수 있도록 백 엔드의 기능 향상에 최선을 다하고 있습니다. |
| WinRM 구성 |osProfile 하의 WinRM 구성 |Windows 원격 관리 구성은 마이그레이션의 일부로 변경되지 않은 상태로 이동됩니다. |
| 가용성 집합 속성 |가용성 집합 리소스 |클래식 배포 모델에서 가용성 집합 사양은 VM의 속성이었습니다. 마이그레이션에서는 가용성 집합이 최상위 리소스가 됩니다. 클라우드 서비스당 둘 이상의 가용성 집합 또는 클라우드 서비스의 가용성 집합에 없는 하나 이상의 가용성 집합 및 VM 구성은 지원되지 않습니다. |
| VM의 네트워크 구성 |기본 네트워크 인터페이스 |VM의 네트워크 구성은 마이그레이션 후 기본 네트워크 인터페이스 리소스로 표현됩니다. 가상 네트워크에 없는 VM의 경우 마이그레이션 중 내부 IP 주소가 변경됩니다. |
| VM의 여러 네트워크 인터페이스 |네트워크 인터페이스 |VM에 여러 네트워크 인터페이스가 연결된 경우 각 네트워크 인터페이스는 Resource Manager 배포 모델의 마이그레이션 중 모든 속성과 마찬가지로 최상위 리소스가 됩니다. |
| 부하 분산된 끝점 집합 |부하 분산 장치 |클래식 배포 모델에서 플랫폼은 모든 클라우드 서비스에 대한 암시적 부하 분산 장치를 할당받습니다. 마이그레이션 중에는 새로운 부하 분산 장치 리소스를 만들며 부하 분산 끝점 집합이 부하 분산 장치 규칙이 됩니다. |
| 인바운드 NAT 규칙 |인바운드 NAT 규칙 |VM에 정의된 입력 끝점은 마이그레이션 중에 부하 분산 장치의 인바운드 NAT(Network Address Translation) 규칙으로 변환됩니다. |
| VIP 주소 |DNS 이름이 포함된 공용 IP 주소 |가상 IP 주소는 공용 IP 주소가 되며, 부하 분산 장치와 연결됩니다. |
| 가상 네트워크 |가상 네트워크 |가상 네트워크는 모든 속성과 함께 Resource Manager 배포 모델로 마이그레이션됩니다. `-migrated`이름을 사용하여 새 리소스 그룹이 생성됩니다. [지원되지 않는 구성](virtual-machines-windows-migration-classic-resource-manager.md)이 있습니다. |
| 예약된 IP |정적 할당 방법의 공용 IP 주소 |부하 분산 장치와 연결되어 있고 예약된 IP는 클라우드 서비스 또는 가상 컴퓨터의 마이그레이션과 함께 마이그레이션됩니다. 연결되지 않고 예약된 IP 마이그레이션은 현재 지원되지 않습니다. |
| VM당 공용 IP 주소 |동적 할당 방법의 공용 IP 주소 |VM에 연결된 공용 IP 주소는 할당 방법이 정적으로 설정된 공용 IP 주소 리소스로 변환됩니다. |
| NSG |NSG |서브넷과 연결된 네트워크 보안 그룹은 마이그레이션 중 Resource Manager 배포 모델로 복제됩니다. 마이그레이션 중 클래식 배포 모델의 NSG는 제거되지 않습니다. 하지만 마이그레이션이 진행 중인 동안에는 NSG의 관리 평면 작업이 차단됩니다. |
| DNS 서버 |DNS 서버 |가상 네트워크 또는 VM과 연결된 DNS 서버는 해당 리소스 마이그레이션 중 모든 속성과 함께 마이그레이션됩니다. |
| UDR |UDR |서브넷과 연결된 사용자 정의 경로는 마이그레이션 중 Resource Manager 배포 모델로 복제됩니다. 마이그레이션 중 클래식 배포 모델의 UDR는 제거되지 않습니다. 마이그레이션이 진행 중인 동안에는 UDR의 관리 평면 작업이 차단됩니다. |
| VM 네트워크 구성의 IP 전달 속성 |NIC의 IP 전달 속성 |마이그레이션 중 VM의 IP 전달 속성이 네트워크 인터페이스의 속성으로 변환됩니다. |
| 여러 IP가 포함된 부하 분산 장치 |여러 공용 IP 리소스가 포함된 부하 분산 장치 |부하 분산 장치와 연결된 모든 공용 IP는 공용 IP 리소스로 변환되며 마이그레이션 후 부하 분산 장치와 연결됩니다. |
| VM의 내부 DNS 이름 |NIC의 내부 DNS 이름 |마이그레이션하는 동안 VM의 내부 DNS 접미사는 NIC의 "InternalDomainNameSuffix"라는 읽기 전용 속성으로 마이그레이션됩니다. 마이그레이션 후 접미사는 그대로 유지되며 VM 확인은 이전처럼 계속 작동해야 합니다. |
| 가상 네트워크 게이트웨이 |가상 네트워크 게이트웨이 |가상 네트워크 게이트웨이 속성은 변경되지 않고 마이그레이션됩니다. 게이트웨이와 연결된 VIP는 변경하지 않습니다. |
| 로컬 네트워크 사이트 |로컬 네트워크 게이트웨이 |로컬 네트워크 사이트 속성은 로컬 네트워크 게이트웨이라는 새 리소스로 변경되지 않고 마이그레이션됩니다. 이는 온-프레미스 주소 접두사 및 원격 게이트웨이 IP를 나타냅니다. |
| 연결 참조 |연결 |네트워크 구성에서 게이트웨이 및 로컬 네트워크 사이트 간 연결 참조는 마이그레이션 후에 리소스 관리자에서 [Connection]이라는 새로 만든 리소스에 의해 표시됩니다. 네트워크 구성 파일에서 연결 참조의 모든 속성은 변경되지 않은 상태로 새로 만든 [Connection] 리소스에 복사됩니다. VNet을 나타내는 로컬 네트워크 사이트에 두 개의 IPsec 터널을 만들어 클래식의 VNet 간을 연결합니다. 로컬 네트워크 게이트웨이 없이 Resource Manager 모델에서 Vnet2Vnet 연결 형식으로 변환됩니다. |

## <a name="illustration-of-a-simple-migration-walkthrough"></a>간단한 마이그레이션 연습의 설명
다음 스크린샷에서 준비 단계 이후 VM(가상 네트워크에 없음)이 포함된 기존 클라우드 서비스를 확인할 수 있습니다.

![준비 후 클래식 표현](./media/virtual-machines-windows-migration-classic-resource-manager/classic-migration-prepare-portal.png)

마이그레이션 프로세스가 완료되면 다음 스크린샷에 새 리소스 그룹에 새 리소스가 생성되었다고 표시됩니다. ![준비 후 Resource Manager 표현](./media/virtual-machines-windows-migration-classic-resource-manager/resourcemanager-migration-prepare-portal.png)

## <a name="next-steps"></a>다음 단계
클래식 IaaS 리소스를 Resource Manager로 마이그레이션하는 작업을 이해했으므로 리소스 마이그레이션을 시작할 수 있습니다.

* [PowerShell을 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션](virtual-machines-windows-ps-migration-classic-resource-manager.md)
* [CLI를 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션](virtual-machines-linux-cli-migration-classic-resource-manager.md)
* [클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션](virtual-machines-windows-migration-classic-resource-manager.md)
* [커뮤니티 PowerShell 스크립트를 사용하여 클래식 가상 컴퓨터를 Azure Resource Manager로 복제](virtual-machines-windows-migration-scripts.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [가장 일반적인 마이그레이션 오류 검토](virtual-machines-migration-errors.md)




<!--HONumber=Jan17_HO5-->


