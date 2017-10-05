---
title: "Configurare il codificatore Telestream Wirecast per inviare un flusso live a velocità in bit singola | Microsoft Docs"
description: "In questo argomento viene illustrato come configurare il codificatore live Wirecast per inviare un flusso a velocità in bit singola a canali AMS abilitati per la codifica live. "
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
ms.openlocfilehash: c4df14f24650ce431dfb31cc774cab6d3cf3aef0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-wirecast-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="ffd63-103">Usare il codificatore Wirecast per inviare un flusso live a velocità in bit singola.</span><span class="sxs-lookup"><span data-stu-id="ffd63-103">Use the Wirecast encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ffd63-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="ffd63-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="ffd63-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="ffd63-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="ffd63-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="ffd63-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="ffd63-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="ffd63-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="ffd63-108">In questo argomento viene illustrato come configurare il codificatore [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) per inviare un flusso a velocità in bit singola a canali AMS abilitati per la codifica live.</span><span class="sxs-lookup"><span data-stu-id="ffd63-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="ffd63-109">Per altre informazioni, vedere [Uso di canali abilitati per l'esecuzione della codifica live con Servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="ffd63-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="ffd63-110">In questa esercitazione viene illustrato come gestire Servizi multimediali di Azure (AMS) con lo strumento Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="ffd63-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="ffd63-111">Questo strumento può essere eseguito solo in PC Windows.</span><span class="sxs-lookup"><span data-stu-id="ffd63-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="ffd63-112">Gli utenti di sistemi Mac o Linux possono usare il Portale di Azure per creare [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="ffd63-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffd63-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ffd63-113">Prerequisites</span></span>
* [<span data-ttu-id="ffd63-114">Creare un account Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="ffd63-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="ffd63-115">Verificare che sia presente un endpoint di streaming in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ffd63-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="ffd63-116">Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="ffd63-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="ffd63-117">Installare la versione più recente dello strumento [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="ffd63-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="ffd63-118">Avviare lo strumento e connettersi al proprio account AMS.</span><span class="sxs-lookup"><span data-stu-id="ffd63-118">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="ffd63-119">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ffd63-119">Tips</span></span>
* <span data-ttu-id="ffd63-120">Se possibile, usare una connessione a Internet con cablaggio fisico.</span><span class="sxs-lookup"><span data-stu-id="ffd63-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="ffd63-121">È buona norma raddoppiare le velocità in bit di streaming in fase di determinazione dei requisiti di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="ffd63-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="ffd63-122">Anche se non si tratta di un requisito obbligatorio, contribuirà a ridurre l'impatto della congestione della rete.</span><span class="sxs-lookup"><span data-stu-id="ffd63-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="ffd63-123">Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.</span><span class="sxs-lookup"><span data-stu-id="ffd63-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="ffd63-124">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="ffd63-124">Create a channel</span></span>
1. <span data-ttu-id="ffd63-125">Nello strumento AMSE passare alla scheda **Live** e fare clic con il pulsante destro del mouse all'interno dell'area del canale.</span><span class="sxs-lookup"><span data-stu-id="ffd63-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="ffd63-126">Scegliere **Create channel**</span><span class="sxs-lookup"><span data-stu-id="ffd63-126">Select **Create channel…**</span></span> <span data-ttu-id="ffd63-127">dal menu.</span><span class="sxs-lookup"><span data-stu-id="ffd63-127">from the menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="ffd63-129">Specificare un nome di canale. Il campo della descrizione è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ffd63-129">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="ffd63-130">In Impostazioni del canale selezionare **Standard** per l'opzione di codifica live con il protocollo di input impostato su **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="ffd63-131">È possibile confermare tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="ffd63-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="ffd63-132">Assicurarsi che l'opzione **Avvia ora il nuovo canale** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="ffd63-132">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="ffd63-133">Fare clic su **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="ffd63-135">Per l'avvio del canale possono essere richiesti fino a 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="ffd63-135">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="ffd63-136">Durante l'avvio di canale è possibile [configurare il codificatore](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="ffd63-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffd63-137">Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto.</span><span class="sxs-lookup"><span data-stu-id="ffd63-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="ffd63-138">Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="ffd63-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="ffd63-139"><a id=configure_wirecast_rtmp></a>Configurare il codificatore Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="ffd63-139"><a id=configure_wirecast_rtmp></a>Configure the Telestream Wirecast encoder</span></span>
<span data-ttu-id="ffd63-140">In questa esercitazione vengono usate le seguenti impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="ffd63-140">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="ffd63-141">Nel resto di questa sezione vengono descritti in maggiore dettaglio i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ffd63-141">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="ffd63-142">**Video**:</span><span class="sxs-lookup"><span data-stu-id="ffd63-142">**Video**:</span></span>

* <span data-ttu-id="ffd63-143">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="ffd63-143">Codec: H.264</span></span>
* <span data-ttu-id="ffd63-144">Profilo: alto (livello 4.0)</span><span class="sxs-lookup"><span data-stu-id="ffd63-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="ffd63-145">Velocità in bit: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="ffd63-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="ffd63-146">Fotogramma chiave: 2 secondi (60 secondi)</span><span class="sxs-lookup"><span data-stu-id="ffd63-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="ffd63-147">Frequenza dei fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="ffd63-147">Frame Rate: 30</span></span>

<span data-ttu-id="ffd63-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="ffd63-148">**Audio**:</span></span>

* <span data-ttu-id="ffd63-149">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="ffd63-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="ffd63-150">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="ffd63-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="ffd63-151">Frequenza di campionamento: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="ffd63-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="ffd63-152">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="ffd63-152">Configuration steps</span></span>
1. <span data-ttu-id="ffd63-153">Aprire l'applicazione Telestream Wirecast sul computer utilizzato e impostare per il flusso RTP.</span><span class="sxs-lookup"><span data-stu-id="ffd63-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="ffd63-154">Configurare l'output accedendo alla scheda **Output** e selezionando **Output Settings…** (Impostazioni di output...).</span><span class="sxs-lookup"><span data-stu-id="ffd63-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="ffd63-155">Assicurarsi che **Destinazione di uscita** sia impostato su **RTMP Server** (Server RTMP).</span><span class="sxs-lookup"><span data-stu-id="ffd63-155">Make sure the **Output Destination** is set to **RTMP Server**.</span></span>
3. <span data-ttu-id="ffd63-156">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-156">Click **OK**.</span></span>
4. <span data-ttu-id="ffd63-157">Nella pagina delle impostazioni impostare il campo **Destinazione** su **Servizi multimediali di Azure**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span></span>

    <span data-ttu-id="ffd63-158">Il profilo di codifica è già pre-selezionato per **Azure H.264 720p 16:9 (1280x720)**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="ffd63-159">Per personalizzare queste impostazioni, selezionare l'icona raffigurante un ingranaggio a destra dell'elenco a discesa e poi scegliere **Nuovo predefinito**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="ffd63-161">Configura le impostazioni predefinite del codificatore.</span><span class="sxs-lookup"><span data-stu-id="ffd63-161">Configure encoder presets.</span></span>

    <span data-ttu-id="ffd63-162">Denominare il set di impostazioni e verificare le seguenti impostazioni consigliate:</span><span class="sxs-lookup"><span data-stu-id="ffd63-162">Name the preset, and check for the following recommended settings:</span></span>

    <span data-ttu-id="ffd63-163">**Video**</span><span class="sxs-lookup"><span data-stu-id="ffd63-163">**Video**</span></span>

   * <span data-ttu-id="ffd63-164">Codificatore: MainConcept h. 264</span><span class="sxs-lookup"><span data-stu-id="ffd63-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="ffd63-165">Fotogrammi al secondo: 30</span><span class="sxs-lookup"><span data-stu-id="ffd63-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="ffd63-166">Velocità in bit media: 5000 kbit al secondo (può essere regolato in base alle limitazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="ffd63-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="ffd63-167">Profilo: principale</span><span class="sxs-lookup"><span data-stu-id="ffd63-167">Profile: Main</span></span>
   * <span data-ttu-id="ffd63-168">Fotogramma chiave ogni: 60 fotogrammi</span><span class="sxs-lookup"><span data-stu-id="ffd63-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="ffd63-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="ffd63-169">**Audio**</span></span>

   * <span data-ttu-id="ffd63-170">Velocità in bit di destinazione: 192 kbit/sec</span><span class="sxs-lookup"><span data-stu-id="ffd63-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="ffd63-171">Frequenza di campionamento: 44,100 kHz</span><span class="sxs-lookup"><span data-stu-id="ffd63-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="ffd63-173">Premere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-173">Press **Save**.</span></span>

    <span data-ttu-id="ffd63-174">Il campo di codifica è ora il profilo appena creato disponibile per la selezione.</span><span class="sxs-lookup"><span data-stu-id="ffd63-174">The Encoding field now has the newly created profile available for selection.</span></span>

    <span data-ttu-id="ffd63-175">Verificare che venga selezionato il nuovo profilo.</span><span class="sxs-lookup"><span data-stu-id="ffd63-175">Make sure the new profile is selected.</span></span>
7. <span data-ttu-id="ffd63-176">Ottenere l’input URL del canale per assegnargli il Wirecast **RTMP Endpoint**.\\</span><span class="sxs-lookup"><span data-stu-id="ffd63-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="ffd63-177">Passare allo strumento AMSE e controllare lo stato di completamento del canale.</span><span class="sxs-lookup"><span data-stu-id="ffd63-177">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="ffd63-178">Una volta che lo stato è passato da **Avvio in corso** a **In esecuzione**, è possibile ottenere l'URL di input.</span><span class="sxs-lookup"><span data-stu-id="ffd63-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="ffd63-179">Quando il canale è in esecuzione, fare clic con il pulsante destro del mouse sul nome del canale, spostarsi verso il basso per passare il puntatore sull'opzione **Copy Input URL to clipboard** (Copia URL di input negli Appunti) e quindi selezionare **Primary Input URL** (URL di input primario).</span><span class="sxs-lookup"><span data-stu-id="ffd63-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="ffd63-181">Nella finestra **Output Settings** (Impostazioni di output) di Wirecast incollare queste informazioni nel campo **Indirizzo** della sezione relativa all'output e assegnare un nome di flusso.</span><span class="sxs-lookup"><span data-stu-id="ffd63-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="ffd63-183">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-183">Select **OK**.</span></span>
2. <span data-ttu-id="ffd63-184">Nella schermata principale **Wirecast** confermare che le origini di input per video e audio sono pronte e quindi premere **Flusso** nell'angolo superiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="ffd63-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="ffd63-186">Prima di fare clic su **Flusso**, **è necessario** assicurarsi che il canale sia pronto.</span><span class="sxs-lookup"><span data-stu-id="ffd63-186">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="ffd63-187">Assicurarsi inoltre di non lasciare il canale in uno stato pronto senza un feed per l’input/contributo per più di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="ffd63-187">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="ffd63-188">Testare la riproduzione</span><span class="sxs-lookup"><span data-stu-id="ffd63-188">Test playback</span></span>

<span data-ttu-id="ffd63-189">Passare allo strumento AMSE e fare clic con il pulsante destro del mouse sul canale da testare.</span><span class="sxs-lookup"><span data-stu-id="ffd63-189">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="ffd63-190">Nel menu passare il mouse su **Playback the Preview** (Riproduci anteprima) e scegliere **with Azure Media Player** (Con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="ffd63-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="ffd63-191">Se il flusso viene visualizzato nel lettore, ciò indica che il codificatore è stato configurato correttamente per connettersi a AMS.</span><span class="sxs-lookup"><span data-stu-id="ffd63-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="ffd63-192">In caso di errore, sarà necessario reimpostare il canale e regolare le impostazioni del codificatore.</span><span class="sxs-lookup"><span data-stu-id="ffd63-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="ffd63-193">Vedere l’argomento sulla [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) per ricevere istruzioni.</span><span class="sxs-lookup"><span data-stu-id="ffd63-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="ffd63-194">Creare un programma.</span><span class="sxs-lookup"><span data-stu-id="ffd63-194">Create a program</span></span>
1. <span data-ttu-id="ffd63-195">Una volta che viene confermata la riproduzione del canale, creare un programma.</span><span class="sxs-lookup"><span data-stu-id="ffd63-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="ffd63-196">Sotto la scheda **Live** nello strumento AMSE fare clic con il pulsante destro del mouse all'interno dell'area di programma e selezionare **Create New Program** (Crea nuovo programma).</span><span class="sxs-lookup"><span data-stu-id="ffd63-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="ffd63-198">Assegnare un nome al programma e, se necessario, modificare l'opzione **Archive Window Length** (con impostazione predefinita di 4 ore).</span><span class="sxs-lookup"><span data-stu-id="ffd63-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="ffd63-199">È inoltre possibile specificare un percorso di archiviazione o confermare l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ffd63-199">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="ffd63-200">Selezionare la casella di controllo **Start the Program now** .</span><span class="sxs-lookup"><span data-stu-id="ffd63-200">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="ffd63-201">Fare clic su **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="ffd63-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="ffd63-202">La creazione di un programma richiede meno tempo rispetto alla creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="ffd63-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="ffd63-203">Quando il programma è in esecuzione, verificare il funzionamento della riproduzione. A tale scopo, fare clic con il pulsante destro del mouse sul programma e passare **Playback the program(s)** (Riproduci programma/i), quindi scegliere **with Azure Media Player** (Con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="ffd63-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="ffd63-204">Dopo questa verifica, fare nuovamente clic con il pulsante destro del mouse sul programma e scegliere **Copy the Output URL to Clipboard** (Copia URL di output negli Appunti) oppure recuperare queste informazioni dall'opzione **Program information and settings** (Impostazioni e informazioni programma) nel menu.</span><span class="sxs-lookup"><span data-stu-id="ffd63-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="ffd63-205">Il flusso è ora pronto per essere incorporato in un lettore o distribuito per la visualizzazione pubblica live.</span><span class="sxs-lookup"><span data-stu-id="ffd63-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="ffd63-206">risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ffd63-206">Troubleshooting</span></span>
<span data-ttu-id="ffd63-207">Vedere l’argomento sulla [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) per ricevere istruzioni.</span><span class="sxs-lookup"><span data-stu-id="ffd63-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ffd63-208">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ffd63-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ffd63-209">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ffd63-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
