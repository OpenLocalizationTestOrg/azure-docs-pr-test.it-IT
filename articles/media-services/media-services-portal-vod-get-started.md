---
title: Introduzione alla distribuzione di VOD tramite il portale di Azure | Documentazione Microsoft
description: Questa esercitazione illustra il processo di implementazione di un servizio per la distribuzione di contenuto video on demand (VoD) di base con l'applicazione Servizi multimediali di Azure (AMS) usando il portale di Azure.
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
ms.openlocfilehash: a8eeeeff412837acba14b441a3c590edf7e3597a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-the-azure-portal"></a><span data-ttu-id="d0e08-103">Introduzione alla distribuzione di contenuto su richiesta tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d0e08-103">Get started with delivering content on demand using the Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="d0e08-104">Questa esercitazione illustra il processo di implementazione di un servizio per la distribuzione di contenuto video on demand (VoD) di base con l'applicazione Servizi multimediali di Azure (AMS) usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e08-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0e08-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d0e08-105">Prerequisites</span></span>
<span data-ttu-id="d0e08-106">Per completare l'esercitazione è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d0e08-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="d0e08-107">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e08-107">An Azure account.</span></span> <span data-ttu-id="d0e08-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0e08-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="d0e08-109">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d0e08-109">A Media Services account.</span></span> <span data-ttu-id="d0e08-110">Per creare un account Servizi multimediali, vedere [Creare un account Servizi multimediali di Azure con il portale di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d0e08-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="d0e08-111">Questa esercitazione include le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0e08-111">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="d0e08-112">Avviare l'endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e08-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="d0e08-113">Caricare un file video.</span><span class="sxs-lookup"><span data-stu-id="d0e08-113">Upload a video file.</span></span>
3. <span data-ttu-id="d0e08-114">Codificare il file di origine in un set di file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="d0e08-114">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="d0e08-115">Pubblicare l'asset e ottenere gli URL di streaming e di download progressivo.</span><span class="sxs-lookup"><span data-stu-id="d0e08-115">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="d0e08-116">Riprodurre i contenuti.</span><span class="sxs-lookup"><span data-stu-id="d0e08-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="d0e08-117">Avviare gli endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="d0e08-117">Start streaming endpoints</span></span> 

<span data-ttu-id="d0e08-118">Uno degli scenari più frequenti dell'uso di Servizi multimediali di Azure riguarda la distribuzione di contenuto video in streaming a bitrate adattivo.</span><span class="sxs-lookup"><span data-stu-id="d0e08-118">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="d0e08-119">Servizi multimediali include la funzionalità per la creazione dinamica dei pacchetti, che consente di distribuire contenuto con codifica MP4 a bitrate adattivo nei formati supportati da Servizi multimediali, come MPEG DASH, HLS e Smooth Streaming in modalità JIT, senza dover archiviare le versioni predefinite di ognuno di questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e08-119">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="d0e08-120">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-120">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="d0e08-121">Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-121">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="d0e08-122">Per avviare l'endpoint di streaming, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="d0e08-122">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="d0e08-123">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d0e08-123">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d0e08-124">Nella finestra Impostazioni fare clic su Endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e08-124">In the Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="d0e08-125">Fare clic sull'endpoint di streaming predefinito.</span><span class="sxs-lookup"><span data-stu-id="d0e08-125">Click the default streaming endpoint.</span></span> 

    <span data-ttu-id="d0e08-126">Verrà visualizzata la finestra DETTAGLI ENDPOINT DI STREAMING PREDEFINITO.</span><span class="sxs-lookup"><span data-stu-id="d0e08-126">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="d0e08-127">Fare clic sull'icona di avvio.</span><span class="sxs-lookup"><span data-stu-id="d0e08-127">Click the Start icon.</span></span>
5. <span data-ttu-id="d0e08-128">Fare clic sul pulsante Salva per salvare le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="d0e08-128">Click the Save button to save your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="d0e08-129">Caricare file</span><span class="sxs-lookup"><span data-stu-id="d0e08-129">Upload files</span></span>
<span data-ttu-id="d0e08-130">Per riprodurre video in streaming con Servizi multimediali di Azure, è necessario caricare i video di origine, codificarli in bitrate multipli e pubblicare il risultato.</span><span class="sxs-lookup"><span data-stu-id="d0e08-130">To stream videos using Azure Media Services, you need to upload the source videos, encode them into multiple bitrates, and publish the result.</span></span> <span data-ttu-id="d0e08-131">Il primo passaggio è illustrato in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d0e08-131">The first step is covered in this section.</span></span> 

1. <span data-ttu-id="d0e08-132">Nella finestra **Impostazione** fare clic su **Asset**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-132">In the **Setting** window, click **Assets**.</span></span>
   
    ![Caricare file](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="d0e08-134">Fare clic sul pulsante **Upload** .</span><span class="sxs-lookup"><span data-stu-id="d0e08-134">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="d0e08-135">Verrà visualizzata la finestra **Carica un asset video** .</span><span class="sxs-lookup"><span data-stu-id="d0e08-135">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d0e08-136">Non esistono limiti alle dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="d0e08-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="d0e08-137">Passare al video desiderato nel computer locale, selezionarlo e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="d0e08-137">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="d0e08-138">Il caricamento viene avviato ed è possibile visualizzare l'avanzamento sotto il nome del file.</span><span class="sxs-lookup"><span data-stu-id="d0e08-138">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="d0e08-139">Al termine del caricamento, il nuovo asset viene visualizzato nella finestra **Asset** .</span><span class="sxs-lookup"><span data-stu-id="d0e08-139">Once the upload completes, you see the new asset listed in the **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="d0e08-140">Codificare gli asset</span><span class="sxs-lookup"><span data-stu-id="d0e08-140">Encode assets</span></span>

<span data-ttu-id="d0e08-141">Quando si usa Servizi multimediali di Azure, uno degli scenari più frequenti consiste nella distribuzione di contenuti in streaming a velocità in bit adattiva ai client.</span><span class="sxs-lookup"><span data-stu-id="d0e08-141">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="d0e08-142">Servizi multimediali supporta le tecnologie di streaming a bitrate adattivo seguenti: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="d0e08-142">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="d0e08-143">Per preparare i video per lo streaming a bitrate adattivo, è necessario codificare il video di origine in file a più bitrate.</span><span class="sxs-lookup"><span data-stu-id="d0e08-143">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="d0e08-144">Per codificare i video, è consigliabile usare il codificatore **Media Encoder Standard** .</span><span class="sxs-lookup"><span data-stu-id="d0e08-144">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="d0e08-145">Servizi multimediali include la funzionalità per la creazione dinamica dei pacchetti, che consente di distribuire file MP4 a bitrate multipli nei formati MPEG DASH, HLS e Smooth Streaming, senza dover ricreare i pacchetti con questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e08-145">Media Services also provides dynamic packaging, which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to repackage into these streaming formats.</span></span> <span data-ttu-id="d0e08-146">Con la creazione dinamica dei pacchetti si archiviano e si pagano solo i file in un singolo formato di archiviazione e Servizi multimediali crea e fornisce la risposta appropriata in base alle richieste di un client.</span><span class="sxs-lookup"><span data-stu-id="d0e08-146">With dynamic packaging, you only need to store and pay for the files in single storage format and Media Services builds and serves the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="d0e08-147">Per sfruttare i vantaggi della creazione dinamica dei pacchetti, è necessario codificare il file di origine in un set di file MP4 a bitrate multipli. La procedura per la codifica è descritta più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d0e08-147">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

### <a name="to-use-the-portal-to-encode"></a><span data-ttu-id="d0e08-148">Per usare il portale per la codifica</span><span class="sxs-lookup"><span data-stu-id="d0e08-148">To use the portal to encode</span></span>
<span data-ttu-id="d0e08-149">Questa sezione descrive la procedura per la codifica di contenuti con Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="d0e08-149">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="d0e08-150">Nella finestra **Impostazioni** selezionare **Asset**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-150">In the **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="d0e08-151">Nella finestra **Asset** selezionare la risorsa che si vuole codificare.</span><span class="sxs-lookup"><span data-stu-id="d0e08-151">In the **Assets** window, select the asset that you would like to encode.</span></span>
3. <span data-ttu-id="d0e08-152">Fare clic sul pulsante **Codifica** .</span><span class="sxs-lookup"><span data-stu-id="d0e08-152">Press the **Encode** button.</span></span>
4. <span data-ttu-id="d0e08-153">Nella finestra **Codifica un asset** selezionare il processore "Media Encoder Standard" e un set di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d0e08-153">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="d0e08-154">Per informazioni sui set di impostazioni, vedere [Generare automaticamente un bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) e [Set di impostazioni delle attività MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0e08-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="d0e08-155">Se si prevede di controllare il set di impostazioni di codifica usato, tenere presente che è importante selezionare il set di impostazioni più appropriato per il video di input.</span><span class="sxs-lookup"><span data-stu-id="d0e08-155">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="d0e08-156">Ad esempio, se è noto che il video di input ha una risoluzione di 1920x1080 pixel, è possibile usare il set di impostazioni "Codec video H.264 a bitrate multiplo con risoluzione 1080p".</span><span class="sxs-lookup"><span data-stu-id="d0e08-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="d0e08-157">Se il video disponibile è a bassa risoluzione (640x360), non usare il set di impostazioni "Codec video H.264 a bitrate multiplo con risoluzione 1080p".</span><span class="sxs-lookup"><span data-stu-id="d0e08-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="d0e08-158">Per una gestione più semplice, è possibile modificare il nome dell'asset di output e il nome del processo.</span><span class="sxs-lookup"><span data-stu-id="d0e08-158">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Codificare gli asset](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="d0e08-160">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="d0e08-161">Monitorare lo stato del processo di codifica</span><span class="sxs-lookup"><span data-stu-id="d0e08-161">Monitor encoding job progress</span></span>
<span data-ttu-id="d0e08-162">Per monitorare l'avanzamento del processo di codifica, fare clic su **Impostazioni** nella parte superiore della pagina e selezionare **Processi**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-162">To monitor the progress of the encoding job, click **Settings** (at the top of the page) and then select **Jobs**.</span></span>

![Processi](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="d0e08-164">Pubblicare contenuti</span><span class="sxs-lookup"><span data-stu-id="d0e08-164">Publish content</span></span>
<span data-ttu-id="d0e08-165">Perché l'utente possa avere a disposizione un URL da usare per scaricare o riprodurre in streaming i contenuti, è prima necessario "pubblicare" un asset creando un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="d0e08-165">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="d0e08-166">I localizzatori forniscono l'accesso ai file contenuti nell'asset.</span><span class="sxs-lookup"><span data-stu-id="d0e08-166">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="d0e08-167">Servizi multimediali supporta due tipi di localizzatori:</span><span class="sxs-lookup"><span data-stu-id="d0e08-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="d0e08-168">Localizzatori di streaming (OnDemandOrigin) usati per lo streaming adattivo, ad esempio per riprodurre in streaming file MPEG DASH, HLS o Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e08-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="d0e08-169">Per creare un localizzatore di streaming, l'asset deve contenere un file con estensione ISM.</span><span class="sxs-lookup"><span data-stu-id="d0e08-169">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="d0e08-170">Localizzatori progressivi (SAS) usati per la distribuzione di video tramite download progressivo.</span><span class="sxs-lookup"><span data-stu-id="d0e08-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="d0e08-171">Un URL di streaming presenta il formato seguente e può essere usato per riprodurre asset Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e08-171">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="d0e08-172">Per creare un URL di streaming HLS, aggiungere (format=m3u8-aapl) all'URL.</span><span class="sxs-lookup"><span data-stu-id="d0e08-172">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="d0e08-173">Per creare un URL di streaming MPEG DASH, aggiungere (format=mpd-time-csf) all'URL.</span><span class="sxs-lookup"><span data-stu-id="d0e08-173">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="d0e08-174">Un URL di firma di accesso condiviso ha il formato seguente.</span><span class="sxs-lookup"><span data-stu-id="d0e08-174">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="d0e08-175">I localizzatori creati attraverso il portale prima del mese di marzo 2015 hanno una validità di due anni.</span><span class="sxs-lookup"><span data-stu-id="d0e08-175">If you used the portal to create locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="d0e08-176">Per aggiornare la data di scadenza di un localizzatore, è possibile usare le API [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="d0e08-176">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="d0e08-177">Quando si aggiorna la data di scadenza di un localizzatore di firma di accesso condiviso, l'URL viene modificato.</span><span class="sxs-lookup"><span data-stu-id="d0e08-177">When you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="d0e08-178">Per usare il portale per la pubblicazione di un asset</span><span class="sxs-lookup"><span data-stu-id="d0e08-178">To use the portal to publish an asset</span></span>
<span data-ttu-id="d0e08-179">Per pubblicare un asset tramite il portale, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d0e08-179">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="d0e08-180">Selezionare **Impostazioni** > **Asset**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="d0e08-181">Selezionare l'asset da pubblicare.</span><span class="sxs-lookup"><span data-stu-id="d0e08-181">Select the asset that you want to publish.</span></span>
3. <span data-ttu-id="d0e08-182">Fare clic sul pulsante **Pubblica** .</span><span class="sxs-lookup"><span data-stu-id="d0e08-182">Click the **Publish** button.</span></span>
4. <span data-ttu-id="d0e08-183">Selezionare il tipo di localizzatore.</span><span class="sxs-lookup"><span data-stu-id="d0e08-183">Select the locator type.</span></span>
5. <span data-ttu-id="d0e08-184">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-184">Press **Add**.</span></span>
   
    ![Pubblica](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="d0e08-186">L'URL viene aggiunto all'elenco di **URL pubblicati**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-186">The URL is added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="d0e08-187">Riprodurre contenuti dal portale</span><span class="sxs-lookup"><span data-stu-id="d0e08-187">Play content from the portal</span></span>
<span data-ttu-id="d0e08-188">Il portale di Azure fornisce un lettore di contenuti che può essere usato per testare il proprio video.</span><span class="sxs-lookup"><span data-stu-id="d0e08-188">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="d0e08-189">Fare clic sul video richiesto e quindi sul pulsante **Riproduci** .</span><span class="sxs-lookup"><span data-stu-id="d0e08-189">Click the desired video and then click the **Play** button.</span></span>

![Pubblica](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="d0e08-191">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="d0e08-191">Some considerations apply:</span></span>

* <span data-ttu-id="d0e08-192">Per avviare lo streaming, avviare l'esecuzione dell'endpoint di streaming **predefinito**.</span><span class="sxs-lookup"><span data-stu-id="d0e08-192">To begin streaming, start running the **default** streaming endpoint.</span></span>
* <span data-ttu-id="d0e08-193">Verificare che il video sia stato pubblicato.</span><span class="sxs-lookup"><span data-stu-id="d0e08-193">Make sure the video has been published.</span></span>
* <span data-ttu-id="d0e08-194">**Media Player** esegue la riproduzione dall'endpoint di streaming predefinito.</span><span class="sxs-lookup"><span data-stu-id="d0e08-194">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="d0e08-195">Se si vuole eseguire la riproduzione da un endpoint di streaming diverso, fare clic per copiare l'URL e usare un altro lettore,</span><span class="sxs-lookup"><span data-stu-id="d0e08-195">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="d0e08-196">ad esempio [Lettore di Servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d0e08-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0e08-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0e08-197">Next steps</span></span>
<span data-ttu-id="d0e08-198">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d0e08-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d0e08-199">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d0e08-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

