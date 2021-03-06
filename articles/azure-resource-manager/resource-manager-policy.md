---
title: "Azure 리소스 정책 | Microsoft Docs"
description: "Azure Resource Manager 정책을 사용하여 배포하는 동안 일관된 리소스 속성을 설정했는지 확인하는 방법에 대해 설명합니다. 구독 또는 리소스 그룹에 정책을 적용할 수 있습니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: tomfitz
translationtype: Human Translation
ms.sourcegitcommit: 6d459e37b8b39f5d76c4ec86ebb7351c783b81fb
ms.openlocfilehash: 64cb4be184e02519a6c496f8639035201ebb60f8


---
# <a name="resource-policy-overview"></a>리소스 정책 개요
리소스 정책을 사용하면 조직에서 리소스에 대한 규칙을 설정할 수 있습니다. 규칙을 정의하여 비용을 제어하고 리소스를 보다 쉽게 관리할 수 있습니다. 예를 들어, 특정 유형의 가상 컴퓨터를 허용하는지를 지정하거나 모든 리소스에 특정 태그를 요구할 수 있습니다. 정책은 모든 자식 리소스에 의해 상속됩니다. 이에 따라 리소스 그룹에 정책을 적용하면 해당 리소스 그룹의 모든 리소스에 해당 정책을 적용할 수 있습니다.

정책에 대해 이해하기 위한 두 가지 개념이 있습니다.

* 정책 정의 - 정책이 적용되는 시점 및 수행할 작업을 설명합니다.
* 정책 할당 - 정책 정의를 범위(구독 또는 리소스 그룹)에 적용합니다.

이 항목은 정책 정의에 중점을 둡니다. 정책 할당에 대한 정보는 [정책 할당 및 관리](resource-manager-policy-create-assign.md)를 참조하세요.

Azure에서는 일부 기본 제공 정책 정의을 제공하여 정의해야 하는 정책의 수를 줄일 수 있습니다. 기본 제공 정책이 시나리오에서 작동하는 경우 해당 정의를 범위에 할당할 때 사용합니다.

리소스(PUT 및 PATCH 작업)를 만들고 업데이트할 때 정책이 평가됩니다.

> [!NOTE]
> 현재 정책은 태그, 종류 및 위치를 지원하지 않는 리소스 종류(예: Microsoft.Resources/deployments)를 평가하지 않습니다. 이 지원은 나중에 추가됩니다. 이전 버전과의 호환성 문제를 방지하기 위해 정책을 작성할 때 유형을 명시적으로 지정해야 합니다. 예를 들어 형식을 지정하지 않은 태그 정책이 모든 형식에 적용됩니다. 여기서 태그를 지원하지 않는 중첩된 리소스가 있고 배포 리소스 형식을 정책 평가에 추가한 경우에는 템플릿 배포에 실패할 수 있습니다. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>RBAC(역할 기반 액세스 제어)와 어떻게 다르나요?
정책 및 RBAC(역할 기반 액세스 제어) 간에 몇 가지 차이점이 있습니다. RBAC는 다른 범위에 있는 **사용자** 작업에 중점을 둡니다. 예를 들어 사용자가 원하는 범위에서 리소스 그룹에 대한 참가자 역할에 추가됩니다. 따라서 사용자는 해당 리소스 그룹을 변경할 수 있습니다. 정책은 배포하는 동안 **리소스** 속성에 중점을 둡니다. 예를 들어 정책을 통해 프로비전할 수 있는 리소스 종류를 제어하거나 리소스를 프로비전할 수 있는 위치를 제한할 수 있습니다. RBAC와는 달리 정책은 기본적으로 허용 및 명시적 거부 시스템입니다. 

사용자는 RBAC를 통해 인증되어야 정책을 사용할 수 있습니다. 구체적으로 사용자 계정에는 다음 권한이 필요합니다.

* 정책을 정의할 수 있는 `Microsoft.Authorization/policydefinitions/write` 사용 권한
* 정책을 할당할 수 있는 `Microsoft.Authorization/policyassignments/write` 사용 권한 

이러한 사용 권한은 **참가자** 역할에 포함되지 않습니다.

## <a name="policy-definition-structure"></a>정책 정의 구조
JSON을 사용하여 정책 정의를 만듭니다. 정책 정의에는 다음 요소가 포함됩니다.

* 매개 변수
* 표시 이름
* description
* 정책 규칙
  * 논리 평가
  * 영향

다음 예제에서는 리소스가 배포되는 위치를 제한하는 정책을 보여줍니다.

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>매개 변수
매개 변수의 사용은 정책 정의의 수를 줄여 정책 관리를 간소화하는 데 도움이 됩니다. 리소스 속성에 대한 정책을 정의하고(예: 리소스를 배포할 수 있는 위치 제한) 정의에 매개 변수를 포함합니다. 그런 다음 정책을 할당할 때 다른 값(예: 구독에 한 가지 일련의 위치 지정)을 전달하여 다양한 시나리오에 대한 정책 정의를 다시 사용할 수 있습니다.

정책 정의 만들 때 매개 변수를 선언합니다.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

매개 변수의 형식은 문자열 또는 배열이 될 수 있습니다. 메타데이터 속성은 Azure 포털과 같은 도구에 사용되어 사용자 친화적 정보를 표시합니다. 

정책 규칙에서 다음 구문을 사용하여 매개 변수를 참조할 수 있습니다. 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>표시 이름 및 설명

**displayName** 및 **설명**을 사용하여 정책 정의를 식별하고 사용하는 시기에 대한 컨텍스트를 제공합니다.

## <a name="policy-rule"></a>정책 규칙

정책 규칙은 **If** 및 **Then** 블록으로 이루어집니다. **If** 블록에서 정책이 적용되는 시점을 지정하는 하나 이상의 조건을 정의합니다. 이러한 조건에 논리 연산자를 적용하여 정책에 대한 시나리오를 정확하게 정의할 수 있습니다. **Then** 블록에서 **If** 조건이 충족된 경우에 발생하는 효과를 정의합니다.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>논리 연산자
지원되는 논리 연산자는 다음과 같습니다.

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

**not** 구문은 조건의 결과를 반전시킵니다. **allOf** 구문(논리 **And** 작업과 비슷함)은 모든 조건이 true여야 합니다. **anyOf** 구문(논리 **Or** 작업과 비슷함)은 하나 이상의 조건이 true여야 합니다.

논리 연산자를 중첩할 수 있습니다. 다음 예제에서는 **And** 작업 내에 중첩된 **Not** 작업을 표시합니다. 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>조건
조건은 **field**에서 특정 기준을 충족하는지를 평가합니다. 지원되는 조건은 다음과 같습니다.

* `"equals": "value"`
* `"like": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

**like** 조건을 사용하는 경우 값에 와일드카드(*)를 제공할 수 있습니다.

### <a name="fields"></a>필드
조건은 필드를 사용하여 구성됩니다. 필드는 리소스의 상태를 설명하는 데 사용되는 리소스 요청 페이로드의 속성을 나타냅니다.  

다음 필드가 지원됩니다.

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* 속성 별칭

리소스 유형에 대한 특정 속성에 액세스하려면 속성 별칭을 사용합니다. 지원되는 별칭은 다음과 같습니다.

* Microsoft.CDN/profiles/sku.name
* Microsoft.Compute/virtualMachines/imageOffer
* Microsoft.Compute/virtualMachines/imagePublisher
* Microsoft.Compute/virtualMachines/sku.name
* Microsoft.Compute/virtualMachines/imageSku 
* Microsoft.Compute/virtualMachines/imageVersion
* Microsoft.SQL/servers/databases/edition
* Microsoft.SQL/servers/databases/elasticPoolName
* Microsoft.SQL/servers/databases/requestedServiceObjectiveId
* Microsoft.SQL/servers/databases/requestedServiceObjectiveName
* Microsoft.SQL/servers/elasticPools/dtu
* Microsoft.SQL/servers/elasticPools/edition
* Microsoft.SQL/servers/version
* Microsoft.Storage/storageAccounts/accessTier
* Microsoft.Storage/storageAccounts/enableBlobEncryption
* Microsoft.Storage/storageAccounts/sku.name
* Microsoft.Web/serverFarms/sku.name

### <a name="effect"></a>결과
정책은 `deny`, `audit` 및 `append`이라는 세 가지 종류의 효과를 지원합니다. 

* **거부**는 감사 로그에 이벤트를 생성하고 요청을 실패합니다.
* **감사**는 감사 로그에 경고 이벤트를 생성하지만 요청을 실패하지는 않습니다.
* **추가**는 정의된 필드 집합을 요청에 추가합니다. 

**append**의 경우 아래와 같이 details(세부 정보)를 제공해야 합니다.

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

값은 문자열 또는 JSON 형식의 개체일 수 있습니다. 

## <a name="policy-examples"></a>정책 예제

다음 항목에는 정책 예제가 포함됩니다.

* 태그 정책의 예제는 [태그에 리소스 정책 적용](resource-manager-policy-tags.md)을 참조하세요.
* 저장소 정책의 예제는 [저장소 계정에 리소스 정책 적용](resource-manager-policy-storage.md)을 참조하세요.
* 가상 컴퓨터 정책의 예제는 [Linux VM에 리소스 정책 적용](../virtual-machines/virtual-machines-linux-policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 및 [Windows VM에 리소스 정책 적용](../virtual-machines/virtual-machines-windows-policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)을 참조하세요.

### <a name="allowed-resource-locations"></a>허용된 리소스 위치
허용된 위치를 지정하려면 [정책 정의 구조](#policy-definition-structure) 섹션에서 예제를 참조하세요. 이 정책 정의를 할당하려면 리소스 ID `/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c`로 기본 제공 정책을 사용합니다.

### <a name="not-allowed-resource-locations"></a>허용되지 않은 리소스 위치
허용되지 않은 위치를 지정하려면 다음 정책 정의를 사용합니다.

```json
{
  "properties": {
    "parameters": {
      "notAllowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that are not allowed when deploying resources",
          "strongType": "location",
          "displayName": "Not allowed locations"
        }
      }
    },
    "displayName": "Not allowed locations",
    "description": "This policy enables you to block locations that your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "field": "location",
        "in": "[parameters('notAllowedLocations')]"
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

### <a name="allowed-resource-types"></a>허용되는 리소스 유형
다음 예제에서는 Microsoft.Resources, Microsoft.Compute, Microsoft.Storage, Microsoft.Network 리소스 형식에 대한 배포가 가능한 정책을 보여 줍니다. 다른 모든 정책은 거부됩니다.

```json
{
  "if": {
    "not": {
      "anyOf": [
        {
          "field": "type",
          "like": "Microsoft.Resources/*"
        },
        {
          "field": "type",
          "like": "Microsoft.Compute/*"
        },
        {
          "field": "type",
          "like": "Microsoft.Storage/*"
        },
        {
          "field": "type",
          "like": "Microsoft.Network/*"
        }
      ]
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

### <a name="set-naming-convention"></a>명명 규칙 설정
아래 예제에서는 **like** 조건으로 지원되는 와일드 카드의 사용을 보여 줍니다. 이 조건은 앞에서 언급된 패턴(namePrefix\*nameSuffix)과 일치하는 이름이면 요청을 거부한다는 것을 나타냅니다.

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>다음 단계
* 정책 규칙을 정의한 후에 범위에 할당합니다. 정책 할당에 대한 정보는 [정책 할당 및 관리](resource-manager-policy-create-assign.md)를 참조하세요.
* 엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.
* 정책 스키마는 [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)에 게시되어 있습니다. 




<!--HONumber=Feb17_HO3-->


