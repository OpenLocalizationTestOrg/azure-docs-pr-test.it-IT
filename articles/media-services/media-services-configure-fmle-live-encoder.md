---
title: "Configurare il codificatore FMLE per l'invio di un flusso singolo in diretta di velocità in bit | Microsoft Docs"
description: "In questo argomento viene illustrato come configurare il codificatore Flash Media Live Encoder (FMLE) per inviare un flusso a velocità in bit singola a canali AMS abilitati per la codifica live."
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
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="4fb67-103">Usare il codificatore FMLE per inviare un flusso live a velocità in bit singola.</span><span class="sxs-lookup"><span data-stu-id="4fb67-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fb67-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="4fb67-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="4fb67-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="4fb67-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="4fb67-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="4fb67-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="4fb67-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="4fb67-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="4fb67-108">In questo argomento viene illustrato come configurare il codificatore [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) per inviare un flusso a velocità in bit singola a canali AMS abilitati per la codifica live.</span><span class="sxs-lookup"><span data-stu-id="4fb67-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="4fb67-109">Per altre informazioni, vedere [Uso di canali abilitati per l'esecuzione della codifica live con Servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="4fb67-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="4fb67-110">In questa esercitazione viene illustrato come gestire Servizi multimediali di Azure (AMS) con lo strumento Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="4fb67-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="4fb67-111">Questo strumento può essere eseguito solo in PC Windows.</span><span class="sxs-lookup"><span data-stu-id="4fb67-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="4fb67-112">Gli utenti di sistemi Mac o Linux possono usare il Portale di Azure per creare [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="4fb67-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="4fb67-113">Si noti che questa esercitazione descrive l'utilizzo di AAC.</span><span class="sxs-lookup"><span data-stu-id="4fb67-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="4fb67-114">Tuttavia, per impostazione predefinita FMLE non supporta AAC.</span><span class="sxs-lookup"><span data-stu-id="4fb67-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="4fb67-115">È necessario acquistare un plug-in per codificare AAC come da MainConcept: [plug-in AAC](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="4fb67-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fb67-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4fb67-116">Prerequisites</span></span>
* [<span data-ttu-id="4fb67-117">Creare un account Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="4fb67-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="4fb67-118">Verificare che sia presente un endpoint di streaming in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4fb67-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="4fb67-119">Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="4fb67-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="4fb67-120">Installare la versione più recente dello strumento [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="4fb67-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="4fb67-121">Avviare lo strumento e connettersi al proprio account AMS.</span><span class="sxs-lookup"><span data-stu-id="4fb67-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="4fb67-122">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="4fb67-122">Tips</span></span>
* <span data-ttu-id="4fb67-123">Se possibile, usare una connessione a Internet con cablaggio fisico.</span><span class="sxs-lookup"><span data-stu-id="4fb67-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="4fb67-124">È buona norma raddoppiare le velocità in bit di streaming in fase di determinazione dei requisiti di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="4fb67-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="4fb67-125">Anche se non si tratta di un requisito obbligatorio, contribuirà a ridurre l'impatto della congestione della rete.</span><span class="sxs-lookup"><span data-stu-id="4fb67-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="4fb67-126">Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.</span><span class="sxs-lookup"><span data-stu-id="4fb67-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="4fb67-127">Creare un canale</span><span class="sxs-lookup"><span data-stu-id="4fb67-127">Create a channel</span></span>
1. <span data-ttu-id="4fb67-128">Nello strumento AMSE passare alla scheda **Live** e fare clic con il pulsante destro del mouse all'interno dell'area del canale.</span><span class="sxs-lookup"><span data-stu-id="4fb67-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="4fb67-129">Scegliere **Create channel**</span><span class="sxs-lookup"><span data-stu-id="4fb67-129">Select **Create channel…**</span></span> <span data-ttu-id="4fb67-130">dal menu.</span><span class="sxs-lookup"><span data-stu-id="4fb67-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="4fb67-132">Specificare un nome di canale. Il campo della descrizione è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="4fb67-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="4fb67-133">In Impostazioni del canale selezionare **Standard** per l'opzione di codifica live con il protocollo di input impostato su **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="4fb67-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="4fb67-134">È possibile confermare tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="4fb67-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="4fb67-135">Assicurarsi che l'opzione **Avvia ora il nuovo canale** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="4fb67-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="4fb67-136">Fare clic su **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="4fb67-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="4fb67-138">Per l'avvio del canale possono essere richiesti fino a 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="4fb67-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="4fb67-139">Durante l'avvio di canale è possibile [configurare il codificatore](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="4fb67-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fb67-140">Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto.</span><span class="sxs-lookup"><span data-stu-id="4fb67-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="4fb67-141">Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="4fb67-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="4fb67-142"><a id=configure_fmle_rtmp></a>Configurare il codificatore FMLE</span><span class="sxs-lookup"><span data-stu-id="4fb67-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="4fb67-143">In questa esercitazione vengono usate le seguenti impostazioni di output.</span><span class="sxs-lookup"><span data-stu-id="4fb67-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="4fb67-144">Nel resto di questa sezione vengono descritti in maggiore dettaglio i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4fb67-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="4fb67-145">**Video**:</span><span class="sxs-lookup"><span data-stu-id="4fb67-145">**Video**:</span></span>

* <span data-ttu-id="4fb67-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="4fb67-146">Codec: H.264</span></span>
* <span data-ttu-id="4fb67-147">Profilo: alto (livello 4.0)</span><span class="sxs-lookup"><span data-stu-id="4fb67-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="4fb67-148">Velocità in bit: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="4fb67-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="4fb67-149">Fotogramma chiave: 2 secondi (60 secondi)</span><span class="sxs-lookup"><span data-stu-id="4fb67-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="4fb67-150">Frequenza dei fotogrammi: 30</span><span class="sxs-lookup"><span data-stu-id="4fb67-150">Frame Rate: 30</span></span>

<span data-ttu-id="4fb67-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="4fb67-151">**Audio**:</span></span>

* <span data-ttu-id="4fb67-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="4fb67-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="4fb67-153">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="4fb67-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="4fb67-154">Frequenza di campionamento: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="4fb67-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="4fb67-155">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="4fb67-155">Configuration steps</span></span>
1. <span data-ttu-id="4fb67-156">Passare all’interfaccia Flash Media Live Encoder (FMLE) nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4fb67-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="4fb67-157">L'interfaccia è una pagina principale di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="4fb67-157">The interface is one main page of settings.</span></span> <span data-ttu-id="4fb67-158">Annotare le seguenti impostazioni consigliate per iniziare a utilizzare streaming tramite FMLE.</span><span class="sxs-lookup"><span data-stu-id="4fb67-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="4fb67-159">Formato: Frequenza dei fotogrammi h. 264: 30,00</span><span class="sxs-lookup"><span data-stu-id="4fb67-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="4fb67-160">Dimensione di input: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="4fb67-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="4fb67-161">Velocità in bit: Kbps 5000 (può essere regolato in base alle limitazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="4fb67-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="4fb67-163">Quando si utilizzano le origini interlacciate, selezionare l'opzione "Deinterlaccia"</span><span class="sxs-lookup"><span data-stu-id="4fb67-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="4fb67-164">Selezionare l'icona di chiave accanto a formato, queste impostazioni aggiuntive devono essere:</span><span class="sxs-lookup"><span data-stu-id="4fb67-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="4fb67-165">Profilo: principale</span><span class="sxs-lookup"><span data-stu-id="4fb67-165">Profile: Main</span></span>
   * <span data-ttu-id="4fb67-166">Livello: 4.0</span><span class="sxs-lookup"><span data-stu-id="4fb67-166">Level: 4.0</span></span>
   * <span data-ttu-id="4fb67-167">Frequenza dei fotogrammi chiave: 2 secondi</span><span class="sxs-lookup"><span data-stu-id="4fb67-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="4fb67-169">Impostare la seguente impostazione importante dell’audio:</span><span class="sxs-lookup"><span data-stu-id="4fb67-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="4fb67-170">Formato: AAC</span><span class="sxs-lookup"><span data-stu-id="4fb67-170">Format: AAC</span></span>
   * <span data-ttu-id="4fb67-171">Frequenza di campionamento: 44100 kHz</span><span class="sxs-lookup"><span data-stu-id="4fb67-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="4fb67-172">Velocità in bit: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="4fb67-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="4fb67-174">Ottenere l’input URL del canale per assegnargli il FMLE **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="4fb67-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="4fb67-175">Passare allo strumento AMSE e controllare lo stato di completamento del canale.</span><span class="sxs-lookup"><span data-stu-id="4fb67-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="4fb67-176">Una volta che lo stato è passato da **Avvio in corso** a **In esecuzione**, è possibile ottenere l'URL di input.</span><span class="sxs-lookup"><span data-stu-id="4fb67-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="4fb67-177">Quando il canale è in esecuzione, fare clic con il pulsante destro del mouse sul nome del canale, spostarsi verso il basso per passare il puntatore sull'opzione **Copy Input URL to clipboard** (Copia URL di input negli Appunti) e quindi selezionare **Primary Input URL** (URL di input primario).</span><span class="sxs-lookup"><span data-stu-id="4fb67-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="4fb67-179">Incollare le informazioni nel campo **URL FMS** della sezione di output e assegnare un nome di flusso.</span><span class="sxs-lookup"><span data-stu-id="4fb67-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="4fb67-181">Per garantire la ridondanza aggiuntiva, ripetere questi passaggi con l'URL di Input secondari.</span><span class="sxs-lookup"><span data-stu-id="4fb67-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="4fb67-182">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="4fb67-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fb67-183">Prima di fare clic su **Connetti**, **è necessario** assicurarsi che il canale sia pronto.</span><span class="sxs-lookup"><span data-stu-id="4fb67-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="4fb67-184">Assicurarsi inoltre di non lasciare il canale in uno stato pronto senza un feed per l’input/contributo per più di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="4fb67-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="4fb67-185">Testare la riproduzione</span><span class="sxs-lookup"><span data-stu-id="4fb67-185">Test playback</span></span>

<span data-ttu-id="4fb67-186">Passare allo strumento AMSE e fare clic con il pulsante destro del mouse sul canale da testare.</span><span class="sxs-lookup"><span data-stu-id="4fb67-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="4fb67-187">Nel menu passare il mouse su **Playback the Preview** (Riproduci anteprima) e scegliere **with Azure Media Player** (Con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="4fb67-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="4fb67-188">Se il flusso viene visualizzato nel lettore, ciò indica che il codificatore è stato configurato correttamente per connettersi a AMS.</span><span class="sxs-lookup"><span data-stu-id="4fb67-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="4fb67-189">In caso di errore, sarà necessario reimpostare il canale e regolare le impostazioni del codificatore.</span><span class="sxs-lookup"><span data-stu-id="4fb67-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="4fb67-190">Vedere l’argomento sulla [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) per ricevere istruzioni.</span><span class="sxs-lookup"><span data-stu-id="4fb67-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="4fb67-191">Creare un programma.</span><span class="sxs-lookup"><span data-stu-id="4fb67-191">Create a program</span></span>
1. <span data-ttu-id="4fb67-192">Una volta che viene confermata la riproduzione del canale, creare un programma.</span><span class="sxs-lookup"><span data-stu-id="4fb67-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="4fb67-193">Sotto la scheda **Live** nello strumento AMSE fare clic con il pulsante destro del mouse all'interno dell'area di programma e selezionare **Create New Program** (Crea nuovo programma).</span><span class="sxs-lookup"><span data-stu-id="4fb67-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="4fb67-195">Assegnare un nome al programma e, se necessario, modificare l'opzione **Archive Window Length** (con impostazione predefinita di 4 ore).</span><span class="sxs-lookup"><span data-stu-id="4fb67-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="4fb67-196">È inoltre possibile specificare un percorso di archiviazione o confermare l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4fb67-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="4fb67-197">Selezionare la casella di controllo **Start the Program now** .</span><span class="sxs-lookup"><span data-stu-id="4fb67-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="4fb67-198">Fare clic su **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="4fb67-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="4fb67-199">La creazione di un programma richiede meno tempo rispetto alla creazione del canale.</span><span class="sxs-lookup"><span data-stu-id="4fb67-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="4fb67-200">Quando il programma è in esecuzione, verificare il funzionamento della riproduzione. A tale scopo, fare clic con il pulsante destro del mouse sul programma e passare **Playback the program(s)** (Riproduci programma/i), quindi scegliere **with Azure Media Player** (Con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="4fb67-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="4fb67-201">Dopo questa verifica, fare nuovamente clic con il pulsante destro del mouse sul programma e scegliere **Copy the Output URL to Clipboard** (Copia URL di output negli Appunti) oppure recuperare queste informazioni dall'opzione **Program information and settings** (Impostazioni e informazioni programma) nel menu.</span><span class="sxs-lookup"><span data-stu-id="4fb67-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="4fb67-202">Il flusso è ora pronto per essere incorporato in un lettore o distribuito per la visualizzazione pubblica live.</span><span class="sxs-lookup"><span data-stu-id="4fb67-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="4fb67-203">risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="4fb67-203">Troubleshooting</span></span>
<span data-ttu-id="4fb67-204">Vedere l’argomento sulla [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) per ricevere istruzioni.</span><span class="sxs-lookup"><span data-stu-id="4fb67-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4fb67-205">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="4fb67-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4fb67-206">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="4fb67-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
