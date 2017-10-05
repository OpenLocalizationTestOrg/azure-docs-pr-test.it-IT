---
title: Polling di operazioni con esecuzione prolungata | Microsoft Docs
description: Questo argomento descrive come eseguire il polling di operazioni con esecuzione prolungata.
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
ms.openlocfilehash: 7123a2d44d3b7c332afe30fb0fcea88ca29e313a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="0da2f-103">Distribuzione di Live Streaming con Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="0da2f-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="0da2f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0da2f-104">Overview</span></span>

<span data-ttu-id="0da2f-105">Servizi multimediali di Microsoft Azure offre API che inviano richieste a servizi multimediali per avviare operazioni, ad esempio creazione, avvio, arresto o eliminazione di un canale.</span><span class="sxs-lookup"><span data-stu-id="0da2f-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="0da2f-106">Queste operazioni hanno un'esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="0da2f-106">These operations are long-running.</span></span>

<span data-ttu-id="0da2f-107">L'SDK di Servizi multimediali per .NET fornisce le API che inviano la richiesta e attendono il completamento dell'operazione (a livello interno, le API eseguono il polling dell'avanzamento dell'operazione a intervalli definiti).</span><span class="sxs-lookup"><span data-stu-id="0da2f-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="0da2f-108">Ad esempio, quando si chiama channel.Start(), il metodo restituisce dopo l'avvio del canale.</span><span class="sxs-lookup"><span data-stu-id="0da2f-108">For example, when you call channel.Start(), the method returns after the channel is started.</span></span> <span data-ttu-id="0da2f-109">È possibile anche usare la versione asincrona: await channel.StartAsync(). Per informazioni sul modello asincrono basato su attività, vedere [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="0da2f-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="0da2f-110">Le API che inviano una richiesta di operazione e quindi eseguono il polling dello stato fino al completamento dell'operazione vengono definite "metodi di polling".</span><span class="sxs-lookup"><span data-stu-id="0da2f-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span></span> <span data-ttu-id="0da2f-111">Tali metodi (in special modo la versione asincrona) sono consigliati per le applicazioni rich client e/o i servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="0da2f-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="0da2f-112">In alcuni scenari è possibile che un'applicazione non possa attendere una richiesta HTTP con esecuzione prolungata e sia necessario eseguire il polling manuale dell'avanzamento dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="0da2f-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span></span> <span data-ttu-id="0da2f-113">Un esempio tipico può essere un browser che interagisce con un servizio Web senza stato: quando il browser richiede di creare un canale, il servizio Web avvia un'operazione con esecuzione prolungata e restituisce l'ID operazione al browser.</span><span class="sxs-lookup"><span data-stu-id="0da2f-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span></span> <span data-ttu-id="0da2f-114">Il browser potrebbe quindi chiedere al servizio Web di ottenere lo stato dell'operazione in base all'ID.</span><span class="sxs-lookup"><span data-stu-id="0da2f-114">The browser could then ask the web service to get the operation status based on the ID.</span></span> <span data-ttu-id="0da2f-115">L'SDK di Servizi multimediali per .NET fornisce API che sono utili per questo scenario,</span><span class="sxs-lookup"><span data-stu-id="0da2f-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="0da2f-116">definite "metodi di non polling",</span><span class="sxs-lookup"><span data-stu-id="0da2f-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="0da2f-117">che sono caratterizzati dal seguente criterio di denominazione: Send*NomeOperazione*Operation, ad esempio SendCreateOperation.</span><span class="sxs-lookup"><span data-stu-id="0da2f-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="0da2f-118">I metodi Send*NomeOperazione*Operation restituiscono l'oggetto **IOperation**. L'oggetto restituito contiene informazioni che consentono di tenere traccia dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="0da2f-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span></span> <span data-ttu-id="0da2f-119">I metodi Send*NomeOperazione*OperationAsync restituiscono **Task<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="0da2f-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="0da2f-120">Attualmente, le classi seguenti supportano i metodi non polling: **Channel**, **StreamingEndpoint** e **Program**.</span><span class="sxs-lookup"><span data-stu-id="0da2f-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="0da2f-121">Per eseguire il polling dello stato delle operazioni, usare il metodo **GetOperation** sulla classe **OperationBaseCollection**.</span><span class="sxs-lookup"><span data-stu-id="0da2f-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span></span> <span data-ttu-id="0da2f-122">Usare gli intervalli seguenti per controllare lo stato dell'operazione: per le operazioni **Channel** e **StreamingEndpoint**, usare 30 secondi; per le operazioni **Program**, usare 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="0da2f-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0da2f-123">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0da2f-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0da2f-124">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0da2f-124">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="0da2f-125">Esempio</span><span class="sxs-lookup"><span data-stu-id="0da2f-125">Example</span></span>

<span data-ttu-id="0da2f-126">L'esempio seguente definisce una classe denominata **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="0da2f-126">The following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="0da2f-127">Questa definizione di classe può essere un punto di partenza per la definizione di classe del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="0da2f-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="0da2f-128">Per esigenze di semplicità, negli esempi seguenti vengono usate le versioni non asincrone dei metodi.</span><span class="sxs-lookup"><span data-stu-id="0da2f-128">For simplicity, the following examples use the non-async versions of methods.</span></span>

<span data-ttu-id="0da2f-129">Nell'esempio viene inoltre illustrato il modo in cui il client potrebbe usare questa classe.</span><span class="sxs-lookup"><span data-stu-id="0da2f-129">The example also shows how the client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="0da2f-130">Definizione della classe ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="0da2f-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// The ChannelOperations class only implements 
    /// the Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from the App.config file.
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
        /// Initiates the creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name to be given to the new channel</param>  
        /// <returns>  
        /// Operation Id for the long running operation being executed by Media Services. 
        /// Use this operation Id to poll for the channel creation status. 
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
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created channel Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the created channel Id is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle the failure. 
                    // For example, throw an exception. 
                    // Use the following information in the exception: operationId, operation.ErrorMessage.
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

### <a name="the-client-code"></a><span data-ttu-id="0da2f-131">The client code</span><span class="sxs-lookup"><span data-stu-id="0da2f-131">The client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have the newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="0da2f-132">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="0da2f-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0da2f-133">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="0da2f-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

