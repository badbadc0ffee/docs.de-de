---
title: RPC-GrpC-Typen für WCF-Entwickler
description: Eine Überprüfung der von WCF unterstützten Remote Prozedur Aufrufe und ihrer Entsprechungen in GrpC
ms.date: 09/02/2019
ms.openlocfilehash: 58f097bac61395e6810155e8ae9a6bbf2219ec5e
ms.sourcegitcommit: f38e527623883b92010cf4760246203073e12898
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2020
ms.locfileid: "77503445"
---
# <a name="types-of-rpc"></a>RPC-Typen

Als Windows Communication Foundation (WCF)-Entwickler haben Sie wahrscheinlich die folgenden Typen von Remote Prozedur Aufruf (RPC) verwendet:

- Anforderung/Antwort
- Gelegene
  - Unidirektionaler Duplex mit Sitzung
  - Vollduplex Duplex mit Sitzung
- Unidirektional

Es ist möglich, diese RPC-Typen den vorhandenen GrpC-Konzepten relativ natürlich zuzuordnen. In diesem Kapitel werden die einzelnen Bereiche im einzelnen erläutert. In [Kapitel 5](migrate-wcf-to-grpc.md) werden ähnliche Beispiele ausführlicher erläutert.

| WCF | gRPC |
| --- | ---- |
| Reguläre Anforderung/Antwort | Unäroperatoren |
| Duplex Dienst mit Sitzung mithilfe einer Client Rückruf Schnittstelle | Server Streaming |
| Vollduplex Dienst mit Sitzung | Bidirektionales Streaming |
| Unidirektionale Vorgänge | Client Streaming |

## <a name="requestreply"></a>Anforderung/Antwort

Verwenden Sie für einfache Anforderung/Antwort-Methoden, die kleine Datenmengen verwenden und zurückgeben, das einfachste GrpC-Muster, den unären RPC.

```protobuf
service Things {
    rpc Get(GetThingRequest) returns (GetThingResponse);
}
```

```csharp
public class ThingService : Things.ThingsBase
{
    public override async Task<GetThingResponse> Get(GetThingRequest request, ServerCallContext context)
    {
        // Get thing from database
        return new GetThingResponse { Thing = thing };
    }
}
```

```csharp
public async Task ShowThing(int thingId)
{
    var thing = await _thingsClient.GetAsync(new GetThingRequest { ThingId = thingId });
    Console.WriteLine($"{thing.Name}");
}
```

Wie Sie sehen können, ähnelt das Implementieren einer Methode des unären Dienst-RPC-dienstanzvorgangs der Implementierung eines WCF-Vorgangs. Der Unterschied besteht darin, dass Sie mit GrpC eine Basisklassen Methode außer Kraft setzen, anstatt eine Schnittstelle zu implementieren. Auf dem Server geben die GrpC-Basis Methoden immer <xref:System.Threading.Tasks.Task%601>zurück, obwohl der Client sowohl Async-als auch Blockierungs Methoden zum Aufrufen des Dienstanbieter bereitstellt.

## <a name="wcf-duplex-one-way-to-client"></a>WCF Duplex, eine Möglichkeit zum Client

WCF-Anwendungen (mit bestimmten Bindungen) können eine permanente Verbindung zwischen Client und Server herstellen. Der Server kann Daten asynchron an den Client senden, bis die Verbindung geschlossen wurde, indem er eine *Rückruf Schnittstelle* verwendet, die in der <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A?displayProperty=nameWithType>-Eigenschaft angegeben ist.

GrpC-Dienste bieten eine ähnliche Funktionalität wie Nachrichtenströme. Streams werden in Bezug auf die Implementierung nicht *exakt* den WCF-Duplex Diensten zugeordnet, aber Sie können dieselben Ergebnisse erzielen.

### <a name="grpc-streaming"></a>GrpC-Streaming

GrpC unterstützt die Erstellung von permanenten Datenströmen vom Client zum Server und vom Server zum Client. Beide Arten von Datenströmen können gleichzeitig aktiv sein. Diese Fähigkeit wird als bidirektionales Streaming bezeichnet. 

Sie können Datenströme für beliebiges, asynchrones Messaging im Lauf der Zeit verwenden. Oder Sie können Sie verwenden, um große Datasets zu übergeben, die zu groß sind, um Sie in einer einzelnen Anforderung oder Antwort zu generieren und zu senden.

Das folgende Beispiel zeigt ein Server-Streaming-RPC.

```protobuf
service ClockStreamer {
    rpc Subscribe(ClockSubscribeRequest) returns (stream ClockMessage);
}
```

```csharp
public class ClockStreamerService : ClockStreamer.ClockStreamerBase
{
    public override async Task Subscribe(ClockSubscribeRequest request,
        IServerStreamWriter<ClockMessage> responseStream,
        ServerCallContext context)
    {
        while (!context.CancellationToken.IsCancellationRequested)
        {
            var time = DateTimeOffset.UtcNow;
            await responseStream.WriteAsync(new ClockMessage { message = $"The time is {time:t}." });
            await Task.Delay(TimeSpan.FromSeconds(10), context.CancellationToken);
        }
    }
}
```

Dieser Serverdaten Strom kann von einer Client Anwendung verwendet werden, wie im folgenden Code gezeigt:

```csharp
public async Task TellTheTimeAsync(CancellationToken token)
{
    var channel = GrpcChannel.ForAddress("https://localhost:5001");
    var client = new ClockStreamer.ClockStreamerClient(channel);

    var request = new ClockSubscribeRequest();
    var response = client.Subscribe(request);

    await foreach (var update in response.ResponseStream.ReadAllAsync(token))
    {
        Console.WriteLine(update.Message);
    }
}
```

> [!NOTE]
> RPCs mit Server Streaming sind für Dienste im Abonnement Stil nützlich. Sie sind auch nützlich, um große Datasets zu senden, wenn es ineffizient oder unmöglich wäre, das gesamte Dataset im Arbeitsspeicher zu erstellen. Das Streamen von Antworten ist jedoch nicht so schnell wie das Senden `repeated` Felder in einer einzelnen Nachricht. Als Regel sollte Streaming nicht für kleine Datasets verwendet werden.

### <a name="differences-from-wcf"></a>Unterschiede zu WCF

Ein WCF-Duplex Dienst verwendet eine Client Rückruf Schnittstelle, die mehrere Methoden aufweisen kann. Ein GrpC-Server-Streamingdienst kann nur Nachrichten über einen einzigen Stream senden. Wenn Sie mehrere Methoden benötigen, verwenden Sie einen Nachrichtentyp mit einem [beliebigen Feld oder einem Feld](protobuf-any-oneof.md) , um verschiedene Nachrichten zu senden, und schreiben Sie Code im Client, um Sie zu verarbeiten.

In WCF wird die [ServiceContract](xref:System.ServiceModel.ServiceContractAttribute) -Klasse mit der Sitzung aufrechterhalten, bis die Verbindung geschlossen wird. Innerhalb der Sitzung können mehrere Methoden aufgerufen werden. In GrpC sollten die `Task`, die von der Implementierungsmethode zurückgegeben werden, erst beendet werden, wenn die Verbindung geschlossen wird.

## <a name="wcf-one-way-operations-and-grpc-client-streaming"></a>Unidirektionale WCF-Vorgänge und GrpC-Client Streaming

WCF stellt unidirektionale Vorgänge (mit `[OperationContract(IsOneWay = true)]`gekennzeichnet) bereit, die eine Transport spezifische Bestätigung zurückgeben. GrpC-Dienst Methoden geben immer eine Antwort zurück, auch wenn Sie leer ist. Der Client sollte immer auf diese Antwort warten. Für den Nachrichten Stil "Fire-and-Forget" in GrpC können Sie einen clientstreamingdienst erstellen.

### <a name="thing_logproto"></a>thing_log. proto

```protobuf
service ThingLog {
  rpc OpenConnection(stream Thing) returns (ConnectionClosedResponse);
}
```

### <a name="thinglogservicecs"></a>ThingLogService.cs

```csharp
public class ThingLogService : Protos.ThingLog.ThingLogBase
{
    private static readonly ConnectionClosedResponse EmptyResponse = new ConnectionClosedResponse();
    private readonly ILogger<ThingLogService> _logger;
    public ThingLogService(ILogger<ThingLogService> logger)
    {
        _logger = logger;
    }

    public override async Task<CompletedResponse> OpenConnection(IAsyncStreamReader<Thing> requestStream, ServerCallContext context)
    {
        while (await requestStream.MoveNext(context.CancellationToken))
        {
            _logger.LogInformation(requestStream.Current.Description);
        }
        return EmptyResponse;
    }
}
```

### <a name="thinglog-client-example"></a>Thinglog-Client Beispiel

```csharp
public class ThingLogger : IAsyncDisposable
{
    private readonly ThingLog.ThingLogClient _client;
    private readonly AsyncClientStreamingCall<ThingLogRequest, CompletedResponse> _stream;

    public ThingLogger(ThingLog.ThingLogClient client)
    {
        _client = client;
        _stream = client.OpenConnection();
    }

    public async Task WriteAsync(string description)
    {
        await _stream.RequestStream.WriteAsync(new Thing
        {
            Description = description,
            Time = Timestamp.FromDateTimeOffset(DateTimeOffset.UtcNow)
        });
    }

    public async ValueTask DisposeAsync()
    {
        await _stream.RequestStream.CompleteAsync();
        _stream.Dispose();
    }
}
```

Sie können Client Streaming-RPCs für das Fire-and-Forget-Messaging verwenden, wie im vorherigen Beispiel gezeigt. Sie können Sie auch verwenden, um sehr große Datasets an den Server zu senden. Dieselbe Warnung bezüglich der Leistung gilt für kleinere Datasets: Verwenden Sie `repeated` Felder in regulären Nachrichten.

## <a name="wcf-full-duplex-services"></a>WCF-Vollduplex Dienste

Die WCF-Duplex Bindung unterstützt mehrere unidirektionale Vorgänge sowohl für die Dienst Schnittstelle als auch für die Client Rückruf Schnittstelle. Diese Unterstützung ermöglicht laufende Konversationen zwischen Client und Server. GrpC unterstützt ähnliche Funktionen wie bidirektionale Streaming-RPCs, bei denen beide Parameter mit dem `stream`-Modifizierer markiert sind.

### <a name="chatproto"></a>Chat. proto

```protobuf
service Chatter {
    rpc Connect(stream IncomingMessage) returns (stream OutgoingMessage);
}
```

### <a name="chatterservicecs"></a>ChatterService.cs

```csharp
public class ChatterService : Chatter.ChatterBase
{
    private readonly IChatHub _hub;

    public ChatterService(IChatHub hub)
    {
        _hub = hub;
    }

    public override async Task Connect(IAsyncStreamReader<MessageRequest> requestStream, IServerStreamWriter<MessageResponse> responseStream, ServerCallContext context)
    {
        _hub.MessageReceived += async (sender, args) =>
            await responseStream.WriteAsync(new MessageResponse {Text = args.Message});

        while (await requestStream.MoveNext(context.CancellationToken))
        {
            await _hub.SendAsync(requestStream.Current.Text);
        }
    }
}
```

Im vorherigen Beispiel können Sie sehen, dass die Implementierungsmethode sowohl einen Anforderungs Datenstrom (`IAsyncStreamReader<MessageRequest>`) als auch einen Antwortstream (`IServerStreamWriter<MessageResponse>`) empfängt. Die-Methode kann Nachrichten lesen und schreiben, bis die Verbindung geschlossen wird.

### <a name="chatter-client"></a>Chatter-Client

```csharp
public class Chat : IAsyncDisposable
{
    private readonly Chatter.ChatterClient _client;
    private readonly AsyncDuplexStreamingCall<MessageRequest, MessageResponse> _stream;
    private readonly CancellationTokenSource _cancellationTokenSource;
    private readonly Task _readTask;

    public Chat(Chatter.ChatterClient client)
    {
        _client = client;
        _stream = _client.Connect();
        _cancellationTokenSource = new CancellationTokenSource();
        _readTask = ReadAsync(_cancellationTokenSource.Token);
    }

    public async Task SendAsync(string message)
    {
        await _stream.RequestStream.WriteAsync(new MessageRequest {Text = message});
    }

    private async Task ReadAsync(CancellationToken token)
    {
        while (await _stream.ResponseStream.MoveNext(token))
        {
            Console.WriteLine(_stream.ResponseStream.Current.Text);
        }
    }

    public async ValueTask DisposeAsync()
    {
        await _stream.RequestStream.CompleteAsync();
        await _readTask;
        _stream.Dispose();
    }
}
```

>[!div class="step-by-step"]
>[Zurück](wcf-bindings.md)
>[Weiter](metadata.md)
