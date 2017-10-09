---
title: aaaOverview di hello Azure inoltro .NET Standard API | Documenti Microsoft
description: Panoramica dell'API .NET Standard di Inoltro di Azure
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Panoramica dell'API .NET Standard per Connessioni ibride di Inoltro di Azure

In questo articolo riepiloga alcune delle chiave hello Azure inoltro ibrido connessioni .NET Standard [API client](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Generatore di stringhe di connessione di Inoltro

Hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] classe formatta le stringhe di connessione presenti connessioni ibride tooRelay specifico. È possibile utilizzare il formato di hello tooverify di una stringa di connessione o toobuild una stringa di connessione da zero. Vedere hello seguente codice per un esempio:

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

È inoltre possibile passare una connessione stringa direttamente toohello `RelayConnectionStringBuilder` metodo. Questa operazione consente tooverify di stringa di connessione hello in un formato valido. Se uno dei parametri di hello non sono valido, costruttore hello genera un `ArgumentException`.

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a>Flusso di Connessioni ibride
Hello [HybridConnectionStream] [ HCStream] classe è toosend oggetto primario utilizzato hello e ricevere dati da un endpoint di inoltro di Azure, se si sta usando un [HybridConnectionClient] [ HCClient], o un [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Ottenere un flusso di Connessioni ibride

#### <a name="listener"></a>Listener
Tramite [HybridConnectionListener][HCListener] è possibile ottenere un oggetto `HybridConnectionStream` nel modo seguente:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Client
Tramite [HybridConnectionClient][HCClient] è possibile ottenere un oggetto `HybridConnectionStream` nel modo seguente:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Ricezione di dati
Hello [HybridConnectionStream] [ HCStream] classe consente la comunicazione bidirezionale. Nella maggior parte dei casi, viene visualizzato continuamente dal flusso hello. Se si sta leggendo il testo dal flusso hello, è inoltre possibile toouse un [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) oggetto, che semplifica l'analisi dei dati di hello. Ad esempio, è possibile leggere i dati come testo anziché come `byte[]`.

Hello codice legge singole righe di testo dal flusso hello fino a quando non è richiesto un annullamento:

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a>Invio di dati
Dopo aver creato una connessione stabilita, è possibile inviare un endpoint di inoltro toohello di messaggio. Poiché l'oggetto connessione hello eredita [flusso](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), inviare i dati come un `byte[]`. Hello seguente esempio viene illustrato come toodo questo:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

Tuttavia, se si desidera toosend direttamente, senza la necessità di stringa hello tooencode ogni volta, è possibile eseguire il wrapping hello `hybridConnectionStream` dell'oggetto con un [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) oggetto.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sull'inoltro di Azure, visitare i collegamenti:

* [Riferimento su Microsoft.Azure.Relay](/dotnet/api/microsoft.azure.relay)
* [Che cos'è il servizio di inoltro di Azure?](relay-what-is-it.md)
* [API di inoltro disponibili](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener