---
title: modelli di utilizzo della rete CDN Azure aaaAnalyze | Documenti Microsoft
description: "È possibile visualizzare i modelli di utilizzo per la rete CDN utilizzando hello seguenti report: larghezza di banda, dati trasferiti, riscontri, gli stati di Cache, percentuale riscontri Cache, i dati trasferiti IPV4/IPV6."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Analizzare i modelli di utilizzo della rete CDN di Azure

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Guida di Hello seguente passa attraverso hello passaggi tooview hello core report tramite il portale di gestione hello per i profili Verizon. È anche possibile esportare core analitica dati toostorage, hub eventi o analitica di log (oms) per i profili Verizon sia Akamai [tramite il portale di azure hello](cdn-log-analysis.md).

È possibile visualizzare i modelli di utilizzo per la rete CDN utilizzando hello seguenti report:

* Larghezza di banda
* Dati trasferiti
* Riscontri
* Stati della cache
* Percentuale riscontri cache
* Dati trasferiti IPv4/IPV6

## <a name="accessing-core-reports"></a>Accesso ai report di base
1. Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-reports/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
2. Passare il mouse su hello **Analitica** scheda, quindi passare il mouse su hello **report principali** riquadro a comparsa.  Fare clic sul report hello desiderato nel menu hello.
   
    ![Portale di gestione della rete CDN, menu Core Reports (Report di base)](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Larghezza di banda
report di larghezza di banda Hello è costituito da una tabella di dati e di grafico che indica di utilizzo della larghezza di banda hello per HTTP e HTTPS in un periodo di tempo specifico. È possibile visualizzare l'utilizzo della larghezza di banda hello in tutti i POP CDN o una particolare POP. In questo modo si tooview hello picchi nel traffico e la distribuzione in rete CDN viene visualizzata in Mbps.

* Selezionare il traffico toosee tutti i nodi di bordo da tutti i nodi o scegliere l'area o un nodo specifico dall'elenco a discesa hello.
* Selezionare i dati per oggi/questa settimana/mese di inizio intervallo tooview e così via o immettere le date personalizzate, quindi fare clic su "go" toomake che venga aggiornata con la selezione.
* È possibile esportare e download dei dati hello facendo hello excel icona foglio disponibile accanto troppo "go".

report Hello vengono aggiornate ogni 5 minuti.

![Report della larghezza di banda](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Dati trasferiti
Questo report è costituito da una tabella di dati e di grafico che indica di utilizzo di traffico hello per HTTP e HTTPS in un periodo di tempo specifico. È possibile visualizzare l'utilizzo di traffico di hello in tutti i POP CDN o una particolare POP. In questo modo si tooview hello picchi nel traffico e la distribuzione in rete CDN viene visualizzato in GB.

* Selezionare il traffico toosee tutti i nodi di bordo da tutte le note oppure scegliere di area o un nodo specifico dall'elenco a discesa hello.
* Selezionare i dati per oggi/questa settimana/mese di inizio intervallo tooview e così via o immettere le date personalizzate, quindi fare clic su "go" toomake che venga aggiornata con la selezione.
* È possibile esportare e download dei dati hello facendo hello excel icona foglio disponibile accanto troppo "go".

report Hello vengono aggiornate ogni 5 minuti.

![Report dati trasferiti](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>Riscontri (codici di stato)
Questo report viene distribuzione hello richiesta dei codici di stato per il contenuto. Tutte le richieste di contenuto genereranno un codice di stato HTTP. codice di stato Hello descrive come bordo POP gestita la richiesta di hello. Ad esempio, i codici di stato 2xx indicano che tale richiesta hello stato ha servito con successo tooa client, mentre un codice di stato 4xx indica che si è verificato un errore. Per ulteriori informazioni sul codice di stato HTTP, vedere [Codici di stato](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Selezionare i dati per oggi/questa settimana/mese di inizio intervallo tooview e così via o immettere le date personalizzate, quindi fare clic su "go" toomake che venga aggiornata con la selezione.
* È possibile esportare e si trova accanto di foglio di excel di download dei dati hello facendo hello troppo "go".

![Report riscontri](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>Stati della cache
Questo report viene distribuzione hello dei riscontri nella cache e mancati riscontri nella cache per la richiesta del client. Poiché le prestazioni più veloci hello provengono da riscontri nella cache, è possibile ottimizzare le velocità di recapito dei dati dalla riduzione dei mancati riscontri nella cache e di ricerche riuscite nella cache scaduti. Mancati riscontri nella cache possono essere ridotto configurando il tooavoid di server di origine l'assegnazione di intestazioni di risposta "no-cache", evitando la memorizzazione nella cache della stringa di query, ad eccezione in cui è strettamente necessaria e, evitando di codici di risposta non memorizzabile nella cache. Scadenza cache possono essere evitati riscontri effettuando un asset max-age come numero di server di origine toohello le richieste di hello toominimize possibili.

![Report stati della cache](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Gli stati della cache principali includono:
* TCP_HIT: servito dall’Edge. oggetto Hello è nella cache e non ha superato la durata massima.
* TCP_MISS: servito dall'origine. oggetto Hello non era presente nella cache e ha restituito una risposta di hello tooorigin indietro.
* TCP_EXPIRED _MISS: servito dall'origine dopo la riconvalida con l’origine. oggetto Hello è nella cache, ma ha superato la durata massima. Ha restituito una riconvalida con origine oggetto della cache di hello verrà sostituito da una nuova risposta dall'origine.
* TCP_EXPIRED _HIT: servito dall’Edge dopo la riconvalida con l’origine. oggetto Hello è nella cache, ma ha superato la durata massima. Oggetto della cache di hello viene senza modificato ha restituito una riconvalida con il server di origine hello.
* Selezionare i dati per oggi/questa settimana/mese di inizio intervallo tooview e così via o immettere le date personalizzate, quindi fare clic su "go" toomake che venga aggiornata con la selezione.
* È possibile esportare e download dei dati hello facendo hello excel icona foglio disponibile accanto troppo "go".

### <a name="full-list-of-cache-statuses"></a>Elenco completo degli stati della cache
* TCP_HIT - questo stato viene segnalato quando una richiesta viene gestita direttamente dal client toohello hello POP. Un asset è immediatamente disponibile da un popup quando viene memorizzato sul client toohello più vicino di hello POP e ha un valore valido time-to-live o durata (TTL). Durata (TTL) è determinato da hello intestazioni di risposta seguente:
  
  * Cache-Control: s-maxage
  * Cache-Control: max-age
  * Expires
* TCP_MISS - questo stato indica che una versione memorizzata nella cache di hello richiesto asset non trovata nel client toohello più vicino di hello POP. verrà richiesta da un server di origine o un server di origine dello scudo asset Hello. Se il server di origine hello o un server dello scudo di hello origine restituisce un asset, verrà servita toohello client e memorizzato nella cache sul client hello sia server perimetrale hello. In caso contrario, verrà restituito un codice di stato non 200 (ad esempio, 403 Non consentito, 404 Non trovato, ecc.).
* _HIT TCP_EXPIRED - questo stato viene segnalato quando una richiesta che la destinazione di un asset della durata è scaduta, ad esempio quando la durata massima dell'asset hello è scaduta, è stata gestita direttamente dal client toohello hello POP.
  
    Richiesta scaduta in genere risultati in un server di origine toohello richiesta la riconvalida. Affinché un toooccur _HIT TCP_EXPIRED, il server di origine hello deve indicare che una versione più recente dell'asset hello non esiste. Questo tipo di situazione in genere aggiorna le intestazioni Cache-Control e Expires dell’asset.
* _MISS TCP_EXPIRED - questo stato viene segnalato quando una versione più recente di un cespite memorizzati nella cache scaduto viene servita dal client toohello hello POP. Questo errore si verifica quando è scaduto hello durata (TTL) per un asset memorizzati nella cache (ad esempio, max-age scaduto) e il server di origine hello restituisce una versione più recente di tale attività. Questa nuova versione di asset hello verrà utilizzata il client toohello anziché la versione memorizzata nella cache di hello. Inoltre, verranno memorizzata nel server perimetrale hello e nel client hello.
* CONFIG_NOCACHE - questo stato indica che una configurazione specifiche del cliente per il bordo POP impedito di asset hello viene memorizzato nella cache.
* NONE: questo stato indica che un controllo dell’aggiornamento del contenuto della cache non è stato eseguito.
* _MISS TCP_ CLIENT_REFRESH - questo stato viene segnalato quando un client HTTP (ad esempio browser) impone un' tooretrieve bordo POP una nuova versione di un asset non aggiornato dal server di origine hello.
  
    Per impostazione predefinita, i nostri server impediscono un client HTTP di forzare il nostro tooretrieve server edge una nuova versione di asset hello dal server di origine hello.
* PARTIAL_HIT TCP_: questo stato viene segnalato quando un richiesta di un intervallo di byte genera un riscontro per un asset parzialmente memorizzata nella cache. Hello ha richiesto l'intervallo di byte immediatamente servita da client di toohello hello POP.
* UNCACHEABLE - questo stato viene segnalato quando un asset Cache-Control e intestazioni Expires indicano che è necessario non memorizzare nella cache in un POP o da client hello HTTP. Questi tipi di richieste vengono gestiti dal server di origine hello

## <a name="cache-hit-ratio"></a>Percentuale riscontri cache
Questo rapporto indica la percentuale hello di richieste nella cache che sono state soddisfatte direttamente dalla cache.

report di Hello fornisce hello seguenti dettagli:

* Hello richiesto contenuto è stato memorizzato nella cache su più vicino toohello richiedente di hello POP.
* richiesta di Hello è stata gestita direttamente dal bordo hello di rete.
* richiesta di Hello non richiedono la riconvalida con il server di origine hello.

report di Hello non includono:

* Richieste rifiutate a causa di opzioni di filtro toocountry.
* Richieste di asset le cui intestazioni indicano che non devono essere memorizzate nella cache. Ad esempio, le intestazioni Cache-Control: private, Cache-Control: no-cache o Pragma: no-cache impediscono la memorizzazione nella cache di un asset.
* Richieste di intervallo di byte di contenuti parzialmente memorizzati nella cache.

formula Hello è: (HIT TCP_ / (TCP_ HIT + TCP_MISS)) * 100

* Selezionare i dati per oggi/questa settimana/mese di inizio intervallo tooview e così via o immettere le date personalizzate, quindi fare clic su "go" toomake che venga aggiornata con la selezione.
* È possibile esportare e download dei dati hello facendo hello excel icona foglio disponibile accanto troppo "go".

![Report percentuale riscontri cache](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>Dati trasferiti IPv4/IPV6
Questo report mostra la distribuzione dell'utilizzo del traffico hello in IPV4 e IPV6.

![Dati trasferiti IPv4/IPV6](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Selezionare i dati per oggi/questa settimana/mese di inizio intervallo tooview e così via, oppure immettere una data personalizzato.
* Quindi, fare clic su "go" toomake che venga aggiornata con la selezione.

## <a name="considerations"></a>Considerazioni
I report possono essere generati solo all'interno di hello ultimi 18 mesi.

