---
title: "Configurare il codificatore Elemental Live per inviare un flusso live a velocità in bit singola | Microsoft Docs"
description: "In questo argomento viene illustrato come configurare il codificatore Elemental Live per inviare un flusso a velocità in bit singola a canali AMS abilitati per la codifica live."
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
ms.openlocfilehash: 668a3ab46a70c0ee25fa87031d27c0f4333ec89c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="72b0c-103">Usare il codificatore Elemental Live per inviare un flusso live a velocità in bit singola.</span><span class="sxs-lookup"><span data-stu-id="72b0c-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72b0c-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="72b0c-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="72b0c-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="72b0c-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="72b0c-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="72b0c-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="72b0c-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="72b0c-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="72b0c-108">In questo argomento viene illustrato come configurare il codificatore [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) per inviare un flusso a velocità in bit singola a canali AMS abilitati per la codifica live.</span><span class="sxs-lookup"><span data-stu-id="72b0c-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="72b0c-109">Per altre informazioni, vedere [Uso di canali abilitati per l'esecuzione della codifica live con Servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="72b0c-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="72b0c-110">In questa esercitazione viene illustrato come gestire Servizi multimediali di Azure (AMS) con lo strumento Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="72b0c-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="72b0c-111">Questo strumento può essere eseguito solo in PC Windows.</span><span class="sxs-lookup"><span data-stu-id="72b0c-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="72b0c-112">Gli utenti di sistemi Mac o Linux possono usare il Portale di Azure per creare [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="72b0c-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72b0c-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="72b0c-113">Prerequisites</span></span>
* <span data-ttu-id="72b0c-114">Sono necessarie conoscenze pratiche dell'uso dell'interfaccia Web Elemental Live per la creazione di eventi live.</span><span class="sxs-lookup"><span data-stu-id="72b0c-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* [<span data-ttu-id="72b0c-115">Creare un account Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="72b0c-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="72b0c-116">Verificare che sia presente un endpoint di streaming in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="72b0c-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="72b0c-117">Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="72b0c-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="72b0c-118">Installare la versione più recente dello strumento [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="72b0c-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="72b0c-119">Avviare lo strumento e connettersi al proprio account AMS.</span><span class="sxs-lookup"><span data-stu-id="72b0c-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="72b0c-120">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="72b0c-120">Tips</span></span>
* <span data-ttu-id="72b0c-121">Se possibile, usare una connessione a Internet con cablaggio fisico.</span><span class="sxs-lookup"><span data-stu-id="72b0c-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="72b0c-122">È buona norma raddoppiare le velocità in bit di streaming in fase di determinazione dei requisiti di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="72b0c-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="72b0c-123">Anche se non si tratta di un requisito obbligatorio, contribuirà a ridurre l'impatto della congestione della rete.</span><span class="sxs-lookup"><span data-stu-id="72b0c-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="72b0c-124">Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.</span><span class="sxs-lookup"><span data-stu-id="72b0c-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="72b0c-125">Elemental Live con inserimento RTP</span><span class="sxs-lookup"><span data-stu-id="72b0c-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="72b0c-126">In questa sezione viene illustrato come configurare il codificatore Elemental Live che invia un flusso live a velocità in bit singola su RTP.</span><span class="sxs-lookup"><span data-stu-id="72b0c-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="72b0c-127">Per altre informazioni, vedere [Flusso MPEG-TS su RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="72b0c-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="72b0c-128">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="72b0c-128">Create a channel</span></span>

1. <span data-ttu-id="72b0c-129">Nello strumento AMSE passare alla scheda **Live** e fare clic con il pulsante destro del mouse all'interno dell'area del canale.</span><span class="sxs-lookup"><span data-stu-id="72b0c-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="72b0c-130">Scegliere **Create channel**</span><span class="sxs-lookup"><span data-stu-id="72b0c-130">Select **Create channel…**</span></span> <span data-ttu-id="72b0c-131">dal menu.</span><span class="sxs-lookup"><span data-stu-id="72b0c-131">from the menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="72b0c-133">Specificare un nome di canale. Il campo della descrizione è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="72b0c-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="72b0c-134">In Impostazioni del canale selezionare **Standard** per l'opzione Codifica live con il protocollo di input impostato su **RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="72b0c-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="72b0c-135">È possibile confermare tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="72b0c-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="72b0c-136">Assicurarsi che l'opzione **Avvia ora il nuovo canale** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="72b0c-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="72b0c-137">Fare clic su **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="72b0c-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="72b0c-139">Per l'avvio del canale possono essere richiesti fino a 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="72b0c-139">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="72b0c-140">Durante l'avvio di canale è possibile [configurare il codificatore](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="72b0c-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72b0c-141">Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto.</span><span class="sxs-lookup"><span data-stu-id="72b0c-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="72b0c-142">Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="72b0c-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="72b0c-143"><a id=configure_elemental_rtp></a>Configurare il codificatore Elemental Live</span><span class="sxs-lookup"><span data-stu-id="72b0c-143"><a id=configure_elemental_rtp></a>Configure the Elemental Live encoder</span></span>
<span data-ttu-id="72b0c-144">In questa esercitazione vengono usate le seguenti impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="72b0c-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="72b0c-145">Nel resto di questa sezione vengono descritti in maggiore dettaglio i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="72b0c-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="72b0c-146">**Video**:</span><span class="sxs-lookup"><span data-stu-id="72b0c-146">**Video**:</span></span>

* <span data-ttu-id="72b0c-147">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="72b0c-147">Codec: H.264</span></span>
* <span data-ttu-id="72b0c-148">Profilo: alto (livello 4.0)</span><span class="sxs-lookup"><span data-stu-id="72b0c-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="72b0c-149">Velocità in bit: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="72b0c-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="72b0c-150">Fotogramma chiave: 2 secondi (60 secondi)</span><span class="sxs-lookup"><span data-stu-id="72b0c-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="72b0c-151">Frequenza dei fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="72b0c-151">Frame Rate: 30</span></span>

<span data-ttu-id="72b0c-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="72b0c-152">**Audio**:</span></span>

* <span data-ttu-id="72b0c-153">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="72b0c-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="72b0c-154">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="72b0c-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="72b0c-155">Frequenza di campionamento: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="72b0c-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="72b0c-156">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="72b0c-156">Configuration steps</span></span>
1. <span data-ttu-id="72b0c-157">Accedere all'interfaccia Web di **Elemental Live** e configurare il codificatore per lo streaming **UDP/TS**.</span><span class="sxs-lookup"><span data-stu-id="72b0c-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="72b0c-158">Dopo aver creato un nuovo evento, scorrere verso il basso fino ai gruppi di output e aggiungere il gruppo di output **UDP/TS** .</span><span class="sxs-lookup"><span data-stu-id="72b0c-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="72b0c-159">Creare un nuovo output selezionando **Nuovo flusso** e quindi facendo clic su **Aggiungi output**.</span><span class="sxs-lookup"><span data-stu-id="72b0c-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="72b0c-161">È consigliabile che per l'evento Elemental il codice temporale sia impostato sull'orologio di sistema per facilitare la riconnessione del codificatore in caso di un errore di flusso.</span><span class="sxs-lookup"><span data-stu-id="72b0c-161">It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="72b0c-162">Dopo aver creato l'output, fare clic su **Aggiungi flusso**.</span><span class="sxs-lookup"><span data-stu-id="72b0c-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="72b0c-163">È ora possibile configurare le impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="72b0c-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="72b0c-164">Scorrere verso il basso fino al flusso "Flusso 1" appena creato, fare clic sulla scheda **Video** a sinistra ed espandere la sezione delle impostazioni **Avanzate**.</span><span class="sxs-lookup"><span data-stu-id="72b0c-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="72b0c-166">Anche se per Elemental Live è disponibile un'ampia gamma di personalizzazioni, per iniziare con lo streaming verso AMS sono consigliate le impostazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="72b0c-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="72b0c-167">Risoluzione: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="72b0c-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="72b0c-168">Frequenza fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="72b0c-168">Framerate: 30</span></span>
   * <span data-ttu-id="72b0c-169">Dimensioni GOP: 60 fotogrammi</span><span class="sxs-lookup"><span data-stu-id="72b0c-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="72b0c-170">Modalità interlacciamento: progressivo</span><span class="sxs-lookup"><span data-stu-id="72b0c-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="72b0c-171">Velocità in bit: 5000000 bit/s (regolabile in base alle limitazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="72b0c-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="72b0c-173">Ottenere l'URL di input del canale.</span><span class="sxs-lookup"><span data-stu-id="72b0c-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="72b0c-174">Passare allo strumento AMSE e controllare lo stato di completamento del canale.</span><span class="sxs-lookup"><span data-stu-id="72b0c-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="72b0c-175">Una volta che lo stato è passato da **Avvio in corso** a **In esecuzione**, è possibile ottenere l'URL di input.</span><span class="sxs-lookup"><span data-stu-id="72b0c-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="72b0c-176">Quando il canale è in esecuzione, fare clic con il pulsante destro del mouse sul nome del canale, spostarsi verso il basso per passare il puntatore sull'opzione **Copy Input URL to clipboard** (Copia URL di input negli Appunti) e quindi selezionare **Primary Input URL** (URL di input primario).</span><span class="sxs-lookup"><span data-stu-id="72b0c-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="72b0c-178">Incollare queste informazioni nel campo **Destinazione principale** di Elemental.</span><span class="sxs-lookup"><span data-stu-id="72b0c-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="72b0c-179">Per tutte le altre opzioni è possibile mantenere l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="72b0c-179">All other settings can remain the default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="72b0c-181">Per garantire una maggiore ridondanza, ripetere questi passaggi con l'URL di input secondario mediante la creazione di una scheda separata "Output" per lo streaming UDP/TS.</span><span class="sxs-lookup"><span data-stu-id="72b0c-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="72b0c-182">Fare clic su **Crea** (se è stato creato un nuovo evento) o **Aggiorna** (in caso di modifica di un evento preesistente) e quindi procedere con l'avvio del codificatore.</span><span class="sxs-lookup"><span data-stu-id="72b0c-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72b0c-183">Prima di scegliere **Avvia** nell'interfaccia Web di Elemental Live, **è necessario** verificare che il canale sia pronto.</span><span class="sxs-lookup"><span data-stu-id="72b0c-183">Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="72b0c-184">Assicurarsi inoltre di non lasciare il canale in uno stato pronto senza un evento per più di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="72b0c-184">Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="72b0c-185">Dopo 30 secondi di esecuzione del flusso, tornare allo strumento AMSE e testare la riproduzione.</span><span class="sxs-lookup"><span data-stu-id="72b0c-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="72b0c-186">Testare la riproduzione</span><span class="sxs-lookup"><span data-stu-id="72b0c-186">Test playback</span></span>

<span data-ttu-id="72b0c-187">Passare allo strumento AMSE e fare clic con il pulsante destro del mouse sul canale da testare.</span><span class="sxs-lookup"><span data-stu-id="72b0c-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="72b0c-188">Nel menu passare il mouse su **Playback the Preview** (Riproduci anteprima) e scegliere **with Azure Media Player** (Con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="72b0c-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="72b0c-189">Se il flusso viene visualizzato nel lettore, ciò indica che il codificatore è stato configurato correttamente per connettersi a AMS.</span><span class="sxs-lookup"><span data-stu-id="72b0c-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="72b0c-190">In caso di errore, sarà necessario reimpostare il canale e regolare le impostazioni del codificatore.</span><span class="sxs-lookup"><span data-stu-id="72b0c-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="72b0c-191">Vedere l’argomento sulla [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) per ricevere istruzioni.</span><span class="sxs-lookup"><span data-stu-id="72b0c-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="72b0c-192">Creare un programma.</span><span class="sxs-lookup"><span data-stu-id="72b0c-192">Create a program</span></span>
1. <span data-ttu-id="72b0c-193">Una volta che viene confermata la riproduzione del canale, creare un programma.</span><span class="sxs-lookup"><span data-stu-id="72b0c-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="72b0c-194">Sotto la scheda **Live** nello strumento AMSE fare clic con il pulsante destro del mouse all'interno dell'area di programma e selezionare **Create New Program** (Crea nuovo programma).</span><span class="sxs-lookup"><span data-stu-id="72b0c-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="72b0c-196">Assegnare un nome al programma e, se necessario, modificare l'opzione **Archive Window Length** (con impostazione predefinita di 4 ore).</span><span class="sxs-lookup"><span data-stu-id="72b0c-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="72b0c-197">È inoltre possibile specificare un percorso di archiviazione o confermare l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="72b0c-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="72b0c-198">Selezionare la casella di controllo **Start the Program now** .</span><span class="sxs-lookup"><span data-stu-id="72b0c-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="72b0c-199">Fare clic su **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="72b0c-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="72b0c-200">La creazione di un programma richiede meno tempo rispetto alla creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="72b0c-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="72b0c-201">Quando il programma è in esecuzione, verificare il funzionamento della riproduzione. A tale scopo, fare clic con il pulsante destro del mouse sul programma e passare **Playback the program(s)** (Riproduci programma/i), quindi scegliere **with Azure Media Player** (Con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="72b0c-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="72b0c-202">Dopo questa verifica, fare nuovamente clic con il pulsante destro del mouse sul programma e scegliere **Copy the Output URL to Clipboard** (Copia URL di output negli Appunti) oppure recuperare queste informazioni dall'opzione **Program information and settings** (Impostazioni e informazioni programma) nel menu.</span><span class="sxs-lookup"><span data-stu-id="72b0c-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="72b0c-203">Il flusso è ora pronto per essere incorporato in un lettore o distribuito per la visualizzazione pubblica live.</span><span class="sxs-lookup"><span data-stu-id="72b0c-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="72b0c-204">risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="72b0c-204">Troubleshooting</span></span>
<span data-ttu-id="72b0c-205">Vedere l’argomento sulla [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) per ricevere istruzioni.</span><span class="sxs-lookup"><span data-stu-id="72b0c-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="72b0c-206">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="72b0c-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="72b0c-207">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="72b0c-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
