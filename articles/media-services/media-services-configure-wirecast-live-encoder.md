---
title: "aaaConfigure hello Telestream Wirecast encoder toosend un flusso live a velocità in bit singola | Documenti Microsoft"
description: "Questo argomento viene illustrato come tooconfigure hello Wirecast encoder toosend una velocità in bit singola flusso tooAMS canali live che sono abilitati per la codifica live. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="d859a-103">Utilizzare hello Wirecast encoder toosend un flusso live a velocità in bit singola</span><span class="sxs-lookup"><span data-stu-id="d859a-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d859a-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="d859a-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="d859a-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="d859a-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="d859a-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="d859a-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="d859a-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="d859a-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="d859a-108">Questo argomento viene illustrato come hello tooconfigure [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live codificatore toosend un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live.</span><span class="sxs-lookup"><span data-stu-id="d859a-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="d859a-109">Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="d859a-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="d859a-110">Questa esercitazione vengono illustrate le modalità di servizi multimediali di Azure di toomanage (AMS) con lo strumento Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="d859a-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="d859a-111">Questo strumento può essere eseguito solo in PC Windows.</span><span class="sxs-lookup"><span data-stu-id="d859a-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="d859a-112">Se si utilizza Mac o Linux, usare hello toocreate portale Azure [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="d859a-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d859a-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d859a-113">Prerequisites</span></span>
* [<span data-ttu-id="d859a-114">Creare un account Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="d859a-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="d859a-115">Verificare che sia presente un endpoint di streaming in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d859a-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="d859a-116">Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="d859a-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="d859a-117">Installare una versione più recente di hello di hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) strumento.</span><span class="sxs-lookup"><span data-stu-id="d859a-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="d859a-118">Avviare lo strumento hello e tooyour sistema AMS di account di connessione.</span><span class="sxs-lookup"><span data-stu-id="d859a-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="d859a-119">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d859a-119">Tips</span></span>
* <span data-ttu-id="d859a-120">Se possibile, usare una connessione a Internet con cablaggio fisico.</span><span class="sxs-lookup"><span data-stu-id="d859a-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="d859a-121">Una buona regola pratica per determinare i requisiti di larghezza di banda è hello toodouble streaming a velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="d859a-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="d859a-122">Sebbene non sia un requisito obbligatorio, questo risulterà utile ridurre l'impatto di hello congestione della rete.</span><span class="sxs-lookup"><span data-stu-id="d859a-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="d859a-123">Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.</span><span class="sxs-lookup"><span data-stu-id="d859a-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="d859a-124">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="d859a-124">Create a channel</span></span>
1. <span data-ttu-id="d859a-125">Nello strumento AMSE hello passare toohello **Live** scheda e fare clic con il pulsante destro nell'area di canale hello.</span><span class="sxs-lookup"><span data-stu-id="d859a-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="d859a-126">Scegliere **Create channel**</span><span class="sxs-lookup"><span data-stu-id="d859a-126">Select **Create channel…**</span></span> <span data-ttu-id="d859a-127">dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="d859a-127">from hello menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="d859a-129">Specificare un nome di canale, il campo di descrizione hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d859a-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="d859a-130">Selezionare le impostazioni del canale, **Standard** per hello opzione di codifica Live, con hello Input protocollo impostato troppo**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="d859a-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="d859a-131">È possibile confermare tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="d859a-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="d859a-132">Verificare che hello **inizio hello nuovo canale ora** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="d859a-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="d859a-133">Fare clic su **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="d859a-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="d859a-135">canale Hello può richiedere fino a 20 minuti toostart.</span><span class="sxs-lookup"><span data-stu-id="d859a-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="d859a-136">Durante l'avvio di canale hello è possibile [configurare codificatore hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="d859a-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d859a-137">Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto.</span><span class="sxs-lookup"><span data-stu-id="d859a-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="d859a-138">Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="d859a-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="d859a-139"><a id=configure_wirecast_rtmp></a>Configurare Telestream Wirecast encoder hello</span><span class="sxs-lookup"><span data-stu-id="d859a-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="d859a-140">In questa esercitazione hello vengono utilizzate le seguenti impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="d859a-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="d859a-141">Hello in questa sezione descrive in dettaglio i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d859a-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="d859a-142">**Video**:</span><span class="sxs-lookup"><span data-stu-id="d859a-142">**Video**:</span></span>

* <span data-ttu-id="d859a-143">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="d859a-143">Codec: H.264</span></span>
* <span data-ttu-id="d859a-144">Profilo: alto (livello 4.0)</span><span class="sxs-lookup"><span data-stu-id="d859a-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="d859a-145">Velocità in bit: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="d859a-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="d859a-146">Fotogramma chiave: 2 secondi (60 secondi)</span><span class="sxs-lookup"><span data-stu-id="d859a-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="d859a-147">Frequenza dei fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="d859a-147">Frame Rate: 30</span></span>

<span data-ttu-id="d859a-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="d859a-148">**Audio**:</span></span>

* <span data-ttu-id="d859a-149">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="d859a-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="d859a-150">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="d859a-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="d859a-151">Frequenza di campionamento: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="d859a-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="d859a-152">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="d859a-152">Configuration steps</span></span>
1. <span data-ttu-id="d859a-153">Aprire un'applicazione hello Telestream Wirecast sulla macchina hello utilizzato e impostare per lo streaming RTMP.</span><span class="sxs-lookup"><span data-stu-id="d859a-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="d859a-154">Configurare l'output di hello passando toohello **Output** scheda e selezionando **le impostazioni di Output...** .</span><span class="sxs-lookup"><span data-stu-id="d859a-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="d859a-155">Verificare che hello **destinazione dell'Output** è troppo**RTMP Server**.</span><span class="sxs-lookup"><span data-stu-id="d859a-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="d859a-156">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d859a-156">Click **OK**.</span></span>
4. <span data-ttu-id="d859a-157">Nella pagina Impostazioni hello, impostare hello **destinazione** campo toobe **servizi multimediali di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d859a-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="d859a-158">profilo di codifica Hello è preselezionata troppo**h. 264 Azure 720 p 16:9 (1280x720)**.</span><span class="sxs-lookup"><span data-stu-id="d859a-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="d859a-159">toocustomize queste impostazioni, selezionare hello ingranaggio icona toohello diritto di hello elenco a discesa e quindi scegliere **New Preset**.</span><span class="sxs-lookup"><span data-stu-id="d859a-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="d859a-161">Configura le impostazioni predefinite del codificatore.</span><span class="sxs-lookup"><span data-stu-id="d859a-161">Configure encoder presets.</span></span>

    <span data-ttu-id="d859a-162">Hello Nome set di impostazioni e verificare la seguente hello impostazioni consigliate:</span><span class="sxs-lookup"><span data-stu-id="d859a-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="d859a-163">**Video**</span><span class="sxs-lookup"><span data-stu-id="d859a-163">**Video**</span></span>

   * <span data-ttu-id="d859a-164">Codificatore: MainConcept h. 264</span><span class="sxs-lookup"><span data-stu-id="d859a-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="d859a-165">Fotogrammi al secondo: 30</span><span class="sxs-lookup"><span data-stu-id="d859a-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="d859a-166">Velocità in bit media: 5000 kbit al secondo (può essere regolato in base alle limitazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="d859a-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="d859a-167">Profilo: principale</span><span class="sxs-lookup"><span data-stu-id="d859a-167">Profile: Main</span></span>
   * <span data-ttu-id="d859a-168">Fotogramma chiave ogni: 60 fotogrammi</span><span class="sxs-lookup"><span data-stu-id="d859a-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="d859a-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="d859a-169">**Audio**</span></span>

   * <span data-ttu-id="d859a-170">Velocità in bit di destinazione: 192 kbit/sec</span><span class="sxs-lookup"><span data-stu-id="d859a-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="d859a-171">Frequenza di campionamento: 44,100 kHz</span><span class="sxs-lookup"><span data-stu-id="d859a-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="d859a-173">Premere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d859a-173">Press **Save**.</span></span>

    <span data-ttu-id="d859a-174">campo Encoding Hello dispone ora disponibili per la selezione del profilo di hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="d859a-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="d859a-175">Assicurarsi che sia selezionato il nuovo profilo di hello.</span><span class="sxs-lookup"><span data-stu-id="d859a-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="d859a-176">Ottenere l'URL di input del canale hello in ordine tooassign è toohello Wirecast **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="d859a-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="d859a-177">Passare strumento AMSE toohello indietro e controllare lo stato di completamento di hello del canale.</span><span class="sxs-lookup"><span data-stu-id="d859a-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="d859a-178">Una volta hello stato è cambiato da **iniziale** troppo**esecuzione**, è possibile ottenere l'URL di input hello.</span><span class="sxs-lookup"><span data-stu-id="d859a-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="d859a-179">Quando il canale hello è in esecuzione, fare clic con il pulsante destro nome canale hello, spostarsi verso il basso toohover su **Copia URL di Input tooclipboard** e quindi selezionare **URL di Input primaria**.</span><span class="sxs-lookup"><span data-stu-id="d859a-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="d859a-181">In hello Wirecast **le impostazioni di Output** finestra incollare queste informazioni in hello **indirizzo** campo della sezione di output di hello e di assegnare un nome di flusso.</span><span class="sxs-lookup"><span data-stu-id="d859a-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="d859a-183">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="d859a-183">Select **OK**.</span></span>
2. <span data-ttu-id="d859a-184">In hello principale **Wirecast** verificare origini di input per video e audio sono pronti e quindi premere **flusso** nell'angolo superiore sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="d859a-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="d859a-186">Prima di scegliere **flusso**, si **deve** assicurarsi che il canale hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="d859a-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="d859a-187">Inoltre, assicurarsi che non tooleave hello canale in uno stato pronto senza un contributo input feed per più di 15 minuti di >.</span><span class="sxs-lookup"><span data-stu-id="d859a-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="d859a-188">Testare la riproduzione</span><span class="sxs-lookup"><span data-stu-id="d859a-188">Test playback</span></span>

<span data-ttu-id="d859a-189">Passare strumento AMSE toohello e fare clic con il pulsante destro hello canale toobe testato.</span><span class="sxs-lookup"><span data-stu-id="d859a-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="d859a-190">Dal menu di hello, passare il mouse su **hello riproduzione anteprima** e selezionare **con Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="d859a-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="d859a-191">Se il flusso di hello viene visualizzato nel lettore hello, codificatore hello è stato configurato correttamente tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="d859a-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="d859a-192">Se viene ricevuto un errore, il canale hello sarà necessario toobe reimpostazione e il codificatore le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d859a-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="d859a-193">Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="d859a-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="d859a-194">Creare un programma.</span><span class="sxs-lookup"><span data-stu-id="d859a-194">Create a program</span></span>
1. <span data-ttu-id="d859a-195">Una volta che viene confermata la riproduzione del canale, creare un programma.</span><span class="sxs-lookup"><span data-stu-id="d859a-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="d859a-196">In hello **Live** nello strumento AMSE hello, fare clic con il pulsante destro nell'area di programma hello e selezionare **creare un nuovo programma**.</span><span class="sxs-lookup"><span data-stu-id="d859a-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="d859a-198">Nome programma hello e, se necessario, modificare hello **lunghezza dell'intervallo di archivio** (le impostazioni predefinite too4 ore).</span><span class="sxs-lookup"><span data-stu-id="d859a-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="d859a-199">È inoltre possibile specificare un percorso di archiviazione o lasciare hello predefinite.</span><span class="sxs-lookup"><span data-stu-id="d859a-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="d859a-200">Controllare hello **ora inizio hello programma** casella.</span><span class="sxs-lookup"><span data-stu-id="d859a-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="d859a-201">Fare clic su **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="d859a-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="d859a-202">La creazione di un programma richiede meno tempo rispetto alla creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="d859a-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="d859a-203">Quando è in esecuzione il programma hello, confermare la riproduzione facendo clic con il pulsante destro programma hello e passando troppo**riproduzione hello programmi** e quindi selezionando **con Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="d859a-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="d859a-204">Una volta confermato, fare clic nuovamente il programma hello e scegliere **copiare tooClipboard URL di Output di hello** (o recuperare queste informazioni da hello **informazioni e le impostazioni del programma** opzione dal menu di hello).</span><span class="sxs-lookup"><span data-stu-id="d859a-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="d859a-205">flusso Hello è ora pronto toobe incorporato in un lettore o destinatari tooan distribuita per live visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="d859a-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="d859a-206">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="d859a-206">Troubleshooting</span></span>
<span data-ttu-id="d859a-207">Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="d859a-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d859a-208">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="d859a-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d859a-209">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d859a-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
