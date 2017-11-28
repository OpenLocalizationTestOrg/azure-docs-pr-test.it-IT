---
title: Operazioni con esecuzione prolungata aaaPolling | Documenti Microsoft
description: Questo argomento viene illustrato come toopoll operazioni a esecuzione prolungata.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="7d119-103">Distribuzione di Live Streaming con Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="7d119-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="7d119-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7d119-104">Overview</span></span>

<span data-ttu-id="7d119-105">Servizi multimediali di Microsoft Azure offre API che inviano richieste di operazioni di toostart tooMedia Services (ad esempio: creare, avviare, arrestare o eliminare un canale).</span><span class="sxs-lookup"><span data-stu-id="7d119-105">Microsoft Azure Media Services offers APIs that send requests tooMedia Services toostart operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="7d119-106">Queste operazioni hanno un'esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="7d119-106">These operations are long-running.</span></span>

<span data-ttu-id="7d119-107">Hello Media Services .NET SDK fornisce le API che inviano la richiesta hello e attendere hello operazione toocomplete (internamente, Buongiorno API eseguono il polling dell'avanzamento dell'operazione a intervalli definiti).</span><span class="sxs-lookup"><span data-stu-id="7d119-107">hello Media Services .NET SDK provides APIs that send hello request and wait for hello operation toocomplete (internally, hello APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="7d119-108">Ad esempio, quando si chiama canale. Start (), il metodo hello restituisce dopo l'avvio del canale hello.</span><span class="sxs-lookup"><span data-stu-id="7d119-108">For example, when you call channel.Start(), hello method returns after hello channel is started.</span></span> <span data-ttu-id="7d119-109">È inoltre possibile utilizzare la versione asincrona di hello: attesa del canale. StartAsync() (per informazioni sul modello asincrono basato su attività, vedere [toccare](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="7d119-109">You can also use hello asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="7d119-110">Le API che inviano una richiesta di operazione e quindi eseguire il polling per lo stato di hello fino al completamento dell'operazione hello vengono definite "metodi di polling".</span><span class="sxs-lookup"><span data-stu-id="7d119-110">APIs that send an operation request and then poll for hello status until hello operation is complete are called “polling methods”.</span></span> <span data-ttu-id="7d119-111">Questi metodi (in particolare versione asincrona di hello) sono consigliati per le applicazioni rich client e/o i servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="7d119-111">These methods (especially hello Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="7d119-112">Esistono scenari in cui un'applicazione non può attendere una richiesta http a esecuzione prolungata e desidera toopoll hello dell'avanzamento dell'operazione manualmente.</span><span class="sxs-lookup"><span data-stu-id="7d119-112">There are scenarios where an application cannot wait for a long running http request and wants toopoll for hello operation progress manually.</span></span> <span data-ttu-id="7d119-113">Un esempio tipico sarebbe un browser che interagisce con un servizio web senza stato: quando il browser di hello richiede toocreate un canale, servizio web hello avvia un'operazione a esecuzione prolungata e restituisce hello browser toohello ID di operazione.</span><span class="sxs-lookup"><span data-stu-id="7d119-113">A typical example would be a browser interacting with a stateless web service: when hello browser requests toocreate a channel, hello web service initiates a long running operation and returns hello operation ID toohello browser.</span></span> <span data-ttu-id="7d119-114">browser Hello potrebbe quindi chiedere di hello web servizio tooget hello stato dell'operazione basato sull'ID di hello.</span><span class="sxs-lookup"><span data-stu-id="7d119-114">hello browser could then ask hello web service tooget hello operation status based on hello ID.</span></span> <span data-ttu-id="7d119-115">Hello Media Services .NET SDK fornisce le API che sono utili per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="7d119-115">hello Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="7d119-116">definite "metodi di non polling",</span><span class="sxs-lookup"><span data-stu-id="7d119-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="7d119-117">"metodi di non polling" Hello hanno hello seguente modello di denominazione: inviare*OperationName*operazione (ad esempio, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="7d119-117">hello “non-polling methods” have hello following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="7d119-118">Inviare*OperationName*operazione restituiscono hello **IOperation** oggetto; hello oggetto restituito contiene le informazioni che possono essere utilizzati tootrack hello operazione.</span><span class="sxs-lookup"><span data-stu-id="7d119-118">Send*OperationName*Operation methods return hello **IOperation** object; hello returned object contains information that can be used tootrack hello operation.</span></span> <span data-ttu-id="7d119-119">Hello trasmissione*OperationName*OperationAsync restituiscono **attività<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="7d119-119">hello Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="7d119-120">Attualmente, hello dei seguenti metodi di non polling supporto classi: **canale**, **StreamingEndpoint**, e **programma**.</span><span class="sxs-lookup"><span data-stu-id="7d119-120">Currently, hello following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="7d119-121">toopoll hello dello stato dell'operazione, utilizzare hello **GetOperation** metodo hello **OperationBaseCollection** classe.</span><span class="sxs-lookup"><span data-stu-id="7d119-121">toopoll for hello operation status, use hello **GetOperation** method on hello **OperationBaseCollection** class.</span></span> <span data-ttu-id="7d119-122">Utilizzare hello seguente lo stato dell'operazione intervalli toocheck hello: per **canale** e **StreamingEndpoint** operazioni, usare 30 secondi; per **programma** operazioni, utilizzare 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="7d119-122">Use hello following intervals toocheck hello operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="7d119-123">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d119-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="7d119-124">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7d119-124">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="7d119-125">Esempio</span><span class="sxs-lookup"><span data-stu-id="7d119-125">Example</span></span>

<span data-ttu-id="7d119-126">esempio Hello definisce una classe denominata **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="7d119-126">hello following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="7d119-127">Questa definizione di classe può essere un punto di partenza per la definizione di classe del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="7d119-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="7d119-128">Per semplicità, hello negli esempi seguenti utilizzano versioni non asincrone hello dei metodi.</span><span class="sxs-lookup"><span data-stu-id="7d119-128">For simplicity, hello following examples use hello non-async versions of methods.</span></span>

<span data-ttu-id="7d119-129">esempio Hello Mostra anche come client hello possibile utilizzare questa classe.</span><span class="sxs-lookup"><span data-stu-id="7d119-129">hello example also shows how hello client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="7d119-130">Definizione della classe ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="7d119-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a><span data-ttu-id="7d119-131">codice client Hello</span><span class="sxs-lookup"><span data-stu-id="7d119-131">hello client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="7d119-132">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="7d119-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7d119-133">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="7d119-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

