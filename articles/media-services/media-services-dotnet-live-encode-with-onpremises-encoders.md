---
title: Come eseguire lo streaming live con codificatori locali mediante .NET | Microsoft Docs
description: Questo argomento illustra come usare .NET per eseguire la codifica live con codificatori in locale.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 15908152-d23c-4d55-906a-3bfd74927db5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/18/2017
ms.author: cenkdin;juliako
ms.openlocfilehash: 3ef6065f5b9e05e0ea5716548699943a2c877bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-net"></a><span data-ttu-id="b6304-103">Come eseguire lo streaming live con codificatori locali mediante .NET</span><span class="sxs-lookup"><span data-stu-id="b6304-103">How to perform live streaming with on-premises encoders using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6304-104">Portale</span><span class="sxs-lookup"><span data-stu-id="b6304-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="b6304-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b6304-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="b6304-106">REST</span><span class="sxs-lookup"><span data-stu-id="b6304-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="b6304-107">Questa esercitazione illustra come usare l'SDK di Servizi multimediali di Azure per .NET per creare un **canale** configurato per la distribuzione pass-through.</span><span class="sxs-lookup"><span data-stu-id="b6304-107">This tutorial walks you through the steps of using the Azure Media Services .NET SDK to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b6304-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b6304-108">Prerequisites</span></span>
<span data-ttu-id="b6304-109">Per completare l'esercitazione è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b6304-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="b6304-110">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="b6304-110">An Azure account.</span></span>
* <span data-ttu-id="b6304-111">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b6304-111">A Media Services account.</span></span>    <span data-ttu-id="b6304-112">Per creare un account Servizi multimediali, vedere [Creare un account Servizi multimediali di Azure con il portale di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b6304-112">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="b6304-113">Configurare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="b6304-113">Set up your dev environment.</span></span> <span data-ttu-id="b6304-114">Per ulteriori informazioni, vedere [Configurare l'ambiente](media-services-set-up-computer.md).</span><span class="sxs-lookup"><span data-stu-id="b6304-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span></span>
* <span data-ttu-id="b6304-115">Una webcam.</span><span class="sxs-lookup"><span data-stu-id="b6304-115">A webcam.</span></span> <span data-ttu-id="b6304-116">Ad esempio, [codificatore Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="b6304-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="b6304-117">È consigliabile esaminare i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="b6304-117">Recommended to review the following articles:</span></span>

* [<span data-ttu-id="b6304-118">Codificatori live e supporto RTMP di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="b6304-118">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="b6304-119">Streaming live con codificatori locali che creano flussi a bitrate multipli</span><span class="sxs-lookup"><span data-stu-id="b6304-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b6304-120">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b6304-120">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="b6304-121">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b6304-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="example"></a><span data-ttu-id="b6304-122">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6304-122">Example</span></span>
<span data-ttu-id="b6304-123">Il seguente esempio di codice illustra come ottenere le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6304-123">The following code example demonstrates how to achieve the following tasks:</span></span>

* <span data-ttu-id="b6304-124">Connettersi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b6304-124">Connect to Media Services</span></span>
* <span data-ttu-id="b6304-125">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="b6304-125">Create a channel</span></span>
* <span data-ttu-id="b6304-126">Aggiornare il canale</span><span class="sxs-lookup"><span data-stu-id="b6304-126">Update the channel</span></span>
* <span data-ttu-id="b6304-127">Recuperare l'endpoint di input del canale.</span><span class="sxs-lookup"><span data-stu-id="b6304-127">Retrieve the channel’s input endpoint.</span></span> <span data-ttu-id="b6304-128">È necessario fornire l'endpoint di input al codificatore live locale.</span><span class="sxs-lookup"><span data-stu-id="b6304-128">The input endpoint should be provided to the on-premises live encoder.</span></span> <span data-ttu-id="b6304-129">Il codificatore live converte i segnali dalla fotocamera ai flussi che vengono inviati all'endpoint di input del canale (inserimento).</span><span class="sxs-lookup"><span data-stu-id="b6304-129">The live encoder converts signals from the camera to streams that are sent to the channel’s input (ingest) endpoint.</span></span>
* <span data-ttu-id="b6304-130">Recuperare l'endpoint di anteprima del canale</span><span class="sxs-lookup"><span data-stu-id="b6304-130">Retrieve the channel’s preview endpoint</span></span>
* <span data-ttu-id="b6304-131">Creare e avviare un programma</span><span class="sxs-lookup"><span data-stu-id="b6304-131">Create and start a program</span></span>
* <span data-ttu-id="b6304-132">Creare un localizzatore necessario per accedere al programma</span><span class="sxs-lookup"><span data-stu-id="b6304-132">Create a locator needed to access the program</span></span>
* <span data-ttu-id="b6304-133">Creare e avviare uno StreamingEndpoint</span><span class="sxs-lookup"><span data-stu-id="b6304-133">Create and start a StreamingEndpoint</span></span>
* <span data-ttu-id="b6304-134">Aggiornare l'endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="b6304-134">Update the streaming endpoint</span></span>
* <span data-ttu-id="b6304-135">Arresto delle risorse</span><span class="sxs-lookup"><span data-stu-id="b6304-135">Shut down resources</span></span>

>[!IMPORTANT]
><span data-ttu-id="b6304-136">Verificare che l'endpoint di streaming da cui si vuole trasmettere il contenuto sia nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="b6304-136">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
>[!NOTE]
><span data-ttu-id="b6304-137">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="b6304-137">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="b6304-138">Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento).</span><span class="sxs-lookup"><span data-stu-id="b6304-138">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="b6304-139">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="b6304-139">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="b6304-140">Per informazioni su come configurare un codificatore live, vedere [Codificatori live e supporto RTMP di Servizi multimediali di Azure](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span><span class="sxs-lookup"><span data-stu-id="b6304-140">For information on how to configure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Net;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSLiveTest
    {
        class Program
        {
        private const string StreamingEndpointName = "streamingendpoint001";
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

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

            IChannel channel = CreateAndStartChannel();

            // Set the Live Encoder to point to the channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            // Use the previewEndpoint to preview and verify
            // that the input from the encoder is actually reaching the Channel.
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            IProgram program = CreateAndStartProgram(channel);
            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);
            IStreamingEndpoint streamingEndpoint = CreateAndStartStreamingEndpoint(false);

            // Once you are done streaming, clean up your resources.
            Cleanup(streamingEndpoint, channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            //If you want to change the Smooth fragments to HLS segment ratio, you would set the ChannelCreationOptions’s Output property.

            IChannel channel = _context.Channels.Create(
            new ChannelCreationOptions
            {
            Name = ChannelName,
            Input = CreateChannelInput(),
            Preview = CreateChannelPreview()
            });

            //Starting and stopping Channels can take some time to execute. To determine the state of operations after calling Start or Stop, query the IChannel.State .

            channel.Start();

            return channel;
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
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access to IP addresses.
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
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access to IP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForChannel(IChannel channel)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            channel.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            channel.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            channel.Update();
        }

        public static IProgram CreateAndStartProgram(IChannel channel)
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            // Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
            // however each Program must have a unique name within your Media Services account.
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            program.Start();

            return program;
        }

        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            

            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                "Live Stream Policy",
                ArchiveWindowLength,
                AccessPermissions.Read
                )
            );

            return locator;
        }

        public static IStreamingEndpoint CreateAndStartStreamingEndpoint(bool createNew)
        {
            IStreamingEndpoint streamingEndpoint = null;
            if (createNew)
            {
            var options = new StreamingEndpointCreationOptions
            {
                Name = StreamingEndpointName,
                ScaleUnits = 1,
                AccessControl = GetAccessControl(),
                CacheControl = GetCacheControl()
            };

            streamingEndpoint = _context.StreamingEndpoints.Create(options);
            }
            else
            {
            streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            }


            if (streamingEndpoint.State == StreamingEndpointState.Stopped)
            streamingEndpoint.Start();

            return streamingEndpoint;
        }

        private static StreamingEndpointAccessControl GetAccessControl()
        {
            return new StreamingEndpointAccessControl
            {
            IPAllowList = new List<IPRange>
                {
                new IPRange
                {
                    Name = "Allow all",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                }
                },

            AkamaiSignatureHeaderAuthenticationKeyList = new List<AkamaiSignatureHeaderAuthenticationKey>
                {
                new AkamaiSignatureHeaderAuthenticationKey
                {
                    Identifier = "My key",
                    Expiration = DateTime.UtcNow + TimeSpan.FromDays(365),
                    Base64Key = Convert.ToBase64String(GenerateRandomBytes(16))
                }
                }
            };
        }

        private static byte[] GenerateRandomBytes(int length)
        {
            var bytes = new byte[length];
            using (var rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(bytes);
            }

            return bytes;
        }

        private static StreamingEndpointCacheControl GetCacheControl()
        {
            return new StreamingEndpointCacheControl
            {
            MaxAge = TimeSpan.FromSeconds(1000)
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            streamingEndpoint.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            streamingEndpoint.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            streamingEndpoint.Update();
        }

        public static void Cleanup(IStreamingEndpoint streamingEndpoint,
                        IChannel channel)
        {
            if (streamingEndpoint != null)
            {
            streamingEndpoint.Stop();
            if(streamingEndpoint.Name != "default")
                streamingEndpoint.Delete();
            }

            IAsset asset;
            if (channel != null)
            {

            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                program.Stop();
                program.Delete();

                if (asset != null)
                {
                foreach (var l in asset.Locators)
                    l.Delete();

                asset.Delete();
                }
            }

            channel.Stop();
            channel.Delete();
            }
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="b6304-141">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="b6304-141">Next Step</span></span>
<span data-ttu-id="b6304-142">Analizzare i percorsi di apprendimento dei Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b6304-142">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b6304-143">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b6304-143">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

