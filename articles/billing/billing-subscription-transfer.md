---
title: "Azure 구독의 소유권 양도 | Microsoft Docs"
description: "다른 사용자에게 Azure 구독을 전송하는 방법과 프로세스에 대한 몇 가지 질문과 대답(FAQ)"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: c8ecdc1e-c9c5-468c-a024-94ae41e64702
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genli
translationtype: Human Translation
ms.sourcegitcommit: 1faa99b774d5f6cc4e4939ee465809710fd31524
ms.openlocfilehash: 0cb3237f923faa32d77285775dafde55d678c7db


---
# <a name="transferring-ownership-of-an-azure-subscription"></a>Azure 구독의 소유권 양도

계정 센터에서 종량제, Visual Studio, Action Pack 또는 BizSpark 구독을 다른 사용자에게 양도할 수 있습니다. 이러한 구독 유형에 대한 Azure 외부 서비스 양도도 지원됩니다. 

다음 경우에 Azure 구독의 소유권을 양도하려고 할 수 있습니다.

* Azure 구독 청구 소유권을 다른 사람에게 양도해야 합니다.
* Azure에 등록하는 데 사용된 계정을 변경하려고 합니다. Microsoft 계정을 사용하려고 했으나 대신 회사 또는 학교 계정을 사용하게 되었습니다.
* Azure 구독을 한 디렉터리에서 다른 컴퓨터로 이동하려고 합니다.
* 다른 테넌트에 있는 Azure 및 Office 365를 통합하려고 합니다.

구독을 다른 제품으로 변경하려면 [Azure 구독을 다른 제품으로 전환](billing-how-to-switch-azure-offer.md)을 참조하세요. 

## <a name="how-to-transfer-ownership-of-an-azure-subscription"></a>Azure 구독의 소유권을 양도하는 방법
> [!VIDEO https://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/Transfer-an-Azure-subscription/player]
>
>

1. <https://account.windowsazure.com/Subscriptions>에 로그인합니다. 소유권 양도를 수행하려면 계정 관리자여야 합니다. 구독의 계정 관리자가 누구인지 알아보는 방법은 [질문과 대답](#faq)을 참조하세요.

2. 양도할 구독을 선택합니다.

3. **구독 양도** 옵션을 클릭합니다. 단추가 보이지 않으면 [FAQ](#no-button)를 참조하세요.

   ![Azure 계정 구독 탭](./media/billing-subscription-transfer/image1.png)
4. 프롬프트에 따라 받는 사람을 지정 합니다.

   ![구독 양도 대화 상자](./media/billing-subscription-transfer/image2.PNG)
5. 받는 사람은 수락 링크가 포함된 전자 메일을 자동으로 받게 됩니다.

   ![받는 사람에게 구독 양도 전자 메일](./media/billing-subscription-transfer/image3.png)
6. 받는 사람은 링크를 클릭하고 지불 정보 입력 등의 지침을 따릅니다.

   ![첫 번째 구독 양도 웹 페이지](./media/billing-subscription-transfer/image4.png)

   ![두 번째 구독 양도 웹 페이지](./media/billing-subscription-transfer/image5.png)
7. 성공! 구독이 이제 양도됩니다.

<a id="faq"></a>

## <a name="frequently-asked-questions-faq"></a>질문과 대답(FAQ)
* <a name="whoisaa"></a> **구독의 계정 관리자는 누구인가요?**

  계정 관리자는 Azure 구독을 등록 또는 구입한 사람입니다. 이러한 사용자는 [계정 센터](https://account.windowsazure.com/Home/Index)에 액세스하고, 구독 만들기, 구독 취소, 구독에 대한 청구 변경 또는 서비스 관리자 변경 등의 다양한 관리 작업을 수행할 수 있는 권한이 있습니다. 구독에 대한 계정 관리자를 잘 모를 경우 다음 단계를 사용하여 확인하세요.

  1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
  2. 허브 메뉴에서 **구독**을 선택합니다.
  3. 확인하려는 구독을 선택한 다음 **설정**에서 확인합니다.
  4. **속성**을 선택합니다. 구독의 계정 관리자는 **계정 관리자** 상자에 표시됩니다.  

* **모든 것이 양도되나요? 양도 항목에 리소스 그룹, VM, 디스크 및 기타 실행 중인 서비스가 포함되나요?**

  예, VM, 디스크, 웹 사이트 등 모든 리소스가 새 소유자에게 양도됩니다. 그러나 여러분이 설정한 [관리자 역할](billing-add-change-azure-subscription-administrator.md) 및 [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md) 정책은 양도되지 않습니다. 

* <a id="no-button"></a> **구독 양도 단추가 보이지 않는 이유는 무엇인가요?**

  **구독 양도** 단추가 보이지 않으면 해당 제품의 구독 양도가 지원되지 않는 것입니다. [고객 지원에 문의하세요](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

* **구독 양도로 인해 서비스 가동 중지 시간이 발생합니까?**

  서비스에 영향은 없습니다. 구독을 양도하면 현재 계정 관리자의 구독이 취소되고 받는 사람의 계정에서 구독이 만들어집니다. 새 구독은 기본 Azure 서비스에 연결됩니다. 구독 ID는 동일합니다.

* **어떻게 이 프로세스를 사용하여 구독 디렉터리를 변경하나요?**

  계정 관리자가 속한 디렉터리에 Azure 구독이 생성됩니다. 디렉터리를 변경하려면 구독을 대상 디렉터리의 사용자 계정으로 전달합니다. 해당 사용자가 전달을 수락하는 절차를 완료하면 구독이 자동으로 대상 디렉터리로 이동합니다.

* **다른 조직으로부터 구독 청구 소유권을 양도 받은 경우, 내 리소스에 계속 액세스할 수 있습니까?**

  구독을 다른 테넌트에 양도하는 경우, 이전 테넌트와 연결된 사용자는 구독에 액세스할 수 없게 됩니다. 사용자가 더 이상 서비스 관리자 또는 공동 관리자가 아닌 경우에도 다른 보안 메커니즘을 통해 다음 항목을 포함하여 구독에 액세스할 수도 있습니다.

  * 구독 리소스에 대한 관리자 권한을 사용자에게 부여하는 관리 인증서. 자세한 내용은 [Azure용 관리 인증서 만들기 및 업로드](../cloud-services/cloud-services-certs-create.md)를 참조하세요.
  * 저장소와 같은 서비스에 대한 액세스 키. 자세한 내용은 [Azure 저장소 계정 정보](../storage/storage-create-storage-account.md)를 참조하세요.
  * Azure Virtual Machines 같은 서비스에 대한 원격 액세스 자격 증명.

  이는 완전한 목록이 아닙니다. 받는 사람은 리소스에 액세스를 제한해야 하는 경우 서비스와 연결된 암호 업데이트를 고려해야 합니다. 대부분의 리소스는 다음과 같이 업데이트할 수 있습니다.

    1. [Azure 포털](https://portal.azure.com)로 이동합니다.
    2. 허브 메뉴에서 **모든 리소스**를 선택합니다.
    3. 리소스를 선택합니다. 
    4. 리소스 블레이드에서 **설정**을 클릭합니다. 여기서 기존 암호를 보고 업데이트할 수 있습니다.

* **청구 주기 도중에 구독을 양도하는 경우 전체 청구 주기에 대해 받는 사람이 지불해야 합니까?**

  양도가 완료되는 지점까지 보고된 사용량에 대한 지불 책임은 보낸 사람에게 있습니다. 받는 사람은 양도 받는 시점부터 보고된 사용량에 대해 지불 책임이 있습니다. 양도하기 전에 발생하지만 나중에 보고되는 일부 사용량이 있을 수 있습니다. 이 사용량은 받은 사람의 청구서에 포함됩니다.

* **받는 사람은 사용량 및 청구 내역에 액세스할 수 있습니까?**

  받는 사람이 사용할 수 있는 유일한 정보는 마지막 청구 금액입니다. 첫 번째 청구가 생성하기 전에 구독이 양도된 경우에는 현재 잔액도 공개됩니다. 나머지 사용량 및 청구 내역은 구독과 함께 양도되지 않습니다.

* **양도하는 동안 제품을 변경할 수 있습니까?**

  제품을 동일하게 유지해야 합니다. 제품을 변경하려면 [Azure 구독을 다른 제품으로 전환](billing-how-to-switch-azure-offer.md)을 참조하세요.

* **다른 국가에서 사용자 계정에 대 한 구독을 양도할 수 있습니까?**

  아니요. 다른 국가의 사용자 계정으로 구독을 양도할 수는 없습니다. 받는 사람의 사용자 계정은 동일한 국가에 있어야 합니다.

* **받는 사람이 다른 지불 방법을 사용할 수 있나요?**

  예. 그렇지만 현재 구독 청구 내역이 두 계정으로 분할됩니다.  

* **Azure 구독을 양도하면 결제 방법에 영향을 주나요?**

  구독을 양도하려면 구독 지불을 위해 신용 카드 또는 이와 비슷한 결제 방법을 제공해야 합니다. 예를 들어 Bob이 Jane에게 구독을 양도하고 Jane이 양도를 수락하는 경우 Jane은 구독을 결제하는 데 사용할 결제 방법도 제공해야 합니다. 양도가 완료되면 Jane에게 구독이 양도되므로 Bob에게 더 이상 청구되지 않습니다.

* **내 Azure 구독에 대한 데이터 및 서비스를 새 구독으로 마이그레이션하려면 어떻게 해야 하나요?**

  구독 소유권을 양도할 수 없는 경우 리소스를 수동으로 마이그레이션할 수 있습니다. [새 리소스 그룹 또는 구독으로 리소스 이동](../azure-resource-manager/resource-group-move-resources.md)을 참조하세요.

## <a name="transfer-subscription-ownership-for-enterprise-agreement-ea-customers"></a>EA(기업 계약) 고객의 구독 소유권 양도
엔터프라이즈 관리자는 등록 내 구독 소유권을 양도할 수 있습니다. 양도를 시작하려면 EA 포털에서 [계정 소유권 양도](https://ea.azure.com/helpdocs/changeAccountOwnerForASubscription)를 참조하세요.

## <a name="next-steps-after-accepting-ownership-of-a-subscription"></a>구독 소유권을 수락한 후 다음 단계
1. 이제 계정 관리자입니다. 서비스 관리자 및 공동 관리자를 검토하고 업데이트합니다. [Azure 클래식 포털](https://manage.windowsazure.com)에서 설정으로 이동하여 관리자를 관리합니다. [관리자 역할에 대해 알아봅니다](billing-add-change-azure-subscription-administrator.md).

2. 구독 및 서비스에 대해 RBAC(역할 기반 액세스 제어)를 사용할 수도 있습니다. [Azure Portal](https://portal.azure.com)을 방문합니다. [RBAC에 대한 자세한 정보](../active-directory/role-based-access-control-configure.md)

3. 이 구독의 서비스와 연결된 자격 증명을 업데이트합니다. 내용은 다음과 같습니다.
   
   * 구독 리소스에 대한 관리자 권한을 사용자에게 부여하는 관리 인증서. 자세한 내용은 [Create and upload a management certificate for Azure](../cloud-services/cloud-services-certs-create.md)
   
   * 저장소와 같은 서비스에 대한 액세스 키. 자세한 내용은 [Azure Storage 계정 정보](../storage/storage-create-storage-account.md)를 참조하세요.
   
   * Azure Virtual Machines 같은 서비스에 대한 원격 액세스 자격 증명. 

4. [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)에서 [이 구독에 대한 청구 경고를 업데이트](billing-set-up-alerts.md)합니다. 

5. 파트너와 함께 작업하는 경우 이 구독에서 파트너 ID를 업데이트하는 것이 좋습니다. [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)에서 파트너 ID를 업데이트할 수 있습니다.


## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.
다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요. 





<!--HONumber=Feb17_HO2-->


