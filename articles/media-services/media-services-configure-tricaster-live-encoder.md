---
title: "Configurare il codificatore NewTek TriCaster per inviare un flusso live a velocità in bit singola | Microsoft Docs"
description: "In questo argomento viene illustrato come configurare il codificatore Tricaster per inviare un flusso a velocità in bit singola a canali AMS abilitati per la codifica live."
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
ms.openlocfilehash: 42b012fb98bd0504c931ce391d63aecca8c3d311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="42e7b-103">Utilizzare il codificatore NewTek TriCaster per inviare un flusso live a velocità in bit singola.</span><span class="sxs-lookup"><span data-stu-id="42e7b-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="42e7b-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="42e7b-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="42e7b-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="42e7b-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="42e7b-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="42e7b-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="42e7b-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="42e7b-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="42e7b-108">In questo argomento viene illustrato come configurare il codificatore live [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) per inviare un flusso a velocità in bit singola a canali AMS abilitati per la codifica live.</span><span class="sxs-lookup"><span data-stu-id="42e7b-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="42e7b-109">Per altre informazioni, vedere [Uso di canali abilitati per l'esecuzione della codifica live con Servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="42e7b-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="42e7b-110">In questa esercitazione viene illustrato come gestire Servizi multimediali di Azure (AMS) con lo strumento Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="42e7b-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="42e7b-111">Questo strumento può essere eseguito solo in PC Windows.</span><span class="sxs-lookup"><span data-stu-id="42e7b-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="42e7b-112">Gli utenti di sistemi Mac o Linux possono usare il Portale di Azure per creare [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="42e7b-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="42e7b-113">Quando si usa Tricaster per l'invio di un feed di contributo ai canali AMS abilitati per la codifica live, in particolare quando si usano alcune funzionalità di Tricaster, ad esempio tagli rapidi tra i feed o passaggi all'interno e all'esterno di slate, sono possibili anomalie audio/video nell'evento live.</span><span class="sxs-lookup"><span data-stu-id="42e7b-113">When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="42e7b-114">Il team di AMS sta lavorando per risolvere questi problemi. Fino a quel momento non è consigliabile usare queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="42e7b-114">The AMS team is working on fixing these issues, until then, it is not recommend to use these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="42e7b-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="42e7b-115">Prerequisites</span></span>
* [<span data-ttu-id="42e7b-116">Creare un account Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="42e7b-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="42e7b-117">Verificare che sia presente un endpoint di streaming in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="42e7b-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="42e7b-118">Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="42e7b-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="42e7b-119">Installare la versione più recente dello strumento [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="42e7b-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="42e7b-120">Avviare lo strumento e connettersi al proprio account AMS.</span><span class="sxs-lookup"><span data-stu-id="42e7b-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="42e7b-121">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="42e7b-121">Tips</span></span>
* <span data-ttu-id="42e7b-122">Se possibile, usare una connessione a Internet con cablaggio fisico.</span><span class="sxs-lookup"><span data-stu-id="42e7b-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="42e7b-123">È buona norma raddoppiare le velocità in bit di streaming in fase di determinazione dei requisiti di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="42e7b-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="42e7b-124">Anche se non si tratta di un requisito obbligatorio, contribuirà a ridurre l'impatto della congestione della rete.</span><span class="sxs-lookup"><span data-stu-id="42e7b-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="42e7b-125">Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.</span><span class="sxs-lookup"><span data-stu-id="42e7b-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="42e7b-126">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="42e7b-126">Create a channel</span></span>
1. <span data-ttu-id="42e7b-127">Nello strumento AMSE passare alla scheda **Live** e fare clic con il pulsante destro del mouse all'interno dell'area del canale.</span><span class="sxs-lookup"><span data-stu-id="42e7b-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="42e7b-128">Scegliere **Create channel**</span><span class="sxs-lookup"><span data-stu-id="42e7b-128">Select **Create channel…**</span></span> <span data-ttu-id="42e7b-129">dal menu.</span><span class="sxs-lookup"><span data-stu-id="42e7b-129">from the menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="42e7b-131">Specificare un nome di canale. Il campo della descrizione è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="42e7b-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="42e7b-132">In Impostazioni del canale selezionare **Standard** per l'opzione di codifica live con il protocollo di input impostato su **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="42e7b-133">È possibile confermare tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="42e7b-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="42e7b-134">Assicurarsi che l'opzione **Avvia ora il nuovo canale** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="42e7b-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="42e7b-135">Fare clic su **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="42e7b-137">Per l'avvio del canale possono essere richiesti fino a 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="42e7b-137">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="42e7b-138">Durante l'avvio di canale è possibile [configurare il codificatore](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="42e7b-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42e7b-139">Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto.</span><span class="sxs-lookup"><span data-stu-id="42e7b-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="42e7b-140">Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="42e7b-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="42e7b-141"><a id=configure_tricaster_rtmp></a>Configurare il codificatore NewTek TriCaster</span><span class="sxs-lookup"><span data-stu-id="42e7b-141"><a id=configure_tricaster_rtmp></a>Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="42e7b-142">In questa esercitazione vengono usate le seguenti impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="42e7b-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="42e7b-143">Nel resto di questa sezione vengono descritti in maggiore dettaglio i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="42e7b-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="42e7b-144">**Video**:</span><span class="sxs-lookup"><span data-stu-id="42e7b-144">**Video**:</span></span>

* <span data-ttu-id="42e7b-145">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="42e7b-145">Codec: H.264</span></span>
* <span data-ttu-id="42e7b-146">Profilo: alto (livello 4.0)</span><span class="sxs-lookup"><span data-stu-id="42e7b-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="42e7b-147">Velocità in bit: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="42e7b-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="42e7b-148">Fotogramma chiave: 2 secondi (60 secondi)</span><span class="sxs-lookup"><span data-stu-id="42e7b-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="42e7b-149">Frequenza dei fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="42e7b-149">Frame Rate: 30</span></span>

<span data-ttu-id="42e7b-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="42e7b-150">**Audio**:</span></span>

* <span data-ttu-id="42e7b-151">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="42e7b-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="42e7b-152">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="42e7b-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="42e7b-153">Frequenza di campionamento: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="42e7b-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="42e7b-154">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="42e7b-154">Configuration steps</span></span>
1. <span data-ttu-id="42e7b-155">Creare un nuovo progetto **NewTek TriCaster** in base a quale origine di input del video si sta utilizzando.</span><span class="sxs-lookup"><span data-stu-id="42e7b-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="42e7b-156">Una volta all'interno di tale progetto, cercare il pulsante **Flusso** e scegliere l'icona raffigurante un ingranaggio per accedere al menu di configurazione del flusso.</span><span class="sxs-lookup"><span data-stu-id="42e7b-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="42e7b-158">Una volta aperto il menu, fare clic su **New** sotto l'intestazione di connessione.</span><span class="sxs-lookup"><span data-stu-id="42e7b-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="42e7b-159">Quando richiesto per il tipo di connessione, selezionare **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="42e7b-161">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-161">Click **OK**.</span></span>
5. <span data-ttu-id="42e7b-162">Un profilo FMLE può ora essere importato facendo clic sulla freccia a discesa sotto **Streaming Profile** (Profilo streaming) e passando a **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="42e7b-164">Passare a dove è stato salvato il profilo FMLE configurato.</span><span class="sxs-lookup"><span data-stu-id="42e7b-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="42e7b-165">Selezionarlo e premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="42e7b-166">Una volta caricato il profilo, andare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="42e7b-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="42e7b-167">Ottenere l’input URL del canale per assegnargli il Tricaster **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="42e7b-168">Passare allo strumento AMSE e controllare lo stato di completamento del canale.</span><span class="sxs-lookup"><span data-stu-id="42e7b-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="42e7b-169">Una volta che lo stato è passato da **Avvio in corso** a **In esecuzione**, è possibile ottenere l'URL di input.</span><span class="sxs-lookup"><span data-stu-id="42e7b-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="42e7b-170">Quando il canale è in esecuzione, fare clic con il pulsante destro del mouse sul nome del canale, spostarsi verso il basso per passare il puntatore sull'opzione **Copy Input URL to clipboard** (Copia URL di input negli Appunti) e quindi selezionare **Primary Input URL** (URL di input primario).</span><span class="sxs-lookup"><span data-stu-id="42e7b-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="42e7b-172">Incollare le informazioni nel campo **Location** (Posizione) sotto **Flash Server** (Server flash) all'interno del progetto Tricaster.</span><span class="sxs-lookup"><span data-stu-id="42e7b-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="42e7b-173">Assegnare un nome di flusso nel campo **ID flusso** .</span><span class="sxs-lookup"><span data-stu-id="42e7b-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="42e7b-174">Se le informazioni relative al flusso sono state aggiunte al profilo FMLE, è possibile anche importarle in questa sezione facendo clic su **Importa impostazioni**, andando al profilo FMLE salvato e facendo clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="42e7b-175">I campi rilevanti Flash Server devono popolarsi con le informazioni da FMLE.</span><span class="sxs-lookup"><span data-stu-id="42e7b-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="42e7b-177">Al termine, fare clic su **OK** nella parte inferiore della schermata.</span><span class="sxs-lookup"><span data-stu-id="42e7b-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="42e7b-178">Quando gli input audio e video nel Tricaster sono pronti, iniziare lo streaming di AMS facendo clic sul pulsante **Flusso** .</span><span class="sxs-lookup"><span data-stu-id="42e7b-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="42e7b-180">Prima di fare clic su **Flusso**, **è necessario** assicurarsi che il canale sia pronto.</span><span class="sxs-lookup"><span data-stu-id="42e7b-180">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="42e7b-181">Assicurarsi inoltre di non lasciare il canale in uno stato pronto senza un feed per l’input/contributo per più di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="42e7b-181">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="42e7b-182">Testare la riproduzione</span><span class="sxs-lookup"><span data-stu-id="42e7b-182">Test playback</span></span>
<span data-ttu-id="42e7b-183">Passare allo strumento AMSE e fare clic con il pulsante destro del mouse sul canale da testare.</span><span class="sxs-lookup"><span data-stu-id="42e7b-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="42e7b-184">Nel menu passare il mouse su **Playback the Preview** (Riproduci anteprima) e scegliere **with Azure Media Player** (Con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="42e7b-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="42e7b-185">Se il flusso viene visualizzato nel lettore, ciò indica che il codificatore è stato configurato correttamente per connettersi a AMS.</span><span class="sxs-lookup"><span data-stu-id="42e7b-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="42e7b-186">In caso di errore, sarà necessario reimpostare il canale e regolare le impostazioni del codificatore.</span><span class="sxs-lookup"><span data-stu-id="42e7b-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="42e7b-187">Vedere l’argomento sulla [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) per ricevere istruzioni.</span><span class="sxs-lookup"><span data-stu-id="42e7b-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="42e7b-188">Creare un programma.</span><span class="sxs-lookup"><span data-stu-id="42e7b-188">Create a program</span></span>
1. <span data-ttu-id="42e7b-189">Una volta che viene confermata la riproduzione del canale, creare un programma.</span><span class="sxs-lookup"><span data-stu-id="42e7b-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="42e7b-190">Sotto la scheda **Live** nello strumento AMSE fare clic con il pulsante destro del mouse all'interno dell'area di programma e selezionare **Create New Program** (Crea nuovo programma).</span><span class="sxs-lookup"><span data-stu-id="42e7b-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="42e7b-192">Assegnare un nome al programma e, se necessario, modificare l'opzione **Archive Window Length** (con impostazione predefinita di 4 ore).</span><span class="sxs-lookup"><span data-stu-id="42e7b-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="42e7b-193">È inoltre possibile specificare un percorso di archiviazione o confermare l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="42e7b-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="42e7b-194">Selezionare la casella di controllo **Start the Program now** .</span><span class="sxs-lookup"><span data-stu-id="42e7b-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="42e7b-195">Fare clic su **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="42e7b-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="42e7b-196">La creazione di un programma richiede meno tempo rispetto alla creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="42e7b-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="42e7b-197">Quando il programma è in esecuzione, verificare il funzionamento della riproduzione. A tale scopo, fare clic con il pulsante destro del mouse sul programma e passare **Playback the program(s)** (Riproduci programma/i), quindi scegliere **with Azure Media Player** (Con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="42e7b-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="42e7b-198">Dopo questa verifica, fare nuovamente clic con il pulsante destro del mouse sul programma e scegliere **Copy the Output URL to Clipboard** (Copia URL di output negli Appunti) oppure recuperare queste informazioni dall'opzione **Program information and settings** (Impostazioni e informazioni programma) nel menu.</span><span class="sxs-lookup"><span data-stu-id="42e7b-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="42e7b-199">Il flusso è ora pronto per essere incorporato in un lettore o distribuito per la visualizzazione pubblica live.</span><span class="sxs-lookup"><span data-stu-id="42e7b-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="42e7b-200">risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="42e7b-200">Troubleshooting</span></span>
<span data-ttu-id="42e7b-201">Vedere l’argomento sulla [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) per ricevere istruzioni.</span><span class="sxs-lookup"><span data-stu-id="42e7b-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="42e7b-202">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="42e7b-202">Next step</span></span>
<span data-ttu-id="42e7b-203">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="42e7b-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="42e7b-204">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="42e7b-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
