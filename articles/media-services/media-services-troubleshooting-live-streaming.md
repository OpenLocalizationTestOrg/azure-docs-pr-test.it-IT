---
title: Guida per la risoluzione dei problemi relativi allo streaming live | Microsoft Docs
description: Questo argomento offre suggerimenti per la risoluzione dei problemi relativi allo streaming live.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: fa91baf7c494941fccf0e6ca38b930f3c2a521ce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="86097-103">Guida per la risoluzione dei problemi relativi allo streaming live</span><span class="sxs-lookup"><span data-stu-id="86097-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="86097-104">Questo argomento offre suggerimenti per la risoluzione di alcuni problemi relativi allo streaming live.</span><span class="sxs-lookup"><span data-stu-id="86097-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span></span>

## <a name="issues-related-to-on-premises-encoders"></a><span data-ttu-id="86097-105">Problemi relativi ai codificatori locali</span><span class="sxs-lookup"><span data-stu-id="86097-105">Issues related to on-premises encoders</span></span>
<span data-ttu-id="86097-106">In questa sezione sono disponibili suggerimenti su come risolvere i problemi relativi ai codificatori locali configurati per l'invio di un flusso a velocità in bit singola ai canali AMS abilitati per la codifica live.</span><span class="sxs-lookup"><span data-stu-id="86097-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-to-see-logs"></a><span data-ttu-id="86097-107">Problema: i log non sono reperibili</span><span class="sxs-lookup"><span data-stu-id="86097-107">Problem: Would like to see logs</span></span>
* <span data-ttu-id="86097-108">**Problema potenziale**: non è possibile trovare i log del codificatore che potrebbero essere utili per risolvere problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="86097-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="86097-109">**Telestream Wirecast**: in genere è possibile trovare i log di in C:\Utenti\{nome utente}\AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="86097-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="86097-110">**Elemental Live**: è possibile trovare i collegamenti ai log nel portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="86097-110">**Elemental Live**: You can find has links to logs on the management portal.</span></span> <span data-ttu-id="86097-111">Fare clic su **Stats**, quindi su **Logs**.</span><span class="sxs-lookup"><span data-stu-id="86097-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="86097-112">Nella pagina **Log Files** verrà visualizzato un elenco di log per tutti gli elementi LiveEvent. Selezionare quello corrispondente alla sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="86097-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span></span> 
  * <span data-ttu-id="86097-113">**Flash Media Live Encoder**: per trovare **Log Directory...**, passare alla scheda **Encoding Log**.</span><span class="sxs-lookup"><span data-stu-id="86097-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="86097-114">Problema: non esiste alcuna opzione per l'output di un flusso progressivo</span><span class="sxs-lookup"><span data-stu-id="86097-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="86097-115">**Potenziale problema**: il codificatore usato non esegue automaticamente il deinterlacciamento.</span><span class="sxs-lookup"><span data-stu-id="86097-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="86097-116">**Passaggi per la risoluzione dei problemi**: cercare un'opzione di deinterlacciamento all'interno dell'interfaccia del codificatore.</span><span class="sxs-lookup"><span data-stu-id="86097-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span></span> <span data-ttu-id="86097-117">Dopo aver abilitato il deinterlacciamento, verificare di nuovo se sono disponibili impostazioni per l'output progressivo.</span><span class="sxs-lookup"><span data-stu-id="86097-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a><span data-ttu-id="86097-118">Problema: dopo aver provato varie impostazioni di output per il codificatore è ancora impossibile connettersi.</span><span class="sxs-lookup"><span data-stu-id="86097-118">Problem: Tried several encoder output settings and still unable to connect.</span></span>
* <span data-ttu-id="86097-119">**Potenziale problema**: il canale di codifica di Azure non è stato reimpostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="86097-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="86097-120">**Passaggi per la risoluzione dei problemi**: verificare che il codificatore non effettui più il push ad AMS, arrestare e reimpostare il canale.</span><span class="sxs-lookup"><span data-stu-id="86097-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span></span> <span data-ttu-id="86097-121">Quando è di nuovo in esecuzione, provare a connettere il codificatore con le nuove impostazioni.</span><span class="sxs-lookup"><span data-stu-id="86097-121">Once running again, try connecting your encoder with the new settings.</span></span> <span data-ttu-id="86097-122">Se il problema persiste, provare a creare un canale del tutto nuovo. A volte i canali possono risultare danneggiati dopo diversi tentativi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="86097-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="86097-123">**Potenziale problema**: le dimensioni GOP o le impostazioni del fotogramma chiave non sono ottimali.</span><span class="sxs-lookup"><span data-stu-id="86097-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="86097-124">**Passaggi per la risoluzione dei problemi**: l'intervallo consigliato per le dimensioni GOP o il fotogramma chiave è di 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="86097-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="86097-125">Alcuni codificatori calcolano questa impostazione come numero di fotogrammi, mentre altri usano i secondi.</span><span class="sxs-lookup"><span data-stu-id="86097-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="86097-126">Ad esempio, per l'output di 30fps, le dimensioni GOP sarebbero di 60 fotogrammi, equivalenti a 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="86097-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span></span>  
* <span data-ttu-id="86097-127">**Potenziale problema**: le porte chiuse bloccano il flusso.</span><span class="sxs-lookup"><span data-stu-id="86097-127">**Potential issue**: Closed ports are blocking the stream.</span></span> 
  
    <span data-ttu-id="86097-128">**Passaggi per la risoluzione dei problemi**: durante lo streaming tramite RTP, controllare le impostazioni del firewall e/o del proxy per assicurarsi che le porte in uscita 1935 e 1936 siano aperte.</span><span class="sxs-lookup"><span data-stu-id="86097-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="86097-129">Per lo streaming RTP, verificare che la porta in uscita 2010 sia aperta.</span><span class="sxs-lookup"><span data-stu-id="86097-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a><span data-ttu-id="86097-130">Problema: quando si configura il codificatore per lo streaming con il protocollo RTP, non è disponibile alcun campo per l'immissione del nome host.</span><span class="sxs-lookup"><span data-stu-id="86097-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span></span>
* <span data-ttu-id="86097-131">**Potenziale problema**: molti codificatori RTP non consentono i nomi host e sarà necessario acquisire un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="86097-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span></span>  
  
    <span data-ttu-id="86097-132">**Passaggi per la risoluzione dei problemi**: per trovare l'indirizzo IP, aprire un prompt dei comandi in qualsiasi computer.</span><span class="sxs-lookup"><span data-stu-id="86097-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="86097-133">A tale scopo, in Windows aprire l'avvio per Esegui (WIN+R) e digitare "cmd" per aprire.</span><span class="sxs-lookup"><span data-stu-id="86097-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span></span>  
  
    <span data-ttu-id="86097-134">Una volta aperto il prompt dei comandi, digitare "Ping [nome Host AMS]".</span><span class="sxs-lookup"><span data-stu-id="86097-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="86097-135">È possibile derivare il nome host omettendo il numero di porta dall'URL di inserimento di Azure, come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="86097-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span></span> 
  
    <span data-ttu-id="86097-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="86097-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="86097-138">Se dopo aver seguito le procedure di risoluzione dei problemi non è ancora possibile eseguire correttamente il flusso, inviare un ticket di supporto tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="86097-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="86097-139">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="86097-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="86097-140">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="86097-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

