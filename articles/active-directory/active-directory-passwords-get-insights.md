---
title: "정보 얻기: Azure AD 암호 관리 보고서 | Microsoft Docs"
description: "이 문서에서는 사용자의 조직에서 암호 관리 작업에 대한 정보를 얻기 위해 보고서를 사용하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: asteen
manager: femila
editor: curtand
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: asteen
translationtype: Human Translation
ms.sourcegitcommit: dcda8b30adde930ab373a087d6955b900365c4cc
ms.openlocfilehash: 9e66d3d4877b0f04d101da73aa819b76857b7e18


---
# <a name="how-to-get-operational-insights-with-password-management-reports"></a>암호 관리 보고서와 함께 Operational Insights를 얻는 방법
> [!IMPORTANT]
> **로그인하는 데 문제가 있나요?** 그렇다면 [암호를 변경하고 재설정하는 방법은 다음과 같습니다](active-directory-passwords-update-your-own-password.md).
> 
> 

이 섹션에서는 Azure Active Directory의 암호 관리 보고서를 사용하여 조직에서 사용자 암호 재설정을 사용하여 변경하는 방법을 볼 수 있는 방법을 설명합니다.

* [**암호 관리 보고서 개요**](#overview-of-password-management-reports)
* [**암호 관리 보고서를 보는 방법**](#how-to-view-password-management-reports)
* [**조직에서 암호 재설정 등록 활동 보기**](#view-password-reset-registration-activity)
* [**조직에서 암호 재설정 활동 보기**](#view-password-reset-activity)

## <a name="overview-of-password-management-reports"></a>암호 관리 보고서 개요
암호 재설정을 배포하면 조직에서 가장 일반적인 다음 단계 중 하나는 조직에서 사용 중인 방법을 보는 것입니다.  예를 들어, 사용자가 암호 재설정을 위해 등록되는 방법 또는 지난 몇 일 내에 수행된 암호 재설정 횟수에 대한 정보를 얻을 수 있습니다.  다음은 현재 [Azure 관리 포털](https://manage.windowsazure.com) 에 있는 암호 관리 보고서로 답변할 수 있는 일반적인 질문들입니다.

* 얼마나 많은 사람들이 암호 재설정을 위해 등록합니까?
* 누가 암호 재설정을 위해 등록합니까?
* 사람들이 등록하는 데이터는 무엇입니까?
* 지난 7일 동안 얼마나 많은 사람들이 자신의 암호를 재설정했습니까?
* 사용자나 관리자가 자신의 암호를 재설정하는 가장 일반적인 방법은 무엇입니까?
* 암호 재설정을 시도할 때 사용자나 관리자가 직면하는 공통적인 문제는 무엇입니까?
* 어느 관리자가 자신의 암호를 자주 재설정합니까?
* 암호 재설정에 대해 의심스러운 활동이 있습니까?

## <a name="how-to-view-password-management-reports"></a>암호 관리 보고서를 보는 방법
암호 관리 보고서를 찾으려면 다음 단계를 따릅니다.

1. **Azure 관리 포털** 의 [Active Directory](https://manage.windowsazure.com)확장을 클릭합니다.
2. 포털에 표시되는 목록에서 디렉터리를 선택합니다.
3. **보고서** 탭을 클릭합니다.
4. **활동 로그** 섹션을 잠급니다.
5. **암호 재설정 활동** 보고서 또는 **암호 재설정 등록 활동** 보고서 중 하나를 선택합니다.
   
   ![][001]

## <a name="how-to-access-password-management-reports-from-an-api"></a>API에서 암호 관리 보고서에 액세스하는 방법
이제 2015년 8월을 기준으로 Azure AD 보고서 및 이벤트는 암호 재설정 및 암호 재설정 등록 보고서에 포함된 모든 정보를 검색하도록 지원합니다.

이 데이터에 액세스하려면 작은 앱 또는 스크립트를 작성하여 서버에서 검색해야 합니다. [Azure AD Reporting API를 시작하는 방법을 알아봅니다](active-directory-reporting-api-getting-started.md)

작동하는 스크립트가 있으면 다음으로 시나리오에 맞게 검색할 수 있는 암호 재설정 및 등록 이벤트를 검사하려 합니다.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): 암호 재설정 이벤트에 대해 사용 가능한 열을 나열합니다.
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): 암호 재설정 등록 이벤트에 대해 사용 가능한 열을 나열합니다.

## <a name="view-password-reset-registration-activity"></a>암호 재설정 등록 활동 보기
암호 재설정 등록 활동 보고서는 조직 내에서 발생한 모든 암호 재설정 등록을 보여줍니다.  암호 재설정 등록은 암호 재설정 등록 포털([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup))에서 인증 정보를 성공적으로 등록한 사용자에 대한 이 보고서에 표시됩니다.

* **최대 시간 범위**: 1개월
* **최대 행 수**: 무제한
* **다운로드 가능**: 예, CSV 파일을 통해
  
    ![][002]

### <a name="description-of-report-columns"></a>보고서 열 설명
다음 목록에서는 각 보고서의 열에 대해 자세히 설명합니다.

* **사용자** – 암호 재설정 등록 작업을 시도한 사용자입니다.
* **역할** – 디렉터리에서 사용자의 역할입니다.
* **날짜 및 시간** – 시도한 날짜 및 시간입니다.
* **등록된 데이터** – 암호 재설정 등록 중 사용자가 제공한 인증 데이터입니다.

### <a name="description-of-report-values"></a>보고서 값 설명
다음 테이블에서 각 열에 대해 허용되는 다른 값을 설명합니다.

| 열 | 허용되는 값과 해당 의미 |
| --- | --- |
| 등록된 데이터 |**대체 전자 메일** – 인증하는 데 사용자가 사용한 대체 전자 메일 또는 인증 전자 메일<p><p>**사무실 전화** – 인증하는 데 사용자가 사용한 사무실 전화<p>**휴대폰** – 인증하는 데 사용자가 사용한 휴대폰 또는 인증 전화<p>**보안 질문** – 인증하는 데 사용자가 사용한 보안 질문<p>**위의 조합(예: 대체 전자 메일 + 휴대폰)** – 2개의 게이트 정책이 지정되고 암호 재설정 요청을 인증하는 데 사용자가 사용한 두 메서드를 표시합니다. |

## <a name="view-password-reset-activity"></a>암호 재설정 활동 보기
이 보고서는 조직 내에서 발생한 모든 암호 재설정 시도를 보여줍니다.

* **최대 시간 범위**: 1개월
* **최대 행 수**: 무제한
* **다운로드 가능**: 예, CSV 파일을 통해
  
    ![][003]

### <a name="description-of-report-columns"></a>보고서 열 설명
다음 목록에서는 각 보고서의 열에 대해 자세히 설명합니다.

1. **사용자** – 암호 재설정 작업을 시도한 사용자(사용자가 암호를 재설정할 때 제공되는 사용자 ID 필드에 따라).
2. **역할** – 디렉터리에서 사용자의 역할입니다.
3. **날짜 및 시간** – 시도한 날짜 및 시간입니다.
4. **사용된 메서드** –이 재설정 작업에 사용자가 사용한 인증 메서드입니다.
5. **결과** – 암호 재설정 작업의 최종 결과입니다.
6. **세부 정보** – 암호 재설정 결과로 왜 이 값이 생성되었는지에 대한 자세한 설명입니다.  또한 예기치 않은 오류를 해결하기 위해 수행할 수 있는 완화 단계를 포함합니다.

### <a name="description-of-report-values"></a>보고서 값 설명
다음 테이블에서 각 열에 대해 허용되는 다른 값을 설명합니다.

| 열 | 허용되는 값과 해당 의미 |
| --- | --- |
| 사용된 메서드 |**대체 전자 메일** – 인증하는 데 사용자가 사용한 대체 전자 메일 또는 인증 전자 메일<p>**사무실 전화** – 인증하는 데 사용자가 사용한 사무실 전화<p>**휴대폰** – 인증하는 데 사용자가 사용한 휴대폰 또는 인증 전화<p>**보안 질문** – 인증하는 데 사용자가 사용한 보안 질문<p>**위의 조합(예: 대체 전자 메일 + 휴대폰)** – 2개의 게이트 정책이 지정되고 암호 재설정 요청을 인증하는 데 사용자가 사용한 두 메서드를 표시합니다. |
| 결과 |**중단됨** – 사용자가 암호 재설정을 시작하지만 완료하지 않고 중간에서 중단됩니다.<p>**차단됨** -사용자의 계정이 암호 재설정 페이지를 사용하거나 24시간 동안 너무 여러 번 단일 암호 재설정 게이트를 사용하여 암호를 재설정할 수 없습니다.<p>**취소됨** – 사용자가 암호 재설정을 시작했지만 취소 단추를 클릭하여 도중 세션을 취소했습니다. <p>**연결된 관리자** – 세션 중 사용자가 해결할 수 없는 문제가 생겨 사용자가 암호 재설정 작업을 완료하는 대신 “관리자에게 문의” 링크를 클릭했습니다.<p>**실패함** – 사용자가 기능을 사용하도록 구성되지 않았기 때문에 암호를 재설정할 수 없습니다(라이선스 없음, 누락된 인증 정보, 암호 관리 온-프레미스지만 쓰기 저장이 꺼져 있음).<p>**성공함** - 암호가 재설정되었습니다. |
| 세부 정보 |아래 테이블을 참조하세요. |

### <a name="allowed-values-for-details-column"></a>세부 정보 열에 대해 허용되는 값
다음은 암호 재설정 활동 보고서를 사용하는 경우 예상할 수 있는 결과 형식 목록입니다.

| 세부 정보 | 결과 형식 |
| --- | --- |
| 사용자가 전자 메일 확인 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 모바일 SMS 확인 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 모바일 음성 통화 확인 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 사무실 음성 통화 확인 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 보안 질문 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 사용자 ID를 입력한 후 중단함 |Abandoned |
| 사용자가 전자 메일 확인 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 모바일 SMS 확인 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 모바일 음성 통화 확인 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 사무실 음성 통화 확인 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 보안 질문 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 새 암호를 선택하기 전에 중단함 |Abandoned |
| 사용자가 새 암호를 선택하는 중에 중단함 |Abandoned |
| 사용자가 너무 많은 잘못된 SMS 확인 코드를 입력하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 모바일 음성 인증을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 사무실 음성 인증을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 보안 질문에 답변을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 전화번호 확인을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 필수 인증 방법을 전달하기 전에 취소함 |Cancelled |
| 사용자가 새 암호를 전송하기 전에 취소함 |Cancelled |
| 사용자 전자 메일 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 사용자가 모바일 SMS 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 사용자가 모바일 음성 통화 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 사용자가 사무실 음성 통화 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 사용자가 보안 질문 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 이 사용자에 대한 암호 재설정이 사용되지 않습니다. 이를 해결하려면 구성 탭에서 암호 재설정 사용합니다. |Failed |
| 사용자에게 라이선스가 없습니다. 이를 해결하기 위해 사용자에게 라이선스를 추가할 수 있습니다. |Failed |
| 사용자가 쿠키를 사용하지 않고 장치에서 다시 설정하려고 시도함 |Failed |
| 사용자의 계정에 정의된 인증 메서드가 부족합니다. 이를 해결하려면 인증 정보를 추가합니다. |Failed |
| 사용자의 암호는 관리 대상 온-프레미스입니다. 이를 해결하려면 암호 쓰기 저장을 사용하도록 설정할 수 있습니다. |Failed |
| 온-프레미스 암호 재설정 서비스에 접근할 수 없습니다. 동기화 컴퓨터의 이벤트 로그를 확인합니다. |Failed |
| 사용자의 온-프레미스 암호를 재설정하는 중에 문제가 발생했습니다. 동기화 컴퓨터의 이벤트 로그를 확인합니다. |Failed |
| 이 사용자는 암호 재설정 사용자 그룹의 멤버가 아닙니다. 이를 해결하려면 해당 그룹에 이 사용자를 추가합니다. |Failed |
| 암호 재설정은 이 테넌트에 대해 완전히 비활성화되었습니다. 이를 해결하려면 [여기](http://aka.ms/ssprtroubleshoot) 를 참조하세요. |Failed |
| 사용자가 성공적으로 암호를 재설정함 |성공함 |

## <a name="links-to-password-reset-documentation"></a>암호 재설정 설명서에 대한 링크
다음은 모든 Azure AD 암호 재설정 설명서 페이지에 대한 링크입니다.

* **로그인하는 데 문제가 있나요?** 그렇다면 [암호를 변경하고 재설정하는 방법은 다음과 같습니다](active-directory-passwords-update-your-own-password.md).
* [**작동 방식**](active-directory-passwords-how-it-works.md) - 6개의 다양한 구성 요소 서비스 및 기능에 대해 알아봅니다.
* [**시작하기**](active-directory-passwords-getting-started.md) -사용자가 클라우드 또는 온-프레미스 암호를 다시 설정하고 변경할 수 있는 방법에 대해 알아봅니다.
* [**사용자 지정**](active-directory-passwords-customize.md) - 모양과 느낌 및 조직의 요구에 맞게 서비스의 동작을 사용자 지정하는 방법에 대해 알아봅니다
* [**모범 사례**](active-directory-passwords-best-practices.md) - 사용자의 조직에서 신속하게 배포하고 효과적으로 암호를 관리하는 방법에 대해 알아봅니다.
* [**FAQ**](active-directory-passwords-faq.md) -자주 묻는 질문에 답변합니다.
* [**문제해결**](active-directory-passwords-troubleshoot.md) -신속하게 서비스와의 문제를 해결하는 방법에 대해 알아봅니다.
* [**자세히 알아보기**](active-directory-passwords-learn-more.md) -서비스의 작동 원리 방식의 기술적 측면을 자세히 알아봅니다.

[001]: ./media/active-directory-passwords-get-insights/001.jpg "Image_001.jpg"
[002]: ./media/active-directory-passwords-get-insights/002.jpg "Image_002.jpg"
[003]: ./media/active-directory-passwords-get-insights/003.jpg "Image_003.jpg"



<!--HONumber=Feb17_HO2-->


