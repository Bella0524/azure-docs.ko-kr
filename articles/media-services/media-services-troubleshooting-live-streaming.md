---
title: "라이브 스트리밍 문제 해결 가이드 | Microsoft Docs"
description: "이 토픽에서는 라이브 스트리밍 문제를 해결하는 방법에 대한 제안을 제공합니다."
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/12/2016
ms.author: juliako
translationtype: Human Translation
ms.sourcegitcommit: 0c77ee0f612c1cbef551a129a22cf3f125e6f29d
ms.openlocfilehash: 69fa0a7802ca39f86ada0af47b7a99e56436f973


---
# <a name="troubleshooting-guide-for-live-streaming"></a>라이브 스트리밍 문제 해결 가이드
이 토픽에서는 일부 라이브 스트리밍 문제를 해결하는 방법에 대한 제안을 제공합니다.

## <a name="issues-related-to-on-premises-encoders"></a>온-프레미스 인코더와 관련된 문제
이 섹션에서는 라이브 인코딩에 사용할 수 있는 AMS 채널에 단일 비트 전송률 스트림을 보내도록 구성된 온-프레미스 인코더와 관련된 문제를 해결하는 방법에 대한 제안을 제공합니다.

### <a name="problem-would-like-to-see-logs"></a>문제: 로그를 참조하려고 합니다.
* **잠재적인 문제**: 문제를 디버그할 때 도움이 될 만한 인코더 로그를 찾을 수 없습니다.
  
  * **Telestream Wirecast**: 보통 C:\Users\{username}\AppData\Roaming\Wirecast\에서 로그를 찾을 수 있습니다. 
  * **Elemental Live**: 관리 포털에서 로그에 대한 링크를 찾을 수 있습니다. **통계**, **로그**를 차례로 클릭합니다. **로그 파일** 페이지에 모든 LiveEvent 항목에 대한 로그의 목록이 표시됩니다. 현재 세션과 일치하는 로그를 선택합니다. 
  * **Flash Media Live Encoder**: **Encoding 로그** 탭으로 이동하여 **로그 디렉터리...**를 찾을 수 있습니다.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>문제: 점진적 스트림을 출력하기 위한 옵션이 없습니다.
* **잠재적인 문제**: 사용 중인 인코더가 자동으로 디인터레이스하지 않습니다. 
  
    **문제해결 단계**: 인코더 인터페이스 내에서 디인터레이스 옵션을 찾아보십시오. 디인터레이스를 사용하도록 설정한 후 다시 점진적 출력 설정을 확인합니다. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a>문제: 여러 인코더 출력 설정을 시도했는데 여전히 연결할 수 없습니다.
* **잠재적인 문제**: Azure 인코딩 채널이 올바르게 다시 설정되지 않았습니다. 
  
    **문제 해결 단계**: 인코더가 더 이상 AMS에 푸시하지 않는지 확인하고 채널을 중지한 다음 다시 설정합니다. 다시 실행한 후 새 설정으로 인코더를 연결해 보십시오. 여전히 문제가 해결되지 않으면 새 채널을 전체적으로 다시 만들어 보십시오. 때에 따라 여러 번 시도가 실패한 후 채널이 손상될 수 있습니다.  
* **잠재적인 문제**: GOP 크기 또는 키프레임 설정이 최적의 상태가 아닙니다. 
  
    **문제 해결 단계**: 권장 GOP 크기 또는 키프레임 간격은 2초입니다. 일부 인코더는 이 설정을 프레임 단위로 계산하는 반면, 다른 인코더는 초를 사용합니다. 예: 30fps를 출력할 때 GOP 크기는 60 프레임이며, 이는 2초와 같습니다.  
* **잠재적인 문제**: 닫힌 포트가 스트림을 차단하고 있습니다. 
  
    **문제 해결 단계**: RTMP 통해 스트리밍할 때 방화벽 및/또는 프록시 설정을 점검하여 아웃바운드 포트 1935 및 1936이 열려 있는지 확인합니다. RTP 스트리밍을 사용하는 경우 아웃바운드 포트 2010이 열려 있는지 확인합니다. 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a>문제: RTP 프로토콜을 사용하여 인코더를 스트림으로 구성하면 호스트 이름을 입력할 장소가 없습니다.
* **잠재적인 문제**: 많은 인코더는 호스트 이름에 허용되지 않으며 IP 주소를 획득해야 합니다.  
  
    **문제 해결 단계**: IP 주소를 찾으려면 모든 컴퓨터에서 명령 프롬프트를 엽니다. Windows에서 이 작업을 수행하려면 실행 시작 관리자(WIN + R)를 열고 "cmd"를 입력하여 엽니다.  
  
    명령 프롬프트를 연 후에 "Ping [AMS 호스트 이름]"을 입력합니다. 
  
    호스트 이름은 다음 예제에서 강조한 것처럼 Azure Ingest URL에서 포트 번호를 생략하여 파생시킬 수 있습니다. 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> 문제 해결 단계를 수행한 후에도 여전히 성공적으로 스트리밍되지 않으면 Azure Portal을 사용하여 지원 티켓을 제출하세요.
> 
> 

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]




<!--HONumber=Feb17_HO3-->


