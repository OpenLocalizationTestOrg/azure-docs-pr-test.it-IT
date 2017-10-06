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
# <a name="troubleshooting-guide-for-live-streaming"></a>Guida per la risoluzione dei problemi relativi allo streaming live
Questo argomento fornisce suggerimenti su come tootroubleshoot live alcuni problemi di flusso.

## <a name="issues-related-tooon-premises-encoders"></a>I problemi relativi a codificatori tooon locali
Questa sezione fornisce suggerimenti su come i codificatori tootroubleshoot problemi locale tooon correlati che sono configurati toosend un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live.

### <a name="problem-would-like-toosee-logs"></a>Problema: Desidera toosee log
* **Problema potenziale**: non è possibile trovare i log del codificatore che potrebbero essere utili per risolvere problemi di debug.
  
  * **Telestream Wirecast**: in genere è possibile trovare i log di in C:\Utenti\{nome utente}\AppData\Roaming\Wirecast\ 
  * **Live elementare**: È possibile trovare ha toologs collegamenti nel portale di gestione di hello. Fare clic su **Stats**, quindi su **Logs**. In hello **i file di Log** pagina, verrà visualizzato un elenco dei log per tutti hello elementi LiveEvent; selezionare hello una corrispondenza la sessione corrente. 
  * **Flash Media Encoder Live**: È possibile trovare hello **Directory dei Log...**  passando toohello **codifica Log** scheda.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Problema: non esiste alcuna opzione per l'output di un flusso progressivo
* **Potenziale problema**: codificatore hello in uso non Deinterlaccia automaticamente. 
  
    **Risoluzione dei problemi**: cercare un'opzione nell'interfaccia di codificatore hello deinterlacciamento. Dopo aver abilitato il deinterlacciamento, verificare di nuovo se sono disponibili impostazioni per l'output progressivo. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>Problema: Tentato diverse impostazioni di output del codificatore e tooconnect risulta ancora impossibile.
* **Potenziale problema**: il canale di codifica di Azure non è stato reimpostato correttamente. 
  
    **Risoluzione dei problemi**: codificatore di verificare che hello è push non è più tooAMS, arrestare e reimpostare il canale hello. Una volta nuovamente in esecuzione, provare a connettersi codificatore con le nuove impostazioni hello. Se ancora non viene corretto il problema di hello, provare a creare un nuovo canale completamente, in alcuni casi i canali possono venire danneggiati dopo diversi tentativi non riusciti.  
* **Potenziale problema**: dimensioni GOP hello o le impostazioni di fotogrammi chiave non sono ottimali. 
  
    **Passaggi per la risoluzione dei problemi**: l'intervallo consigliato per le dimensioni GOP o il fotogramma chiave è di 2 secondi. Alcuni codificatori calcolano questa impostazione come numero di fotogrammi, mentre altri usano i secondi. Ad esempio: quando l'output a 30fps, hello dimensioni GOP sarebbe 60 frame, che è equivalente too2 secondi.  
* **Potenziale problema**: porte chiuse bloccano flusso hello. 
  
    **Risoluzione dei problemi**: durante lo streaming tramite RTMP, controllare i firewall e/o tooconfirm le impostazioni proxy che siano aperte le porte in uscita 1935 e 1936. Per lo streaming RTP, verificare che la porta in uscita 2010 sia aperta. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>Problema: Quando si configura hello codificatore toostream con protocollo RTP hello, non è non tooenter un nome host.
* **Potenziale problema**: codificatori RTP molti non consentono di nomi host e un indirizzo IP sarà necessario toobe acquisito.  
  
    **Risoluzione dei problemi**: toofind hello indirizzo IP, aprire un prompt dei comandi in qualsiasi computer. toodo in Windows, aprire hello esecuzione dell'utilità di avvio (WIN + R) e digitare "cmd" tooopen.  
  
    Una volta aperto hello il prompt dei comandi, digitare "Ping [nome Host AMS]". 
  
    nome host Hello è possibile derivare omettendo il numero di porta hello da hello Azure URL di inserimento, come illustrato nel seguente esempio hello: 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> Se dopo avere eseguito procedure di risoluzione dei problemi di hello di che è comunque possibile correttamente il flusso, inviare un ticket di supporto utilizzando hello portale di Azure.
> 
> 

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

