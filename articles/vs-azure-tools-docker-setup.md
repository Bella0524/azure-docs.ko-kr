---
title: "VirtualBox 및 Docker 호스트 구성 | Microsoft Docs"
description: "Docker 컴퓨터 및 VirtualBox를 사용하여 기본 Docker 인스턴스를 구성하는 단계별 지침입니다."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
translationtype: Human Translation
ms.sourcegitcommit: dcda8b30adde930ab373a087d6955b900365c4cc
ms.openlocfilehash: e9465afb560a73d74f853c19094b3ee75b8c470c


---
# <a name="configure-a-docker-host-with-virtualbox"></a>VirtualBox 및 Docker 호스트 구성
## <a name="overview"></a>개요
이 문서에서는 Docker 컴퓨터 및 VirtualBox를 사용하여 기본 Docker 인스턴스를 구성하는 과정을 안내합니다. [Windows 베타용 Docker](http://beta.docker.com/)를 사용하는 경우 이 구성은 필요하지 않습니다.

## <a name="prerequisites"></a>필수 조건
다음과 같은 도구를 설치해야 합니다.

* [Docker 도구 상자](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a>Windows PowerShell과 함께 Docker 클라이언트 구성
Docker 클라이언트를 구성하려면 단순히 Windows PowerShell을 열고 다음 단계를 수행합니다.

1. 기본 docker 호스트 인스턴스를 만듭니다.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. 기본 인스턴스가 구성되어 실행 중인지 확인합니다. ('기본'이라는 인스턴스가 실행되는 것이 표시됩니다.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls output][0]
3. 기본값을 현재 호스트로 설정하고 셸을 구성합니다.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. 활성 Docker 컨테이너를 표시합니다. 목록이 비어 있어야 합니다.
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps output][1]

> [!NOTE]
> 개발 컴퓨터를 다시 부팅할 때마다 로컬 Docker 호스트를 다시 시작해야 합니다.
> 이렇게 하려면 명령 프롬프트에서 다음 명령을 실행합니다. `docker-machine start default`
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png



<!--HONumber=Feb17_HO3-->


