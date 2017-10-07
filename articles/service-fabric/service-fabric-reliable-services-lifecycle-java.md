---
title: aaaOverview di hello del ciclo di vita di servizi di Azure Service Fabric affidabile | Documenti Microsoft
description: Informazioni sugli eventi del ciclo di vita diversi hello in servizi di Service Fabric affidabili
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Panoramica del ciclo di vita di Reliable Services
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java su Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Quando si pensa hello cicli di vita di servizi affidabili, funzionalità di base di hello del ciclo di vita hello sono hello più importante. In generale:

* Durante l'avvio
  * I servizi vengono costruiti
  * Hanno un tooconstruct opportunità e restituire zero o più listener
  * Qualsiasi listener restituito sono aperte, consentendo la comunicazione con il servizio hello
  * viene chiamato il metodo di runAsync Hello del servizio, consentendo di hello servizio toodo a esecuzione prolungata o di lavoro in background
* Durante l'arresto
  * toorunAsync passato di Hello annullamento token viene annullato e vengono chiuse listener hello
  * Una volta completato, hello servizio oggetto eliminato

Sono disponibili informazioni dettagliate sugli hello esatto di ordinamento di questi eventi. In particolare, ordine hello degli eventi può cambiare leggermente a seconda che sia di hello servizio affidabile Stateless o informazioni sullo stato. Inoltre, per i servizi con stati, abbiamo toodeal con uno scenario di scambio primario hello. Durante questa sequenza, ruolo hello database primario replica tooanother trasferiti (o torna) senza l'arresto del servizio hello. Infine, abbiamo toothink sulle condizioni di errore o di.

## <a name="stateless-service-startup"></a>Avvio di un servizio senza stato
Hello ciclo di vita di un servizio senza stato è piuttosto semplice. Ecco l'ordine di hello degli eventi:

1. Hello servizio viene costruito
2. Quindi si verificano due cose in parallelo:
    - Viene chiamato `StatelessService.createServiceInstanceListeners()` e viene aperto qualsiasi listener restituito (viene chiamato `CommunicationListener.openAsync()` su ogni listener)
    - metodo runAsync del servizio di Hello (`StatelessService.runAsync()`) viene chiamato
3. Se presente, viene chiamato metodo onOpenAsync di hello del servizio (in particolare, `StatelessService.onOpenAsync()` viene chiamato. si tratta di un override insolito ma comunque disponibile).

È importante toonote che non vi sia alcun ordinamento tra toocreate chiamate hello e i listener hello aperto e runAsync. listener Hello venga aperto prima dell'avvio di runAsync. Analogamente, runAsync rischia di richiamato prima che il listener di comunicazione hello è aperto o anche costruito. Se è necessario eseguire qualsiasi sincronizzazione, viene lasciato in qualità di implementatore toohello esercizio. Soluzioni comuni:

* Talvolta i listener non possono funzionare fino a quando non vengono create altre informazioni o eseguite determinate operazioni. Per i servizi senza stati che possono in genere eseguire le operazioni nel costruttore del servizio hello durante hello `createServiceInstanceListeners()` chiamare, o come parte della costruzione di hello del listener hello stesso.
* Hello codice runAsync non talvolta toostart fino a quando non sono aperti listener hello. In questo caso è necessario un po' di coordinamento in più. Una soluzione comune è alcuni flag all'interno di listener hello che indica quando vengono completati, cui è archiviato runAsync prima di continuare a utilizzare tooactual.

## <a name="stateless-service-shutdown"></a>Arresto di un servizio senza stato
Quando un servizio senza stato di arresto, hello stesso modello viene seguito, solo in senso inverso:

1. In parallelo
    - Tutti i listener aperti vengono chiusi (viene chiamato `CommunicationListener.closeAsync()` su ogni listener)
    - token di annullamento Hello passato troppo`runAsync()` viene annullata (controllo del token di annullamento hello `isCancelled` proprietà restituisce true e se la chiamata del token hello `throwIfCancellationRequested` metodo genera un `CancellationException`)
2. Una volta `closeAsync()` completa per ogni listener e `runAsync()` completa inoltre del servizio hello `StatelessService.onCloseAsync()` metodo viene chiamato, se presente (nuovo si tratta di una sostituzione non comune).
3. Dopo aver `StatelessService.onCloseAsync()` viene completato, viene eliminato l'oggetto servizio hello

## <a name="notes-on-service-lifecycle"></a>Note sul ciclo di vita del servizio
* Entrambi hello `runAsync()` metodo e hello `createServiceInstanceListeners` chiamate sono facoltative. Un servizio può averne una, entrambe o nessuna. Ad esempio, se il servizio di hello non tutto il relativo lavoro risposta toouser chiamate, non è necessario per tale tooimplement `runAsync()`. Sono necessari solo i listener di comunicazione hello e il codice associato. Analogamente, la creazione e la restituzione di listener di comunicazione è facoltativo, come servizio di hello potrebbe avere solo sfondo toodo di lavoro e deve pertanto solo tooimplement`runAsync()`
* È valido per un servizio toocomplete `runAsync()` correttamente e restituito da esso. Questo non è considerato una condizione di errore e rappresenta operazioni in background hello di hello servizio completato. Per i servizi reliable con stati `runAsync()` deve essere chiamato nuovamente se servizio hello sono stati abbassato di livello dal database primario e quindi promossa tooprimary indietro.
* Se un servizio viene terminato da `runAsync()` generando alcune eccezione imprevista, si tratta di un errore e l'oggetto servizio hello è stato arrestato e segnalato un errore di integrità.
* Sebbene non esista alcun limite di tempo restituito da questi metodi, immediatamente perdere toowrite possibilità hello e pertanto non è possibile completare qualsiasi lavoro effettivo. È consigliabile che venga restituito al più presto dopo aver ricevuto la richiesta di annullamento hello. Se il servizio non risponde toothese API chiamate in una quantità ragionevole di tempo che Service Fabric potrebbe forzare la terminazione del servizio. In genere ciò accade solo durante gli aggiornamenti delle applicazioni o quando viene eliminato un servizio. Questo timeout è di 15 minuti per impostazione predefinita.
* Errori di hello `onCloseAsync()` comporterà percorso `onAbort()` la chiamata che è un'opportunità di sforzo ultima possibilità per hello service tooclean backup e rilasciare le risorse che sono richiesti.

> [!NOTE]
> Reliable Services con stato non è ancora supportato in Java.
>
>

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooReliable servizi](service-fabric-reliable-services-introduction.md)
* [Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Uso avanzato del modello di programmazione Reliable Services](service-fabric-reliable-services-advanced-usage.md)
