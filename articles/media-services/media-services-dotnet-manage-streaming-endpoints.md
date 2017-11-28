---
title: Gestire gli endpoint di streaming con .NET SDK. | Documentazione Microsoft
description: Questo argomento illustra come gestire gli endpoint di streaming mediante il portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 2f4f464f8604b6f453d6b50b736c6a3a889a3408
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="b900b-104">Gestire gli endpoint di streaming con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b900b-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="b900b-105">Assicurarsi di rivedere l'argomento sulla [panoramica](media-services-streaming-endpoints-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b900b-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="b900b-106">Vedere anche [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="b900b-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="b900b-107">Il codice in questo argomento illustra come eseguire queste attività tramite SDK di Servizi multimediali di Azure per .NET:</span><span class="sxs-lookup"><span data-stu-id="b900b-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="b900b-108">Esaminare l'endpoint di streaming predefinito.</span><span class="sxs-lookup"><span data-stu-id="b900b-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="b900b-109">Creare/aggiungere un nuovo endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="b900b-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="b900b-110">Se si prevedono più reti CDN o una rete CDN e l'accesso diretto, potrebbero essere necessari più endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="b900b-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b900b-111">Il costo verrà addebitato solo quando StreamingEndpoint è in stato di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b900b-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="b900b-112">Aggiornare l'endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="b900b-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="b900b-113">Chiamare la funzione Update().</span><span class="sxs-lookup"><span data-stu-id="b900b-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="b900b-114">Eliminare l'endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="b900b-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b900b-115">Gli endpoint di streaming predefiniti non possono essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="b900b-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="b900b-116">Per informazioni su come ridimensionare l'endpoint di streaming, vedere [questo](media-services-portal-scale-streaming-endpoints.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="b900b-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b900b-117">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b900b-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="b900b-118">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b900b-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="b900b-119">Aggiungere il codice che gestisce gli endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="b900b-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="b900b-120">Sostituire il codice nel file Program.cs con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b900b-120">Replace the code in the Program.cs with the following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="b900b-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b900b-121">Next steps</span></span>
<span data-ttu-id="b900b-122">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b900b-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b900b-123">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b900b-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

