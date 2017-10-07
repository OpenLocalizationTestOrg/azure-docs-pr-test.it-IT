---
title: ottimizzazione di download di file aaaLarge tramite hello rete CDN di Azure
description: Descrizione approfondita dell'ottimizzazione dei download di file di grandi dimensioni
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
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Ottimizzazione di download di file di grandi dimensioni tramite hello rete CDN di Azure

Le dimensioni dei file di contenuto pubblicato su Internet hello continuare toogrow scadenza tooenhanced funzionalità grafica migliorata e contenuto multimediale. Questa crescita dipende da numerosi fattori: penetrazione a banda larga, i dispositivi di archiviazione economica più grandi, generalizzata aumento dei dispositivi ad alta definizione video e connesso a Internet (IoT). Critico tooensure un'esperienza uniforme e piacevole consumer è un meccanismo di recapito veloci ed efficienti per i file di grandi dimensioni.

La distribuzione di file di grandi dimensioni pone diverse sfide. In primo luogo, toodownload tempo medio di hello un file di grandi dimensioni può essere significativo poiché applicazioni potrebbero non scaricare tutti i dati in modo sequenziale. In alcuni casi, le applicazioni potrebbero scaricare ultima parte di hello di un file prima della prima parte hello. Quando viene richiesto solo una piccola quantità di un file o un utente posiziona il download, download hello può non riuscire. download di Hello anche potrebbe subire un ritardo fino a quando non dopo hello rete di distribuzione di contenuti (CDN) recupera l'intero file hello dal server di origine hello. 

In secondo luogo, la latenza tra il computer di un utente e file hello hello determina la velocità di hello in corrispondenza del quale è possibile visualizzare il contenuto. Inoltre, problemi di congestione e capacità di rete possono influire sulla velocità effettiva. Maggiore distanze tra server e utenti creano ulteriori opportunità per toooccur perdita di pacchetti, riducendo così qualità. riduzione della qualità Hello dovuta a velocità effettiva limitata e perdita di pacchetti maggiore potrebbe aumentare il tempo di attesa hello per un toofinish di download di file. 

In terzo luogo, molti file di grandi dimensioni non vengono distribuiti interamente. Gli utenti potrebbero annullare un download a metà o guardare solo hello primi minuti di un video MP4 lungo. Pertanto, software e i supporti di società di recapito si toodeliver solo parte di hello di un file richiesto. Distribuzione efficiente di hello richiesto parti consente di ridurre il traffico in uscita hello dal server di origine hello. Distribuzione efficiente riduce inoltre memoria hello e richieste dei / o sul server di origine hello. 

Hello Azure Content Delivery Network da Akamai offre ora una funzionalità che fornisce file di grandi dimensioni in modo efficiente toousers tutto il mondo hello su larga scala. funzionalità di Hello riduce le latenze perché riduce il carico di hello sui server di origine hello. Questa funzionalità è disponibile con livello di prezzo Standard Akamai hello.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>Configurare un endpoint di rete CDN toooptimize il recapito di file di grandi dimensioni

È possibile configurare la distribuzione di toooptimize endpoint rete CDN per i file di grandi dimensioni tramite hello portale di Azure. È inoltre possibile utilizzare le API REST o uno qualsiasi dei hello client SDK toodo questo. Hello passaggi seguenti viene illustrato il processo di hello tramite hello portale di Azure.

1. un nuovo endpoint su hello tooadd **profilo CDN** selezionare **Endpoint**.

    ![Nuovo endpoint](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. In hello **ottimizzato per** elenco a discesa, seleziona **download di file di grandi dimensioni**.

    ![Selezione dell'ottimizzazione per file di grandi dimensioni](./media/cdn-large-file-optimization/02_Creating.png)


Dopo aver creato l'endpoint rete CDN hello, si applica le ottimizzazioni di file di grandi dimensioni hello per tutti i file che corrispondono a determinati criteri. Questo processo viene descritto nella seguente sezione Hello.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Ottimizza per il recapito di file di grandi dimensioni con hello rete CDN di Azure da Akamai

funzionalità di tipo ottimizzazione file di grandi dimensioni Hello attiva rete ottimizzazioni e le configurazioni toodeliver file di grandi dimensioni in modo più veloce e più rispondente. La distribuzione web generali con Akamai memorizza nella cache i file solo sotto 1,8 GB e possono tunnel (non cache) file too150 GB. Ottimizzazione di file di grandi dimensioni vengono memorizzati nella cache i file di backup too150 GB.

Questa ottimizzazione è efficace in determinate condizioni. Le condizioni includono la modalità di funzionamento di server di origine hello e dimensioni hello e tipi di file di hello richiesti. Prima di passare i dettagli su questi argomenti, è necessario comprendere il funzionamento di ottimizzazione hello. 

### <a name="object-chunking"></a>Suddivisione degli oggetti in blocchi 

Hello Azure Content Delivery Network da Akamai utilizza una tecnica denominata oggetto suddivisione in blocchi. Quando viene richiesto un file di grandi dimensioni, le parti più piccole del file hello hello rete CDN recupera dall'origine hello. Dopo che il server di edge/POP CDN hello riceve una richiesta di file completo o l'intervallo di byte, verifica se il tipo di file hello è supportato per l'ottimizzazione. Controlla inoltre se il tipo di file hello soddisfa i requisiti di dimensione file hello. Se la dimensione del file hello è maggiore di 10 MB, server perimetrale della rete CDN di hello richiede file hello dall'origine hello in blocchi di 2 MB. 

Dopo il blocco di hello arriva hello perimetrale della rete CDN, ha memorizzato nella cache e immediatamente servita toohello utente. rete CDN Hello quindi blocco successivo esegue la prelettura di hello in parallelo. La prelettura assicura che il contenuto di hello rimane un blocco avanti rispetto all'utente di hello, che riduce la latenza. Questo processo continua fino a hello intero file viene scaricato (se richiesto), tutti gli intervalli di byte devono (se richiesto), o client hello termina la connessione hello. 

Per ulteriori informazioni sulla richiesta di intervallo di byte di hello, vedere [7233 RFC](https://tools.ietf.org/html/rfc7233).

Hello rete CDN memorizza nella cache di eventuali blocchi di come vengono ricevuti. intero file Hello privo di toobe memorizzati nella cache nella cache di hello rete CDN. Le richieste successive per gli intervalli di byte o di file hello vengono soddisfatte dalla cache della rete CDN hello. Se non tutti i blocchi di hello vengono memorizzati nella cache nella rete CDN hello, prelettura è blocchi toorequest utilizzato dall'origine hello. Questa ottimizzazione si basa sulla capacità di hello hello origine toosupport intervallo di byte delle richieste del server. _Se il server di origine hello non supporta le richieste di intervallo di byte, questa ottimizzazione non è efficace._ 

### <a name="caching"></a>Memorizzazione nella cache
L'ottimizzazione per file di grandi dimensioni usa tempi di scadenza della memorizzazione nella cache predefiniti diversi rispetto alla distribuzione Web generica. Differenzia la memorizzazione nella cache positiva e negativa in base ai codici di risposta HTTP. Se il server di origine hello specifica un'ora di scadenza tramite un controllo della cache o scade intestazione nella risposta hello, hello CDN soddisfa tale valore. Quando non viene specificata l'origine hello e file hello corrisponde alle condizioni di tipo e dimensioni hello per questo tipo di ottimizzazione, hello CDN Usa valori predefiniti di hello per l'ottimizzazione di file di grandi dimensioni. In caso contrario, hello CDN Usa valori predefiniti per la distribuzione web generali.


|    | Distribuzione Web generica | Ottimizzazione per file di grandi dimensioni 
--- | --- | --- 
Memorizzazione nella cache: positiva <br> HTTP 200, 203, 300, <br> 301, 302 e 410 | 7 giorni |1 giorno  
Memorizzazione nella cache: negativa <br> HTTP 204, 305, 404, <br> e 405 | None | 1 secondo 

### <a name="deal-with-origin-failure"></a>Gestire gli errori di origine

la lunghezza di timeout di lettura origine Hello aumenta da due secondi per minuti, tootwo recapito web generali per il tipo di ottimizzazione di hello file di grandi dimensioni. Aumento di questo account per tooavoid di dimensioni più grandi file hello una connessione di un timeout prematuro.

Allo scadere di una connessione, hello CDN ripete un numero di volte prima dell'invio di un errore di "504 - Timeout del Gateway" toohello client. 

### <a name="conditions-for-large-file-optimization"></a>Condizioni per l'ottimizzazione dei file di grandi dimensioni

Hello nella tabella seguente sono elencati i set di hello di toobe criteri soddisfatti per l'ottimizzazione di file di grandi dimensioni:

Condizione | Valori 
--- | --- 
Tipi di file supportati | 3g2, 3gp, asf, avi, bz2, dmg, exe, f4v, flv, <br> gz, hdp, iso, jxr, m4v, mkv, mov, mp4, <br> mpeg, mpg, mts, pkg, qt, rm, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, zip  
Dimensione minima dei file | 10 MB 
Dimensione massima dei file | 150 GB 
Caratteristiche del server di origine | Deve supportare richieste di intervalli di byte 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Ottimizza per il recapito di file di grandi dimensioni con hello rete CDN di Azure da Verizon

Hello Azure Content Delivery Network da Verizon recapita i file di grandi dimensioni senza un limite sulle dimensioni del file. Funzionalità aggiuntive sono attivate per il recapito toomake predefinito dei file di grandi dimensioni più veloce.

### <a name="complete-cache-fill"></a>Riempimento completo della cache

funzionalità di riempimento completo della cache di Hello predefinito consente hello CDN toopull un file nella cache di hello quando una richiesta iniziale viene abbandonata o perso. 

Il riempimento completo della cache è particolarmente utile per asset di grandi dimensioni. In genere, gli utenti non scaricano dall'inizio toofinish. ma usano il download progressivo. comportamento predefinito di Hello forza hello edge server tooinitiate un recupero in background dell'asset hello dal server di origine hello. Asset hello in seguito, è nella cache locale del server perimetrale hello. Dopo la completa dell'oggetto hello è nella cache di hello, server perimetrale hello soddisfa le richieste di intervallo di byte toohello della rete CDN per l'oggetto memorizzato nella cache di hello.

comportamento predefinito di Hello può essere disabilitato tramite hello motore regole di business nel livello Verizon Premium hello.

### <a name="peer-cache-fill-hot-filing"></a>Hotfiling del riempimento della cache peer

funzionalità di archiviazione a caldo riempimento Hello predefinito peer cache utilizza un algoritmo sofisticato proprietario. Usa bordo aggiuntiva la memorizzazione nella cache di server in base alla larghezza di banda e aggregazione richieste metriche toofulfill client per gli oggetti di grandi dimensioni, diffusi. Questa funzionalità impedisce una situazione in cui un numero elevato di richieste aggiuntive viene inviato a server di origine tooa dell'utente. 

### <a name="conditions-for-large-file-optimization"></a>Condizioni per l'ottimizzazione dei file di grandi dimensioni

funzionalità di ottimizzazione Hello per Verizon sono attivate per impostazione predefinita. Non viene applicato alcun limite per le dimensioni massime dei file. 

## <a name="additional-considerations"></a>Considerazioni aggiuntive

Prendere in considerazione hello seguenti aspetti aggiuntivi per questo tipo di ottimizzazione.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Rete di distribuzione dei contenuti di Azure con tecnologia Akamai

- processo di suddivisione in blocchi Hello genera server di origine toohello altre richieste. Tuttavia, hello complessiva volume di dati rilasciati dall'origine hello è molto più piccolo. Risultati della suddivisione in blocchi in migliori caratteristiche di memorizzazione nella cache al hello CDN.

- Memoria e la pressione dei / o vengono ridotte a origine hello perché vengono recapitati parti più piccole del file hello.

- Per i blocchi memorizzati nella cache di hello CDN, non sono presenti ulteriori richieste origine toohello fino a quando il contenuto di hello scade o viene rimosso dalla cache di hello.

- Gli utenti possono apportare intervallo richiede toohello rete CDN e vengono trattati come qualsiasi file normali. Ottimizzazione si applica solo se è un tipo di file valido e l'intervallo di byte hello è compreso tra 10 MB e 150 GB. Se le dimensioni medie dei file hello richiesta sono inferiore a 10 MB, è possibile invece recapito web generali toouse.

### <a name="azure-content-delivery-network-from-verizon"></a>Rete di distribuzione dei contenuti di Azure con tecnologia Verizon

tipo di ottimizzazione recapito Hello web generale possibile recapitare i file di grandi dimensioni.
