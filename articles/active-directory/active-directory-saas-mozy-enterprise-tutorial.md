---
title: "자습서: Mozy Enterprise와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory에서 Mozy Enterprise를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/26/2017
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 991a7d112bc0cd65466be394dbb1aad9ca823681
ms.openlocfilehash: 726880186693756941538f767dfba40c54ac9fd9


---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a>자습서: Mozy Enterprise와 Azure Active Directory 통합
이 자습서는 Azure 및 Mozy Enterprise의 통합을 보여 주기 위한 것입니다.  
이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.

* 유효한 Azure 구독
* Mozy Enterprise 테넌트

이 자습서를 완료한 후 Mozy Enterprise에 할당한 Azure AD 사용자가 Mozy Enterprise 회사 사이트(서비스 공급자가 시작한 로그온)에서 또는 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 SSO(Single Sign-On)할 수 있습니다.

이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.

1. Mozy Enterprise에 응용 프로그램 통합 사용
2. Single Sign-On 구성
3. 사용자 프로비전 구성
4. 사용자 할당

![시나리오](./media/active-directory-saas-mozy-enterprise-tutorial/IC777308.png "시나리오")

## <a name="enabling-the-application-integration-for-mozy-enterprise"></a>Mozy Enterprise에 응용 프로그램 통합 사용
이 섹션은 Mozy Enterprise에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.

**Mozy Enterprise에 응용 프로그램 통합을 사용하도록 설정하려면**

1. Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.
   
   ![Active Directory](./media/active-directory-saas-mozy-enterprise-tutorial/IC700993.png "Active Directory")
2. **디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.
3. 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.
   
   ![응용 프로그램](./media/active-directory-saas-mozy-enterprise-tutorial/IC700994.png "응용 프로그램")
4. 페이지 맨 아래에 있는 **추가** 를 클릭합니다.
   
   ![응용 프로그램 추가](./media/active-directory-saas-mozy-enterprise-tutorial/IC749321.png "응용 프로그램 추가")
5. **수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.
   
   ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-mozy-enterprise-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. **검색 상자**에 **mozy enterprise**를 입력합니다.
   
   ![응용 프로그램 갤러리](./media/active-directory-saas-mozy-enterprise-tutorial/IC777309.png "응용 프로그램 갤러리")
7. 결과 창에서 **Mozy Enterprise**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.
   
   ![Mozy Enterprise](./media/active-directory-saas-mozy-enterprise-tutorial/IC777310.png "Mozy Enterprise")
   
## <a name="configuring-single-sign-on"></a>Single Sign-On 구성

이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 Mozy Enterprise에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.  

이 절차의 일부로 base-64로 인코딩된 인증서 파일을 Mozy Enterprise 테넌트에 업로드해야 합니다. 이 절차를 잘 모르는 경우 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)

**Single Sign-On을 구성하려면 다음 단계를 수행합니다.**

1. Azure 클래식 포털의 **Mozy Enterprise** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-mozy-enterprise-tutorial/IC771709.png "Single Sign-On 구성")
2. **Mozy Enterprise에 대한 사용자 로그온 방법을 선택하세요.** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-mozy-enterprise-tutorial/IC777311.png "Single Sign-On 구성")
3. **앱 URL 구성** 페이지의 **Mozy Enterprise 로그인 URL** 텍스트 상자에 "*https://\<tenant-name\>.Mozyenterprise.com*" 패턴을 사용하여 URL을 입력한 후 **다음**을 클릭합니다.
   
   ![앱 URL 구성](./media/active-directory-saas-mozy-enterprise-tutorial/IC777312.png "앱 URL 구성")
4. **Mozy Enterprise에서 Single Sign-On 구성** 페이지에서 인증서를 다운로드하려면 **인증서 다운로드**를 클릭한 다음 컴퓨터에 인증서 파일을 저장합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-mozy-enterprise-tutorial/IC777313.png "Single Sign-On 구성")
5. 다른 웹 브라우저 창에서 Mozy Enterprise 회사 사이트에 관리자로 로그인합니다.
6. **구성** 섹션에서 **인증 정책**을 클릭합니다.
   
   ![인증 정책](./media/active-directory-saas-mozy-enterprise-tutorial/IC777314.png "인증 정책")
7. **인증 정책** 섹션에서 다음 단계를 수행합니다.
   
   ![인증 정책](./media/active-directory-saas-mozy-enterprise-tutorial/IC777315.png "인증 정책")
   
   1. **디렉터리 서비스**를 **공급자**로 선택합니다.
   2. **LDAP 푸시 사용**을 선택합니다.
   3. **SAML 인증** 탭을 클릭합니다.
   4. Azure 클래식 포털의 **Mozy Enterprise에서 Single Sign-On 구성** 대화 상자 페이지에서 **인증 요청 URL** 값을 복사한 다음 **인증 URL** 텍스트 상자에 붙여넣습니다.
   5. Azure 클래식 포털의 **Mozy Enterprise에서 Single Sign-On 구성** 대화 상자 페이지에서 **ID 공급자 ID** 값을 복사한 다음 **SAML 끝점** 텍스트 상자에 붙여넣습니다.
   6. 다운로드한 인증서에서 **Base-64로 인코딩된** 파일을 만듭니다.  
   
      >[!TIP]
      >자세한 내용은 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)
      >  
   7. Base&64;로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **SAML 인증서** 텍스트 상자에 붙여 넣습니다.
   8. **SSO를 사용하여 관리자가 네트워크 자격 증명으로 로그인**을 선택합니다.
   9. **변경 내용 저장**을 클릭합니다.
8. Azure 클래식 포털의 **Mozy Enterprise에서 Single Sign-On 구성** 대화 상자 페이지에서 Single Sign-On 구성 확인을 선택한 다음 **완료**를 클릭합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-mozy-enterprise-tutorial/IC777316.png "Single Sign-On 구성")
   
## <a name="configuring-user-provisioning"></a>사용자 프로비전 구성

Azure AD 사용자가 Mozy Enterprise에 로그인할 수 있도록 하려면 Mozy Enterprise로 프로비전되어야 합니다.  
Mozy Enterprise의 경우 프로비전은 수동 작업입니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. **Mozy Enterprise** 테넌트에 로그인합니다.
2. **사용자**를 클릭한 후 **새 사용자 추가**를 클릭합니다.
   
   ![사용자](./media/active-directory-saas-mozy-enterprise-tutorial/IC777317.png "사용자")
   
   > [!NOTE]
   > **Mozy**가 **인증 정책**에서 공급자로 선택된 경우에만 **새 사용자 추가** 옵션이 표시됩니다. SAML 인증이 구성된 경우 Single Sign-On을 통해 처음 로그인 시 사용자가 자동으로 추가됩니다.
   > 
    
3. 새 사용자 대화 상자 페이지에서 다음 단계를 수행합니다.
   
   ![사용자 추가](./media/active-directory-saas-mozy-enterprise-tutorial/IC777318.png "사용자 추가")
   
  1. **그룹 선택** 목록에서 그룹을 선택합니다.
  2. **사용자 유형** 목록에서 유형을 선택합니다.
  3. **사용자 이름** 텍스트 상자에 Azure AD 사용자의 이름을 입력합니다.
  4. **이메일** 텍스트 상자에 Azure AD 사용자의 이메일 주소를 입력합니다.
  5. **사용자 명령 이메일 보내기**를 선택합니다.
  6. **사용자 추가**를 클릭합니다.
   > [!NOTE]
   > 사용자를 만든 후 활성화되기 전에 계정을 확인하기 위해 링크가 포함된 Azure AD 사용자에게 이메일이 전송됩니다.


> [!NOTE]
> 다른 Mozy Enterprise 사용자 계정 생성 도구 또는 Mozy Enterprise가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.
> 
> 

## <a name="assigning-users"></a>사용자 할당
구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.

**Mozy Enterprise에 사용자를 할당하려면 다음 단계를 수행합니다.**

1. Azure 클래식 포털에서 테스트 계정을 만듭니다.
2. **Mozy Enterprise** 응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.
   
   ![사용자 할당](./media/active-directory-saas-mozy-enterprise-tutorial/IC777319.png "사용자 할당")
3. 테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.
   
   ![예](./media/active-directory-saas-mozy-enterprise-tutorial/IC767830.png "예")

Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.




<!--HONumber=Feb17_HO1-->


