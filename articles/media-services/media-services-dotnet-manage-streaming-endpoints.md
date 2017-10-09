---
title: aaaManage streaming endpoint con .NET SDK. | Microsoft Docs
description: Questo argomento viene illustrato come endpoint di streaming toomanage con hello portale di Azure.
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
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="ac029-104">Gestire gli endpoint di streaming con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ac029-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="ac029-105">Verificare che hello tooreview [Panoramica](media-services-streaming-endpoints-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="ac029-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="ac029-106">Vedere anche [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="ac029-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="ac029-107">codice Hello in questo argomento viene illustrato come hello toodo seguenti attività mediante hello Azure Media Services .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="ac029-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="ac029-108">Esaminare il valore predefinito hello endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="ac029-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="ac029-109">Creare/aggiungere un nuovo endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="ac029-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="ac029-110">È possibile toohave più endpoint di streaming se si prevede di toohave CDN diversa o una rete CDN e l'accesso diretto.</span><span class="sxs-lookup"><span data-stu-id="ac029-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac029-111">Il costo verrà addebitato solo quando StreamingEndpoint è in stato di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ac029-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="ac029-112">Aggiornare l'endpoint di streaming hello.</span><span class="sxs-lookup"><span data-stu-id="ac029-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="ac029-113">Verificare che toocall hello funzione Update ().</span><span class="sxs-lookup"><span data-stu-id="ac029-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="ac029-114">Eliminare l'endpoint di streaming hello.</span><span class="sxs-lookup"><span data-stu-id="ac029-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="ac029-115">Impossibile eliminare l'endpoint di streaming predefinito di Hello.</span><span class="sxs-lookup"><span data-stu-id="ac029-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="ac029-116">Per informazioni su come tooscale hello endpoint di streaming, vedere [questo](media-services-portal-scale-streaming-endpoints.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="ac029-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ac029-117">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac029-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="ac029-118">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ac029-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="ac029-119">Aggiungere il codice che gestisce gli endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="ac029-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="ac029-120">Sostituire il codice di hello in hello Program.cs con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="ac029-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from hello App.config file.
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


## <a name="next-steps"></a><span data-ttu-id="ac029-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac029-121">Next steps</span></span>
<span data-ttu-id="ac029-122">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ac029-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ac029-123">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ac029-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

