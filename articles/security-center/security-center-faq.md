---
title: "Azure Security Center FAQ(질문과 대답) | Microsoft Docs"
description: "이 FAQ는 Azure 보안 센터에 대한 질문에 답변합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/08/2017
ms.author: terrylan
translationtype: Human Translation
ms.sourcegitcommit: 40f8f1b52c39a170a57168db9227a7c2fa069570
ms.openlocfilehash: 466d4a566ebb426f48e8c271e1305b844842d638


---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Azure 보안 센터 FAQ(질문과 대답)
이 FAQ는 증가된 가시성으로 위협을 예방, 감지 및 대응하고 Microsoft Azure 리소스의 보안을 제어하는 서비스인 Azure Security Center에 관한 질문에 답변합니다.

## <a name="general-questions"></a>일반적인 질문
### <a name="what-is-azure-security-center"></a>Azure 보안 센터란?
Azure 보안 센터는 Azure 리소스의 보안에 대한 향상된 가시성과 제어권을 통해 위협을 예방하고 감지하며 위협에 대응하는 데 도움이 됩니다. 이는 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

### <a name="how-do-i-get-azure-security-center"></a>Azure 보안 센터를 이용하려면 어떻게 해야 하나요?
Azure 보안 센터는 Microsoft Azure 구독을 사용하도록 설정되어 있으며 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)에서 액세스합니다. [포털에 로그인](https://portal.azure.com)하여 **찾아보기**를 선택하고 **Security Center**로 스크롤합니다.  

## <a name="billing"></a>결제
### <a name="how-does-billing-work-for-azure-security-center"></a>Azure 보안 센터에 대한 청구는 어떻게 작동합니까?
보안 센터는 무료 및 표준의 두 계층으로 제공됩니다.

무료 계층에서는 보안 정책을 설정하고 필요한 컨트롤 구성 프로세스를 안내하는 보안 경고, 인시던트 및 권장 사항을 수신할 수 있습니다. 또한 무료 계층에서는 Azure 구독에 통합된 파트너 솔루션 및 Azure 리소스의 보안 상태도 모니터링할 수 있습니다.

표준 계층에서는 무료 계층의 기능 외에 고급 검색 기능(위협 인텔리전스, 행동 분석, 충돌 분석, 변칙 검색)도 제공합니다. 표준 계층의 무료 90일 평가판을 사용할 수 있습니다. 업그레이드하려면 [보안 정책](security-center-policies.md#set-security-policies-for-subscriptions)에서 가격 책정 계층을 선택합니다. 자세한 내용은 [Security Center 가격 책정](security-center-pricing.md)을 참조하세요.

## <a name="permissions"></a>권한
Azure Security Center는 Azure에서 사용자, 그룹 및 서비스에 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 제공하는 [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md)를 사용합니다.

Security Center는 리소스 구성을 평가하여 보안 문제 및 취약성을 식별합니다. Security Center에서는 리소스가 속한 구독이나 리소스 그룹에 대한 소유자, 참가자 또는 독자 역할을 할당 받을 때 리소스와 관련된 항목만 볼 수 있습니다.

Security Center의 역할 및 허용된 작업에 대한 자세한 내용은 [Azure Security Center의 권한](security-center-permissions.md)을 참조하세요.

## <a name="data-collection"></a>데이터 수집
Security Center는 해당 보안 상태를 평가하고 보안 권장 사항을 제공하며 위협에 경고하기 위해 Virtual Machines에서 데이터를 수집합니다. 보안 센터에 처음 액세스할 경우 구독의 모든 가상 컴퓨터에서 데이터 수집을 활성화합니다. 데이터 수집을 사용하는 것이 좋지만 보안 센터 정책에서 [데이터 수집을 사용하지 않도록 설정](#how-do-i-disable-data-collection) 하여 옵트아웃(opt out)할 수 있습니다.

### <a name="how-do-i-disable-data-collection"></a>데이터 컬렉션을 사용하지 않도록 설정하려면 어떻게 해야 하나요?
언제든지 보안 정책에서 구독에 대해 **데이터 수집** 을 사용하지 않도록 설정할 수 있습니다. 이렇게 하려면 [Azure Portal에 로그인](https://portal.azure.com)하여 **찾아보기**, **Security Center**, **정책**을 차례로 선택합니다.  구독을 선택하면 새 블레이드가 열리고 **데이터 수집**을 해제하는 옵션이 제공됩니다. Azure 모니터링 에이전트는 데이터 수집을 해제하면 구독의 기존 가상 컴퓨터에서 자동으로 제거됩니다.

> [!NOTE]
> Azure 구독 수준 및 리소스 그룹 수준에서 보안 정책을 설정할 수 있지만 데이터 수집을 해제하려면 구독을 선택해야 합니다.
>
>

### <a name="how-do-i-enable-data-collection"></a>데이터 컬렉션을 사용하도록 설정하려면 어떻게 해야 하나요?
보안 정책에서 Azure 구독에 대한 데이터 수집을 사용하도록 설정할 수 있습니다. 데이터 수집을 사용하도록 설정하려면 [Azure Portal에 로그인](https://portal.azure.com)하여 **찾아보기**, **Security Center**, **정책**을 차례로 선택합니다. **데이터 수집**을 **켜기**로 설정하고 데이터를 수집할 저장소 계정을 구성합니다(질문 “[내 데이터는 어디에 저장되나요?](#where-is-my-data-stored)” 참조). **데이터 수집** 을 사용하도록 설정하면 구독에서 모든 지원되는 가상 컴퓨터에서 보안 구성 및 이벤트 정보를 자동으로 수집합니다.

> [!NOTE]
> Azure 구독 수준 및 리소스 그룹 수준에서 보안 정책을 설정할 수 있지만 데이터 수집은 구독 수준에서만 구성할 수 있습니다.
>
>

### <a name="what-happens-when-data-collection-is-enabled"></a>데이터 수집을 사용하도록 설정하면 어떻게 될까요?
데이터 수집은 Azure 모니터링 에이전트 및 Azure 보안 모니터링 확장을 통해 사용하도록 설정됩니다. Azure 보안 모니터링 확장은 다양한 보안 관련 구성을 검사하여 ETW([Windows용 이벤트 추적](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx))로 보냅니다. 또한 운영 체제는 이벤트 로그 항목을 만듭니다.  Azure 모니터링 에이전트는 이벤트 로그 항목을 읽으며 ETW는 이를 추적하고 분석을 위해 저장소 계정에 복사합니다.  이는 보안 정책에 구성된 저장소 계정입니다. 저장소 계정에 대한 자세한 내용은 질문 "[내 데이터는 어디에 저장되나요?](#where-is-my-data-stored)"를 참조하세요.

### <a name="does-the-monitoring-agent-or-security-monitoring-extension-impact-the-performance-of-my-servers"></a>모니터링 에이전트 또는 보안 모니터링 확장은 내 서버의 성능에 영향을 미치나요?
에이전트 및 확장은 시스템 리소스의 명목 양을 소비하며 성능에 거의 영향을 미치지 않습니다. 성능 영향과 에이전트 및 확장에 대한 자세한 내용은 [계획 및 작업 가이드](security-center-planning-and-operations-guide.md#data-collection-and-storage)를 참조하세요.

### <a name="where-is-my-data-stored"></a>내 데이터는 어디에 저장되나요?
가상 컴퓨터를 실행 중인 각 영역에 대해 가상 컴퓨터에서 수집한 데이터가 저장되는 저장소 계정을 선택합니다. 이렇게 하면 쉽게 개인 정보 및 데이터 독립성과 같은 지리적 영역에 데이터를 유지할 수 있습니다. 보안 정책에서 구독에 대한 저장소 계정을 선택합니다. 이렇게 하려면 [Azure Portal에 로그인](https://portal.azure.com)하여 **찾아보기**, **Security Center**, **정책**을 차례로 선택합니다. 구독을 선택하면 새 블레이드가 열립니다. 지역을 선택하려면 **저장소 계정 선택**을 선택합니다. 각 지역에 대한 저장소 계정을 선택하지 않으면, 사용자를 위해 저장소 계정을 만들고 securitydata 리소스 그룹에 배치합니다.

> [!NOTE]
> Azure 구독 수준 및 리소스 그룹 수준에서 보안 정책을 설정할 수 있지만 저장소 계정에 대한 지역은 구독 수준에서만 선택할 수 있습니다.
>
>

Azure Storage 및 저장소 계정에 대해 자세히 알아보려면 [저장소 문서](https://azure.microsoft.com/documentation/services/storage/) 및 [Azure Storage 계정 정보](../storage/storage-create-storage-account.md)를 참조하세요.

## <a name="using-azure-security-center"></a>Azure 보안 센터 사용
### <a name="what-is-a-security-policy"></a>보안 정책이란?
보안 정책은 지정된 구독 또는 리소스 그룹 내에서 리소스에 대해 권장되는 제어 집합을 정의합니다. Azure 보안 센터에서 회사의 보안 요구 사항 및 응용 프로그램 형식 또는 각 구독의 데이터 민감도에 따라 Azure 구독 및 리소스 그룹에 대한 정책을 정의합니다.

예를 들어 개발 또는 테스트에 사용되는 리소스의 요구사항은 프로덕션 응용 프로그램에 사용되는 보안 요구 사항과 다릅니다. 마찬가지로 PII(Personally Identifiable Information) 같은 규제된 데이터를 가진 응용 프로그램에 대해서는 더 높은 수준의 보안이 필요할 수 있습니다. Azure Security Center에서 사용하도록 설정한 보안 정책에 따라 보안 권장 사항과 모니터링이 결정됩니다. 보안 정책에 대해 자세히 알아보려면 [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)을 참조하세요.

> [!NOTE]
> 구독 수준 정책과 리소스 그룹 수준 정책 간에 충돌이 발생한 경우 리소스 그룹 수준 정책이 우선 적용됩니다.
>
>

### <a name="who-can-modify-a-security-policy"></a>보안 정책을 누가 수정할 수 있나요?
보안 정책은 각 구독 또는 리소스 그룹에 대해 구성됩니다. 구독 수준 또는 리소스 그룹 수준에서 보안 정책을 수정하려면 해당 구독의 소유자 또는 참가자여야 합니다.

보안 정책을 구성하는 방법을 자세히 알아보려면 [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)을 참조하세요.

### <a name="what-is-a-security-recommendation"></a>보안 권장 사항이란?
Azure 보안 센터에서는 Azure 리소스의 보안 상태를 분석합니다. 잠재적인 보안 취약성이 식별되면 권장 사항이 생성됩니다. 권장 사항은 필요한 컨트롤을 구성하는 과정을 안내합니다. 예:

* 맬웨어 방지 프로그램을 프로비전하면 악성 소프트웨어를 식별하여 제거하는 데 도움이 됩니다.
* [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 및 가상 컴퓨터에 대한 트래픽 제어 규칙 구성
* 웹 응용 프로그램의 대상을 지정한 공격에 대해 방어하는 데 도움이 되는 웹 응용 프로그램 방화벽 프로비전
* 누락된 시스템 업데이트 배포
* 권장 기준과 일치하지 않는 OS 구성 해결

보안 정책에 사용하도록 설정된 권장 사항만 여기에 표시됩니다.

### <a name="how-can-i-see-the-current-security-state-of-my-azure-resources"></a>내 Azure 리소스의 현재 보안 상태를 확인하려면 어떻게 해야 하나요?
**Security Center** 블레이드의 **리소스 상태** 타일에 현재 환경의 전체 보안 상태가 가상 컴퓨터, 웹 응용 프로그램 및 다른 리소스별로 요약되어 표시됩니다. 각 리소스에는 잠재적 보안 취약성이 식별되었는지 나타내는 표시기가 있습니다. 리소스 상태 타일을 클릭하면 리소스가 표시되며 주의가 필요하거나 문제가 있을 수 있는 위치를 식별합니다.

### <a name="what-triggers-a-security-alert"></a>보안 경고를 트리거하는 것은 무엇인가요?
Azure Security Center는 리소스, 네트워크 및 맬웨어 방지 프로그램과 방화벽 같은 파트너 솔루션에서 자동으로 로그 데이터를 수집, 분석 및 결합합니다. 위협이 감지되었을 때 보안 경고가 생성됩니다. 감지되는 사항의 예:

* 알려진 악성 IP 주소와 통신하는 손상된 가상 컴퓨터
* Windows 오류 보고를 사용 하여 감지된 고급 맬웨어
* 가상 컴퓨터에 대한 무작위 공격
* 맬웨어 방지 프로그램 또는 웹 응용 프로그램 방화벽 등과 같은 통합된 파트너 보안 솔루션에서의 보안 경고

### <a name="whats-the-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>Microsoft 보안 응답 센터와 Azure 보안 센터에서 감지 및 경고된 위협 간의 차이점은 무엇입니까?
Microsoft 보안 대응 센터(MSRC)는 Azure 네트워크 및 인프라의 선택 보안 모니터링을 수행하고 타사에서 위협 인텔리전스 및 남용 불만 사항을 받습니다. MSRC는 불법적인 또는 권한 없는 당사자가 고객 데이터에 액세스했거나 고객의 Azure 사용이 사용 제한에 대한 조건을 준수하지 않는 것을 인식하면 보안 사고 관리자는 고객에게 알립니다. 보안 연락처를 지정하지 않은 경우 대개 Azure Security Center에 지정된 보안 연락처 또는 Azure 구독 소유자에게 메일을 전송하는 방식으로 알림이 수행됩니다.

보안 센터는 지속적으로 고객의 Azure 환경을 모니터링하고 다양한 잠재적인 악의적 활동을 자동으로 검색하도록 분석을 적용하는 Azure 서비스입니다. 이러한 감지는 보안 센터 대시보드에서 보안 경고로 표시됩니다.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Azure Security Center에서는 어떤 Azure 리소스를 모니터링하나요?
Azure Security Center에서는 다음과 같은 Azure 리소스를 모니터링합니다.

* 가상 컴퓨터(VM)( [Cloud Services](../cloud-services/cloud-services-choose-me.md)포함)
* Azure 가상 네트워크
* Azure SQL 서비스
* VM 및 [App Service Environment](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>가상 컴퓨터
### <a name="what-types-of-virtual-machines-are-supported"></a>어떤 유형의 가상 컴퓨터가 지원되나요?
[클래식 및 Resource Manager 배포 모델](../azure-classic-rm.md)을 모두 사용하여 작성된 VM(가상 컴퓨터)에 대해 보안 상태 모니터링 및 권장 사항이 제공됩니다.

지원되는 Windows VM:

* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

지원되는 Linux VM:

* Ubuntu 버전 12.04, 14.04, 16.04, 16.10
* Debian 버전 7, 8
* CentOS 버전 6.\*, 7.*
* RHEL(Red Hat Enterprise Linux) 버전 6.\*, 7.*
* SUSE Linux Enterprise Server(SLES) 버전 11 SP4+, 12.*
* Oracle Linux 버전 6.\*, 7.*

클라우드 서비스에서 실행 중인 VM도 지원됩니다. 프로덕션 슬롯에서 실행되는 클라우드 서비스 웹 및 작업자 역할만 모니터링됩니다. 클라우드 서비스에 대한 자세한 내용은 [클라우드 서비스 개요](../cloud-services/cloud-services-choose-me.md)를 참조하세요.

### <a name="why-doesnt-azure-security-center-recognize-the-antimalware-solution-running-on-my-azure-vm"></a>Azure Security Center가 내 Azure VM에서 실행 중인 맬웨어 방지 솔루션을 인식하지 못하는 이유는 무엇인가요?
Azure Security Center는 Azure 확장을 통해 설치된 맬웨어 방지 프로그램만 확인할 수 있습니다. 예를 들어 보안 센터는 사용자가 제공한 이미지에 미리 설치되어 있거나, 구성 관리 시스템 등의 고유한 프로세스를 사용하여 가상 컴퓨터에 설치한 맬웨어 방지 프로그램을 검색할 수 없습니다.

### <a name="why-do-i-get-the-message-missing-scan-data-for-my-vm"></a>VM에 대해 "검사 데이터 누락" 메시지가 표시되는 이유는 무엇인가요?
Azure Security Center에서 데이터 수집을 사용하도록 설정한 후 검사 데이터가 입력될 때까지는 다소 시간이 걸릴 수 있습니다(1시간 이내). VM이 중지된 상태이면 검사를 수행해도 데이터가 입력되지 않습니다.

### <a name="why-do-i-get-the-message-vm-agent-is-missing"></a>"VM 에이전트가 누락됨" 메시지가 표시되는 이유는 무엇인가요?
데이터 수집을 사용하도록 설정하려면 VM에 VM 에이전트를 설치해야 합니다. Azure 마켓플레이스에서 배포된 VM에 VM 에이전트가 기본적으로 설치됩니다. 다른 VM에 VM 에이전트를 설치하는 방법에 대한 자세한 내용은 블로그 게시물 [VM 에이전트 및 확장](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)을 참조하세요.



<!--HONumber=Feb17_HO2-->


