---
title: "aaaConfigure hello FMLE codificatore toosend un flusso live a velocità in bit singola | Documenti Microsoft"
description: "Questo argomento viene illustrato come tooconfigure hello toosend codificatore Flash multimediali Live codificatore (FMLE) un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="083f9-103">Utilizzare hello FMLE codificatore toosend un flusso live a velocità in bit singola</span><span class="sxs-lookup"><span data-stu-id="083f9-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="083f9-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="083f9-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="083f9-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="083f9-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="083f9-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="083f9-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="083f9-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="083f9-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="083f9-108">Questo argomento viene illustrato come hello tooconfigure [Flash Media Encoder Live](http://www.adobe.com/products/flash-media-encoder.html) toosend codificatore (FMLE) una velocità in bit singola tooAMS canali abilitati per la codifica live del flusso.</span><span class="sxs-lookup"><span data-stu-id="083f9-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="083f9-109">Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="083f9-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="083f9-110">Questa esercitazione vengono illustrate le modalità di servizi multimediali di Azure di toomanage (AMS) con lo strumento Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="083f9-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="083f9-111">Questo strumento può essere eseguito solo in PC Windows.</span><span class="sxs-lookup"><span data-stu-id="083f9-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="083f9-112">Se si utilizza Mac o Linux, usare hello toocreate portale Azure [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="083f9-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="083f9-113">Si noti che questa esercitazione descrive l'utilizzo di AAC.</span><span class="sxs-lookup"><span data-stu-id="083f9-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="083f9-114">Tuttavia, per impostazione predefinita FMLE non supporta AAC.</span><span class="sxs-lookup"><span data-stu-id="083f9-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="083f9-115">È necessario un plug-in per la codifica AAC toopurchase ad esempio da codec altamente ottimizzati: [AAC di plug-in](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="083f9-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="083f9-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="083f9-116">Prerequisites</span></span>
* [<span data-ttu-id="083f9-117">Creare un account Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="083f9-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="083f9-118">Verificare che sia presente un endpoint di streaming in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="083f9-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="083f9-119">Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="083f9-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="083f9-120">Installare una versione più recente di hello di hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) strumento.</span><span class="sxs-lookup"><span data-stu-id="083f9-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="083f9-121">Avviare lo strumento hello e tooyour sistema AMS di account di connessione.</span><span class="sxs-lookup"><span data-stu-id="083f9-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="083f9-122">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="083f9-122">Tips</span></span>
* <span data-ttu-id="083f9-123">Se possibile, usare una connessione a Internet con cablaggio fisico.</span><span class="sxs-lookup"><span data-stu-id="083f9-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="083f9-124">Una buona regola pratica per determinare i requisiti di larghezza di banda è hello toodouble streaming a velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="083f9-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="083f9-125">Sebbene non sia un requisito obbligatorio, questo risulterà utile ridurre l'impatto di hello congestione della rete.</span><span class="sxs-lookup"><span data-stu-id="083f9-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="083f9-126">Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.</span><span class="sxs-lookup"><span data-stu-id="083f9-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="083f9-127">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="083f9-127">Create a channel</span></span>
1. <span data-ttu-id="083f9-128">Nello strumento AMSE hello passare toohello **Live** scheda e fare clic con il pulsante destro nell'area di canale hello.</span><span class="sxs-lookup"><span data-stu-id="083f9-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="083f9-129">Scegliere **Create channel**</span><span class="sxs-lookup"><span data-stu-id="083f9-129">Select **Create channel…**</span></span> <span data-ttu-id="083f9-130">dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="083f9-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="083f9-132">Specificare un nome di canale, il campo di descrizione hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="083f9-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="083f9-133">Selezionare le impostazioni del canale, **Standard** per hello opzione di codifica Live, con hello Input protocollo impostato troppo**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="083f9-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="083f9-134">È possibile confermare tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="083f9-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="083f9-135">Verificare che hello **inizio hello nuovo canale ora** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="083f9-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="083f9-136">Fare clic su **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="083f9-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="083f9-138">canale Hello può richiedere fino a 20 minuti toostart.</span><span class="sxs-lookup"><span data-stu-id="083f9-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="083f9-139">Durante l'avvio di canale hello è possibile [configurare codificatore hello](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="083f9-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="083f9-140">Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto.</span><span class="sxs-lookup"><span data-stu-id="083f9-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="083f9-141">Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="083f9-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="083f9-142"><a id=configure_fmle_rtmp></a>Configurare il codificatore FMLE hello</span><span class="sxs-lookup"><span data-stu-id="083f9-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="083f9-143">In questa esercitazione hello vengono utilizzate le seguenti impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="083f9-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="083f9-144">Hello in questa sezione descrive in dettaglio i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="083f9-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="083f9-145">**Video**:</span><span class="sxs-lookup"><span data-stu-id="083f9-145">**Video**:</span></span>

* <span data-ttu-id="083f9-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="083f9-146">Codec: H.264</span></span>
* <span data-ttu-id="083f9-147">Profilo: alto (livello 4.0)</span><span class="sxs-lookup"><span data-stu-id="083f9-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="083f9-148">Velocità in bit: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="083f9-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="083f9-149">Fotogramma chiave: 2 secondi (60 secondi)</span><span class="sxs-lookup"><span data-stu-id="083f9-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="083f9-150">Frequenza dei fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="083f9-150">Frame Rate: 30</span></span>

<span data-ttu-id="083f9-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="083f9-151">**Audio**:</span></span>

* <span data-ttu-id="083f9-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="083f9-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="083f9-153">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="083f9-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="083f9-154">Frequenza di campionamento: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="083f9-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="083f9-155">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="083f9-155">Configuration steps</span></span>
1. <span data-ttu-id="083f9-156">Passare toohello che Flash Live codificatore multimediale (FMLE) interfaccia sul computer hello in uso.</span><span class="sxs-lookup"><span data-stu-id="083f9-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="083f9-157">interfaccia Hello è una pagina principale di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="083f9-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="083f9-158">Per prendere nota dei seguenti hello consigliati tooget impostazioni introduttiva streaming mediante FMLE.</span><span class="sxs-lookup"><span data-stu-id="083f9-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="083f9-159">Formato: Frequenza dei fotogrammi h. 264: 30,00</span><span class="sxs-lookup"><span data-stu-id="083f9-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="083f9-160">Dimensione di input: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="083f9-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="083f9-161">Velocità in bit: Kbps 5000 (può essere regolato in base alle limitazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="083f9-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="083f9-163">Quando tramite interlacciata origini, il segno di spunta hello "Deinterlaccia" opzione</span><span class="sxs-lookup"><span data-stu-id="083f9-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="083f9-164">Icona chiave inglese hello selezionare tooFormat Avanti, queste impostazioni aggiuntive devono essere:</span><span class="sxs-lookup"><span data-stu-id="083f9-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="083f9-165">Profilo: principale</span><span class="sxs-lookup"><span data-stu-id="083f9-165">Profile: Main</span></span>
   * <span data-ttu-id="083f9-166">Livello: 4.0</span><span class="sxs-lookup"><span data-stu-id="083f9-166">Level: 4.0</span></span>
   * <span data-ttu-id="083f9-167">Frequenza dei fotogrammi chiave: 2 secondi</span><span class="sxs-lookup"><span data-stu-id="083f9-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="083f9-169">Impostare hello impostazione audio importanti seguenti:</span><span class="sxs-lookup"><span data-stu-id="083f9-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="083f9-170">Formato: AAC</span><span class="sxs-lookup"><span data-stu-id="083f9-170">Format: AAC</span></span>
   * <span data-ttu-id="083f9-171">Frequenza di campionamento: 44100 kHz</span><span class="sxs-lookup"><span data-stu-id="083f9-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="083f9-172">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="083f9-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="083f9-174">Ottenere l'URL di input del canale hello in ordine tooassign è del toohello FMLE **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="083f9-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="083f9-175">Passare strumento AMSE toohello indietro e controllare lo stato di completamento di hello del canale.</span><span class="sxs-lookup"><span data-stu-id="083f9-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="083f9-176">Una volta hello stato è cambiato da **iniziale** troppo**esecuzione**, è possibile ottenere l'URL di input hello.</span><span class="sxs-lookup"><span data-stu-id="083f9-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="083f9-177">Quando il canale hello è in esecuzione, fare clic con il pulsante destro nome canale hello, spostarsi verso il basso toohover su **Copia URL di Input tooclipboard** e quindi selezionare **URL di Input primaria**.</span><span class="sxs-lookup"><span data-stu-id="083f9-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="083f9-179">Incollare le informazioni in hello **URL FMS** campo della sezione di output di hello e di assegnare un nome di flusso.</span><span class="sxs-lookup"><span data-stu-id="083f9-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="083f9-181">Per garantire la ridondanza aggiuntiva, ripetere questi passaggi con hello secondario URL di Input.</span><span class="sxs-lookup"><span data-stu-id="083f9-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="083f9-182">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="083f9-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="083f9-183">Prima di scegliere **Connetti**, si **deve** assicurarsi che il canale hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="083f9-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="083f9-184">Inoltre, assicurarsi che non tooleave hello canale in uno stato pronto senza un contributo input feed per più di 15 minuti di >.</span><span class="sxs-lookup"><span data-stu-id="083f9-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="083f9-185">Testare la riproduzione</span><span class="sxs-lookup"><span data-stu-id="083f9-185">Test playback</span></span>

<span data-ttu-id="083f9-186">Passare strumento AMSE toohello e fare clic con il pulsante destro hello canale toobe testato.</span><span class="sxs-lookup"><span data-stu-id="083f9-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="083f9-187">Dal menu di hello, passare il mouse su **hello riproduzione anteprima** e selezionare **con Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="083f9-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="083f9-188">Se il flusso di hello viene visualizzato nel lettore hello, codificatore hello è stato configurato correttamente tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="083f9-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="083f9-189">Se viene ricevuto un errore, il canale hello sarà necessario toobe reimpostazione e il codificatore le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="083f9-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="083f9-190">Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="083f9-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="083f9-191">Creare un programma.</span><span class="sxs-lookup"><span data-stu-id="083f9-191">Create a program</span></span>
1. <span data-ttu-id="083f9-192">Una volta che viene confermata la riproduzione del canale, creare un programma.</span><span class="sxs-lookup"><span data-stu-id="083f9-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="083f9-193">In hello **Live** nello strumento AMSE hello, fare clic con il pulsante destro nell'area di programma hello e selezionare **creare un nuovo programma**.</span><span class="sxs-lookup"><span data-stu-id="083f9-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="083f9-195">Nome programma hello e, se necessario, modificare hello **lunghezza dell'intervallo di archivio** (le impostazioni predefinite too4 ore).</span><span class="sxs-lookup"><span data-stu-id="083f9-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="083f9-196">È inoltre possibile specificare un percorso di archiviazione o lasciare hello predefinite.</span><span class="sxs-lookup"><span data-stu-id="083f9-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="083f9-197">Controllare hello **ora inizio hello programma** casella.</span><span class="sxs-lookup"><span data-stu-id="083f9-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="083f9-198">Fare clic su **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="083f9-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="083f9-199">La creazione di un programma richiede meno tempo rispetto alla creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="083f9-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="083f9-200">Quando è in esecuzione il programma hello, confermare la riproduzione facendo clic con il pulsante destro programma hello e passando troppo**riproduzione hello programmi** e quindi selezionando **con Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="083f9-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="083f9-201">Una volta confermato, fare clic nuovamente il programma hello e scegliere **copiare tooClipboard URL di Output di hello** (o recuperare queste informazioni da hello **informazioni e le impostazioni del programma** opzione dal menu di hello).</span><span class="sxs-lookup"><span data-stu-id="083f9-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="083f9-202">flusso Hello è ora pronto toobe incorporato in un lettore o destinatari tooan distribuita per live visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="083f9-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="083f9-203">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="083f9-203">Troubleshooting</span></span>
<span data-ttu-id="083f9-204">Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="083f9-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="083f9-205">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="083f9-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="083f9-206">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="083f9-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
