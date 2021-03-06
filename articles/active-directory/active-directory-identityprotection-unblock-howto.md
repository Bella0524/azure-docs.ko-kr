---
title: "Azure Active Directory ID 보호 - 사용자를 차단 해제하는 방법 | Microsoft Docs"
description: "Azure Active Directory ID 보호 정책에 의해 차단된 사용자를 차단 해제하는 방법을 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 사용자 차단 해제"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: markvi
translationtype: Human Translation
ms.sourcegitcommit: 87c73981c74fc763fd1aec6c283e934c77008441
ms.openlocfilehash: d17fa0ffb0c55d49487804cd28d8903107069f06


---
# <a name="azure-active-directory-identity-protection---how-to-unblock-users"></a>Azure Active Directory ID 보호 - 사용자를 차단 해제하는 방법
Azure Active Directory ID 보호를 사용하여 구성된 조건을 만족하는 경우에 사용자를 차단하는 정책을 구성할 수 있습니다. 일반적으로 차단된 사용자 연락처는 데스크가 차단 해제되도록 돕습니다. 이 항목은 차단된 사용자를 해제하기 위해 수행할 수 있는 단계를 설명합니다.

## <a name="determine-the-reason-for-blocking"></a>차단 이유를 확인합니다.
사용자를 차단 해제하는 첫 번째 단계로 다음 단계가 좌우되는 사용자를 차단한 정책의 유형을 결정해야 합니다.
Azure Active Directory ID보호를 사용하여 로그인 위험 정책 또는 사용자 위험 정책으로 사용자를 차단할 수 있습니다.

로그인을 시도하는 동안 사용자에게 표시된 대화 상자의 제목에서 사용자를 차단한 정책 유형을 가져올 수 있습니다.

| 정책 | 사용자 대화 상자 |
| --- | --- |
| 로그인 위험 |![차단된 로그인](./media/active-directory-identityprotection-unblock-howto/02.png) |
| 사용자 위험 |![차단된 계정](./media/active-directory-identityprotection-unblock-howto/104.png) |

다음에 의해 차단된 사용자:

* 로그인 위험 정책은 의심스러운 로그인이라고도 함
* 사용자 위험 정책은 위험한 계정이라고도 함

## <a name="unblocking-suspicious-sign-ins"></a>의심스러운 로그인 차단 해제
의심스러운 로그인을 차단 해제하기 위해 다음 옵션이 있습니다.

1. **친숙한 위치 또는 장치에서 로그인** - 차단된 의심스러운 로그인에 대한 일반적인 이유는 알 수 없는 위치 또는 장치에서의 로그인 시도입니다. 사용자는 친숙한 위치 또는 장치에서 로그인을 시도하여 차단 이유인지 여부를 빠르게 확인할 수 있습니다.
2. **정책에서 제외** - 로그인 정책의 현재 구성이 특정 사용자에 대해 문제를 일으킨다고 생각하는 경우 여기에서 사용자를 제외할 수 있습니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.
3. **정책 비활성화** - 정책 구성이 모든 사용자에 대해 문제를 일으킨다고 생각하는 경우 정책을 비활성화할 수 있습니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.

## <a name="unblocking-accounts-at-risk"></a>위험한 계정 차단 해제
위험한 계정을 차단 해제하기 위해 다음 옵션이 있습니다.

1. **암호 재설정** - 사용자의 암호를 다시 설정할 수 있습니다. 자세한 내용은 [수동으로 안전한 암호 다시 설정](active-directory-identityprotection.md#manual-secure-password-reset) 을 참조하세요.
2. **모든 위험 이벤트 해제** - 액세스 차단에 대해 구성된 사용자 위험 수준에 도달한 경우 사용자 위험 정책은 사용자를 차단합니다. 수동으로 보고된 위험 이벤트를 닫아서 사용자의 위험 수준을 줄일 수 있습니다. 자세한 내용은 [수동으로 위험 이벤트 닫기](active-directory-identityprotection.md#closing-risk-events-manually)를 참조하세요.
3. **정책에서 제외** - 로그인 정책의 현재 구성이 특정 사용자에 대해 문제를 일으킨다고 생각하는 경우 여기에서 사용자를 제외할 수 있습니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.
4. **정책 비활성화** - 정책 구성이 모든 사용자에 대해 문제를 일으킨다고 생각하는 경우 정책을 비활성화할 수 있습니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
 Azure AD ID 보호에 대해 자세히 살펴보시겠습니까? [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 확인하세요.



<!--HONumber=Nov16_HO3-->


