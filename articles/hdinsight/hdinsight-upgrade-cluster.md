---
title: "Windows 기반 HDInsight에서 Linux 기반 HDInsight로 마이그레이션 -Azure | Microsoft Docs"
description: "Windows 기반 HDInsight 클러스터에서 Linux 기반 HDInsight 클러스터로 마이그레이션하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: bhanupr
editor: bhanupr
ms.assetid: 
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/11/2017
ms.author: bhanupr
translationtype: Human Translation
ms.sourcegitcommit: 8c59375290e410c34ba25d4e5d8e8f9f8de0cafe
ms.openlocfilehash: ceb5f5c639633d7118a057927b236b51b54f8fa7


---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a>HDInsight 클러스터를 최신 버전으로 업그레이드
최신 HDInsight 기능을 활용하려면 HDInsight 클러스터를 최신 버전으로 업그레이드하는 것이 좋습니다. 아래 지침에 따라 HDInsight 클러스터 버전을 업그레이드합니다.

> [!NOTE]
> HDInsight 클러스터 버전 3.2 및 3.3은 곧 사용이 중단될 예정입니다. 지원되는 HDInsight 버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.
>
>

## <a name="upgrade-tasks"></a>업그레이드 작업
HDInsight 클러스터를 업그레이드하는 워크플로는 다음과 같습니다.

![업그레이드 워크플로 다이어그램](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. HDInsight 클러스터를 업그레이드할 때 필요할 수 있는 변경 내용을 이해하려면 이 문서의 각 섹션을 읽어보세요.
2. 클러스터를 테스트/품질 보증 환경으로 만듭니다. 클러스터를 만드는 방법에 대한 자세한 내용은 [Linux 기반 HDInsight 클러스터를 만드는 방법 알아보기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.
3. 기존 작업, 데이터 원본 및 싱크를 새 환경으로 복사합니다. 자세한 내용은 [테스트 환경에 데이터 복사](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment)를 참조하세요.
4. 작업이 새 클러스터에서 예상대로 작동하는지 확인하려면 유효성 검사 테스트를 수행합니다.


예상대로 작동하는 것이 확인되면 마이그레이션을 위해 가동 중지 시간을 예약합니다. 이 가동 중지 시간 동안 다음 작업을 수행합니다.

1.  클러스터 노드에 로컬로 저장된 모든 임시 데이터를 백업합니다. 예를 들어 헤드 노드에 직접 저장된 데이터가 있는 경우입니다.
2.  기존 클러스터를 삭제합니다.
3.  이전 클러스터에서 사용된 것과 동일한 기본 데이터 저장소를 사용하여 최신(또는 지원되는) HDI 버전과 동일한 VNET 서브넷에서 클러스터를 만듭니다. 이렇게 하면 새 클러스터에서 기존의 프로덕션 데이터에 대해 작업을 계속할 수 있습니다.
4.  백업한 모든 임시 데이터를 가져옵니다.
5.  새 클러스터를 사용하여 작업을 시작하거나 계속 처리합니다.

## <a name="next-steps"></a>다음 단계
* [Linux 기반 HDInsight 클러스터를 만드는 방법 알아보기](hdinsight-hadoop-provision-linux-clusters.md)
* [Windows 클라이언트에서 SSH를 사용하여 Linux 기반 클러스터에 연결](hdinsight-hadoop-linux-use-ssh-windows.md)
* [Linux, Unix 또는 Mac 클라이언트에서 SSH를 사용하여 Linux 기반 클러스터에 연결](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Ambari를 사용하여 Linux 기반 클러스터 관리](hdinsight-hadoop-manage-ambari.md)




<!--HONumber=Feb17_HO1-->


