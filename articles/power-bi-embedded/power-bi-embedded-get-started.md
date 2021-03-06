---
title: "Microsoft Power BI Embedded 시작"
description: "Power BI Embedded, 대화형 Power BI 보고서를 비즈니스 인텔리전스 응용 프로그램에 추가"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
translationtype: Human Translation
ms.sourcegitcommit: fd0ddf8275ab58eb3c411123b776654fb46cae5d
ms.openlocfilehash: 5770bbfcf700b1cefea6d22e0d5f025c1660e744


---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Microsoft Power BI Embedded 시작
**Power BI Embedded** 는 응용 프로그램 개발자가 자신의 응용 프로그램에 대화형 Power BI 보고서를 추가할 수 있는 Azure 서비스입니다. **Power BI Embedded** 는 사용자가 로그인하는 방식을 다시 디자인하거나 변경하지 않고 기존 응용 프로그램을 사용합니다.

**Microsoft Power BI Embedded** 의 리소스는 [Azure ARM API](https://msdn.microsoft.com/library/mt712306.aspx)를 통해 프로비전됩니다. 이 경우에 프로비전하는 리소스는 **Power BI 작업 영역 컬렉션**입니다.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>작업 영역 컬렉션 만들기
**작업 영역 컬렉션** 은 응용 프로그램에 포함될 콘텐츠에 대한 최상위 Azure 리소스 및 컨테이너입니다. **작업 영역 컬렉션** 은 두 가지 방법으로 만들 수 있습니다.

* 수동으로 Azure 포털 사용
* 프로그래밍 방식으로 Azure Resource Manager(ARM) API 사용

Azure 포털을 사용하여 **작업 영역 컬렉션** 을 빌드하는 단계를 살펴 보겠습니다.

1. **Azure 포털**( [http://portal.azure.com](http://portal.azure.com))을 열고 로그인합니다.
2. 위쪽 패널에서 **+ 새로 만들기** 를 클릭합니다.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. **데이터 + 분석**에서 **Power BI Embedded**를 클릭합니다.
4. **워크스페이스 컬렉션 블레이드**에서 필요한 정보를 입력합니다. **가격 책정**이 경우 [Power BI Embedded 가격](http://go.microsoft.com/fwlink/?LinkID=760527)을 참조하세요.
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. **만들기**를 클릭합니다.

**작업 영역 컬렉션** 을 프로비전하려면 몇 분 정도 걸립니다. 완료되면 **작업 영역 컬렉션 블레이드**가 표시됩니다.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

**만들기 블레이드** 에는 작업 영역을 만들고 콘텐츠를 여기에 배포하는 API를 호출하는 데 필요한 정보가 들어 있습니다.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Power BI API 액세스 키 보기
Power BI REST API를 호출하는 데 필요한 정보의 가장 중요한 부분 중 하나는 **선택키**입니다. API 요청을 인증하는 데 사용되는 **앱 토큰** 을 생성하는 데 사용됩니다. **선택키**를 보려면 **설정 블레이드**에서 **선택키**를 클릭합니다. **앱 토큰**에 대한 자세한 내용은 [Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)를 참조하세요.

   ![](media/power-bi-embedded-get-started/access-keys.png)

두 개의 키가 있는 것을 확인할 수 있습니다.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

이러한 키를 복사하고 응용 프로그램에 안전하게 저장합니다. **작업 영역 컬렉션**의 모든 콘텐츠에 대한 액세스를 제공하므로 이러한 키를 암호처럼 처리하는 것이 중요합니다.

두 키가 나열되지만 한 번에 하나의 키만 필요합니다. 두 번째 키가 제공되므로 서비스에 대한 액세스를 중단하지 않고 정기적으로 키를 다시 생성할 수 있습니다.

이제 응용 프로그램에 대한 Power BI의 인스턴스, **선택키**가 있으며 보고서를 사용자 자신의 앱에 가져올 수 있습니다. 보고서를 가져오는 방법을 알아보기 전에 다음 섹션에서 앱에 포함할 Power BI 데이터 집합 및 보고서를 만드는 방법에 대해 설명합니다.

## <a name="working-with-workspaces"></a>작업 영역에서 작업

작업 영역 컬렉션을 만든 후에는 보고서 및 데이터 집합을 보관할 작업 영역을 만들어야 합니다. 작업 영역을 만들려면 [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx)를 사용해야 합니다.

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app"></a>앱에 포함할 Power BI 데이터 집합 및 보고서 만들기
이제 응용 프로그램에 대한 Power BI의 인스턴스를 만들었고 **선택키**가 있으므로 포함할 Power BI 데이터 집합 및 보고서를 만들어야 합니다. 데이터 집합 및 보고서는 **Power BI Desktop**을 사용하여 만들 수 있습니다. [Power BI 데스크톱은 무료로](https://go.microsoft.com/fwlink/?LinkId=521662)다운로드할 수 있습니다. 또는 빠르게 시작하려면 [소매 분석 샘플 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)를 다운로드할 수 있습니다.

> [!NOTE]
> **Power BI Desktop**을 사용하는 방법에 대해 알아보려면 [Power BI Desktop 시작](https://powerbi.microsoft.com/en-us/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop)을 참조하세요.

**Power BI Desktop**에서 데이터의 복사본을 **Power BI Desktop**으로 가져오거나 **DirectQuery**를 사용하는 데이터 원본에 직접 연결하여 데이터 원본에 연결합니다.

**가져오기**와 **DirectQuery** 사용 간의 차이점은 다음과 같습니다.

| 가져오기 | DirectQuery |
| --- | --- |
| 테이블, 열 *및 데이터* 를 **Power BI 데스크톱**으로 가져오거나 복사합니다. 시각화로 작업하면서 **Power BI 데스크톱** 으로 데이터의 복사본을 쿼리합니다. 기본 데이터에서 발생한 모든 변경 내용을 보려면 현재 데이터 집합을 다시 새로 고치거나 가져오거나 완료해야 합니다. |*테이블 및 열* 만 **Power BI 데스크톱**으로 가져오거나 복사합니다. 시각화로 작업하면서 **Power BI 데스크톱** 으로 기본 데이터 원본을 쿼리하므로 항상 최신 데이터가 표시됩니다. |

데이터 원본에 연결하는 방법에 대 한 자세한 내용은 [데이터 원본에 연결](power-bi-embedded-connect-datasource.md)을 참조하세요.

**Power BI 데스크톱**에 작업을 저장하면 PBIX 파일이 만들어집니다. 이 파일에는 보고서가 포함됩니다. 또한 데이터를 가져오는 경우 PBIX에 전체 데이터 집합이 포함되고 **DirectQuery**를 사용하는 경우 PBIX에 데이터 집합 스키마만 포함됩니다. [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx)를 사용하여 프로그래밍 방식으로 PBIX를 작업 영역에 배포합니다.

> [!NOTE]
> **Power BI Embedded** 에는 데이터 집합이 가리키는 서버 및 데이터베이스를 변경하고 데이터 집합에서 데이터베이스에 연결하는 데 사용할 서비스 계정 자격 증명을 설정하기 위한 추가 API가 있습니다. [SetAllConnections 게시](https://msdn.microsoft.com/library/mt711505.aspx) 및 [게이트웨이 데이터 원본 패치](https://msdn.microsoft.com/library/mt711498.aspx)를 참조하세요.

## <a name="next-steps"></a>다음 단계
이전 단계에서 작업 영역 컬렉션과 첫 번째 보고서 및 데이터 집합을 만들었습니다. 이제 **Power BI Embedded**에 대한 코드를 작성하는 방법을 알아볼 시간입니다. 시작을 도와주기 위해 샘플 웹앱을 만들었습니다. [샘플 시작](power-bi-embedded-get-started-sample.md). 샘플에서는 다음 작업 방법을 보여 줍니다.

* 콘텐츠 프로비전
  * 작업 영역 만들기
  * PBIX 파일 가져오기
  * 연결 문자열을 업데이트하고 데이터 집합에 대한 자격 증명을 설정합니다.
* 보고서를 안전하게 포함

## <a name="see-also"></a>참고 항목
* [샘플 시작](power-bi-embedded-get-started-sample.md)
* [Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)
* [Power BI 데스크톱](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

궁금한 점이 더 있나요? [Power BI 커뮤니티를 이용하세요.](http://community.powerbi.com/)




<!--HONumber=Feb17_HO1-->


