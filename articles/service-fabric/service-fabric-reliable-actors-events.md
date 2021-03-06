---
title: "행위자 기반 Azure 마이크로 서비스의 이벤트 | Microsoft Docs"
description: "서비스 패브릭 Reliable Actors의 이벤트에 대해 소개합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/30/2016
ms.author: amanbha
translationtype: Human Translation
ms.sourcegitcommit: 7033955fa9c18b2fa1a28d488ad5268d598de287
ms.openlocfilehash: 92df9505416c5b4326f007dbf4b920f2c7ec3bd8


---
# <a name="actor-events"></a>행위자 이벤트
행위자 이벤트는 행위자에서 클라이언트로 최상의 알림을 보낼 수 있는 방법을 제공합니다. 행위자 이벤트는 행위자-클라이언트 간 통신을 위해 디자인되었으며 행위자-행위자 간 통신에는 사용하지 않아야 합니다.

다음 코드 조각에서는 응용 프로그램에서 행위자 이벤트를 사용하는 방법을 보여 줍니다.

행위자가 게시한 이벤트를 설명하는 인터페이스를 정의합니다. 이 인터페이스는 `IActorEvents` 인터페이스에서 파생되어야 합니다. 메서드의 인수는 [데이터 계약 직렬화 가능](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)해야 합니다. 이벤트 알림은 단방향으로 최대한 제공되므로 메서드는 void를 반환해야 합니다.

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```

행위자 인터페이스에서 행위자에 의해 게시된 이벤트를 선언합니다.

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```

클라이언트쪽에서는 이벤트 처리기를 구현합니다.

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

클라이언트에서 이벤트를 게시하고 이벤트를 구독하는 행위자에 대한 프록시를 만듭니다.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

장애 조치 발생 시 행위자는 서로 다른 프로세스 또는 노드로 장애 조치(failover)가 될 수 있습니다. 행위자 프록시는 활성 구독을 관리하고 자동으로 재구독합니다. `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API를 통해 재구독 간격을 제어할 수 있습니다. 구독을 취소하려면 `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API를 사용합니다.

행위자에서 이벤트 발생 시 해당 이벤트를 게시하기만 하면 됩니다. 이벤트에 구독자가 여럿 있는 경우는 행위자 런타임에서 구독자들에게 알림을 보냅니다.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```

## <a name="next-steps"></a>다음 단계
* [행위자 다시 표시](service-fabric-reliable-actors-reentrancy.md)
* [행위자 진단 및 성능 모니터링](service-fabric-reliable-actors-diagnostics.md)
* [행위자 API 참조 설명서](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [샘플 코드](https://github.com/Azure/servicefabric-samples)




<!--HONumber=Jan17_HO4-->


