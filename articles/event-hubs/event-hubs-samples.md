---
title: "Azure Event Hubs 샘플 | Microsoft Docs"
description: "Event Hubs 샘플"
services: event-hubs
documentationcenter: na
author: jtaubensee
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: jotaub;sethm
translationtype: Human Translation
ms.sourcegitcommit: 5b02054546ebf25766be6bb2837aebc502b67a67
ms.openlocfilehash: 9c50b7caefe06bceac8035a0d274e13a96547fea

---

# <a name="event-hubs-samples"></a>Event Hubs 샘플 

이 Event Hubs 샘플은 [Azure Event Hubs](/azure/event-hubs/)의 주요 기능을 보여 줍니다. 이 문서는 사용할 수 있는 샘플 각각을 링크를 사용하여 범주화하고 설명합니다.

이 문서가 작성되었을 때 Event Hubs 샘플은 다음 여러 위치에 배치되었습니다.

- [MSDN 개발자 코드 샘플](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs-dotnet/tree/master/samples)

다른 버전의 .NET Framework에 대한 자세한 내용은 [프레임워크 및 대상](/dotnet/articles/standard/frameworks)을 참조하세요.

시간이 지남에 따라 더 많은 샘플이 추가될 예정이므로 업데이트가 있는지 자주 확인하세요.

## <a name="net-standard"></a>.NET Standard

다음 샘플은 [.NET Standard 라이브러리](/dotnet/articles/standard/library)에 대해 [Event Hubs 클라이언트](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md)를 사용하여 이벤트를 송수신하는 방법을 보여 줍니다.

### <a name="send-events"></a>이벤트 전송 

[전송 시작](https://github.com/Azure/azure-event-hubs-dotnet/tree/master/samples/SampleSender) 샘플은 이벤트 허브로 이벤트를 전송하는 .NET Core 콘솔 응용 프로그램을 작성하는 방법을 보여 줍니다.

### <a name="receive-events"></a>이벤트 수신 

[이벤트 프로세서 호스트를 사용하여 수신 시작](https://github.com/Azure/azure-event-hubs-dotnet/tree/master/samples/SampleEphReceiver) 샘플은 [이벤트 프로세서 호스트](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)를 사용하여 이벤트 허브에서 메시지를 수신하는 .NET Core 콘솔 응용 프로그램입니다. 

## <a name="net-framework"></a>.NET Framework   

이러한 샘플은 [.NET Framework 라이브러리](https://msdn.microsoft.com/library/w0x726c2.aspx)를 대상으로 하는 Azure Event Hubs의 기타 다양한 기능을 보여 줍니다.
 
### <a name="notify-users-of-events-received"></a>수신된 이벤트를 사용자에게 알림

[AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) 샘플은 센서 또는 다른 시스템으로부터 받은 데이터를 사용자에게 알립니다.

### <a name="get-started-with-event-hubs"></a>이벤트 허브 시작 

[Event Hubs 시작](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) 샘플은 이벤트 허브 만들기, 이벤트 허브로 이벤트 전송, [이벤트 프로세서 호스트](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)를 사용하여 이벤트 소비 등, Event Hubs의 기본 기능을 보여 줍니다.

### <a name="scale-out-event-processing"></a>이벤트 처리 확장 

[이벤트 처리 확장](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) 샘플은 [이벤트 프로세서 호스트](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)를 사용하여 Event Hubs 스트림 사용 워크로드를 분산하는 방법을 보여 줍니다. 또한 이벤트 스트림을 관리하도록 **EventProcessor** 및 **EventProcessorFactory** 개체를 구현하는 방법도 보여 줍니다. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>SQL의 데이터를 이벤트 허브로 끌어오기

[SQL 데이터 끌어오기](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) 샘플은 SQL 테이블의 데이터를 끌어와 이벤트 허브에 푸시하여 다운스트림 분석 응용 프로그램에 대한 입력으로 사용하도록 하는 방법을 보여 줍니다.

### <a name="pull-web-data-into-an-event-hub"></a>웹 데이터를 이벤트 허브로 끌어오기 

[웹에서 데이터 가져오기](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) 샘플은 공용 피드의 데이터를 끌어와(예: 교통 부서의 트래픽 정보 피드) 이벤트 허브로 푸시하는 방법을 보여 줍니다.

## <a name="next-steps"></a>다음 단계

다음 링크에서 .NET Framework 버전에 대해 자세히 알아보세요.

- [프레임워크 및 대상](/dotnet/articles/standard/frameworks)
- [.NET Framework 4.6 및 4.5](https://msdn.microsoft.com/library/w0x726c2.aspx)

Event Hubs에 대한 자세한 내용은 다음 문서를 참조하세요.

- [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
- [이벤트 허브 만들기](event-hubs-create.md)
- [Event Hubs FAQ](event-hubs-faq.md)


<!--HONumber=Feb17_HO1-->


