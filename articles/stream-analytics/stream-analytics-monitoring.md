---
title: "Stream Analytics 작업 모니터링 이해 | Microsoft Docs"
description: "Stream Analytics 작업 모니터링 이해"
keywords: "쿼리 모니터"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 01/24/2017
ms.author: jeffstok
translationtype: Human Translation
ms.sourcegitcommit: e9ea21be1fabb5846c4f3b7b05f3a93298830e57
ms.openlocfilehash: 5119d1d6c02b8e080a9e0905ae21a2bddefab03a


---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a>Stream Analytics 작업 모니터링 및 쿼리를 모니터링하는 방법 이해

## <a name="introduction-the-monitor-page"></a>소개: 모니터 페이지
Azure Portal은 쿼리 및 작업 성능을 모니터링하고 문제를 해결하는 데 사용할 수 있는 핵심 성과 메트릭을 표시합니다. 이러한 메트릭을 보려면 메트릭을 보려고 하는 Stream Analytics 작업으로 이동하고 개요 페이지에서 **모니터링** 섹션을 봅니다.  

![모니터링 링크](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

다음과 같은 창이 표시됩니다.

![작업 모니터링 대시보드](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Stream Analytics에 사용 가능한 메트릭
| 메트릭                 | 정의                               |
| ---------------------- | ---------------------------------------- |
| SU % 사용률       | 작업의 크기 조정 탭에서 작업에 할당한 스트리밍 단위의 사용률입니다. 이 표시가 80% 이상에 도달하면 이벤트 처리가 지연되거나 진행을 중단할 가능성이 큽니다. |
| 입력 이벤트           | Stream Analytics 작업이 받은 데이터의 양(이벤트 수)입니다. 입력 소스로 전송되는 이벤트의 유효성을 검사하는 데 사용할 수 있습니다. |
| 출력 이벤트          | Stream Analytics 작업이 출력 대상에 보낸 데이터의 양입니다(이벤트 수). |
| 순서 비지정 이벤트    | 이벤트 순서 지정 정책에 기반하여 조정된 타임스탬프를 받거나 삭제된 순서가 정해지지 않은 수신 이벤트의 수입니다. 잘못된 순서 허용 시간 설정의 구성에 의해 영향을 받을 수 있습니다. |
| 데이터 변환 오류 | Stream Analytics 작업에 의해 발생하는 데이터 변환 오류 수입니다. |
| 런타임 오류         | Stream Analytics 작업을 실행하는 동안 발생한 총 오류 수입니다. |
| 늦은 입력 이벤트      | 지연 도착 허용 시간 설정의 이벤트 순서 지정 정책 구성에 기반하여 타임스탬프가 조정되었거나 삭제된 소스에서 늦게 도착한 이벤트의 수입니다. |
| 기능 요청      | Azure Machine Learning 함수(있는 경우)에 대한 호출 수입니다. |
| 실패한 기능 요청 | 실패한 Azure Machine Learning 함수 호출(있는 경우) 수입니다. |
| 함수 이벤트        | Azure Machine Learning 함수(있는 경우)에 전송된 이벤트 수입니다. |
| 입력 이벤트 바이트      | Stream Analytics 작업이 받은 데이터의 양(바이트)입니다. 입력 소스로 전송되는 이벤트의 유효성을 검사하는 데 사용할 수 있습니다. |


## <a name="customizing-monitoring-in-the-azure-portal"></a>Azure Portal에서 모니터링 사용자 지정하기
차트 편집 설정에서 차트 유형, 표시되는 메트릭 및 시간 범위를 조정할 수 있습니다. 자세한 내용은 [모니터링을 사용자 지정하는 방법](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)을 참조하세요.

  ![쿼리 모니터 시간 그래프](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [Azure Stream Analytics 소개](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-get-started.md)
* [Azure 스트림 분석 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure 스트림 분석 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)




<!--HONumber=Jan17_HO1-->


