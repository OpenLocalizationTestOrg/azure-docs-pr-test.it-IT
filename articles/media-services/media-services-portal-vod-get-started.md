---
title: aaaGet avviato con recapito tramite il portale di Azure hello VoD | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello dell'implementazione di un servizio di distribuzione di contenuti video on Demand (VoD) base con l'applicazione di servizi multimediali di Azure (AMS) utilizzando hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="963b0-103">Iniziare con la distribuzione di contenuti su richiesta utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="963b0-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="963b0-104">In questa esercitazione vengono illustrati i passaggi hello dell'implementazione di un servizio di distribuzione di contenuti video on Demand (VoD) base con l'applicazione di servizi multimediali di Azure (AMS) utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="963b0-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="963b0-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="963b0-105">Prerequisites</span></span>
<span data-ttu-id="963b0-106">di seguito Hello sono esercitazione hello toocomplete necessarie:</span><span class="sxs-lookup"><span data-stu-id="963b0-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="963b0-107">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="963b0-107">An Azure account.</span></span> <span data-ttu-id="963b0-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="963b0-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="963b0-109">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="963b0-109">A Media Services account.</span></span> <span data-ttu-id="963b0-110">toocreate un account di servizi multimediali, vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="963b0-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="963b0-111">In questa esercitazione include hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="963b0-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="963b0-112">Avviare l'endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="963b0-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="963b0-113">Caricare un file video.</span><span class="sxs-lookup"><span data-stu-id="963b0-113">Upload a video file.</span></span>
3. <span data-ttu-id="963b0-114">Codificare il file di origine hello in un set di file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="963b0-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="963b0-115">Pubblicare l'asset hello e get streaming e l'URL di download progressivo.</span><span class="sxs-lookup"><span data-stu-id="963b0-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="963b0-116">Riprodurre i contenuti.</span><span class="sxs-lookup"><span data-stu-id="963b0-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="963b0-117">Avviare gli endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="963b0-117">Start streaming endpoints</span></span> 

<span data-ttu-id="963b0-118">Quando si lavora con uno degli scenari più comuni di hello recapita video tramite velocità in bit adattive servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="963b0-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="963b0-119">Servizi multimediali fornisce creazione dinamica dei pacchetti, che consente di toodeliver la velocità in bit adattiva contenuto MP4 in formato con codificata in streaming formati supportati da servizi multimediali (MPEG DASH, HLS, Smooth Streaming) just-in-time, senza che sia necessario toostore preconfezionata versioni di ciascuno di questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="963b0-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="963b0-120">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="963b0-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="963b0-121">lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="963b0-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="963b0-122">toostart hello endpoint di streaming, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="963b0-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="963b0-123">Accedere all'indirizzo hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="963b0-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="963b0-124">Nella finestra Impostazioni hello, fare clic su endpoint di Streaming.</span><span class="sxs-lookup"><span data-stu-id="963b0-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="963b0-125">Fare clic su predefinito hello endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="963b0-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="963b0-126">verrà visualizzata la finestra Dettagli dell'ENDPOINT di STREAMING predefinito Hello.</span><span class="sxs-lookup"><span data-stu-id="963b0-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="963b0-127">Fare clic sull'icona di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="963b0-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="963b0-128">Fare clic su toosave pulsante di hello Salva le modifiche.</span><span class="sxs-lookup"><span data-stu-id="963b0-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="963b0-129">Caricare file</span><span class="sxs-lookup"><span data-stu-id="963b0-129">Upload files</span></span>
<span data-ttu-id="963b0-130">toostream video tramite servizi multimediali di Azure, è necessario video di origine tooupload hello, codificarli in più velocità in bit e pubblicare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="963b0-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="963b0-131">in questa sezione verrà illustrata innanzitutto Hello.</span><span class="sxs-lookup"><span data-stu-id="963b0-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="963b0-132">In hello **impostazione** finestra, fare clic su **asset**.</span><span class="sxs-lookup"><span data-stu-id="963b0-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![Caricare file](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="963b0-134">Fare clic su hello **caricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="963b0-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="963b0-135">Hello **caricare una risorsa video** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="963b0-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="963b0-136">Non esistono limiti alle dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="963b0-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="963b0-137">Sfoglia video toohello desiderato nel computer in uso, selezionarlo e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="963b0-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="963b0-138">Avvia il caricamento di Hello ed è possibile visualizzare lo stato di avanzamento hello in nome file hello.</span><span class="sxs-lookup"><span data-stu-id="963b0-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="963b0-139">Una volta completato il caricamento di hello, viene visualizzato di nuovo asset hello elencati in hello **asset** finestra.</span><span class="sxs-lookup"><span data-stu-id="963b0-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="963b0-140">Codificare gli asset</span><span class="sxs-lookup"><span data-stu-id="963b0-140">Encode assets</span></span>

<span data-ttu-id="963b0-141">Quando si lavora con servizi multimediali di Azure offre uno degli scenari più comuni di hello client tooyour streaming velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="963b0-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="963b0-142">Servizi multimediali supporta hello velocità in bit adattive tecnologie seguente: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="963b0-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="963b0-143">tooprepare i video per lo streaming a velocità in bit adattiva, è necessario tooencode l'origine video in file più velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="963b0-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="963b0-144">È consigliabile utilizzare hello **Media Encoder Standard** tooencode codificatore video.</span><span class="sxs-lookup"><span data-stu-id="963b0-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="963b0-145">Servizi multimediali offre anche creazione dinamica dei pacchetti, che consente di toodeliver MP4s l'asset MP4 in hello seguenti formati di streaming: MPEG DASH, HLS, Smooth Streaming, senza che sia necessario toorepackage in questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="963b0-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="963b0-146">Con creazione dinamica dei pacchetti, è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali di compilazioni e opera in base alle richieste da un client la risposta appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="963b0-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="963b0-147">Il vantaggio di tootake creazione dinamica dei pacchetti, è necessario tooencode il file di origine in un set di file MP4 a più velocità in bit (hello codifica passaggi sono illustrati più avanti in questa sezione).</span><span class="sxs-lookup"><span data-stu-id="963b0-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="963b0-148">toouse hello portale tooencode</span><span class="sxs-lookup"><span data-stu-id="963b0-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="963b0-149">In questa sezione descrive i passaggi di hello è possibile eseguire tooencode il contenuto con Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="963b0-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="963b0-150">In hello **impostazioni** selezionare **asset**.</span><span class="sxs-lookup"><span data-stu-id="963b0-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="963b0-151">In hello **asset** finestra, che si desidera tooencode asset di hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="963b0-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="963b0-152">Hello premere **Encode** pulsante.</span><span class="sxs-lookup"><span data-stu-id="963b0-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="963b0-153">In hello **codificare un asset** finestra e processore "Media Encoder Standard" hello selezionare un set di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="963b0-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="963b0-154">Per informazioni sui set di impostazioni, vedere [Generare automaticamente un bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) e [Set di impostazioni delle attività MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="963b0-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="963b0-155">Se si prevede di toocontrol viene utilizzato il set di impostazioni di codifica, questo tenere presenti: è importante hello tooselect set di impostazioni che è più appropriato per il video di input.</span><span class="sxs-lookup"><span data-stu-id="963b0-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="963b0-156">Ad esempio, se si conosce il video di input dispone di una risoluzione di 1920x1080 pixel, è possibile utilizzare hello "H264 bitrate multiplo con risoluzione 1080p" predefinito.</span><span class="sxs-lookup"><span data-stu-id="963b0-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="963b0-157">Se il video disponibile è a bassa risoluzione (640x360), non usare il set di impostazioni "Codec video H.264 a bitrate multiplo con risoluzione 1080p".</span><span class="sxs-lookup"><span data-stu-id="963b0-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="963b0-158">Per facilitare la gestione, è un'opzione di modifica nome hello dell'asset di output di hello e nome hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="963b0-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Codificare gli asset](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="963b0-160">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="963b0-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="963b0-161">Monitorare lo stato del processo di codifica</span><span class="sxs-lookup"><span data-stu-id="963b0-161">Monitor encoding job progress</span></span>
<span data-ttu-id="963b0-162">lo stato di avanzamento di toomonitor hello di hello codifica processo, fare clic su **impostazioni** (in alto hello hello pagina) e quindi selezionare **processi**.</span><span class="sxs-lookup"><span data-stu-id="963b0-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![Processi](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="963b0-164">Pubblicare contenuti</span><span class="sxs-lookup"><span data-stu-id="963b0-164">Publish content</span></span>
<span data-ttu-id="963b0-165">tooprovide l'utente con un URL che possa essere utilizzati toostream o scaricare il contenuto, è innanzitutto necessario troppo "pubblica" l'asset creando un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="963b0-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="963b0-166">I localizzatori forniscono accesso toofiles contenuti in hello asset.</span><span class="sxs-lookup"><span data-stu-id="963b0-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="963b0-167">Servizi multimediali supporta due tipi di localizzatori:</span><span class="sxs-lookup"><span data-stu-id="963b0-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="963b0-168">Streaming localizzatori (OnDemandOrigin) usati per streaming adattivo (ad esempio, toostream MPEG DASH, HLS o Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="963b0-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="963b0-169">toocreate un localizzatore di streaming dell'asset deve contenere un file con estensione ISM.</span><span class="sxs-lookup"><span data-stu-id="963b0-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="963b0-170">Localizzatori progressivi (SAS) usati per la distribuzione di video tramite download progressivo.</span><span class="sxs-lookup"><span data-stu-id="963b0-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="963b0-171">È possibile utilizzare asset Smooth Streaming tooplay un URL di streaming ha hello seguente formato.</span><span class="sxs-lookup"><span data-stu-id="963b0-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="963b0-172">aggiungere toobuild un URL di streaming HLS (formato = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="963b0-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="963b0-173">aggiungere toobuild un URL di streaming di contenuto MPEG DASH (formato = mpd-tempo-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="963b0-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="963b0-174">Un URL SAS è hello seguente formato.</span><span class="sxs-lookup"><span data-stu-id="963b0-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="963b0-175">Se si utilizza i localizzatori toocreate portale hello prima marzo 2015, sono stati creati i localizzatori con una data di scadenza di due anni.</span><span class="sxs-lookup"><span data-stu-id="963b0-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="963b0-176">tooupdate data di scadenza su un indicatore di posizione, utilizzare [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API.</span><span class="sxs-lookup"><span data-stu-id="963b0-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="963b0-177">Quando si aggiorna la data di scadenza hello di un localizzatore SAS, hello URL cambia.</span><span class="sxs-lookup"><span data-stu-id="963b0-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="963b0-178">toouse hello portale toopublish un asset</span><span class="sxs-lookup"><span data-stu-id="963b0-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="963b0-179">toouse hello portale toopublish un asset, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="963b0-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="963b0-180">Selezionare **Impostazioni** > **Asset**.</span><span class="sxs-lookup"><span data-stu-id="963b0-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="963b0-181">Selezionare asset hello che si desidera toopublish.</span><span class="sxs-lookup"><span data-stu-id="963b0-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="963b0-182">Fare clic su hello **pubblica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="963b0-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="963b0-183">Selezionare il tipo di localizzatore hello.</span><span class="sxs-lookup"><span data-stu-id="963b0-183">Select hello locator type.</span></span>
5. <span data-ttu-id="963b0-184">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="963b0-184">Press **Add**.</span></span>
   
    ![Pubblica](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="963b0-186">URL di Hello viene aggiunto l'elenco toohello di **URL pubblicato**.</span><span class="sxs-lookup"><span data-stu-id="963b0-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="963b0-187">Riprodurre il contenuto dal portale hello</span><span class="sxs-lookup"><span data-stu-id="963b0-187">Play content from hello portal</span></span>
<span data-ttu-id="963b0-188">portale di Azure Hello fornisce un lettore di contenuti che è possibile utilizzare tootest video.</span><span class="sxs-lookup"><span data-stu-id="963b0-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="963b0-189">Fare clic su video hello desiderato e quindi fare clic su hello **riprodurre** pulsante.</span><span class="sxs-lookup"><span data-stu-id="963b0-189">Click hello desired video and then click hello **Play** button.</span></span>

![Pubblica](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="963b0-191">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="963b0-191">Some considerations apply:</span></span>

* <span data-ttu-id="963b0-192">toobegin streaming, avviare hello in esecuzione **predefinito** endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="963b0-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="963b0-193">Verificare che sia stato pubblicato hello video.</span><span class="sxs-lookup"><span data-stu-id="963b0-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="963b0-194">Questo **Media player** riprodotto dal valore predefinito di hello endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="963b0-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="963b0-195">Se si desidera tooplay da un valore non predefinito, endpoint di streaming fare clic su URL hello toocopy e usare un altro lettore.</span><span class="sxs-lookup"><span data-stu-id="963b0-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="963b0-196">ad esempio [Lettore di Servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="963b0-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="963b0-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="963b0-197">Next steps</span></span>
<span data-ttu-id="963b0-198">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="963b0-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="963b0-199">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="963b0-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

