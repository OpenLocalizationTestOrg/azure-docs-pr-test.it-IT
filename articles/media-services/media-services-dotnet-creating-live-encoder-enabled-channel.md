---
title: "aaaHow tooperform live streaming con flussi più velocità in bit toocreate di servizi multimediali di Azure .NET | Documenti Microsoft"
description: "Questa esercitazione percorsi sono illustrati i passaggi hello di creazione di un canale che riceve un flusso live a velocità in bit singola e lo codifica flusso a velocità in bit toomulti mediante .NET SDK."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22088e6a78a49bd839575614a7c17a411ae8081c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-net"></a><span data-ttu-id="1ff69-103">Come tooperform lo streaming live usando servizi multimediali di Azure toocreate più velocità in bit flussi con .NET</span><span class="sxs-lookup"><span data-stu-id="1ff69-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ff69-104">Portale</span><span class="sxs-lookup"><span data-stu-id="1ff69-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="1ff69-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1ff69-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="1ff69-106">API REST</span><span class="sxs-lookup"><span data-stu-id="1ff69-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="1ff69-107">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ff69-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="1ff69-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="1ff69-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="1ff69-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1ff69-109">Overview</span></span>
<span data-ttu-id="1ff69-110">In questa esercitazione illustra hello passaggi della creazione di un **canale** che riceve un flusso live a velocità in bit singola e lo codifica flusso toomulti velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="1ff69-110">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

<span data-ttu-id="1ff69-111">Per ulteriori informazioni teoriche tooChannels correlati che sono abilitati per la codifica live, vedere [Live streaming con flussi di servizi multimediali di Azure toocreate più velocità in bit](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="1ff69-111">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="1ff69-112">Scenario comune di streaming live</span><span class="sxs-lookup"><span data-stu-id="1ff69-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="1ff69-113">Hello alla procedura seguente vengono descritti le attività coinvolte nella creazione di applicazioni comuni di streaming in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="1ff69-113">hello following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="1ff69-114">Attualmente, hello max consigliata la durata di un evento in tempo reale è 8 ore.</span><span class="sxs-lookup"><span data-stu-id="1ff69-114">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="1ff69-115">Se è necessario un canale toorun per lunghi periodi di tempo, contattare amslived all'indirizzo Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="1ff69-115">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="1ff69-116">Connettere un computer tooa videocamera.</span><span class="sxs-lookup"><span data-stu-id="1ff69-116">Connect a video camera tooa computer.</span></span> <span data-ttu-id="1ff69-117">Avviare e configurare un codificatore live locale che può restituire un flusso a velocità in bit singola in uno dei seguenti protocolli hello: RTP (MPEG-TS), Smooth Streaming o RTMP.</span><span class="sxs-lookup"><span data-stu-id="1ff69-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="1ff69-118">Per altre informazioni, vedere l'argomento relativo a [codificatori live e supporto RTMP di Servizi multimediali di Azure](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="1ff69-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="1ff69-119">Questa operazione può essere eseguita anche dopo la creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="1ff69-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="1ff69-120">Creare e avviare un canale.</span><span class="sxs-lookup"><span data-stu-id="1ff69-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="1ff69-121">URL di inserimento recuperare hello del canale.</span><span class="sxs-lookup"><span data-stu-id="1ff69-121">Retrieve hello Channel ingest URL.</span></span>

    <span data-ttu-id="1ff69-122">URL di inserimento Hello viene utilizzato dal codificatore live di hello toosend hello flusso toohello canale.</span><span class="sxs-lookup"><span data-stu-id="1ff69-122">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>

4. <span data-ttu-id="1ff69-123">Recuperare l'URL di anteprima del canale hello.</span><span class="sxs-lookup"><span data-stu-id="1ff69-123">Retrieve hello Channel preview URL.</span></span>

    <span data-ttu-id="1ff69-124">Utilizzare questo tooverify URL che il canale riceve correttamente flusso live hello.</span><span class="sxs-lookup"><span data-stu-id="1ff69-124">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>

5. <span data-ttu-id="1ff69-125">Creare un asset.</span><span class="sxs-lookup"><span data-stu-id="1ff69-125">Create an asset.</span></span>
6. <span data-ttu-id="1ff69-126">Se si desidera per hello asset toobe crittografati in modo dinamico durante la riproduzione, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ff69-126">If you want for hello asset toobe dynamically encrypted during playback, do hello following:</span></span>
7. <span data-ttu-id="1ff69-127">Creare una chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="1ff69-127">Create a content key.</span></span>
8. <span data-ttu-id="1ff69-128">Configurare criteri di autorizzazione della chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="1ff69-128">Configure hello content key's authorization policy.</span></span>
9. <span data-ttu-id="1ff69-129">Configurare i criteri di distribuzione degli asset (usati per la creazione dinamica dei pacchetti e la crittografia dinamica).</span><span class="sxs-lookup"><span data-stu-id="1ff69-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="1ff69-130">Creare un programma e specificare asset hello toouse creato.</span><span class="sxs-lookup"><span data-stu-id="1ff69-130">Create a program and specify toouse hello asset that you created.</span></span>
11. <span data-ttu-id="1ff69-131">Pubblicare l'asset hello associata hello programma creando un localizzatore OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1ff69-131">Publish hello asset associated with hello program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="1ff69-132">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="1ff69-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="1ff69-133">endpoint da cui si desidera toostream contenuto di streaming Hello è toobe in hello **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="1ff69-133">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

12. <span data-ttu-id="1ff69-134">Avviare il programma di hello quando sei pronto toostart streaming e l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1ff69-134">Start hello program when you are ready toostart streaming and archiving.</span></span>
13. <span data-ttu-id="1ff69-135">Facoltativamente, codificatore live hello può essere segnalato toostart un annuncio.</span><span class="sxs-lookup"><span data-stu-id="1ff69-135">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="1ff69-136">annuncio Hello viene inserito nel flusso di output di hello.</span><span class="sxs-lookup"><span data-stu-id="1ff69-136">hello advertisement is inserted in hello output stream.</span></span>
14. <span data-ttu-id="1ff69-137">Arrestare il programma hello ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello.</span><span class="sxs-lookup"><span data-stu-id="1ff69-137">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span>
15. <span data-ttu-id="1ff69-138">Eliminare programma hello (e facoltativamente elimina hello asset).</span><span class="sxs-lookup"><span data-stu-id="1ff69-138">Delete hello Program (and optionally delete hello asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="1ff69-139">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1ff69-139">What you'll learn</span></span>
<span data-ttu-id="1ff69-140">In questo argomento illustra come tooexecute diverse operazioni su canali e i programmi usando Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="1ff69-140">This topic shows you how tooexecute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="1ff69-141">Poiché molte operazioni hanno un'esecuzione prolungata, vengono usate API .NET che gestiscono questo tipo di operazioni.</span><span class="sxs-lookup"><span data-stu-id="1ff69-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="1ff69-142">Hello argomento Mostra come segue hello toodo:</span><span class="sxs-lookup"><span data-stu-id="1ff69-142">hello topic shows how toodo hello following:</span></span>

1. <span data-ttu-id="1ff69-143">Creare e avviare un canale.</span><span class="sxs-lookup"><span data-stu-id="1ff69-143">Create and start a channel.</span></span> <span data-ttu-id="1ff69-144">Vengono usate API con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="1ff69-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="1ff69-145">Ottenere i canali hello inserimento (input) dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="1ff69-145">Get hello channels ingest (input) endpoint.</span></span> <span data-ttu-id="1ff69-146">Codificatore toohello che può inviare un flusso live a velocità in bit singola deve essere fornito da questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="1ff69-146">This endpoint should be provided toohello encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="1ff69-147">Ottenere l'endpoint di anteprima hello.</span><span class="sxs-lookup"><span data-stu-id="1ff69-147">Get hello preview endpoint.</span></span> <span data-ttu-id="1ff69-148">Questo endpoint viene utilizzato toopreview il flusso.</span><span class="sxs-lookup"><span data-stu-id="1ff69-148">This endpoint is used toopreview your stream.</span></span>
4. <span data-ttu-id="1ff69-149">Creare un asset che verrà utilizzato toostore il contenuto.</span><span class="sxs-lookup"><span data-stu-id="1ff69-149">Create an asset that will be used toostore your content.</span></span> <span data-ttu-id="1ff69-150">i criteri di distribuzione asset Hello devono essere configurati anche, come illustrato in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="1ff69-150">hello asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="1ff69-151">Creare un programma e specificare asset hello toouse creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1ff69-151">Create a program and specify toouse hello asset that was created earlier.</span></span> <span data-ttu-id="1ff69-152">Avviare il programma hello.</span><span class="sxs-lookup"><span data-stu-id="1ff69-152">Start hello program.</span></span> <span data-ttu-id="1ff69-153">Vengono usate API con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="1ff69-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="1ff69-154">Creare un localizzatore per hello asset, in modo che il contenuto di hello venga pubblicato e può essere trasmesso tooyour client.</span><span class="sxs-lookup"><span data-stu-id="1ff69-154">Create a locator for hello asset, so hello content gets published and can be streamed tooyour clients.</span></span>
7. <span data-ttu-id="1ff69-155">Mostrare e nascondere slate.</span><span class="sxs-lookup"><span data-stu-id="1ff69-155">Show and hide slates.</span></span> <span data-ttu-id="1ff69-156">Avviare e arrestare annunci.</span><span class="sxs-lookup"><span data-stu-id="1ff69-156">Start and stop advertisements.</span></span> <span data-ttu-id="1ff69-157">Vengono usate API con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="1ff69-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="1ff69-158">Pulire il canale e tutte le risorse associate di hello.</span><span class="sxs-lookup"><span data-stu-id="1ff69-158">Clean up your channel and all hello associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ff69-159">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1ff69-159">Prerequisites</span></span>
<span data-ttu-id="1ff69-160">di seguito Hello sono esercitazione hello toocomplete obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1ff69-160">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="1ff69-161">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="1ff69-161">An Azure account.</span></span> <span data-ttu-id="1ff69-162">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="1ff69-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1ff69-163">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="1ff69-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="1ff69-164">È possibile ottenere crediti che possono essere utilizzati tootry out a pagamento di servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ff69-164">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="1ff69-165">Anche dopo hello crediti, è possibile tenere conto di hello e utilizzare servizi di Azure gratuiti e funzionalità, ad esempio funzionalità di App Web hello in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1ff69-165">Even after hello credits are used up, you can keep hello account and use free Azure services and features, such as hello Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="1ff69-166">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1ff69-166">A Media Services account.</span></span> <span data-ttu-id="1ff69-167">toocreate un account di servizi multimediali, vedere [crea Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1ff69-167">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="1ff69-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, o Express) o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="1ff69-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="1ff69-169">È necessario usare Media Services .NET SDK versione 3.2.0.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1ff69-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="1ff69-170">Una webcam e un codificatore in grado di inviare un flusso live a velocità in bit singola.</span><span class="sxs-lookup"><span data-stu-id="1ff69-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="1ff69-171">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="1ff69-171">Considerations</span></span>
* <span data-ttu-id="1ff69-172">Attualmente, hello max consigliata la durata di un evento in tempo reale è 8 ore.</span><span class="sxs-lookup"><span data-stu-id="1ff69-172">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="1ff69-173">Se è necessario un canale toorun per lunghi periodi di tempo, contattare amslived all'indirizzo Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="1ff69-173">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="1ff69-174">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="1ff69-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="1ff69-175">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="1ff69-175">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="1ff69-176">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="1ff69-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="1ff69-177">Scaricare un esempio</span><span class="sxs-lookup"><span data-stu-id="1ff69-177">Download sample</span></span>

<span data-ttu-id="1ff69-178">È possibile scaricare l'esempio hello descritto in questo argomento da [qui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span><span class="sxs-lookup"><span data-stu-id="1ff69-178">You can download hello sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="1ff69-179">Configurare lo sviluppo con Media Services SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="1ff69-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="1ff69-180">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1ff69-180">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="1ff69-181">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="1ff69-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

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

            IChannel channel = CreateAndStartChannel();

            // hello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use hello previewEndpoint toopreview and verify 
            // that hello input from hello encoder is actually reaching hello Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of hello live feed as it reaches hello Channel. 
            // This can be a valuable tool toocheck whether your live feed is actually reaching hello Channel. 
            // hello thumbnail is exposed via hello same end-point as hello Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if hello channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
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

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
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

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set tooStreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order toobe able toopublish and stream hello video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
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

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with hello channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting tootrack ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, hello operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created entity Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello entity Id associated with hello sucessful operation is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle hello failure. 
                // For example, throw an exception. 
                // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="1ff69-182">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="1ff69-182">Next step</span></span>
<span data-ttu-id="1ff69-183">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1ff69-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1ff69-184">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1ff69-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


