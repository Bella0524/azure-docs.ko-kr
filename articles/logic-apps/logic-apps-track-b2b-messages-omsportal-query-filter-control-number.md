---
title: "쿼리를 사용하여 AS2, X12, EDIFACT 메시지 추적 - Azure Logic Apps | Microsoft Docs"
description: "쿼리를 사용하여 Operations Management Suite 포털에서 B2B 메시지를 추적합니다."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
translationtype: Human Translation
ms.sourcegitcommit: 67313e4ff780e6c64dfc3d767ea49167c2a390f4
ms.openlocfilehash: 701a3bbadb340c9390b486a5295eced056db70a0


---
# <a name="track-b2b-messages-in-the-operations-management-suite-portal-by-using-a-query"></a>쿼리를 사용하여 Operations Management Suite 포털에서 B2B 메시지 추적
Operations Management Suite 포털에서 B2B(Business-to-Business) 메시지를 추적하려면 특정 교환 컨트롤 번호에 대한 데이터를 필터링하는 쿼리를 만들면 됩니다.

## <a name="prereqs"></a>선행 조건

디버깅 및 자세한 진단 정보를 보려면 X12 커넥터가 있는 [Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics-and-alerts)의 [통합 계정](logic-apps-monitor-b2b-message.md)에서 진단 기능을 켭니다. 그런 다음 [진단 데이터](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)를 Operations Management Suite 포털에 게시하는 단계를 수행합니다.

## <a name="search-for-an-interchange-control-number"></a>교환 컨트롤 번호 검색

1. 시작 페이지에서 **로그 검색**을 선택합니다.  
![로그 검색 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

2. 검색 상자에 **Type="AzureDiagnostics"**를 입력합니다. 데이터를 필터링하려면 **추가**를 선택합니다.  
![쿼리 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

3. **interchange**를 입력하고 **event_record_messageProperties_interchangeControlNumber_s**를 선택한 후 **추가**를 선택합니다.  
![필터 추가](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query2.png)

4. 데이터를 필터링할 컨트롤 번호를 선택하고 **적용**을 선택합니다.  
![컨트롤 번호 검색](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query3.png)

5. 선택한 컨트롤 번호에 대한 데이터를 필터링하기 위해 만든 쿼리를 찾습니다.   
![쿼리 찾기](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query4.png)

6. 쿼리의 이름을 입력한 후 저장합니다.   
![쿼리 저장](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query5.png)

7. 쿼리를 보고 향후 검색에 사용하려면 **즐겨찾기**를 선택합니다.  
![쿼리 보기](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query7.png)

8. 새 교환 컨트롤 번호를 검색하도록 쿼리를 업데이트할 수 있습니다.  
![쿼리 업데이트](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query6.png)


## <a name="next-steps"></a>다음 단계
* [사용자 지정 추적 스키마](logic-apps-track-integration-account-custom-tracking-schema.md)에 대해 자세히 알아봅니다.   
* [AS2 추적 스키마](logic-apps-track-integration-account-as2-tracking-schemas.md)에 대해 자세히 알아봅니다.    
* [X12 추적 스키마](logic-apps-track-integration-account-x12-tracking-schema.md)에 대해 자세히 알아봅니다.  
* [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)에 대해 자세히 알아봅니다.



<!--HONumber=Jan17_HO5-->


