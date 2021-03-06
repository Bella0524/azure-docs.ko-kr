데이터 팩터리는 각각 다른 작업 부하에서 고객 구독이 보호되도록 하기 위해 다음 기본 제한을 적용한 다중 테넌트 서비스입니다. 지원에 문의하여 최대 한도까지 구독에 대한 제한 수를 늘릴 수 있습니다. 

| **리소스** | **기본 제한** | **최대 제한** |
| --- | --- | --- |
| Azure 구독의 데이터 팩터리 |50 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 데이터 팩터리 내의 파이프라인  |2500 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 데이터 팩터리 내의 데이터 집합 |5000 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 데이터 집합당 동시 조각 |10 |10 |
| 파이프라인 개체에 대한 개체당 바이트<sup>1</sup> |200KB |200KB |
| 데이터 집합 및 연결된 서비스 개체에 대한 개체당 바이트 <sup>1</sup> |100KB |2000KB |
| 구독 내부의 HDInsight 주문형 클러스터 코어<sup>2</sup> |60 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 클라우드 데이터 이동 단위 <sup>3</sup> |8 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 파이프라인 활동 실행에 대한 재시도 횟수 |1000 |MaxInt(32비트) |

<sup>1</sup>파이프라인, 데이터 집합 및 연결된 서비스 개체에서 작업의 논리적 그룹화를 나타냅니다. 이러한 개체에 대한 제한은 Azure 데이터 팩터리 서비스를 통해 이동 및 처리할 수 있는 데이터 규모와는 관련이 없습니다. 데이터 팩터리는 페타바이트의 데이터 처리를 위해 확장되도록 설계되었습니다.

<sup>2</sup> 주문형 HDInsight 코어는 데이터 팩터리를 포함하는 구독 외부에서 할당됩니다. 결과적으로, 위의 제한은 주문형 HDInsight 코어에 대한 데이터 팩터리 실행 코어 제한이며 Azure 구독과 연결된 코어 제한과는 다릅니다.

<sup>3</sup> 클라우드 데이터 이동 단위(DMU)는 클라우드 간 복사 작업에 사용됩니다. Data Factory 내 단일 단위의 힘(CPU, 메모리, 네트워크 리소스 할당의 조합)을 나타내는 척도입니다. 일부 시나리오의 경우 더 많은 DMU를 활용하여 더 높은 복사 처리량을 달성할 수 있습니다. 자세한 내용은 [클라우드 데이터 이동 단위](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) 섹션을 참조하세요.

| **리소스** | **기본 하한값** | **최소 제한** |
| --- | --- | --- |
| 일정 간격 |15분 |15분 |
| 재시도 간의 간격 |1초 |1초 |
| 재시도 시간 제한 값 |1초 |1초 |

### <a name="web-service-call-limits"></a>웹 서비스 호출 제한
Azure Resource Manager에는 API 호출 제한이 있습니다. [Azure 리소스 관리자 API 제한](../articles/azure-subscription-service-limits.md#resource-group-limits)범위 안의 속도로 API 호출을 수행할 수 있습니다. 



<!--HONumber=Feb17_HO3-->


