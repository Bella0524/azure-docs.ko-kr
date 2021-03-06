---
title: "Azure CLI을 사용하여 HDInsight의 Windows 기반 Hadoop 클러스터 만들기"
description: "Azure CLI을 사용하여 Azure HDInsight에 Windows 기반 Hadoop 클러스터를 만드는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c766544c-c16f-4bfa-89d0-592325d24250
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: jgao
translationtype: Human Translation
ms.sourcegitcommit: a2b32f23381ed1f9912edf6432f029e51bdf1be4
ms.openlocfilehash: 393b7e44b21fe510e07b4048ddd3bdbcc31d90a9


---
# <a name="create-windows-based-hadoop-clusters-in-hdinsight-using-azure-cli"></a>Azure CLI을 사용하여 HDInsight의 Windows 기반 Hadoop 클러스터 만들기

[!INCLUDE [selector](../../includes/hdinsight-selector-create-clusters.md)]

Azure CLI을 사용하여 HDInsight에 Windows 기반 Hadoop 클러스터를 만드는 방법을 알아봅니다. 

> [!IMPORTANT]
> Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다. 자세한 내용은 [Windows에서 HDInsight 사용 중단](hdinsight-component-versioning.md#hdi-version-32-and-33-nearing-deprecation-date)을 참조하세요. 이 문서의 정보는 Windows 기반 HDInsight 클러스터에만 적용됩니다. Linux 기반 클러스터 생성에 대한 자세한 내용은 [Azure CLI를 사용하여 HDInsight에 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-cli.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건:
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

이 문서의 지침을 시작하기 전에 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* **Azure CLI**.
  
[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)] 

### <a name="access-control-requirements"></a>액세스 제어 요구 사항
[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="connect-to-azure"></a>Azure에 연결
다음 명령을 사용하여 Azure에 연결합니다.

    azure login

회사 또는 학교 계정을 사용하여 인증하는 방법에 대한 자세한 내용은 [Azure CLI에서 Azure 구독에 연결](../xplat-cli-connect.md)을 참조하세요.

Azure Resource Manager 모드로 전환하려면 다음 명령을 사용합니다.

    azure config mode arm

도움말을 보려면 **-h** 스위치를 사용합니다.  예:

    azure hdinsight cluster create -h

## <a name="create-clusters"></a>클러스터 만들기
HDInsight 클러스터를 만들려면 리소스 관리 그룹 및 Azure Blob Storage 계정이 있어야 합니다. HDInsight 클러스터를 만들려면 다음을 지정해야 합니다.

* **Azure 리소스 그룹**: Azure 리소스 그룹 내에서 Data Lake Analytics 계정을 만들어야 합니다. Azure 리소스 관리자를 사용하면 그룹으로 응용 프로그램에서 리소스와 함께 사용할 수 있습니다. 응용 프로그램에 대한 모든 리소스의 배포, 업데이트 또는 삭제를 조정된 단일 작업으로 수행할 수 있습니다.
  
    구독 중인 리소스 그룹을 나열하려면
  
        azure group list
  
    새 리소스 그룹을 만들려면 다음을 수행합니다.
  
        azure group create -n "<Resource Group Name>" -l "<Azure Location>"
* **HDInsight 클러스터 이름**
* **위치**: HDInsight 클러스터를 지원하는 Azure 데이터 센터 중 하나입니다. 지원되는 위치에 대한 목록은 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.
* **기본 저장소 계정**- HDInsight는 Azure Blob 저장소 컨테이너를 기본 파일 시스템으로 사용합니다. HDInsight 클러스터를 만들려면 먼저 Azure 저장소 계정이 필요합니다.
  
    새 Azure 저장소 계정을 만들려면:
  
        azure storage account create "<Azure Storage Account Name>" -g "<Resource Group Name>" -l "<Azure Location>" --type LRS
  
  > [!NOTE]
  > 저장소 계정은 데이터 센터에 HDInsight와 함께 배치되어야 합니다.
  > ZRS는 테이블을 지원하지 않으므로 저장소 계정 유형은 ZRS일 수 없습니다.
  > 
  > 
  
    Azure Portal을 사용하여 Azure Storage 계정을 만드는 방법에 대한 자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제][azure-create-storageaccount]를 참조하세요.
  
    저장소 계정이 이미 있지만 계정 이름과 계정 키를 모르는 경우 다음 명령을 사용하여 정보를 검색할 수 있습니다.
  
        -- Lists Storage accounts
        azure storage account list
        -- Shows a Storage account
        azure storage account show "<Storage Account Name>"
        -- Lists the keys for a Storage account
        azure storage account keys list "<Storage Account Name>" -g "<Resource Group Name>"
  
    Azure Portal을 사용하여 정보를 얻는 방법에 대한 자세한 내용은 [Azure Storage 계정 정보](../storage/storage-create-storage-account.md#manage-your-storage-account)의 "저장소 계정 관리" 섹션을 참조하세요.
* **(선택 사항) 기본 Blob 컨테이너**: 컨테이너가 없는 경우 **azure hdinsight cluster create** 명령으로 컨테이너를 만듭니다. 미리 컨테이너를 만들도록 선택하는 경우 다음 명령을 사용할 수 있습니다.
  
    azure storage container create --account-name "<Storage Account Name>" --account-key <Storage Account Key> [ContainerName]

저장소 계정이 준비되면 클러스터를 만들 준비가 된 것입니다.

    azure hdinsight cluster create -g <Resource Group Name> -c <HDInsight Cluster Name> -l <Location> --osType <Windows | Linux> --version <Cluster Version> --clusterType <Hadoop | HBase | Spark | Storm> --workerNodeCount 2 --headNodeSize Large --workerNodeSize Large --defaultStorageAccountName <Azure Storage Account Name>.blob.core.windows.net --defaultStorageAccountKey "<Default Storage Account Key>" --defaultStorageContainer <Default Blob Storage Container> --userName admin --password "<HTTP User Password>" --rdpUserName <RDP Username> --rdpPassword "<RDP User Password" --rdpAccessExpiry "03/01/2016"


## <a name="create-clusters-using-configuration-files"></a>구성 파일을 사용하여 클러스터 만들기
일반적으로 HDInsight 클러스터를 만들고 해당 클러스터에서 작업을 실행한 후에 비용을 줄이기 위해 클러스터를 삭제합니다. 명령줄 인터페이스에는 클러스터를 만들 때마다 다시 사용할 수 있도록 구성을 파일에 저장하는 옵션이 있습니다.  

    azure hdinsight config create [options ] <Config File Path> <overwirte>
    azure hdinsight config add-config-values [options] <Config File Path>
    azure hdinsight config add-script-action [options] <Config File Path>

예: 클러스터를 만들 때 실행할 스크립트 동작을 포함하는 구성 파일을 만듭니다.

    azure hdinsight config create "C:\myFiles\configFile.config"
    azure hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <Script Action URI> --name myScriptAction --parameters "-param value"
    azure hdinsight cluster create --configurationPath "C:\myFiles\configFile.config"

## <a name="create-clusters-with-script-action"></a>스크립트 동작을 사용하여 클러스터 만들기
클러스터를 만들 때 실행할 스크립트 동작을 포함하는 구성 파일을 만듭니다.

    azure hdinsight config create "C:\myFiles\configFile.config"
    azure hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

스크립트 동작을 사용하여 클러스터 만들기

    azure hdinsight cluster create -g myarmgroup01 -l westus -y Windows --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01


일반 스크립트 동작에 대한 자세한 내용은 [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정(Linux)](hdinsight-hadoop-customize-cluster.md)을 참조하세요.

## <a name="create-clusters-using-resource-manager-templates"></a>Resource Manager 템플릿을 사용하여 클러스터 만들기
CLI에서 Azure Resource Manager 템플릿을 호출하여 클러스터를 만들 수 있습니다. [Azure CLI를 사용하여 배포](hdinsight-hadoop-create-windows-clusters-arm-templates.md#deploy-with-azure-cli)를 참조하세요.

## <a name="see-also"></a>참고 항목
* [Azure HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md) - HDInsight 클러스터를 시작하는 방법을 알아봅니다.
* [프로그래밍 방식으로 Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md) - 프로그래밍 방식으로 작업을 HDInsight에 제출하는 방법을 알아봅니다.
* [Azure CLI를 사용하여 HDInsight의 Hadoop 클러스터 관리](hdinsight-administer-use-command-line.md)
* [Azure 서비스 관리에서 Mac, Linux 및 Windows용 Azure CLI 사용](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)




<!--HONumber=Feb17_HO1-->


