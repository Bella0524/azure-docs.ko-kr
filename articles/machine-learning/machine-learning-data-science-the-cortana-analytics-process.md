---
title: "팀 데이터 과학 프로세스란 무엇인가요?  | Microsoft Docs"
description: "팀 데이터 과학 프로세스는 고급 분석을 활용하는 지능형 응용 프로그램을 구축하기 위한 체계적인 방법입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: deprecated
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: data-science-process-overview
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 49bb8201a93e622774e197801b566caa03ed28a6


---
# <a name="what-is-the-team-data-science-process-tdsp"></a>TDSP(팀 데이터 과학 프로세스)란 무엇인가요?
[TDSP(팀 데이터 과학 프로세스)](data-science-process-overview.md) 는 데이터 과학자 팀이 응용 프로그램을 제품으로 변환하는 데 필요한 활동의 전체 수명 주기를 효율적으로 공동 작업할 수 있도록 지능적인 응용 프로그램을 빌드하는 데 체계적인 방법을 제공합니다. TDSP는 문제를 정의하고, 필요한 도구 및 환경을 설정하고, 관련 데이터를 분석하고, 예측 모델을 빌드 및 평가한 다음 엔터프라이즈 응용 프로그램에서 이러한 모델을 배포하는 방법에 대한 **지침** 을 제공하는 일련의 단계에 대해 간단히 설명합니다. 

**팀 데이터 과학 프로세스**의 단계는 다음과 같습니다.  

![CAP-워크플로](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

프로세스는 **반복적**입니다. 즉, 새로운 기능과 기존 기능 또는 모델의 구체화된 기능에 대한 이해가 변화해 가며 순서에서 이전에 완료한 단계를 다시 작업해야 합니다. 조직의 기존 개발 및 프로젝트 계획 프로세스는 TDSP에서 정의한 단계 순서에서 작동하도록 **쉽게 조정**됩니다. 

프로세스의 단계는 [TDSP 학습 경로](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 에 다이어그램 및 링크가 제공되어 있으며 아래에 설명되어 있습니다.  

## <a name="preparation-steps"></a>준비 단계
## <a name="p1-plan-the-analytics-project"></a>P1. 분석 프로젝트 계획
비즈니스 목표 및 문제를 정의하여 분석 프로젝트를 시작합니다. 이들을 **비즈니스 요구 사항**측면에서 지정합니다. 이 단계의 주요 목표는 이러한 요구 사항을 만족하기 위해 분석에서 예측해야 하는 주요 비즈니스 변수(판매 예측 또는 주문 중 사기의 확률 등)를 식별하는 것입니다. 그런 다음 분석의 시각에서 프로젝트의 목표를 달성하는 데 필요한 **데이터 원본** 에 대한 이해를 발전시키기 위해 일반적으로 추가 계획이 필수입니다. 예를 들어 문제를 해결하고 프로젝트 목표를 달성하기 위해 다른 종류의 데이터를 더 수집하고 기록해야 한다고 확인되는 경우는 일반적으로 많지 않습니다. 지침에 대해서는 [팀 데이터 과학 프로세스에 대한 환경 계획](machine-learning-data-science-plan-your-environment.md) 및 [Azure Machine Learning의 고급 분석 시나리오](machine-learning-data-science-plan-sample-scenarios.md)를 참조하세요.  

## <a name="p2-setup-analytics-environment"></a>P2. 분석 환경 설정
팀 데이터 과학 프로세스에 대한 분석 환경은 여러 구성 요소를 포함합니다. 

* **데이터 작업 영역** 분석과 모델링을 위해 데이터를 단계화하는 경우 
* **처리 인프라** 데이터 전처리, 탐색 및 모델링을 위해
* **런타임 인프라** 분석 모델을 운영하고 모델을 사용하는 지능형 클라이언트 응용 프로그램을 실행하기 위해  

설정해야 할 분석 인프라는 흔히 코어 운영 체제와 별개인 환경의 일부입니다. 하지만 일반적으로 엔터프라이즈 내의 여러 시스템뿐만 아니라 회사 외부 출처의 데이터도 활용 합니다. 분석 인프라는 순수하게 클라우드 기반 또는 온-프레미스 설정 또는 둘의 혼성 형태일 수 있습니다. 옵션에 대해서는 [팀 데이터 과학 프로세스에서 사용되는 데이터 과학 환경 설정](machine-learning-data-science-environment-setup.md)을 참조하세요.

## <a name="analytics-steps"></a>분석 단계:
## <a name="1-ingest-data-into-the-analytical-environment"></a>1. 분석 환경으로 데이터 수집
첫 단계는 엔터프라이즈 내부 또는 외부와 같은 여러 출처의 관련 데이터를, 해당 데이터를 처리할 수 있는 분석 환경으로 가져오는 것입니다. 원본 데이터의 **형식** 은 대상에서 필요한 형식과 다를 수 있습니다. 따라서 수집 도구에서 데이터 변환을 어느 정도 수행해야 할 수 있습니다. 옵션에 대해서는 [분석용 저장소 환경에 데이터 로드](machine-learning-data-science-ingest-data.md)

초기 데이터 수집 외에도 많은 지능형 응용 프로그램은 진행 중인 학습 프로세스의 일부로 데이터를 정기적으로 새로 고쳐야 합니다. **데이터 파이프라인** 또는 워크플로를 설정하여 이 작업을 수행할 수 있습니다. 이는 솔루션을 배포하는 지능형 응용 프로그램에 사용되는 분석 모델의 재생성과 재평가를 포함하는 프로세스의 반복적 부분입니다. 예를 들어 [Azure Data Factory를 사용하여 온-프레미스 SQL Server에서 SQL Azure로 데이터 이동](machine-learning-data-science-move-sql-azure-adf.md)을 참조하세요.

## <a name="2-explore-and-pre-process-data"></a>2. 데이터 탐색 및 전처리
다음 단계는 **요약 통계**, 관계 등을 조사하고 **시각화** 등과 같은 기술을 사용하여 데이터를 더 깊이 이해하는 것입니다. 또한 **데이터 품질** 과, 값 누락, 데이터 형식 불일치, 일관되지 않은 데이터 관계 등의 무결성 문제도 이 단계에서 처리됩니다. 전처리 변환을 사용하여 원시 데이터를 정리해야 추가 분석 및 모델링을 수행할 수 있습니다. 관련 설명은 [확장된 기계 학습을 위한 데이터 준비 작업](machine-learning-data-science-prepare-data.md)을 참조하세요.

## <a name="3-develop-features"></a>3. 기능 개발
데이터 과학자는 도메인 전문가와 협력하여 데이터 집합의 두드러진 속성을 캡쳐하는 기능을 식별해야 하며 이 기능을 사용하면 계획 중에 식별된 주요 비즈니스 변수를 가장 잘 예측할 수 있습니다. 이러한 새 기능은 기존 데이터에서 파생될 수도 있고 추가 데이터를 수집해야 할 수도 있습니다. 이 프로세스를 **기능 엔지니어링** 이라 하며 효과적인 예측 분석 시스템을 만드는 주요 단계 중 하나입니다. 이 단계에서 도메인 전문지식과 데이터 탐색 단계에서 얻은 통찰력을 창의적으로 결합해야 합니다. 지침에 대해서는 [팀 데이터 과학 프로세스의 기능 엔지니어링](machine-learning-data-science-create-features.md)을 참조하세요.

## <a name="4-create-predictive-models"></a>4. 예측 모델 만들기
데이터 과학자는 정리되고 기능화한 데이터를 사용하여 계획 단계에서 정의한 비즈니스 요구 사항에 의해 식별된 주요 변수를 예측하는 분석 모델을 만듭니다. 기계 학습 시스템은 광범위한 사례에 적용할 수 있는 여러 **모델링 알고리즘** 을 지원합니다. 지침에 대해서는 [팀 Azure 기계 학습을 위한 알고리즘 선택 방법](machine-learning-algorithm-choice.md)을 참조하세요.

데이터 과학자는 자신의 예측 작업에 가장 적절한 모델을 선택해야 하며 여러 모델에서 나온 결과를 최선의 결과를 얻도록 결합해야 하는 경우는 많지 않습니다. 모델링을 위해 입력한 데이터는 대개 다음 세 부분으로 무작위로 나누어집니다.

* 학습 데이터 집합, 
* 유효성 검사 데이터 집합 
* 테스트 데이터 집합 

모델은 **학습 데이터 집합**을 사용하여 구축됩니다. 모델을 실행하고 **유효성 검사 데이터 집합**에 대한 예측 오류를 측정하여 최적의 모델 결합(조정된 매개 변수를 이용한)을 선택합니다. 마지막으로 **테스트 데이터 집합** 을 사용하여 모델을 학습하거나 유효성 검사하는 데 사용되지 않는 독립 데이터에 대해 선택된 모델의 성능을 평가합니다.  절차에 대해서는 [Azure 기계 학습에서 모델 성능을 평가하는 방법](machine-learning-evaluate-model-performance.md)을 참조하세요.

## <a name="5-deploy-and-consume-models"></a>5. 배포 및 사용 모델
제대로 수행되는 모델 집합을 확보한 후 다른 응용 프로그램에서 사용할 수 있도록 해당 모델 집합을 **조작 가능한** 상태로 설정할 수 있습니다. 비즈니스 요구 사항에 따라 **실시간**으로 또는 **일괄 처리** 방식으로 예측을 수행합니다. 조작 가능한 상태로 설정하려면 온라인 웹 사이트, 스프레드 시트, 대시보드나 LOB(기간 업무) 및 백 엔드 응용 프로그램 등 여러 응용 프로그램에서 쉽게 사용하는 **개방형 API 인터페이스** 를 사용하여 모델을 노출해야 합니다. [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

## <a name="summary-and-next-steps"></a>요약 및 다음 단계
[팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)는 고급 분석을 사용하여 지능형 응용 프로그램을 만드는 데 필요한 작업에 대한 **지침을 제공** 하는 일련의 반복 단계로 모델링됩니다. 또한 각 단계는 다양한 Microsoft 기술을 사용하여 기술된 작업을 완료하는 방법에 대한 세부 정보를 제공합니다. 

TDSP에 특정 유형의 **설명서** 아티팩트가 규정되어 있지 않지만, 데이터 탐색, 모델링 및 평가의 결과를 문서화하고 필요한 경우 분석을 반복할 수 있도록 관련 코드를 저장하는 것이 모범 사례입니다. 이렇게 하면 유사한 데이터 및 예측 작업을 수반하는 다른 응용 프로그램에 대해 작업할 때에도 분석 작업을 다시 사용할 수 있습니다.

**특정 시나리오** 에 대한 프로세스의 모든 단계를 보여 주는 종합적인 전체 연습도 제공됩니다. 예를 들어 다음을 참조하세요.

* [실행 중인 팀 데이터 과학 프로세스: SQL Server 사용](machine-learning-data-science-process-sql-walkthrough.md)
* [실행 중인 팀 데이터 과학 프로세스: HDInsight Hadoop 클러스터 사용](machine-learning-data-science-process-hive-walkthrough.md)
* [Azure HD.mdnsight에서 Spark를 사용하는 데이터 과학](machine-learning-data-science-spark-overview.md)
* [Azure Data Lake에서 확장성 있는 데이터 과학: 종단 간 연습](machine-learning-data-science-process-data-lake-walkthrough.md)




<!--HONumber=Nov16_HO3-->


