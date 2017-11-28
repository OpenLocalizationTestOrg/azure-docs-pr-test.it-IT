---
title: "aaaConfigure hello toosend di codificatore Live elementare un flusso live a velocità in bit singola | Documenti Microsoft"
description: "Questo argomento viene illustrato come tooconfigure hello toosend di codificatore Live elementare un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="3663d-103">Utilizzare hello Live elementare codificatore toosend un flusso live a velocità in bit singola</span><span class="sxs-lookup"><span data-stu-id="3663d-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3663d-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="3663d-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="3663d-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="3663d-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="3663d-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="3663d-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="3663d-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="3663d-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="3663d-108">Questo argomento viene illustrato come hello tooconfigure [Live elementare](http://www.elementaltechnologies.com/products/elemental-live) codificatore toosend una velocità in bit singola tooAMS canali abilitati per la codifica live del flusso.</span><span class="sxs-lookup"><span data-stu-id="3663d-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="3663d-109">Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="3663d-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="3663d-110">Questa esercitazione vengono illustrate le modalità di servizi multimediali di Azure di toomanage (AMS) con lo strumento Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="3663d-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="3663d-111">Questo strumento può essere eseguito solo in PC Windows.</span><span class="sxs-lookup"><span data-stu-id="3663d-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="3663d-112">Se si utilizza Mac o Linux, usare hello toocreate portale Azure [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="3663d-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3663d-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3663d-113">Prerequisites</span></span>
* <span data-ttu-id="3663d-114">Deve avere una conoscenza di utilizzo di Live elementare web interfaccia toocreate eventi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="3663d-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="3663d-115">Creare un account Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="3663d-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="3663d-116">Verificare che sia presente un endpoint di streaming in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3663d-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="3663d-117">Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="3663d-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="3663d-118">Installare una versione più recente di hello di hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) strumento.</span><span class="sxs-lookup"><span data-stu-id="3663d-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="3663d-119">Avviare lo strumento hello e tooyour sistema AMS di account di connessione.</span><span class="sxs-lookup"><span data-stu-id="3663d-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="3663d-120">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="3663d-120">Tips</span></span>
* <span data-ttu-id="3663d-121">Se possibile, usare una connessione a Internet con cablaggio fisico.</span><span class="sxs-lookup"><span data-stu-id="3663d-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="3663d-122">Una buona regola pratica per determinare i requisiti di larghezza di banda è hello toodouble streaming a velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="3663d-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="3663d-123">Sebbene non sia un requisito obbligatorio, questo risulterà utile ridurre l'impatto di hello congestione della rete.</span><span class="sxs-lookup"><span data-stu-id="3663d-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="3663d-124">Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.</span><span class="sxs-lookup"><span data-stu-id="3663d-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="3663d-125">Elemental Live con inserimento RTP</span><span class="sxs-lookup"><span data-stu-id="3663d-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="3663d-126">In questa sezione viene illustrato come tooconfigure hello elementare codificatore Live che invia una velocità in bit singola flusso live su RTP.</span><span class="sxs-lookup"><span data-stu-id="3663d-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="3663d-127">Per altre informazioni, vedere [Flusso MPEG-TS su RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="3663d-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="3663d-128">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="3663d-128">Create a channel</span></span>

1. <span data-ttu-id="3663d-129">Nello strumento AMSE hello passare toohello **Live** scheda e fare clic con il pulsante destro nell'area di canale hello.</span><span class="sxs-lookup"><span data-stu-id="3663d-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="3663d-130">Scegliere **Create channel**</span><span class="sxs-lookup"><span data-stu-id="3663d-130">Select **Create channel…**</span></span> <span data-ttu-id="3663d-131">dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="3663d-131">from hello menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="3663d-133">Specificare un nome di canale, il campo di descrizione hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="3663d-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="3663d-134">Selezionare le impostazioni del canale, **Standard** per hello opzione di codifica Live, con hello Input protocollo impostato troppo**RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="3663d-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="3663d-135">È possibile confermare tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="3663d-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="3663d-136">Verificare che hello **inizio hello nuovo canale ora** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="3663d-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="3663d-137">Fare clic su **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="3663d-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="3663d-139">canale Hello può richiedere fino a 20 minuti toostart.</span><span class="sxs-lookup"><span data-stu-id="3663d-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="3663d-140">Durante l'avvio di canale hello è possibile [configurare codificatore hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="3663d-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3663d-141">Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto.</span><span class="sxs-lookup"><span data-stu-id="3663d-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="3663d-142">Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="3663d-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="3663d-143"><a id=configure_elemental_rtp></a>Configurazione del codificatore Live elementare hello</span><span class="sxs-lookup"><span data-stu-id="3663d-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="3663d-144">In questa esercitazione hello vengono utilizzate le seguenti impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="3663d-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="3663d-145">Hello in questa sezione descrive in dettaglio i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3663d-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="3663d-146">**Video**:</span><span class="sxs-lookup"><span data-stu-id="3663d-146">**Video**:</span></span>

* <span data-ttu-id="3663d-147">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="3663d-147">Codec: H.264</span></span>
* <span data-ttu-id="3663d-148">Profilo: alto (livello 4.0)</span><span class="sxs-lookup"><span data-stu-id="3663d-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="3663d-149">Velocità in bit: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="3663d-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="3663d-150">Fotogramma chiave: 2 secondi (60 secondi)</span><span class="sxs-lookup"><span data-stu-id="3663d-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="3663d-151">Frequenza dei fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="3663d-151">Frame Rate: 30</span></span>

<span data-ttu-id="3663d-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="3663d-152">**Audio**:</span></span>

* <span data-ttu-id="3663d-153">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="3663d-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="3663d-154">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="3663d-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="3663d-155">Frequenza di campionamento: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="3663d-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="3663d-156">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="3663d-156">Configuration steps</span></span>
1. <span data-ttu-id="3663d-157">Passare toohello **Live elementare** interfaccia web e impostare il codificatore hello per **UDP/Servizi terminal** streaming.</span><span class="sxs-lookup"><span data-stu-id="3663d-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="3663d-158">Dopo aver creato un nuovo evento, scorrere verso il basso dei gruppi di output toohello e aggiungere hello **UDP/Servizi terminal** gruppo di output.</span><span class="sxs-lookup"><span data-stu-id="3663d-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="3663d-159">Creare un nuovo output selezionando **Nuovo flusso** e quindi facendo clic su **Aggiungi output**.</span><span class="sxs-lookup"><span data-stu-id="3663d-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="3663d-161">È consigliabile che l'evento elementare hello disponga timecode hello impostato troppo codificatore di hello toohelp "Orologio di sistema" riconnessione in caso di hello di un errore di flusso.</span><span class="sxs-lookup"><span data-stu-id="3663d-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="3663d-162">Ora che hello Output è stato creato, fare clic su **aggiungere flusso**.</span><span class="sxs-lookup"><span data-stu-id="3663d-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="3663d-163">le impostazioni di output di Hello possono ora essere configurate.</span><span class="sxs-lookup"><span data-stu-id="3663d-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="3663d-164">Scorrere verso il basso toohello "Stream 1" è stato appena creato, fare clic su hello **Video** scheda hello sinistra ed espandere hello **avanzate** sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="3663d-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="3663d-166">Mentre Live elementare ha un'ampia gamma di personalizzazione disponibili, hello seguente si consigliano le impostazioni per iniziare a usare tooAMS di streaming.</span><span class="sxs-lookup"><span data-stu-id="3663d-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="3663d-167">Risoluzione: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="3663d-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="3663d-168">Frequenza fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="3663d-168">Framerate: 30</span></span>
   * <span data-ttu-id="3663d-169">Dimensioni GOP: 60 fotogrammi</span><span class="sxs-lookup"><span data-stu-id="3663d-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="3663d-170">Modalità interlacciamento: progressivo</span><span class="sxs-lookup"><span data-stu-id="3663d-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="3663d-171">Velocità in bit: 5000000 bit/s (regolabile in base alle limitazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="3663d-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="3663d-173">Ottenere l'URL di input del canale hello.</span><span class="sxs-lookup"><span data-stu-id="3663d-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="3663d-174">Passare strumento AMSE toohello indietro e controllare lo stato di completamento di hello del canale.</span><span class="sxs-lookup"><span data-stu-id="3663d-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="3663d-175">Una volta hello stato è cambiato da **iniziale** troppo**esecuzione**, è possibile ottenere l'URL di input hello.</span><span class="sxs-lookup"><span data-stu-id="3663d-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="3663d-176">Quando il canale hello è in esecuzione, fare clic con il pulsante destro nome canale hello, spostarsi verso il basso toohover su **Copia URL di Input tooclipboard** e quindi selezionare **URL di Input primaria**.</span><span class="sxs-lookup"><span data-stu-id="3663d-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="3663d-178">Incollare le informazioni in hello **destinazione principale** campo hello elementare.</span><span class="sxs-lookup"><span data-stu-id="3663d-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="3663d-179">Tutte le altre impostazioni possono rimanere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="3663d-179">All other settings can remain hello default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="3663d-181">Per garantire la ridondanza aggiuntiva, ripetere questi passaggi con hello secondario URL di Input mediante la creazione di una scheda separata di "Output" per lo Streaming UDP/Servizi terminal.</span><span class="sxs-lookup"><span data-stu-id="3663d-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="3663d-182">Fare clic su **crea** (se è stato creato un nuovo evento) o **aggiornamento** (se la modifica di un evento di pre-esistente) e quindi procedere codificatore hello toostart.</span><span class="sxs-lookup"><span data-stu-id="3663d-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3663d-183">Prima di scegliere **avviare** nell'interfaccia web Live elementare di hello è **deve** assicurarsi che il canale hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="3663d-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="3663d-184">Inoltre, assicurarsi che non tooleave hello canale in uno stato pronto senza un evento per più di 15 minuti di >.</span><span class="sxs-lookup"><span data-stu-id="3663d-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="3663d-185">Dopo il flusso di hello è stata eseguita per 30 secondi, passare la riproduzione dello strumento e test AMSE toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="3663d-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="3663d-186">Testare la riproduzione</span><span class="sxs-lookup"><span data-stu-id="3663d-186">Test playback</span></span>

<span data-ttu-id="3663d-187">Passare strumento AMSE toohello e fare clic con il pulsante destro hello canale toobe testato.</span><span class="sxs-lookup"><span data-stu-id="3663d-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="3663d-188">Dal menu di hello, passare il mouse su **hello riproduzione anteprima** e selezionare **con Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="3663d-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="3663d-189">Se il flusso di hello viene visualizzato nel lettore hello, codificatore hello è stato configurato correttamente tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="3663d-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="3663d-190">Se viene ricevuto un errore, il canale hello sarà necessario toobe reimpostazione e il codificatore le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="3663d-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="3663d-191">Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="3663d-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="3663d-192">Creare un programma.</span><span class="sxs-lookup"><span data-stu-id="3663d-192">Create a program</span></span>
1. <span data-ttu-id="3663d-193">Una volta che viene confermata la riproduzione del canale, creare un programma.</span><span class="sxs-lookup"><span data-stu-id="3663d-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="3663d-194">In hello **Live** nello strumento AMSE hello, fare clic con il pulsante destro nell'area di programma hello e selezionare **creare un nuovo programma**.</span><span class="sxs-lookup"><span data-stu-id="3663d-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="3663d-196">Nome programma hello e, se necessario, modificare hello **lunghezza dell'intervallo di archivio** (le impostazioni predefinite too4 ore).</span><span class="sxs-lookup"><span data-stu-id="3663d-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="3663d-197">È inoltre possibile specificare un percorso di archiviazione o lasciare hello predefinite.</span><span class="sxs-lookup"><span data-stu-id="3663d-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="3663d-198">Controllare hello **ora inizio hello programma** casella.</span><span class="sxs-lookup"><span data-stu-id="3663d-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="3663d-199">Fare clic su **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="3663d-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="3663d-200">La creazione di un programma richiede meno tempo rispetto alla creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="3663d-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="3663d-201">Quando è in esecuzione il programma hello, confermare la riproduzione facendo clic con il pulsante destro programma hello e passando troppo**riproduzione hello programmi** e quindi selezionando **con Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="3663d-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="3663d-202">Una volta confermato, fare clic nuovamente il programma hello e scegliere **copiare tooClipboard URL di Output di hello** (o recuperare queste informazioni da hello **informazioni e le impostazioni del programma** opzione dal menu di hello).</span><span class="sxs-lookup"><span data-stu-id="3663d-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="3663d-203">flusso Hello è ora pronto toobe incorporato in un lettore o destinatari tooan distribuita per live visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="3663d-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="3663d-204">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="3663d-204">Troubleshooting</span></span>
<span data-ttu-id="3663d-205">Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="3663d-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3663d-206">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="3663d-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3663d-207">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="3663d-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
