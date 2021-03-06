---
title: "Azure App Service의 고밀도 호스팅 | Microsoft Docs"
description: "Azure App Service의 고밀도 호스팅"
author: btardif
manager: wpickett
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/11/2017
ms.author: byvinyal
translationtype: Human Translation
ms.sourcegitcommit: 0c2677b388f7a88ff88715a05212633565393cc2
ms.openlocfilehash: 2d5d1d5123ca718b2e7dcdf426b77f91969dc9dc


---
# <a name="high-density-hosting-on-azure-app-service"></a>Azure App Service의 고밀도 호스팅
App Service를 사용할 경우 응용 프로그램은&2;가지 개념에 의해 할당된 용량에서 분리됩니다.

* **응용 프로그램:** 앱 및 해당 런타임 구성을 나타냅니다. 예를 들어 런타임이 로드해야 하는 .NET 버전, 앱 설정 등을 포함합니다.
* **앱 서비스 계획:** 응용 프로그램의 용량, 사용 가능한 기능 집합 및 거주지에 대한 특징을 정의합니다. 예를 들어 특징은 큰(4코어) 컴퓨터, 인스턴스&4;개, 미국 동부에서 프리미엄 기능일 수 있습니다.

앱이 앱 서비스 계획에 항상 연결되어 있지만 앱 서비스 계획은 하나 이상의 앱에 대한 용량을 제공할 수 있습니다.

결과적으로 플랫폼에서는 App Service 계획을 공유하여 단일 앱을 격리하거나 여러 앱 공유 리소스를 가지도록 유연성을 제공합니다.

그러나 여러 앱이 앱 서비스 계획을 공유하는 경우 해당 앱의 인스턴스는 해당 앱 서비스 계획의 모든 인스턴스에서 실행됩니다.

## <a name="per-app-scaling"></a>앱 크기 조정당
*앱 크기 조정당* 은 앱 서비스 계획 수준에서 사용할 수 있는 기능이며 응용 프로그램마다 사용됩니다.

앱 크기 조정당은 호스팅하는 앱 서비스 계획에서 독립적으로 앱을 크기 조정합니다. 이러한 방식으로 앱 서비스 계획은 10개의 인스턴스를 제공하도록 구성될 수 있지만 앱은 그 중의 5개만 크기를 조정하도록 설정될 수 있습니다.

   >[!NOTE]
   >앱 크기 조정당은 **Premium** SKU App Service 계획에 대해서만 사용 가능합니다.
   >

### <a name="per-app-scaling-using-powershell"></a>PowerShell을 사용하여 앱 크기 조정당

```-perSiteScaling $true``` 속성에서 ```New-AzureRmAppServicePlan``` commandlet으로 전달하여 *앱 크기 조정당*으로 구성된 새 계획을 만들 수 있습니다.

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

기존 App Service 계획을 업데이트하여 이 기능을 사용하려는 경우: 

- 대상 계획 가져오기```Get-AzureRmAppServicePlan```
- 속성 로컬 수정```$newASP.PerSiteScaling = $true```
- 변경 내용을 Azure에 다시 게시```Set-AzureRmAppServicePlan``` 

```
    # Get the new App Service Plan and modify the "PerSiteScaling" property.
    $newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
    $newASP

    #Modify the local copy to use "PerSiteScaling" property.
    $newASP.PerSiteScaling = $true
    $newASP
    
    #Post updated app service plan back to azure
    Set-AzureRmAppServicePlan $newASP
```

구성된 계획이 있으면 각 앱에 대한 최대 인스턴스 수를 설정할 수 있습니다.

아래 예제에서 이 앱은 기본 앱 서비스 계획이 규모를 확장하는 인스턴스 수와 상관없이 최대&2;개 인스턴스로 제한됩니다.

```
    # Get the app we want to configure to use "PerSiteScaling"
    $newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
    # Modify the NumberOfWorkers setting to the desired value.
    $newapp.SiteConfig.NumberOfWorkers = 2
    
    # Post updated app back to azure
    Set-AzureRmWebApp $newapp
```

### <a name="per-app-scaling-using-azure-resource-manager"></a>Azure Resource Manager를 사용하여 앱 크기 조정당

다음 *Azure Resource Manager 템플릿*이 만듭니다.

- 10개 인스턴스로 규모를 확장하는 App Service 계획
- 최대&5;개 인스턴스로 확장하도록 구성된 앱

App Service 계획은 **PerSiteScaling** 속성을 true(```"perSiteScaling": true```)로 설정합니다. 앱은 **작업자 수**를 5(```"properties": { "numberOfWorkers": "5" }```)로 설정합니다.

```
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters":{
            "appServicePlanName": { "type": "string" },
            "appName": { "type": "string" }
         },
        "resources": [
        {
            "comments": "App Service Plan with per site perSiteScaling = true",
            "type": "Microsoft.Web/serverFarms",
            "sku": {
                "name": "P1",
                "tier": "Premium",
                "size": "P1",
                "family": "P",
                "capacity": 10
                },
            "name": "[parameters('appServicePlanName')]",
            "apiVersion": "2015-08-01",
            "location": "West US",
            "properties": {
                "name": "[parameters('appServicePlanName')]",
                "perSiteScaling": true
            }
        },
        {
            "type": "Microsoft.Web/sites",
            "name": "[parameters('appName')]",
            "apiVersion": "2015-08-01-preview",
            "location": "West US",
            "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
            "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
            "resources": [ {
                    "comments": "",
                    "type": "config",
                    "name": "web",
                    "apiVersion": "2015-08-01",
                    "location": "West US",
                    "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                    "properties": { "numberOfWorkers": "5" }
             } ]
         }]
    }
```

## <a name="recommended-configuration-for-high-density-hosting"></a>고밀도 호스팅에 대한 권장된 구성
앱 크기 조정당은 공용 Azure 지역 및 앱 서비스 환경 모두에서 사용할 수 있는 기능입니다. 그러나 권장되는 전략은 해당 고급 기능 및 큰 용량의 풀을 활용하도록 앱 서비스 환경을 사용하는 것입니다.  

앱에 대해 고밀도 호스팅을 구성하려면 이 단계를 수행합니다.

1. App Service 환경을 구성하고 고밀도 호스팅 시나리오에 전용으로 사용되는 작업자 풀을 선택합니다.
2. 단일 앱 서비스 계획을 만들고 확장하여 작업자 풀에서 모든 사용 가능한 용량을 사용합니다.
3. App Service 계획에서 PerSiteScaling 플래그를 true로 설정합니다.
4. 새 앱이 만들어지고 **1**로 설정된 **numberOfWorkers** 속성이 있는 해당 App Service 계획에 할당됩니다. 이 구성을 사용하면 작업자 풀에서 고밀도가 가능해 집니다.
5. 작업자 수는 앱마다 독립적으로 구성되어 필요에 따라 추가 리소스를 부여할 수 있습니다. 예를 들어, 높은 사용량 앱은 **numberOfWorkers**를 **3**으로 설정하여 앱에 대한 처리 용량을 늘리는 반면 낮은 사용량 앱은 **numberOfWorkers**를 **1**로 설정합니다.




<!--HONumber=Jan17_HO2-->


