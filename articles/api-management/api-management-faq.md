---
title: "Azure API 관리 FAQ | Microsoft Docs"
description: "Azure API Management에서 일반적인 질문과 대답, 패턴 및 모범 사례를 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
translationtype: Human Translation
ms.sourcegitcommit: 8d5c21f8e746a9bcddc2eb9b0294836e0de55bf2
ms.openlocfilehash: 6300aa7030cfd29ec4b8b1db7b42227855fddbcf

---
# <a name="azure-api-management-faqs"></a>Azure API Management FAQ
Azure API Management에 대한 일반적인 질문과 대답, 패턴 및 모범 사례를 가져옵니다.

## <a name="contact-us"></a>문의처
* [Microsoft Azure API Management 팀에게 어떻게 질문할 수 있습니까?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>질문과 대답
* [기능이 미리 보기 상태인 경우 어떤 의미입니까?](#what-does-it-mean-when-a-feature-is-in-preview)
* [API Management 게이트웨이와 백 엔드 서비스 간의 연결을 어떻게 보호할 수 있습니까?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [API Management 서비스 인스턴스를 새 인스턴스에 복사하려면 어떻게 해야 합니까?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [API 관리 인스턴스를 프로그래밍 방식으로 관리할 수 있습니까?](#can-i-manage-my-api-management-instance-programmatically)
* [관리자 그룹에 사용자를 추가하려면 어떻게 해야 합니까?](#how-do-i-add-a-user-to-the-administrators-group)
* [추가하려는 정책을 정책 편집기에서 사용할 수 없는 이유는 무엇입니까?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [API Management에서 API 버전 관리를 사용하려면 어떻게 해야 합니까?](#how-do-i-use-api-versioning-in-api-management)
* [단일 API에서 여러 환경을 설정하려면 어떻게 해야 합니까?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [API Management와 함께 SOAP를 사용할 수 있습니까?](#can-i-use-soap-with-api-management)
* [API 관리 게이트웨이 IP 주소가 상수입니까? 그것을 방화벽 규칙에 사용할 수 있습니까?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [AD FS 보안을 통해 OAuth 2.0 권한 부여 서버를 구성할 수 있습니까?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [여러 지리적 위치에 배포할 때 API Management에서 사용하는 라우팅 방법은 무엇입니까?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Azure Resource Manager 템플릿을 사용하여 API Management 서비스 인스턴스를 만들 수 있습니까?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [백 엔드에 대해 자체 서명된 SSL 인증서를 사용할 수 있습니까?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [GIT 리포지토리를 복제하려고 할 때 인증 실패가 발생하는 이유는 무엇입니까?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [API Management는 Azure ExpressRoute와 함께 작동합니까?](#does-api-management-work-with-azure-expressroute)
* [구독 간에 API Management 서비스를 이동할 수 있습니까?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [내 API를 가져오는 데 제한 사항 또는 알려진 문제가 있나요?](#api-management-api-import-restrictions)

### <a name="how-can-i-ask-the-microsoft-azure-api-management-team-a-question"></a>Microsoft Azure API Management 팀에게 어떻게 질문할 수 있습니까?
다음 옵션 중 하나를 사용하여 문의할 수 있습니다.

* [API Management MSDN 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt)에 질문을 게시합니다.
* <mailto:apimgmt@microsoft.com>에 전자 메일을 보냅니다.
* [Azure 피드백 포럼](https://feedback.azure.com/forums/248703-api-management)에서 기능 요청을 보냅니다.

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>기능이 미리 보기 상태인 경우 어떤 의미입니까?
기능이 미리 보기 상태인 경우 기능 작동 방법에 대한 피드백을 찾고 있음을 의미합니다. 기능이 미리 보기 상태인 경우 기능적으로 완전하지만 고객 피드백에 대한 응답으로 변경 내용을 만들 가능성이 있습니다. 프로덕션 환경에서 미리 보기에 있는 기능에 의존하지 않는 것이 좋습니다. 미리 보기 상태의 기능에 대한 의견이 있는 경우 [Microsoft Azure API Management 팀에게 어떻게 질문할 수 있습니까?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)의 옵션 중 하나를 통해 알려 주세요.

### <a name="how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services"></a>API Management 게이트웨이와 백 엔드 서비스 간의 연결을 어떻게 보호할 수 있습니까?
API Management 게이트웨이와 백 엔드 서비스 간의 연결을 보호하는 몇 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

* HTTP 기본 인증을 사용할 수 있습니다. 자세한 내용은 [API 설정 구성](api-management-howto-create-apis.md#configure-api-settings)을 참조하세요.
* [Azure API Management에서 클라이언트 인증서 인증을 사용하여 백 엔드 서비스를 보호하는 방법](api-management-howto-mutual-certificates.md)에 설명된 대로 SSL 상호 인증을 사용할 수 있습니다.
* 백 엔드 서비스에서 IP 허용 목록을 사용할 수 있습니다. 표준 또는 프리미엄 계층 API Management 인스턴스를 사용하는 경우 게이트웨이의 IP 주소가 일관성 있게 유지됩니다. 이 IP 주소를 허용하도록 허용 목록을 구성할 수 있습니다. Azure Portal의 대시보드에서 API Management 인스턴스의 IP 주소를 가져올 수 있습니다.
* API Management 인스턴스를 Azure Virtual Network에 연결합니다. 자세한 내용은 [Azure API Management에서 VPN 연결을 설정하는 방법](api-management-howto-setup-vpn.md)을 참조하세요.

### <a name="how-do-i-copy-my-api-management-service-instance-to-a-new-instance"></a>API Management 서비스 인스턴스를 새 인스턴스에 복사하려면 어떻게 해야 합니까?
API Management 인스턴스를 새 인스턴스로 복사하려는 경우 몇 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

* API Management의 백업 및 복원 기능을 사용할 수 있습니다. 자세한 내용은 [Azure API Management에서 서비스 백업 및 복원을 사용하여 재해 복구를 구현하는 방법](api-management-howto-disaster-recovery-backup-restore.md)을 참조하세요.
* 사용자 고유의 백업을 만들고 [API Management REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx)를 사용하여 기능을 복원합니다. REST API를 사용하여 원하는 서비스 인스턴스에서 엔터티를 저장 및 복원합니다.
* Git를 사용하여 서비스 구성을 다운로드한 다음 새 인스턴스에 업로드합니다. 자세한 내용은 [Git를 사용하여 API Management 서비스 구성을 저장 및 구성하는 방법](api-management-configuration-repository-git.md)을 참조하세요.

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>API 관리 인스턴스를 프로그래밍 방식으로 관리할 수 있습니까?
예, 다음을 사용하여 프로그래밍 방식으로 API Management를 관리할 수 있습니다.

* [API Management REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx)
* [Microsoft Azure ApiManagement 서비스 관리 라이브러리 SDK](http://aka.ms/apimsdk)
* [서비스 배포](https://msdn.microsoft.com/library/mt619282.aspx) 및 [서비스 관리](https://msdn.microsoft.com/library/mt613507.aspx) PowerShell cmdlet

### <a name="how-do-i-add-a-user-to-the-administrators-group"></a>관리자 그룹에 사용자를 추가하려면 어떻게 해야 합니까?
관리자 그룹에 사용자를 추가하는 방법은 다음과 같습니다.

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. 업데이트하려는 API Management 인스턴스가 있는 리소스 그룹으로 이동합니다.
3. API Management에서 **API Management 참여자** 역할을 사용자에게 할당합니다.

이제 새롭게 추가된 참여자는 Azure PowerShell [cmdlet](https://msdn.microsoft.com/library/mt613507.aspx)을 사용할 수 있습니다. 관리자 권한으로 로그인하는 방법은 다음과 같습니다.

1. `Login-AzureRmAccount` cmdlet을 사용하여 로그인합니다.
2. `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`를 사용하여 서비스가 있는 구독에 컨텍스트를 설정합니다.
3. `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`을(를) 사용하여 Single Sign-On URL을 가져옵니다.
4. URL을 사용하여 관리 포털에 액세스합니다.
### <a name="why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor"></a>추가하려는 정책을 정책 편집기에서 사용할 수 없는 이유는 무엇입니까?
추가하려는 정책이 정책 편집기에서 흐리게 표시되거나 음영으로 표시되는 경우 정책에 대해 올바른 범위에 있는지 확인합니다. 각 정책 문은 특정 범위 및 정책 섹션에서 사용하도록 되어 있습니다. 정책의 정책 섹션 및 범위를 검토하려면 [API Management 정책](https://msdn.microsoft.com/library/azure/dn894080.aspx)에서 정책의 사용 섹션을 확인하세요.

### <a name="how-do-i-use-api-versioning-in-api-management"></a>API Management에서 API 버전 관리를 사용하려면 어떻게 해야 합니까?
API Management에서 API 버전 관리를 사용하는 몇 가지 옵션이 있습니다.

* API Management에서 다른 버전을 나타내는 API를 구성할 수 있습니다. 예를 들어 두 개의 다른 API인 MyAPIv1 및 MyAPIv2가 있을 수 있습니다. 개발자는 개발자가 사용하려는 버전을 선택할 수 있습니다.
* 버전 세그먼트를 포함하지 않는 서비스 URL로(예: https://my.api) API를 구성할 수도 있습니다. 그런 다음 각 작업의 [URL 다시 쓰기](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) 템플릿에서 버전 세그먼트를 구성합니다. 예를 들어 /resource라는 [URL 템플릿](api-management-howto-add-operations.md#url-template) 및 /v1/Resource라는 [URL 다시 쓰기](api-management-howto-add-operations.md#rewrite-url-template) 템플릿이 포함된 작업을 가질 수 있습니다. 각 작업에 대해 별도로 버전 세그먼트 값을 변경할 수 있습니다.
* API 서비스 URL의 “기본” 버전 세그먼트를 유지하려면 선택한 작업에서 백 엔드 요청 경로를 변경하기 위해 [백 엔드 서비스 설정](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) 정책을 사용하는 정책을 설정합니다.
### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>단일 API에서 여러 환경을 설정하려면 어떻게 해야 합니까?
단일 API에서 여러 환경(예: 테스트 환경 및 프로덕션 환경)을 설정하는 두 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

* 동일한 테넌트에 다른 API를 호스팅할 수 있습니다.
* 다른 테넌트에 동일한 API를 호스팅할 수 있습니다.

### <a name="can-i-use-soap-with-api-management"></a>API Management와 함께 SOAP를 사용할 수 있습니까?
이제 [SOAP 통과](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) 지원을 사용할 수 있습니다. 관리자는 해당 SOAP 서비스의 WSDL을 가져올 수 있고 Azure API Management는 SOAP 프런트 엔드를 만듭니다. 개발자 포털 설명서, 테스트 콘솔, 정책 및 분석을 SOAP 서비스에 모두 사용할 수 있습니다.

### <a name="is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>API 관리 게이트웨이 IP 주소가 상수입니까? 그것을 방화벽 규칙에 사용할 수 있습니까?
표준 계층 및 프리미엄 계층에서 API Management 테넌트의 공용 IP 주소(VIP)는 일부 예외를 제외하고 테넌트의 수명 동안 정적입니다. IP 주소는 다음 상황에서 변경됩니다.

* 서비스가 삭제된 다음 다시 생성되었습니다.
* 서비스 구독이 일시 중단된 다음(예: 미지불) 복원되었습니다.
* Azure Virtual Network를 추가하거나 제거합니다(프리미엄 계층에서만 Virtual Network를 사용할 수 있음).

다중 지역 배포의 경우 지역이 비워진 다음 복원되는 경우 지역 주소가 변경됩니다(프리미엄 계층에서만 다중 지역 배포를 사용할 수 있음).

다중 지역 배포를 위해 구성된 프리미엄 계층 테넌트는 지역 당 하나의 공용 IP 주소에 할당됩니다.

Azure Portal의 테넌트 페이지에서 IP 주소(또는 다중 지역 배포에서 여러 IP 주소)를 가져올 수 있습니다.

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>AD FS 보안을 통해 OAuth 2.0 권한 부여 서버를 구성할 수 있습니까?
AD FS(Active Directory Federation Services) 보안으로 OAuth 2.0 권한 부여 서버를 구성하는 방법을 알아보려면 [API Management에서 ADFS 사용](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/)을 참조하세요.

### <a name="what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations"></a>여러 지리적 위치에 배포할 때 API Management에서 사용하는 라우팅 방법은 무엇입니까?
API Management는 여러 지리적 위치에 배포할 때 [성능 트래픽 라우팅 방법](../traffic-manager/traffic-manager-routing-methods.md#performance-traffic-routing-method)을 사용합니다. 들어오는 트래픽은 가장 가까운 API 게이트웨이로 라우팅됩니다. 한 지역이 오프라인 상태가 되면, 들어오는 트래픽은 다음으로 가까운 게이트웨이로 자동으로 라우팅됩니다. [Traffic Manager 라우팅 방법](../traffic-manager/traffic-manager-routing-methods.md)에서 라우팅 방법에 대해 자세히 알아봅니다.

### <a name="can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance"></a>Azure Resource Manager 템플릿을 사용하여 API Management 서비스 인스턴스를 만들 수 있습니까?
예. [Azure API Management 서비스](http://aka.ms/apimtemplate) 빠른 시작 템플릿을 참조하세요.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>백 엔드에 대해 자체 서명된 SSL 인증서를 사용할 수 있습니까?
예. 백 엔드에 자체 서명된 SSL(Secure Sockets Layer) 인증서를 사용하는 방법은 다음과 같습니다.

1. API Management를 사용하여 [백 엔드](https://msdn.microsoft.com/library/azure/dn935030.aspx) 엔터티를 만듭니다.
2. **skipCertificateChainValidation** 속성을 **true**로 설정합니다.
3. 자체 서명된 인증서를 더 이상 허용하지 않으려면 백 엔드 엔터티를 삭제하거나 **skipCertificateChainValidation** 속성을 **false**로 설정합니다.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository"></a>Git 리포지토리를 복제하려고 할 때 인증 실패가 발생하는 이유는 무엇입니까?
Git 자격 증명 관리자를 사용하는 경우 또는 Visual Studio를 사용하여 Git 리포지토리를 복제하려는 경우 Windows 자격 증명 대화 상자와 함께 알려진 문제가 발생할 수 있습니다. 대화 상자는 암호 길이를 127자로 제한하고 Microsoft에서 생성된 암호를 자릅니다. 암호 길이를 줄이는 작업 중입니다. 현재는 Git 리포지토리를 복제하는 데 Git Bash를 사용하세요.

### <a name="does-api-management-work-with-azure-expressroute"></a>API Management는 Azure ExpressRoute와 함께 작동합니까?
예. API Management는 Azure ExpressRoute와 함께 작동합니다.

### <a name="can-i-move-an-api-management-service-from-one-subscription-to-another"></a>구독 간에 API Management 서비스를 이동할 수 있습니까?
예. 방법을 알아보려면 [새 리소스 그룹 또는 구독으로 리소스 이동](../azure-resource-manager/resource-group-move-resources.md)을 참조하세요.

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>내 API를 가져오는 데 제한 사항 또는 알려진 문제가 있나요?
Open API(Swagger), WSDL 및 WADL 형식에 대해 [알려진 문제 및 제한 사항](api-management-api-import-restrictions.md)입니다.



<!--HONumber=Feb17_HO2-->


