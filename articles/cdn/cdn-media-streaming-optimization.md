---
title: aaaMedia streaming ottimizzazione tramite hello rete CDN di Azure
description: Ottimizzazione dei file di streaming multimediale per una distribuzione uniforme
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>Ottimizzazione tramite hello rete CDN di Azure per i flussi multimediali 
 
Utilizzo di video ad alta definizione sta aumentando in hello Internet, che crea problemi per il recapito efficiente dei file di grandi dimensioni. I clienti prevede che la riproduzione uniforme di video su richiesta o in tempo reale risorse video su una vasta gamma di client e reti in tutto il mondo hello. Critico tooensure un'esperienza uniforme e piacevole consumer è un meccanismo di recapito veloci ed efficienti per i file dei flussi multimediali.  

Flussi multimediali in diretta sono particolarmente difficile toodeliver a causa di grandi dimensioni dei file hello e numero di utenti simultanei. Ritardi causano tooleave gli utenti. Perché non possono essere memorizzato nella cache di flussi live anticipo e le latenze di grandi dimensioni non sono accettabili tooviewers, frammenti video devono essere recapitati in modo tempestivo. 

modelli di richiesta Hello di streaming forniscono anche alcune implicazioni. Quando viene rilasciata un flusso live comune o una nuova serie di video su richiesta, migliaia toomillions dei visualizzatori potrebbe richiedere di flusso hello hello contemporaneamente. In questo caso, richiesta smart consolidamento è essenziale toonot sovraccaricare il server di origine di hello quando asset hello non memorizzato nella cache ancora.
 
Hello Azure Content Delivery Network da Akamai offre ora una funzionalità che offre flussi multimediali in modo efficiente toousers tutto il mondo hello su larga scala. funzionalità di Hello riduce le latenze perché riduce il carico di hello sui server di origine hello. Questa funzionalità è disponibile con livello di prezzo Standard Akamai hello. 

Hello Azure Content Delivery Network da Verizon recapita i flussi multimediali direttamente nel tipo di ottimizzazione recapito hello web generali.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Configurare un endpoint toooptimize flussi multimediali in hello Azure Content Delivery Network da Akamai
 
È possibile configurare la distribuzione di contenuti (CDN) di rete endpoint toooptimize per file di grandi dimensioni tramite hello portale di Azure. È inoltre possibile utilizzare le API REST o uno qualsiasi dei hello client SDK toodo questo. Hello passaggi seguenti viene illustrato il processo di hello tramite hello portale di Azure:

1. un nuovo endpoint su hello tooadd **profilo CDN** selezionare **Endpoint**.
  
    ![Nuovo endpoint](./media/cdn-media-streaming-optimization/01_Adding.png)

2. In hello **ottimizzato per** elenco a discesa, seleziona **Video in streaming multimediali richiesta** per risorse video on Demand. Se si desidera creare una combinazione di streaming di video on demand e live, selezionare **Streaming multimediale generale**.

    ![Streaming selezionato](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Dopo aver creato endpoint hello, si applica l'ottimizzazione di hello per tutti i file che corrispondono a determinati criteri. Questo processo viene descritto nella seguente sezione Hello. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>Le ottimizzazioni per hello Azure Content Delivery Network da Akamai dei flussi multimediali
 
L'ottimizzazione dello streaming multimediale di Akamai è efficace per lo streaming multimediale live o di video on demand che usa singoli frammenti multimediali per la distribuzione. Questo processo è diverso da quello di trasferimento di un singolo asset di grandi dimensioni tramite il download progressivo oppure tramite l'uso di richieste di intervallo di byte. Per informazioni su questo stile di distribuzione di file multimediali, vedere [Ottimizzazione di file di grandi dimensioni](cdn-large-file-optimization.md).


Hello supporto generale di recapito o video on Demand recapito ottimizzazione tipi di supporto utilizzano una rete CDN con asset di file multimediali toodeliver le ottimizzazioni di back-end più velocemente. Vengono anche usate le configurazioni per le risorse di file multimediali basate sulle procedure consigliate apprese nel tempo.

### <a name="caching"></a>Memorizzazione nella cache

Se hello Azure Content Delivery Network da Akamai rileva che tale asset hello è un manifesto di streaming o del frammento, vengono utilizzate diverse date di scadenza memorizzazione nella cache dal recapito web generali. (Vedere l'elenco completo di hello in hello nella tabella seguente). Come sempre, vengono rispettate cache-control o Expires intestazioni inviate dall'origine hello. Se l'asset hello non è una risorsa multimediale, memorizza nella cache con date di scadenza hello per il recapito web generali.

tempo di memorizzazione nella cache negativo breve Hello è utile per l'offload di origine quando molti utenti richiedono un frammento che non esiste ancora. Un esempio è un flusso in tempo reale in cui i pacchetti hello non sono disponibili dall'origine hello che secondo. intervallo più memorizzazione nella cache di Hello consente inoltre di eseguire l'offload richieste dall'origine hello perché in genere non viene modificato il contenuto video.
 

|    | Generale<br> Web<br>di contenuti | Generale<br> diagramma<br> streaming | Video on Demand <br>diagramma<br> streaming  
--- | --- | --- | ---
Memorizzazione nella cache: positiva <br> HTTP 200, 203, 300, <br> 301, 302 e 410 | 7 giorni |365 giorni | 365 giorni   
Memorizzazione nella cache: negativa <br> HTTP 204, 305, 404, <br> e 405 | None | 1 secondo | 1 secondo
 
### <a name="deal-with-origin-failure"></a>Gestione degli errori di origine  

La distribuzione di file multimediali generali e di video on demand prevede il timeout dell'origine e il log di tentativi in base alle procedure consigliate per i modelli di richiesta tipici. Ad esempio, poiché multimediali generale sono destinata in tempo reale e il recapito di contenuti video on Demand, viene utilizzato un timeout di connessione più breve a causa di natura scadenza toohello di streaming live.

Allo scadere di una connessione, hello CDN ripete un numero di volte prima dell'invio di un errore di "504 - Timeout del Gateway" toohello client. 

Quando un file corrisponde hello tipo e dimensioni condizioni elenco di file, hello CDN utilizza il comportamento di hello per i flussi multimediali. In caso contrario, usa la distribuzione Web generale.
   
### <a name="conditions-for-media-streaming-optimization"></a>Condizioni per l'ottimizzazione dello streaming multimediale 

Hello nella tabella seguente sono elencati i set di hello di toobe criteri soddisfatti per l'ottimizzazione dei flussi multimediali: 
 
Tipi di streaming supportati | Estensioni di file  
--- | ---  
Apple HLS | m3u8, m3u, m3ub, key, ts, aac
Adobe HDS | f4m, f4x, drmmeta, bootstrap, f4f,<br>Struttura URL Seg-Frag <br> (espressione regolare corrispondente: ^(/.*)Seq(\d+)-Frag(\d+)
DASH | mpd, dash, divx, ismv, m4s, m4v, mp4, mp4v, <br> sidx, webm, mp4a, m4a, isma
Smooth Streaming | /manifest/,/QualityLevels/Fragments/
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>Le ottimizzazioni per hello Azure Content Delivery Network da Verizon dei flussi multimediali

Hello Azure Content Delivery Network da Verizon offre flussi multimediali direttamente utilizzando il tipo di ottimizzazione recapito hello web generali. Alcune funzionalità in hello CDN agevolare direttamente l'inserimento di asset di file multimediali per impostazione predefinita.

### <a name="partial-cache-sharing"></a>Condivisione della cache parziale

La condivisione della cache parziali consente le richieste di contenuto toonew tooserve parzialmente memorizzata nella cache di hello CDN. Ad esempio, se hello toohello di richiesta prima della rete CDN determina un mancato riscontro nella cache, hello inviata toohello origine. Sebbene questo contenuto incompleto venga caricato nella cache della rete CDN hello, altri toohello richieste della rete CDN può iniziare a ottenere questi dati. 

### <a name="cache-fill-wait-time"></a>Tempo di attesa di riempimento della cache

 funzionalità tempo di attesa riempimento della cache di Hello forza hello edge server toohold le successive richieste di hello stessa risorsa fino a risposta HTTP intestazioni ricevuti dal server di origine hello. Se le intestazioni di risposta HTTP da origine hello arrivano prima della scadenza del timer hello, fuori hello aumento delle dimensioni della cache vengono servite tutte le richieste che vengono messe in attesa. In hello stesso tempo hello cache viene riempita da dati dall'origine hello. Per impostazione predefinita, il tempo di attesa riempimento cache di hello è too3, 000 millisecondi. 

