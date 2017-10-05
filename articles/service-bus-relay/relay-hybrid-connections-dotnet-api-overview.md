---
title: Panoramica delle API .NET Standard di Inoltro di Azure | Microsoft Docs
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
ms.openlocfilehash: f3f4a2e721b1a75a5b92a5c17a9939c7013340d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="635a2-103">Panoramica dell'API .NET Standard per Connessioni ibride di Inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="635a2-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="635a2-104">In questo articolo vengono riepilogate alcune delle principali [API client](/dotnet/api/microsoft.azure.relay) .NET Standard per Connessioni ibride di Inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="635a2-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="635a2-105">Generatore di stringhe di connessione di Inoltro</span><span class="sxs-lookup"><span data-stu-id="635a2-105">Relay Connection String Builder</span></span>

<span data-ttu-id="635a2-106">La classe [RelayConnectionStringBuilder][RelayConnectionStringBuilder] genera stringhe in un formato specifico per Connessioni ibride di inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="635a2-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="635a2-107">È possibile usarla per verificare il formato di una stringa di connessione o per generarne una da zero.</span><span class="sxs-lookup"><span data-stu-id="635a2-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="635a2-108">Per un esempio, vedere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="635a2-108">See the following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of the Hybrid Connection}";
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

<span data-ttu-id="635a2-109">È inoltre possibile passare direttamente una stringa di connessione al metodo `RelayConnectionStringBuilder`.</span><span class="sxs-lookup"><span data-stu-id="635a2-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="635a2-110">Questa operazione consente di verificare che il formato della stringa di connessione sia valido.</span><span class="sxs-lookup"><span data-stu-id="635a2-110">This operation enables you to verify that the connection string is in a valid format.</span></span> <span data-ttu-id="635a2-111">Se uno dei parametri non è valido, il costruttore genera un'eccezione `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="635a2-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare the connectionStringBuilder so that it can be used outside of the loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create the connectionStringBuilder using the supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="635a2-112">Flusso di Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="635a2-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="635a2-113">La classe [HybridConnectionStream][HCStream] è l'oggetto principale usato per inviare e ricevere dati da un endpoint di Inoltro di Azure, sia che si lavori con un [HybridConnectionClient][HCClient] o un [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="635a2-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="635a2-114">Ottenere un flusso di Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="635a2-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="635a2-115">Listener</span><span class="sxs-lookup"><span data-stu-id="635a2-115">Listener</span></span>
<span data-ttu-id="635a2-116">Tramite [HybridConnectionListener][HCListener] è possibile ottenere un oggetto `HybridConnectionStream` nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="635a2-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="635a2-117">Client</span><span class="sxs-lookup"><span data-stu-id="635a2-117">Client</span></span>
<span data-ttu-id="635a2-118">Tramite [HybridConnectionClient][HCClient] è possibile ottenere un oggetto `HybridConnectionStream` nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="635a2-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="635a2-119">Ricezione di dati</span><span class="sxs-lookup"><span data-stu-id="635a2-119">Receiving data</span></span>
<span data-ttu-id="635a2-120">La classe [HybridConnectionStream][HCStream] consente la comunicazione bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="635a2-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="635a2-121">Nella maggior parte dei casi si ha una ricezione costante dal flusso.</span><span class="sxs-lookup"><span data-stu-id="635a2-121">In most cases, you continuously receive from the stream.</span></span> <span data-ttu-id="635a2-122">Se si legge testo da un flusso, è anche possibile usare un oggetto [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) per usufruire di una più semplice analisi dei dati.</span><span class="sxs-lookup"><span data-stu-id="635a2-122">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span></span> <span data-ttu-id="635a2-123">Ad esempio, è possibile leggere i dati come testo anziché come `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="635a2-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="635a2-124">Il codice seguente legge singole righe di testo dal flusso fino a quando non viene richiesto l'annullamento.</span><span class="sxs-lookup"><span data-stu-id="635a2-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel the while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from the 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of the processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="635a2-125">Invio di dati</span><span class="sxs-lookup"><span data-stu-id="635a2-125">Sending data</span></span>
<span data-ttu-id="635a2-126">Dopo aver stabilito una connessione, è possibile inviare un messaggio all'endpoint di Inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="635a2-126">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="635a2-127">Poiché l'oggetto connessione eredita [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), inviare i dati come un `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="635a2-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="635a2-128">L'esempio seguente illustra come farlo:</span><span class="sxs-lookup"><span data-stu-id="635a2-128">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="635a2-129">Tuttavia, se si desidera inviare testo direttamente e senza dover codificare la stringa ogni volta, è possibile eseguire il wrapping dell'oggetto `hybridConnectionStream` con un oggetto [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="635a2-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="635a2-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="635a2-130">Next steps</span></span>
<span data-ttu-id="635a2-131">Per altre informazioni su Inoltro di Azure, visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="635a2-131">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="635a2-132">Riferimento su Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="635a2-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="635a2-133">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="635a2-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="635a2-134">API di inoltro disponibili</span><span class="sxs-lookup"><span data-stu-id="635a2-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener