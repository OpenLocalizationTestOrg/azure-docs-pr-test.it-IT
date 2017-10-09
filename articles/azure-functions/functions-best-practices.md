---
title: aaaBest procedure consigliate per le funzioni di Azure | Documenti Microsoft
description: Informazioni su modelli e procedure consigliate per Funzioni di Azure.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: funzioni di azure, modelli, procedure consigliate, funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>Ottimizzare le prestazioni di hello e l'affidabilità delle funzioni di Azure

Questo articolo fornisce informazioni aggiuntive tooimprove hello prestazioni e affidabilità delle app di funzione. 


## <a name="avoid-long-running-functions"></a>Evitare funzioni con esecuzione prolungata

Le funzioni con esecuzione prolungata e di grandi dimensioni possono causare problemi di timeout imprevisti. Una funzione può risultare lungo a causa di dipendenze di Node.js toomany. L'importazione delle dipendenze può anche fare aumentare i tempi di caricamento causando timeout imprevisti. Le dipendenze vengono caricate in modo sia esplicito che implicito. Un singolo modulo caricato dal codice potrebbe caricare i propri moduli aggiuntivi.  

Quando è possibile, suddividere le funzioni di grandi dimensioni in gruppi di funzioni più piccoli che possono interagire tra loro e restituire rapidamente le risposte. Ad esempio, un webhook o una funzione di attivazione HTTP potrebbe richiedere una risposta di riconoscimento all'interno di un determinato limite di tempo; è comune per webhook toorequire un intervento immediato. È possibile passare i payload di hello HTTP trigger in una coda toobe elaborati da una funzione di attivazione coda. Questo approccio consente il lavoro effettivo toodefer hello e restituire una risposta immediata.


## <a name="cross-function-communication"></a>Comunicazioni tra funzioni

Quando si integra più funzioni, è in genere un best practice toouse le code di archiviazione per le comunicazioni di funzione tra.  Hello principale, infatti, le code di archiviazione sono più economiche e tooprovision molto più semplice. 

Singoli messaggi in una coda di archiviazione sono limitati in dimensioni too64 KB. Se è necessario toopass i messaggi di grandi dimensioni tra le funzioni, una coda di Service Bus di Azure potrebbe essere le dimensioni dei messaggi utilizzati toosupport too256 KB.

Gli argomenti del bus di servizio sono utili se è necessario filtrare i messaggi prima dell'elaborazione.

Gli hub eventi sono utili toosupport le comunicazioni di volumi elevati.


## <a name="write-functions-toobe-stateless"></a>Scrivere funzioni toobe senza stato 

Le funzioni devono essere senza stato e idempotenti se possibile. Associare ai dati eventuali informazioni obbligatorie sullo stato. Ad esempio, un ordine in fase di elaborazione probabilmente ha un membro `state` associato. Una funzione è riuscito a elaborare un ordine in base a tale stato mentre funzione hello stessa rimane senza stato. 

Le funzioni idempotenti sono consigliate in particolare con i trigger timer. Ad esempio, se si dispone di un elemento che è assolutamente necessario eseguire una volta al giorno, viene scritto in modo è possibile eseguire qualsiasi momento durante il giorno hello con hello stessi risultati. funzione Hello può uscire quando non sono presenti operazioni per un determinato giorno. Anche se un'esecuzione precedente non è riuscito toocomplete hello prossima esecuzione deve prelevare dove era stata interrotta.


## <a name="write-defensive-functions"></a>Scrivere funzioni difensive

Si supponga che la funzione possa rilevare un'eccezione in qualsiasi momento. Durante l'esecuzione successiva hello, progettare le funzioni con hello possibilità toocontinue da un punto di errore precedente. Si consideri uno scenario che richiede hello seguenti azioni:

1. Query per 10.000 righe in un database.
2. Creare un messaggio nella coda per ognuna di tali righe tooprocess ulteriormente verso il basso la riga hello.
 
In base alla complessità del sistema, è possibile che i servizi downstream coinvolti non funzionino correttamente, che si verifichino interruzioni della rete, che vengano raggiunti i limiti di quota e così via. Tutti questi elementi possono influire sulla funzione in qualsiasi momento. È necessario toodesign toobe le funzioni pronti a.

Come reagisce il codice in caso di errore dopo l'inserimento di 5.000 di tali elementi in una coda per l'elaborazione? Tenere traccia degli elementi in un set già completato. In caso contrario, è possibile inserirli di nuovo la volta successiva. Ciò può influire in modo negativo sul flusso di lavoro. 

Se un elemento della coda è già stato elaborato, consentire toobe la funzione alcuna operazione.

È possibile sfruttare le misure di difesa già fornito per i componenti che si utilizza nella piattaforma Azure funzioni hello. Ad esempio, vedere **la gestione dei messaggi di coda non elaborabile** nella documentazione di hello per [coda di archiviazione di Azure attiva](functions-bindings-storage-queue.md#trigger).
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>Non combinazione di test e produzione di codice in hello stesso app (funzione)

Le funzioni all'interno di un'app per le funzioni condividono le risorse. Ad esempio, la memoria è condivisa. Se si usa un'app di funzione nell'ambiente di produzione, non aggiungere funzioni relative ai test e tooit risorse. per evitare possibili sovraccarichi imprevisti durante l'esecuzione del codice di produzione.

Prestare attenzione a quello che si carica nelle app per le funzioni di produzione. Memoria Media viene calcolata in ogni funzione nell'app hello.

Se si usa un assembly condiviso a cui si fa riferimento in più funzioni di .Net, inserirlo in una cartella condivisa comune. Assembly di riferimento hello con un toohello simile istruzione esempio seguente: 

    #r "..\Shared\MyAssembly.dll". 

In caso contrario, è facile tooaccidentally distribuire più versioni di test dello stesso file binario che si comportano in modo diverso tra le funzioni hello.

Non usare la registrazione dettagliata nel codice di produzione. Ha un impatto negativo sulle prestazioni.



## <a name="use-async-code-but-avoid-blocking-calls"></a>Usare codice asincrono ma evitare di bloccare le chiamate

La programmazione asincrona è una procedura consigliata. Tuttavia, non sempre fare riferimento a hello `Result` proprietà o chiamare `Wait` metodo su un `Task` istanza. Questo approccio può causare un esaurimento toothread.


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello seguenti risorse:

Poiché Funzioni di Azure usa Servizio app di Azure, è consigliabile vedere anche le linee guida del servizio app.
* [Schemi e procedure per le ottimizzazioni delle prestazioni HTTP](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

