---
title: Guida per lo streaming in tempo reale per aaaTroubleshooting | Documenti Microsoft
description: Questo argomento fornisce suggerimenti su come tootroubleshoot live streaming problemi.
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
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="b500f-103">Guida per la risoluzione dei problemi relativi allo streaming live</span><span class="sxs-lookup"><span data-stu-id="b500f-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="b500f-104">Questo argomento fornisce suggerimenti su come tootroubleshoot live alcuni problemi di flusso.</span><span class="sxs-lookup"><span data-stu-id="b500f-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="b500f-105">I problemi relativi a codificatori tooon locali</span><span class="sxs-lookup"><span data-stu-id="b500f-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="b500f-106">Questa sezione fornisce suggerimenti su come i codificatori tootroubleshoot problemi locale tooon correlati che sono configurati toosend un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live.</span><span class="sxs-lookup"><span data-stu-id="b500f-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="b500f-107">Problema: Desidera toosee log</span><span class="sxs-lookup"><span data-stu-id="b500f-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="b500f-108">**Problema potenziale**: non è possibile trovare i log del codificatore che potrebbero essere utili per risolvere problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="b500f-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="b500f-109">**Telestream Wirecast**: in genere è possibile trovare i log di in C:\Utenti\{nome utente}\AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="b500f-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="b500f-110">**Live elementare**: È possibile trovare ha toologs collegamenti nel portale di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="b500f-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="b500f-111">Fare clic su **Stats**, quindi su **Logs**.</span><span class="sxs-lookup"><span data-stu-id="b500f-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="b500f-112">In hello **i file di Log** pagina, verrà visualizzato un elenco dei log per tutti hello elementi LiveEvent; selezionare hello una corrispondenza la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="b500f-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="b500f-113">**Flash Media Encoder Live**: È possibile trovare hello **Directory dei Log...**  passando toohello **codifica Log** scheda.</span><span class="sxs-lookup"><span data-stu-id="b500f-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="b500f-114">Problema: non esiste alcuna opzione per l'output di un flusso progressivo</span><span class="sxs-lookup"><span data-stu-id="b500f-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="b500f-115">**Potenziale problema**: codificatore hello in uso non Deinterlaccia automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b500f-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="b500f-116">**Risoluzione dei problemi**: cercare un'opzione nell'interfaccia di codificatore hello deinterlacciamento.</span><span class="sxs-lookup"><span data-stu-id="b500f-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="b500f-117">Dopo aver abilitato il deinterlacciamento, verificare di nuovo se sono disponibili impostazioni per l'output progressivo.</span><span class="sxs-lookup"><span data-stu-id="b500f-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="b500f-118">Problema: Tentato diverse impostazioni di output del codificatore e tooconnect risulta ancora impossibile.</span><span class="sxs-lookup"><span data-stu-id="b500f-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="b500f-119">**Potenziale problema**: il canale di codifica di Azure non è stato reimpostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b500f-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="b500f-120">**Risoluzione dei problemi**: codificatore di verificare che hello è push non è più tooAMS, arrestare e reimpostare il canale hello.</span><span class="sxs-lookup"><span data-stu-id="b500f-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="b500f-121">Una volta nuovamente in esecuzione, provare a connettersi codificatore con le nuove impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="b500f-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="b500f-122">Se ancora non viene corretto il problema di hello, provare a creare un nuovo canale completamente, in alcuni casi i canali possono venire danneggiati dopo diversi tentativi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="b500f-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="b500f-123">**Potenziale problema**: dimensioni GOP hello o le impostazioni di fotogrammi chiave non sono ottimali.</span><span class="sxs-lookup"><span data-stu-id="b500f-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="b500f-124">**Passaggi per la risoluzione dei problemi**: l'intervallo consigliato per le dimensioni GOP o il fotogramma chiave è di 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="b500f-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="b500f-125">Alcuni codificatori calcolano questa impostazione come numero di fotogrammi, mentre altri usano i secondi.</span><span class="sxs-lookup"><span data-stu-id="b500f-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="b500f-126">Ad esempio: quando l'output a 30fps, hello dimensioni GOP sarebbe 60 frame, che è equivalente too2 secondi.</span><span class="sxs-lookup"><span data-stu-id="b500f-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="b500f-127">**Potenziale problema**: porte chiuse bloccano flusso hello.</span><span class="sxs-lookup"><span data-stu-id="b500f-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="b500f-128">**Risoluzione dei problemi**: durante lo streaming tramite RTMP, controllare i firewall e/o tooconfirm le impostazioni proxy che siano aperte le porte in uscita 1935 e 1936.</span><span class="sxs-lookup"><span data-stu-id="b500f-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="b500f-129">Per lo streaming RTP, verificare che la porta in uscita 2010 sia aperta.</span><span class="sxs-lookup"><span data-stu-id="b500f-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="b500f-130">Problema: Quando si configura hello codificatore toostream con protocollo RTP hello, non è non tooenter un nome host.</span><span class="sxs-lookup"><span data-stu-id="b500f-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="b500f-131">**Potenziale problema**: codificatori RTP molti non consentono di nomi host e un indirizzo IP sarà necessario toobe acquisito.</span><span class="sxs-lookup"><span data-stu-id="b500f-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="b500f-132">**Risoluzione dei problemi**: toofind hello indirizzo IP, aprire un prompt dei comandi in qualsiasi computer.</span><span class="sxs-lookup"><span data-stu-id="b500f-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="b500f-133">toodo in Windows, aprire hello esecuzione dell'utilità di avvio (WIN + R) e digitare "cmd" tooopen.</span><span class="sxs-lookup"><span data-stu-id="b500f-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="b500f-134">Una volta aperto hello il prompt dei comandi, digitare "Ping [nome Host AMS]".</span><span class="sxs-lookup"><span data-stu-id="b500f-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="b500f-135">nome host Hello è possibile derivare omettendo il numero di porta hello da hello Azure URL di inserimento, come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="b500f-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="b500f-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="b500f-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="b500f-138">Se dopo avere eseguito procedure di risoluzione dei problemi di hello di che è comunque possibile correttamente il flusso, inviare un ticket di supporto utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b500f-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="b500f-139">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b500f-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b500f-140">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b500f-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

