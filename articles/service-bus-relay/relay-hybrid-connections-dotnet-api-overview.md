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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="56245-103">Panoramica dell'API .NET Standard per Connessioni ibride di Inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="56245-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="56245-104">In questo articolo riepiloga alcune delle chiave hello Azure inoltro ibrido connessioni .NET Standard [API client](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="56245-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="56245-105">Generatore di stringhe di connessione di Inoltro</span><span class="sxs-lookup"><span data-stu-id="56245-105">Relay Connection String Builder</span></span>

<span data-ttu-id="56245-106">Hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] classe formatta le stringhe di connessione presenti connessioni ibride tooRelay specifico.</span><span class="sxs-lookup"><span data-stu-id="56245-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="56245-107">È possibile utilizzare il formato di hello tooverify di una stringa di connessione o toobuild una stringa di connessione da zero.</span><span class="sxs-lookup"><span data-stu-id="56245-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="56245-108">Vedere hello seguente codice per un esempio:</span><span class="sxs-lookup"><span data-stu-id="56245-108">See hello following code for an example:</span></span>

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

<span data-ttu-id="56245-109">È inoltre possibile passare una connessione stringa direttamente toohello `RelayConnectionStringBuilder` metodo.</span><span class="sxs-lookup"><span data-stu-id="56245-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="56245-110">Questa operazione consente tooverify di stringa di connessione hello in un formato valido.</span><span class="sxs-lookup"><span data-stu-id="56245-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="56245-111">Se uno dei parametri di hello non sono valido, costruttore hello genera un `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="56245-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

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

## <a name="hybrid-connection-stream"></a><span data-ttu-id="56245-112">Flusso di Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="56245-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="56245-113">Hello [HybridConnectionStream] [ HCStream] classe è toosend oggetto primario utilizzato hello e ricevere dati da un endpoint di inoltro di Azure, se si sta usando un [HybridConnectionClient] [ HCClient], o un [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="56245-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="56245-114">Ottenere un flusso di Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="56245-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="56245-115">Listener</span><span class="sxs-lookup"><span data-stu-id="56245-115">Listener</span></span>
<span data-ttu-id="56245-116">Tramite [HybridConnectionListener][HCListener] è possibile ottenere un oggetto `HybridConnectionStream` nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="56245-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="56245-117">Client</span><span class="sxs-lookup"><span data-stu-id="56245-117">Client</span></span>
<span data-ttu-id="56245-118">Tramite [HybridConnectionClient][HCClient] è possibile ottenere un oggetto `HybridConnectionStream` nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="56245-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="56245-119">Ricezione di dati</span><span class="sxs-lookup"><span data-stu-id="56245-119">Receiving data</span></span>
<span data-ttu-id="56245-120">Hello [HybridConnectionStream] [ HCStream] classe consente la comunicazione bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="56245-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="56245-121">Nella maggior parte dei casi, viene visualizzato continuamente dal flusso hello.</span><span class="sxs-lookup"><span data-stu-id="56245-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="56245-122">Se si sta leggendo il testo dal flusso hello, è inoltre possibile toouse un [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) oggetto, che semplifica l'analisi dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="56245-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="56245-123">Ad esempio, è possibile leggere i dati come testo anziché come `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="56245-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="56245-124">Hello codice legge singole righe di testo dal flusso hello fino a quando non è richiesto un annullamento:</span><span class="sxs-lookup"><span data-stu-id="56245-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

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

### <a name="sending-data"></a><span data-ttu-id="56245-125">Invio di dati</span><span class="sxs-lookup"><span data-stu-id="56245-125">Sending data</span></span>
<span data-ttu-id="56245-126">Dopo aver creato una connessione stabilita, è possibile inviare un endpoint di inoltro toohello di messaggio.</span><span class="sxs-lookup"><span data-stu-id="56245-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="56245-127">Poiché l'oggetto connessione hello eredita [flusso](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), inviare i dati come un `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="56245-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="56245-128">Hello seguente esempio viene illustrato come toodo questo:</span><span class="sxs-lookup"><span data-stu-id="56245-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="56245-129">Tuttavia, se si desidera toosend direttamente, senza la necessità di stringa hello tooencode ogni volta, è possibile eseguire il wrapping hello `hybridConnectionStream` dell'oggetto con un [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) oggetto.</span><span class="sxs-lookup"><span data-stu-id="56245-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="56245-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56245-130">Next steps</span></span>
<span data-ttu-id="56245-131">toolearn ulteriori informazioni sull'inoltro di Azure, visitare i collegamenti:</span><span class="sxs-lookup"><span data-stu-id="56245-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="56245-132">Riferimento su Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="56245-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="56245-133">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="56245-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="56245-134">API di inoltro disponibili</span><span class="sxs-lookup"><span data-stu-id="56245-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener