---
title: "aaaConfigure hello NewTek TriCaster codificatore toosend un flusso live a velocità in bit singola | Documenti Microsoft"
description: "Questo argomento viene illustrato come hello tooconfigure Tricaster toosend codificatore una velocità in bit singola flusso tooAMS canali live che sono abilitati per la codifica live."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="8bfa1-103">Utilizzare hello NewTek TriCaster codificatore toosend un flusso live a velocità in bit singola</span><span class="sxs-lookup"><span data-stu-id="8bfa1-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bfa1-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="8bfa1-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="8bfa1-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="8bfa1-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="8bfa1-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="8bfa1-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="8bfa1-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="8bfa1-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="8bfa1-108">Questo argomento viene illustrato come hello tooconfigure [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live codificatore toosend un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="8bfa1-109">Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="8bfa1-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="8bfa1-110">Questa esercitazione vengono illustrate le modalità di servizi multimediali di Azure di toomanage (AMS) con lo strumento Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="8bfa1-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="8bfa1-111">Questo strumento può essere eseguito solo in PC Windows.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="8bfa1-112">Se si utilizza Mac o Linux, usare hello toocreate portale Azure [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="8bfa1-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8bfa1-113">Quando tramite Tricaster per l'invio di un contributo feed tooAMS canali abilitati per la codifica live, potrebbe essere necessario anomalie di video o audio nell'evento in tempo reale Se si utilizzano determinate funzionalità di Tricaster, ad esempio rapido Taglia tra feed o il passaggio a/da Slate .</span><span class="sxs-lookup"><span data-stu-id="8bfa1-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="8bfa1-114">Hello AMS team lavora in corretto questi problemi, fino a quel momento, è consigliabile non toouse queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="8bfa1-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8bfa1-115">Prerequisites</span></span>
* [<span data-ttu-id="8bfa1-116">Creare un account Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="8bfa1-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="8bfa1-117">Verificare che sia presente un endpoint di streaming in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="8bfa1-118">Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="8bfa1-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="8bfa1-119">Installare una versione più recente di hello di hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) strumento.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="8bfa1-120">Avviare lo strumento hello e tooyour sistema AMS di account di connessione.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="8bfa1-121">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="8bfa1-121">Tips</span></span>
* <span data-ttu-id="8bfa1-122">Se possibile, usare una connessione a Internet con cablaggio fisico.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="8bfa1-123">Una buona regola pratica per determinare i requisiti di larghezza di banda è hello toodouble streaming a velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="8bfa1-124">Sebbene non sia un requisito obbligatorio, questo risulterà utile ridurre l'impatto di hello congestione della rete.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="8bfa1-125">Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="8bfa1-126">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="8bfa1-126">Create a channel</span></span>
1. <span data-ttu-id="8bfa1-127">Nello strumento AMSE hello passare toohello **Live** scheda e fare clic con il pulsante destro nell'area di canale hello.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="8bfa1-128">Scegliere **Create channel**</span><span class="sxs-lookup"><span data-stu-id="8bfa1-128">Select **Create channel…**</span></span> <span data-ttu-id="8bfa1-129">dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-129">from hello menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="8bfa1-131">Specificare un nome di canale, il campo di descrizione hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="8bfa1-132">Selezionare le impostazioni del canale, **Standard** per hello opzione di codifica Live, con hello Input protocollo impostato troppo**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="8bfa1-133">È possibile confermare tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="8bfa1-134">Verificare che hello **inizio hello nuovo canale ora** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="8bfa1-135">Fare clic su **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="8bfa1-137">canale Hello può richiedere fino a 20 minuti toostart.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="8bfa1-138">Durante l'avvio di canale hello è possibile [configurare codificatore hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="8bfa1-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8bfa1-139">Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="8bfa1-140">Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="8bfa1-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="8bfa1-141"><a id=configure_tricaster_rtmp></a>Configurare hello NewTek TriCaster codificatore</span><span class="sxs-lookup"><span data-stu-id="8bfa1-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="8bfa1-142">In questa esercitazione hello vengono utilizzate le seguenti impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="8bfa1-143">Hello in questa sezione descrive in dettaglio i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="8bfa1-144">**Video**:</span><span class="sxs-lookup"><span data-stu-id="8bfa1-144">**Video**:</span></span>

* <span data-ttu-id="8bfa1-145">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="8bfa1-145">Codec: H.264</span></span>
* <span data-ttu-id="8bfa1-146">Profilo: alto (livello 4.0)</span><span class="sxs-lookup"><span data-stu-id="8bfa1-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="8bfa1-147">Velocità in bit: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="8bfa1-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="8bfa1-148">Fotogramma chiave: 2 secondi (60 secondi)</span><span class="sxs-lookup"><span data-stu-id="8bfa1-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="8bfa1-149">Frequenza dei fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="8bfa1-149">Frame Rate: 30</span></span>

<span data-ttu-id="8bfa1-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="8bfa1-150">**Audio**:</span></span>

* <span data-ttu-id="8bfa1-151">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="8bfa1-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="8bfa1-152">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="8bfa1-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="8bfa1-153">Frequenza di campionamento: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="8bfa1-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="8bfa1-154">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="8bfa1-154">Configuration steps</span></span>
1. <span data-ttu-id="8bfa1-155">Creare un nuovo progetto **NewTek TriCaster** in base a quale origine di input del video si sta utilizzando.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="8bfa1-156">Una volta all'interno di tale progetto, cercare hello **flusso** pulsante e fare clic su hello ingranaggio icona Avanti tooit tooaccess hello flusso menu configurazione.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="8bfa1-158">Se il menu di hello è aperta, fare clic su **New** titolo connessione hello.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="8bfa1-159">Quando richiesto per il tipo di connessione hello, selezionare **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="8bfa1-161">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-161">Click **OK**.</span></span>
5. <span data-ttu-id="8bfa1-162">Un profilo FMLE può ora essere importato facendo clic sulla freccia sotto a discesa hello **profilo Streaming** e la navigazione troppo**Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="8bfa1-164">Passare toowhere hello configurato FMLE profilo è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="8bfa1-165">Selezionarlo e premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="8bfa1-166">Una volta caricato il profilo di hello, procedere toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="8bfa1-167">Ottenere l'URL di input del canale hello in ordine tooassign è toohello Tricaster **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="8bfa1-168">Passare strumento AMSE toohello indietro e controllare lo stato di completamento di hello del canale.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="8bfa1-169">Una volta hello stato è cambiato da **iniziale** troppo**esecuzione**, è possibile ottenere l'URL di input hello.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="8bfa1-170">Quando il canale hello è in esecuzione, fare clic con il pulsante destro nome canale hello, spostarsi verso il basso toohover su **Copia URL di Input tooclipboard** e quindi selezionare **URL di Input primaria**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="8bfa1-172">Incollare le informazioni in hello **percorso** campo **Flash Server** all'interno di progetto di hello Tricaster.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="8bfa1-173">Assegnare un nome di flusso in hello **ID flusso** campo.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="8bfa1-174">Se le informazioni di flusso è stato aggiunto il profilo FMLE toohello, anche possibile importare toothis sezione facendo **importare le impostazioni**, passando profilo FMLE toohello salvato e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="8bfa1-175">campi Flash Server rilevanti Hello devono popolare con le informazioni di hello di FMLE.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="8bfa1-177">Al termine, fare clic su **OK** in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="8bfa1-178">Quando gli input audio e video in hello Tricaster pronti, iniziare lo streaming tooAMS facendo hello **flusso** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="8bfa1-180">Prima di scegliere **flusso**, si **deve** assicurarsi che il canale hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="8bfa1-181">Inoltre, assicurarsi che non tooleave hello canale in uno stato pronto senza un contributo input feed per più di 15 minuti di >.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="8bfa1-182">Testare la riproduzione</span><span class="sxs-lookup"><span data-stu-id="8bfa1-182">Test playback</span></span>
<span data-ttu-id="8bfa1-183">Passare strumento AMSE toohello e fare clic con il pulsante destro hello canale toobe testato.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="8bfa1-184">Dal menu di hello, passare il mouse su **hello riproduzione anteprima** e selezionare **con Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="8bfa1-185">Se il flusso di hello viene visualizzato nel lettore hello, codificatore hello è stato configurato correttamente tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="8bfa1-186">Se viene ricevuto un errore, il canale hello sarà necessario toobe reimpostazione e il codificatore le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="8bfa1-187">Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="8bfa1-188">Creare un programma.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-188">Create a program</span></span>
1. <span data-ttu-id="8bfa1-189">Una volta che viene confermata la riproduzione del canale, creare un programma.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="8bfa1-190">In hello **Live** nello strumento AMSE hello, fare clic con il pulsante destro nell'area di programma hello e selezionare **creare un nuovo programma**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="8bfa1-192">Nome programma hello e, se necessario, modificare hello **lunghezza dell'intervallo di archivio** (le impostazioni predefinite too4 ore).</span><span class="sxs-lookup"><span data-stu-id="8bfa1-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="8bfa1-193">È inoltre possibile specificare un percorso di archiviazione o lasciare hello predefinite.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="8bfa1-194">Controllare hello **ora inizio hello programma** casella.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="8bfa1-195">Fare clic su **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="8bfa1-196">La creazione di un programma richiede meno tempo rispetto alla creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="8bfa1-197">Quando è in esecuzione il programma hello, confermare la riproduzione facendo clic con il pulsante destro programma hello e passando troppo**riproduzione hello programmi** e quindi selezionando **con Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="8bfa1-198">Una volta confermato, fare clic nuovamente il programma hello e scegliere **copiare tooClipboard URL di Output di hello** (o recuperare queste informazioni da hello **informazioni e le impostazioni del programma** opzione dal menu di hello).</span><span class="sxs-lookup"><span data-stu-id="8bfa1-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="8bfa1-199">flusso Hello è ora pronto toobe incorporato in un lettore o destinatari tooan distribuita per live visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="8bfa1-200">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="8bfa1-200">Troubleshooting</span></span>
<span data-ttu-id="8bfa1-201">Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="8bfa1-202">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="8bfa1-202">Next step</span></span>
<span data-ttu-id="8bfa1-203">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="8bfa1-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8bfa1-204">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="8bfa1-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
