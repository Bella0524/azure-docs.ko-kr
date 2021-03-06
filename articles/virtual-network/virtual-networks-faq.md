---
title: Azure Virtual Network FAQ | Microsoft Docs
description: "Microsoft Azure Virtual Network에 대해 자주 묻는 질문에 답변합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
translationtype: Human Translation
ms.sourcegitcommit: e1f7b85308d7482e0066809737749e73029cd758
ms.openlocfilehash: eed133ba2f0a5e1665afd39b2122d3aacd3cc40a


---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Azure Virtual Network FAQ(질문과 대답)

## <a name="virtual-network-basics"></a>Virtual Network 기본 사항

### <a name="what-is-an-azure-virtual-network-vnet"></a>Azure VNet(Virtual Network)이란?
Azure VNet(Virtual Network)은 클라우드의 사용자 네트워크를 나타내는 표현입니다. 구독 전용 Azure 클라우드를 논리적으로 격리한 것이 가상 네트워크입니다. VNet을 사용하여 Azure에서 VPN(가상 사설망)을 프로비전 및 관리할 수 있으며 필요에 따라 VNet을 Azure에서 다른 VNet 또는 온-프레미스 IT 인프라와 연결하여 하이브리드 또는 크로스-프레미스 솔루션을 만들 수 있습니다. 생성한 각 VNet은 각각의 CIDR 블록을 가지며 CIDR 블록이 겹치지 않는 한 다른 VNet 및 온-프레미스 네트워크에 연결할 수 있습니다. 또한 VNet에 대한 DNS 서버 설정 및 VNet의 서브넷으로 구분에 대한 제어권을 가집니다.

VNet을 다음에 사용합니다.

* 사설 클라우드만 사용하는 전용 VNet 만들기경우에 따라 솔루션에 대한 크로스-프레미스 구성을 필요로 하지 않습니다. VNet을 만들 때 VNet 내의 서비스 및 VM은 클라우드 내에서 안전하게 직접 서로 통신할 수 있습니다. 이는 VNet 내에서 안전하게 트래픽을 유지하면서도 솔루션의 일부로 인터넷 통신을 필요로 하는 VM 및 서비스에 대한 끝점 연결을 구성할 수 있습니다.
* 데이터 센터를 안전하게 확장VNet을 사용하여 기존의 사이트 간(S2S) VPN을 빌드하여 데이터 센터 용량을 안전하게 확장할 수 있습니다. S2S VPN은 IPSEC를 사용하여 회사 VPN 게이트웨이와 Azure 간의 보안 연결을 제공합니다.
* 하이브리드 클라우드 시나리오 활성화VNet은 유연성을 제공하여 다양한 하이브리드 클라우드 시나리오를 지원합니다. 메인프레임 및 Unix 시스템과 같은 모든 형식의 온-프레미스 시스템에 클라우드 기반 응용프로그램을 안전하게 연결할 수 있습니다.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>VNet이 필요한 경우를 어떻게 알 수 있을까요?
[가상 네트워크 개요](virtual-networks-overview.md) 문서는 최상의 네트워크 디자인 옵션을 결정하는 데 도움이 되는 의사 결정 테이블을 제공합니다.

### <a name="how-do-i-get-started"></a>어떻게 시작하나요?
[가상 네트워크 설명서](https://docs.microsoft.com/azure/virtual-network/)를 방문하여 시작합니다. 이 콘텐츠는 모든 VNet 기능에 대한 개요 및 배포 정보를 제공합니다.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>크로스-프레미스 연결 없이 VNet을 사용할 수 있습니까?
예. 하이브리드 연결을 사용하지 않고 VNet을 사용할 수 있습니다. Azure에서 Microsoft Windows Server Active Directory 도메인 컨트롤러와 SharePoint 팜을 실행하려는 경우 특히 유용합니다.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>VNet 간 또는 VNet과 온-프레미스 데이터 센터 간에 WAN 최적화를 수행할 수 있습니까?

예. Azure Marketplace를 통해 여러 공급업체에서 [WAN 최적화 네트워크 가상 어플라이언스](https://azure.microsoft.com/marketplace/?term=wan+optimization)를 배포할 수 있습니다.

## <a name="configuration"></a>구성

### <a name="what-tools-do-i-use-to-create-a-vnet"></a>VNet을 만들려면 어떤 도구를 사용합니까?
다음 도구를 사용하여 VNet을 만들거나 구성할 수 있습니다.

* Azure 포털(클래식 및 리소스 관리자 VNet용)
* 네트워크 구성 파일(netcfg - 클래식 VNet 전용) [네트워크 구성 파일을 사용하여 VNet 구성](virtual-networks-using-network-configuration-file.md) 문서를 참조하세요.
* PowerShell(클래식 및 리소스 관리자 VNet용)
* Azure CLI(클래식 및 리소스 관리자 VNet용)

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>VNet 내에서 사용할 수 있는 주소 범위는 무엇입니까?
공용 IP 주소 범위와 [RFC 1918](http://tools.ietf.org/html/rfc1918)에서 정의된 모든 IP 주소 범위를 사용할 수 있습니다.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>VNet 내에서 공용 IP 주소를 가질 수 있습니까?
예. 공용 IP 주소 범위에 대한 자세한 내용은 [가상 네트워크의 공용 IP 주소 공간](virtual-networks-public-ip-within-vnet.md) 문서를 참조하세요. 사용자의 공용 IP 주소는 인터넷에서 직접 액세스할 수 없습니다.

### <a name="is-there-a-limit-to-the-number-of-subnets-in-my-vnet"></a>VNet 내에서 서브넷 수에 제한이 있습니까?
예. 자세한 내용은 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서를 참조하세요. 서브넷 주소 공간은 서로 겹칠 수 없습니다.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>이러한 서브넷 내에서 IP 주소를 사용하는데 제한 사항이 있습니까?
예. Azure는 각 서브넷 내의 일부 IP 주소를 예약합니다. 서브넷의 첫 번째 및 마지막 IP 주소는 Azure 서비스에 사용되는 3개 이상의 주소와 함께 프로토콜 적합성을 위해 예약됩니다.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>VNet 및 서브넷은 얼마나 크고 얼마나 작을 수 있습니까?
지원되는 가장 작은 서브넷은 /29이며 가장 큰 서브넷은 /8(CIDR 서브넷 정의 사용)입니다.

### <a name="can-i-bring-my-vlans-to-azure-using-vnets"></a>VNet을 사용하여 내 VLAN을 Azure에 가져올 수 있습니까?
아니요. VNet은 계층&3; 오버레이입니다. Azure는 모든 계층&2; 의미 체계를 지원하지 않습니다.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>VNet 및 서브넷에 사용자 지정 라우팅 정책을 지정할 수 있습니까?
예. UDR(사용자 정의 라우팅)을 사용할 수 있습니다. UDR에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](virtual-networks-udr-overview.md)을 참조하세요.

### <a name="do-vnets-support-multicast-or-broadcast"></a>VNet은 멀티 캐스트 또는 브로드캐스트를 지원합니까?
아니요. 멀티 캐스트 또는 브로드캐스트는 지원하지 않습니다.

### <a name="what-protocols-can-i-use-within-vnets"></a>VNet 내에서 사용할 수 있는 프로토콜은 무엇입니까?
VNet 내에서 TCP, UDP 및 ICMP TCP/IP 프로토콜을 사용할 수 있습니다. 멀티 캐스트, 브로드캐스트, IP-IP 캡슐화 패킷 및 GRE(일반 라우팅 캡슐화) 패킷은 VNet 내에서 차단됩니다. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>내 기본 라우터를 VNet 내에서 ping할 수 있습니까?
아니요.

### <a name="can-i-use-tracert-to-diagnose-connectivity"></a>Tracert를 사용하여 연결을 진단할 수 있습니까?
아니요.

### <a name="can-i-add-subnets-after-the-vnet-is-created"></a>VNet을 만든 후 서브넷을 추가할 수 있습니까?
예. 서브넷 주소가 VNet에서 다른 서브넷의 일부가 아닌 경우 언제든지 서브넷을 VNet에 추가할 수 있습니다.

### <a name="can-i-modify-the-size-of-my-subnet-after-i-create-it"></a>서브넷을 만든 후 크기를 수정할 수 있습니까?
예. VNet 내에서 배포된 VM 또는 서비스가 없는 경우 서브넷을 추가, 제거, 확장 또는 축소할 수 있습니다.

### <a name="can-i-modify-subnets-after-i-created-them"></a>서브넷을 만든 후 수정할 수 있습니까?
예. VNet에서 사용되는 CIDR 블록을 추가, 제거 및 수정할 수 있습니다.

### <a name="can-i-connect-to-the-internet-if-i-am-running-my-services-in-a-vnet"></a>VNet에서 서비스를 실행 중인 경우 인터넷에 연결할 수 있습니까?
예. VNet 내에 배포된 모든 서비스는 인터넷에 연결할 수 있습니다. Azure에서 배포된 모든 클라우드 서비스에는 공개적으로 주소를 지정할 수 있는 할당된 VIP가 있습니다. 해당 서비스를 활성화하여 인터넷의 연결을 허용하려면 PaaS 역할에 대한 입력 끝점 및 가상 컴퓨터에 대한 끝점을 정의해야 합니다.

### <a name="do-vnets-support-ipv6"></a>VNet은 IPv6를 지원합니까?
아니요. VNet과 함께 IPv6를 사용할 수 없습니다.

### <a name="can-a-vnet-span-regions"></a>VNet을 사용하여 지역을 확장할 수 있습니까?
아니요. VNet은 단일 지역으로 제한됩니다.

### <a name="can-i-connect-a-vnet-to-another-vnet-in-azure"></a>Azure에서 다른 VNet에 VNet을 연결할 수 있습니까?
예. 다음을 사용하여 하나의 VNet을 다른 VNet에 연결할 수 있습니다.
- Azure VPN 게이트웨이. 자세한 내용은 [VNet 간 연결 구성](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) 문서를 참조하세요. 
- VNet 피어링. 자세한 내용은 [VNet 피어링 개요](virtual-network-peering-overview.md) 문서를 참조하세요.

## <a name="name-resolution-dns"></a>이름 확인(DNS)

### <a name="what-are-my-dns-options-for-vnets"></a>VNet에 대한 DNS 옵션은 무엇입니까?
사용 가능한 모든 DNS 옵션을 안내하는 [VM 및 역할 인스턴스에 대한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md) 페이지의 의사 결정 테이블을 사용하세요.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>VNet에 대한 DNS 서버를 지정할 수 있습니까?
예. VNet 설정에서 DNS 서버 IP 주소를 지정할 수 있습니다. VNet에서 모든 VM에 대한 기본 DNS 서버로 적용됩니다.

### <a name="how-many-dns-servers-can-i-specify"></a>얼마나 많은 DNS 서버 수를 지정할 수 있습니까?
자세한 내용은 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서를 참조하세요.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-the-network"></a>네트워크를 생성 한 후 DNS 서버를 수정할 수 있습니까?
예. VNet에 대한 DNS 서버 목록을 언제든지 변경할 수 있습니다. DNS 서버 목록을 변경하는 경우 새로운 DNS 서버를 선택하기 위해 VNet에서 각 VM을 다시 시작해야 합니다.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>Azure에서 제공하는 DNS란 무엇이며 VNet으로 작동합니까?
Azure에서 제공하는 DNS는 Microsoft에서 제공하는 다중 테넌트 DNS 서비스입니다. Azure는 이 서비스에 모든 VM 및 클라우드 서비스 역할 인스턴스를 등록합니다. 이 서비스는 동일한 클라우드 서비스 내에 포함된 VM 및 역할 인스턴스에 대한 호스트 이름 및 동일한 VNet에서 VM 및 역할 인스턴스에 대한 FQDN으로 이름 확인을 제공합니다. DNS에 대한 자세한 내용은 [VM 및 역할 인스턴스에 대한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md) 문서를 참조하세요.

> [!NOTE]
> 이번에는 Azure에서 제공하는 DNS를 사용한 테넌트 간 이름 확인에 대한 VNet의 첫 100개의 클라우드 서비스에 제한이 있습니다. 사용자 고유의 DNS 서버를 사용하는 경우 이러한 제한이 적용되지 않습니다.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>VM 당/서비스 단위로 DNS 설정을 재정의할 수 있습니까?
예. 클라우드 서비스 별로 DNS 서버를 설정하여 기본 네트워크 설정을 재정의할 수 있습니다. 그러나 가능한 한 네트워크 차원 DNS를 사용하는 것이 좋습니다.

### <a name="can-i-bring-my-own-dns-suffix"></a>고유한 DNS 접미사를 가져올 수 있습니까?
아니요. VNet에 대해 사용자 지정 DNS 접미사를 지정할 수 없습니다.

## <a name="connecting-virtual-machines"></a>가상 컴퓨터 연결

### <a name="can-i-deploy-vms-to-a-vnet"></a>VNet에 VM을 배포할 수 있습니까?
예. 리소스 관리자 배포 모델을 통해 배포된 VM에 연결된 모든 NIC(네트워크 인터페이스)는 VNet에 연결되어야 합니다. 클래식 배포 모델을 통해 배포된 VM은 VNet에 선택적으로 연결할 수 있습니다.

### <a name="what-are-the-different-types-of-ip-addresses-i-can-assign-to-vms"></a>VM에 지정할 수 있는 IP 주소 유형에는 무엇이 있습니까?
* **개인:** 각 VM 내에서 각 NIC에 할당됩니다. 정적 또는 동적 할당 메서드를 사용하여 주소를 할당합니다. VNet의 서브넷 설정에 지정한 범위에서 개인 IP 주소가 할당됩니다. 클래식 배포 모델을 통해 배포된 리소스는 VNet에 연결되지 않은 경우에도 개인 IP 주소를 수신합니다. 리소스가 할당 취소되거나(VM) 삭제될 때까지(VM 또는 클라우드 서비스 배포 슬롯) 동적 개인 IP 주소는 리소스에 할당된 상태로 유지됩니다. 리소스가 삭제될 때까지 정적 개인 IP 주소는 리소스에 할당된 상태로 유지됩니다.
* **공용:** 필요에 따라 Azure Resource Manager 배포 모델을 통해 배포된 VM에 연결된 NIC에 할당됩니다. 정적 또는 동적 할당 메서드를 사용하여 주소를 할당할 수 있습니다. 클래식 배포 모델을 통해 배포된 모든 VM 및 클라우드 서비스 역할 인스턴스는 클라우드 서비스 내에 존재하며 *동적*, 공용 VIP(가상 IP) 주소가 할당됩니다. [예약된 IP 주소](virtual-networks-reserved-public-ip.md)라고 하는 공용 *정적* IP 주소는 필요에 따라 VIP로 할당될 수 있습니다. 클래식 배포 모델을 통해 배포된 개별 VM 또는 클라우드 서비스 역할 인스턴스에 공용 IP 주소를 할당할 수 있습니다. 이러한 주소는 [ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소라고 하며 동적으로 할당될 수 있습니다.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>나중에 만들 VM에 대한 개인 IP 주소를 예약할 수 있습니까?
아니요. 개인 IP 주소를 예약할 수 없습니다. 개인 IP 주소가 사용 가능한 경우 DHCP 서버에서 VM 또는 역할 인스턴스에 할당됩니다. 해당 VM은 개인 IP 주소를 할당하려는 VM일 수도 아닐 수도 있습니다. 그러나 이미 만든 VM의 개인 IP 주소를 사용 가능한 모든 개인 IP 주소로 변경할 수 있습니다.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>VNet에서 VM에 대한 개인 IP 주소가 변경됩니까?
경우에 따라 다릅니다. 동적 개인 IP 주소는 중지(할당 취소) 또는 삭제될 때까지 VM과 함께 유지됩니다. 정적 개인 IP 주소는 삭제될 때까지 VM에서 해제되지 않습니다.

### <a name="can-i-manually-assign-ip-addresses-to-nics-within-the-vm-operating-system"></a>VM 운영 체제 내에서 IP 주소를 NIC에 수동으로 할당할 수 있습니까?
예, 하지만 권장되지 않습니다. VM의 운영 체제 내에서 NIC에 대한 IP 주소를 수동으로 변경하면 Azure VM 내의 NIC에 할당된 IP 주소가 변경되는 경우 VM에 대한 연결 손실을 잠재적으로 초래할 수 있습니다.

### <a name="what-happens-to-my-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-the-operating-system"></a>클라우드 서비스 배포 슬롯을 중지하거나 운영 체제 내에서 VM을 종료하는 경우 IP 주소는 어떻게 됩니까?
아무 일도 일어나지 않습니다. IP 주소(공용 VIP, 공용 및 개인)는 클라우드 서비스 배포 슬롯 또는 VM에 할당된 상태로 유지됩니다. VM이 중지(할당 취소) 또는 삭제되거나 클라우드 서비스 배포 슬롯이 삭제되는 경우에만 동적 주소가 해제됩니다. Azure Portal 내에서 VM에 대해 **중지** 단추를 클릭하면 해당 상태가 중지됨(할당 취소됨)으로 설정됩니다. 이 경우 VM의 IP 주소가 손실됩니다.

### <a name="can-i-move-vms-from-one-subnet-to-another-subnet-in-a-vnet-without-re-deploying"></a>VM을 다시 배포하지 않고 VNet에서 하나의 서브넷에서 다른 서브넷으로 이동할 수 있습니까?
예. [다른 서브넷으로 VM 또는 역할 인스턴스를 이동하는 방법](virtual-networks-move-vm-role-to-subnet.md) 문서에서 자세한 정보를 확인할 수 있습니다.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>VM에 대해 정적 MAC 주소를 구성할 수 있습니까?
아니요. MAC 주소를 정적으로 구성할 수 없습니다.

### <a name="will-the-mac-address-remain-the-same-for-my-vm-once-it-has-been-created"></a>MAC 주소가 만들어진 후 VM에 대해 동일하게 유지됩니까?
예, MAC 주소는 삭제될 때까지 리소스 관리자 또는 클래식 배포 모델을 통해 배포된 VM에 대해 동일하게 유지됩니다. 이전에 MAC 주소는 VM이 중지(할당 취소)되는 경우에 해제되었지만 이제 VM이 할당 취소된 상태에 있을 때에도 MAC 주소는 유지됩니다.

### <a name="can-i-connect-to-the-internet-from-a-vm-in-a-vnet"></a>VNet의 VM에서 인터넷에 연결할 수 있습니까?
예. VNet 내에 배포된 모든 VM 및 클라우드 서비스 역할 인스턴스는 인터넷에 연결할 수 있습니다.

## <a name="azure-services-that-connect-to-vnets"></a>VNet에 연결하는 Azure 서비스

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>VNet에 Azure App Service Web Apps를 사용할 수 있습니까?
예. ASE(앱 서비스 환경)를 사용하여 VNet 내부에 Web Apps를 배포할 수 있습니다. VNet에 대해 지점 및 사이트 간 연결이 구성된 경우 Azure VNet에서 모든 Web Apps를 안전하게 연결하고 리소스에 액세스할 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.

* [앱 서비스 환경에서 웹앱 만들기](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Azure Virtual Network에 앱 통합](../app-service-web/web-sites-integrate-with-vnet.md)
* [웹앱을 통해 VNet 통합 및 하이브리드 연결 사용](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>VNet에서 웹 및 작업자 역할(PaaS)을 사용하여 Cloud Services를 배포할 수 있습니까?
예. (선택 사항) VNet 내에서 Cloud Services 역할 인스턴스를 배포할 수 있습니다. 이를 수행하려면 서비스 구성의 네트워크 구성 섹션에서 VNet 이름 및 역할/서브넷 매핑을 지정합니다. 이진 파일을 업데이트할 필요가 없습니다.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-to-a-vnet"></a>VMSS(가상 컴퓨터 크기 집합)를 VNet에 연결할 수 있습니까?
예. VMSS를 VNet에 연결해야 합니다.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>서비스를 VNet 내부 및 외부로 이동할 수 있습니까?
아니요. 서비스를 VNet 내부 및 외부로 이동할 수 없습니다. 서비스를 삭제하고 다시 배포하여 다른 VNet으로 이동해야 합니다.

## <a name="security"></a>보안

### <a name="what-is-the-security-model-for-vnets"></a>VNet에 대한 보안 모델은 무엇입니까?
VNet은 다른 VNet 및 Azure 인프라에서 호스팅되는 다른 서비스에서 완전히 격리됩니다. VNet은 트러스트 경계입니다.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-to-vnet-connected-resources"></a>VNet에 연결된 리소스에 대해 인바운드 또는 아웃바운드 트래픽 흐름을 제한할 수 있습니까?
예. VNet 또는 둘 다에 연결된 VNet, NIC 내에서 개별 서브넷에 [네트워크 보안 그룹](virtual-networks-nsg.md)을 적용할 수 있습니다.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>VNet에 연결된 리소스 간에 방화벽을 구현할 수 있습니까?
예. Azure Marketplace를 통해 여러 공급업체에서 [방화벽 네트워크 가상 어플라이언스](https://azure.microsoft.com/en-us/marketplace/?term=firewall)를 배포할 수 있습니다.

### <a name="is-there-information-available-about-securing-vnets"></a>VNet 보안에 사용 가능한 정보가 있습니까?
예. 자세한 내용은 [Azure 네트워크 보안 개요](../security/security-network-overview.md) 문서를 참조하세요.

## <a name="apis-schemas-and-tools"></a>API, 스키마 및 도구

### <a name="can-i-manage-vnets-from-code"></a>코드에서 VNet을 관리할 수 있습니까?
예. [Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx) 및 [클래식 (서비스 관리)](http://go.microsoft.com/fwlink/?LinkId=296833) 배포 모델에서 VNet에 대해 REST API를 사용할 수 있습니다.

### <a name="is-there-tooling-support-for-vnets"></a>VNet에 대한 도구 지원이 있습니까?
예. 사용에 대한 자세한 정보:
- [Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md) 및 [클래식](virtual-networks-create-vnet-classic-pportal.md) 배포 모델을 통해 VNet을 배포하는 Azure Portal.
- [리소스 관리자](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) 및 [클래식](/powershell/servicemanagement/azure.networking/v3.1.0/azure.networking) 배포 모델을 통해 배포된 VNet을 관리하는 PowerShell.
- 두 배포 모델을 통해 배포된 VNet을 관리하는 [Azure CLI(명령줄 인터페이스)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources).  



<!--HONumber=Feb17_HO1-->


