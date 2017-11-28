---
title: flusso aaaLive con codificatori locali tramite il portale di Azure hello | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di creazione di un canale configurato per un'operazione di recapito pass-through.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="f1e6b-103">Come tooperform live streaming con locale codificatori utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f1e6b-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1e6b-104">Portale</span><span class="sxs-lookup"><span data-stu-id="f1e6b-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="f1e6b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f1e6b-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="f1e6b-106">REST</span><span class="sxs-lookup"><span data-stu-id="f1e6b-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="f1e6b-107">In questa esercitazione illustra i passaggi hello di hello toocreate portale Azure utilizzando un **canale** che è configurato per un'operazione di recapito pass-through.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f1e6b-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1e6b-108">Prerequisites</span></span>
<span data-ttu-id="f1e6b-109">di seguito Hello sono esercitazione hello toocomplete necessarie:</span><span class="sxs-lookup"><span data-stu-id="f1e6b-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="f1e6b-110">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-110">An Azure account.</span></span> <span data-ttu-id="f1e6b-111">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1e6b-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="f1e6b-112">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-112">A Media Services account.</span></span> <span data-ttu-id="f1e6b-113">toocreate un account di servizi multimediali, vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="f1e6b-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="f1e6b-114">Una webcam.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-114">A webcam.</span></span> <span data-ttu-id="f1e6b-115">Ad esempio, [codificatore Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="f1e6b-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="f1e6b-116">Si consiglia di hello tooreview seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="f1e6b-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="f1e6b-117">Codificatori live e supporto RTMP di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f1e6b-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="f1e6b-118">Panoramica di Live Streaming con Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f1e6b-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="f1e6b-119">Streaming live con codificatori locali che creano flussi a bitrate multipli</span><span class="sxs-lookup"><span data-stu-id="f1e6b-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="f1e6b-120"><a id="scenario"></a>Scenario comune di streaming live</span><span class="sxs-lookup"><span data-stu-id="f1e6b-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="f1e6b-121">Hello passaggi seguenti descrivono le attività coinvolte nella creazione comuni in tempo reale lo streaming di applicazioni che utilizzano canali vengono configurati per il recapito pass-through.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="f1e6b-122">Questa esercitazione viene illustrato come toocreate e gestire un canale di tipo pass-through e gli eventi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="f1e6b-123">Assicurarsi che sia hello endpoint da cui si desidera toostream contenuto di streaming in hello **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="f1e6b-124">Connettere un computer tooa videocamera.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="f1e6b-125">Avviare e configurare un codificatore live locale che genera un flusso in formato RTMP o MP4 frammentato a più bitrate.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="f1e6b-126">Per altre informazioni, vedere l'argomento relativo a [codificatori live e supporto RTMP di Servizi multimediali di Azure](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="f1e6b-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="f1e6b-127">Questa operazione può essere eseguita anche dopo la creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="f1e6b-128">Creare e avviare un canale pass-through.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="f1e6b-129">URL di inserimento recuperare hello del canale.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="f1e6b-130">URL di inserimento Hello viene utilizzato dal codificatore live di hello toosend hello flusso toohello canale.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="f1e6b-131">Recuperare l'URL di anteprima del canale hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="f1e6b-132">Utilizzare questo tooverify URL che il canale riceve correttamente flusso live hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="f1e6b-133">Creare un programma o un evento live.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="f1e6b-134">Quando tramite hello portale di Azure, creazione di un evento in tempo reale crea inoltre un asset.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="f1e6b-135">Avviare hello evento/quando sei pronto toostart streaming e l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="f1e6b-136">Facoltativamente, codificatore live hello può essere segnalato toostart un annuncio.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="f1e6b-137">annuncio Hello viene inserito nel flusso di output di hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="f1e6b-138">Arrestare hello evento/programma ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="f1e6b-139">Eliminare evento hello/programma (e facoltativamente elimina hello asset).</span><span class="sxs-lookup"><span data-stu-id="f1e6b-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="f1e6b-140">Consultare [Live streaming con codificatori locali che creano flussi più velocità in bit](media-services-live-streaming-with-onprem-encoders.md) toolearn sui concetti e considerazioni correlate toolive streaming con codificatori locali e i canali di tipo pass-through.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="f1e6b-141">errori e le notifiche tooview</span><span class="sxs-lookup"><span data-stu-id="f1e6b-141">tooview notifications and errors</span></span>
<span data-ttu-id="f1e6b-142">Se si desidera tooview notifiche e gli errori generati da hello portale di Azure, fare clic sull'icona di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Notifiche](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="f1e6b-144">Creare e avviare eventi e canali pass-through</span><span class="sxs-lookup"><span data-stu-id="f1e6b-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="f1e6b-145">Un canale è associato a eventi e i programmi che consentono la pubblicazione di hello toocontrol e l'archiviazione di segmenti in un flusso in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="f1e6b-146">Gli eventi sono gestiti dai canali.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-146">Channels manage events.</span></span> 

<span data-ttu-id="f1e6b-147">È possibile specificare hello numero di ore che si vuole tooretain hello registrato contenuto per il programma hello, impostazione hello **finestra archivio** lunghezza.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="f1e6b-148">Questo valore può essere impostato da un minimo di 25 ore massimo tooa 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="f1e6b-149">Lunghezza dell'intervallo di archiviazione determina anche l'intervallo di tempo i client possono cercare indietro nel tempo dalla posizione live corrente hello massimo hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="f1e6b-150">Gli eventi è possono eseguire sul periodo di tempo specificato hello, ma il contenuto che non è sincronizzato con la lunghezza della finestra hello viene scartato in modo continuo.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="f1e6b-151">Questo valore di questa proprietà determina anche per quanto tempo hello client possono raggiungere i manifesti.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="f1e6b-152">Ogni evento è associato a un asset.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-152">Each event is associated with an asset.</span></span> <span data-ttu-id="f1e6b-153">evento hello toopublish, è necessario creare un localizzatore OnDemand per asset hello associata.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="f1e6b-154">Con questo localizzatore consente si toobuild un URL di streaming che è possibile fornire tooyour client.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="f1e6b-155">Un canale supporta fino toothree in esecuzione simultanea di eventi in modo è possibile creare più archivi di hello stesso flusso in ingresso.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="f1e6b-156">In questo modo toopublish e archiviare parti diverse di un evento in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="f1e6b-157">Ad esempio, il requisito di business è tooarchive 6 ore di un programma, ma toobroadcast solo ultimi 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="f1e6b-158">tooaccomplish, è necessario toocreate due programmi in esecuzione simultanea.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="f1e6b-159">Un programma è impostato tooarchive 6 ore dell'evento hello ma hello non viene pubblicato.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="f1e6b-160">Hello altro programma è tooarchive insieme per 10 minuti e questo programma viene pubblicato.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="f1e6b-161">Non riutilizzare eventi live esistenti,</span><span class="sxs-lookup"><span data-stu-id="f1e6b-161">You should not reuse existing live events.</span></span> <span data-ttu-id="f1e6b-162">ma creare e avviare un nuovo evento per ogni evento.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="f1e6b-163">Avviare eventi hello quando sei pronto toostart streaming e l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="f1e6b-164">Arrestare il programma hello ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="f1e6b-165">contenuto toodelete archiviato, interrompere ed eliminare evento hello e quindi eliminare asset associato hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="f1e6b-166">Non è possibile eliminare un asset se è utilizzato da un evento. evento Hello deve prima essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="f1e6b-167">Anche dopo aver arrestato ed eliminato evento hello, hello gli utenti sarebbero in grado di toostream il contenuto archiviato come video on demand, per fino a quando non si elimina asset hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="f1e6b-168">Se si desidera hello tooretain archiviato il contenuto, ma non è disponibile per lo streaming, eliminare hello localizzatore di streaming.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="f1e6b-169">toouse hello portale toocreate un canale</span><span class="sxs-lookup"><span data-stu-id="f1e6b-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="f1e6b-170">Questa sezione viene illustrato come hello toouse **creazione rapida** opzione toocreate un canale di tipo pass-through.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="f1e6b-171">Per informazioni più dettagliate sui canali pass-through, vedere [Streaming live con codificatori locali che creano flussi a bitrate multipli](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="f1e6b-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="f1e6b-172">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="f1e6b-173">In hello **impostazioni** finestra, fare clic su **Live streaming**.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![introduttiva](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="f1e6b-175">Hello **Live streaming** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="f1e6b-176">Fare clic su **creazione rapida** toocreate un canale di tipo pass-through con hello RTMP protocollo di inserimento.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="f1e6b-177">Hello **creare un nuovo canale** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="f1e6b-178">Assegnare un nome di nuovo canale hello e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="f1e6b-179">Ciò consente di creare un canale pass-through con hello protocollo di inserimento RTMP.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="f1e6b-180">Creare eventi</span><span class="sxs-lookup"><span data-stu-id="f1e6b-180">Create events</span></span>
1. <span data-ttu-id="f1e6b-181">Selezionare un canale toowhich desiderato tooadd un evento.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="f1e6b-182">Premere il pulsante **Evento live** .</span><span class="sxs-lookup"><span data-stu-id="f1e6b-182">Press **Live Event** button.</span></span>

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="f1e6b-184">Ottenere gli URL di inserimento</span><span class="sxs-lookup"><span data-stu-id="f1e6b-184">Get ingest URLs</span></span>
<span data-ttu-id="f1e6b-185">Una volta creato il canale di hello, è possibile ottenere l'URL che verrà fornito codificatore live toohello di inserimento.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="f1e6b-186">codificatore Hello utilizza questi tooinput URL di un flusso in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Data di creazione](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="f1e6b-188">Evento hello espressioni di controllo</span><span class="sxs-lookup"><span data-stu-id="f1e6b-188">Watch hello event</span></span>
<span data-ttu-id="f1e6b-189">evento hello toowatch, fare clic su **espressioni di controllo** in hello Azure portal o copia a hello URL di streaming e usare un lettore di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Data di creazione](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="f1e6b-191">Evento Live ottengono automaticamente contenuto richiesta tooon convertito all'arresto.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="f1e6b-192">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="f1e6b-192">Clean up</span></span>
<span data-ttu-id="f1e6b-193">Per informazioni più dettagliate sui canali pass-through, vedere [Streaming live con codificatori locali che creano flussi a bitrate multipli](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="f1e6b-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="f1e6b-194">Un canale può essere arrestato solo quando tutti gli eventi i programmi sul canale hello è stati arrestati.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="f1e6b-195">Una volta hello canale viene interrotto, non è soggetta eventuali addebiti.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="f1e6b-196">Quando è necessario toostart nuovamente, disporrà di hello stesso URL di inserimento in modo non sarà necessario tooreconfigure codificatore.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="f1e6b-197">Un canale può essere eliminato solo quando sono stati eliminati tutti gli eventi in tempo reale sul canale hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="f1e6b-198">Visualizzare il contenuto archiviato</span><span class="sxs-lookup"><span data-stu-id="f1e6b-198">View archived content</span></span>
<span data-ttu-id="f1e6b-199">Anche dopo aver arrestato ed eliminato evento hello, hello gli utenti sarebbero in grado di toostream il contenuto archiviato come video on demand, per fino a quando non si elimina asset hello.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="f1e6b-200">Non è possibile eliminare un asset se è utilizzato da un evento. evento Hello deve prima essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="f1e6b-201">Selezionare le risorse, toomanage **impostazione** e fare clic su **asset**.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Asset](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="f1e6b-203">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="f1e6b-203">Next step</span></span>
<span data-ttu-id="f1e6b-204">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="f1e6b-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f1e6b-205">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f1e6b-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

