---
title: "aaaOverview della capacità di hub di eventi di Azure dedicato | Documenti Microsoft"
description: "Panoramica della capacità di Hub eventi dedicato di Microsoft Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Panoramica di Hub eventi dedicato

*Gli hub di eventi dedicato* offre le distribuzioni single-tenant per i clienti con hello requisiti più complessi. Su larga scala completa, hub eventi di Azure può ingresso oltre 2 milioni di eventi al secondo o too2 GB al secondo di telemetria con una latenza di archiviazione e frazioni di secondo completamente durevole. Questo inoltre Abilita integrata soluzioni dall'elaborazione in tempo reale e batch in hello stesso sistema. Con l'archivio di hub di eventi inclusi nell'offerta di hello, è possibile ridurre la complessità di hello della soluzione con un singolo flusso supporta la pipeline in tempo reale e basata su batch.

Hello nella tabella seguente vengono confrontati i livelli di servizio disponibili hello degli hub di eventi. offerta di Hello dedicato hub eventi è un prezzo mensile fissato, toousage rispetto ai prezzi per la maggior parte delle funzionalità di Standard e Basic. livello dedicato Hello offre funzionalità di hello del piano Standard hello, ma con capacità di scala enterprise per i clienti con carichi di lavoro complesse. 

| Funzionalità | Basic | Standard | Dedicato |
| --- |:---:|:---:|:---:|
| Eventi in ingresso | Pagamento per ogni milione di eventi | Pagamento per ogni milione di eventi | Incluso |
| Unità di velocità effettiva (in entrata 1 MB/secondo, in uscita di 2 MB/secondo) | Pagamento per ogni ora | Pagamento per ogni ora | Incluso |
| Dimensioni del messaggio | 256 KB | 256 KB | 1 MB |
| Criteri per i server di pubblicazione | N/D | Sì | Sì |     
| Gruppi di utenti | 1 - Impostazione predefinita | 20 | 20 |
| Risposta a messaggi | Sì | Sì | Sì |
| Numero massimo di unità di velocità effettiva | 20 | 20 (too100 flessibile)  | 1 UC≈200 |
| Connessioni negoziate | 100 incluse | 1.000 incluse | 100 K incluse |
| Connessioni negoziate aggiuntive | N/D | Sì | Sì |
| Conservazione dei messaggi | 1 giorno incluso | 1 giorno incluso | Backup too7 giorni inclusi |
| Archivio (anteprima) | N/D   | Pagamento per ogni ora | Incluso |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Vantaggi della capacità di Hub eventi dedicato

Hello seguenti vantaggi sono disponibile quando si usano gli hub di eventi dedicato:

* Hosting a tenant singolo senza interferenze da altri tenant.
* Messaggio di dimensioni aumentano too1 MB rispetto too256 KB per Standard e Basic.
* Prestazioni sempre ripetibili.
* Capacità toomeet che il potenziamento deve è garantito.
* Scalabile compreso tra 1 e unità di capacità 8 (CU): fornendo too2 un milione eventi in ingresso al secondo.
  * Per gestire la scalabilità hello per dedicato hub eventi, in cui ogni CU può fornire circa hello equivalente 200 unità di velocità effettiva (TU).
* Manutenzione ridotta al minimo: il bilanciamento del carico, gli aggiornamenti del sistema operativo, le patch di protezione e il partizionamento vengono gestiti automaticamente.
* Prezzo mensile fisso.

Dedicato hub eventi rimuove anche alcuni dei limiti di velocità effettiva di hello dell'offerta Standard hello. Unità di velocità effettiva nei livelli Basic e Standard è autorizzare too1000 eventi al secondo o 1 MB al secondo di ingresso per TU e double tale quantità di traffico in uscita. offerta di scala dedicato Hello non presenta alcuna restrizione in entrata e in uscita evento esegue il conteggio. Questi limiti vengono gestiti solo con hello capacità di hello acquistato hub eventi di elaborazione.

Questo servizio è rivolto agli utenti di telemetria più grande hello e toocustomers disponibili con un contratto enterprise agreement.

## <a name="how-tooonboard"></a>Come tooonboard

piattaforma di Hello dedicato hub eventi verrà offerti attraverso un contratto enterprise agreement con diverse dimensioni di per. Ogni aggiornamento Cumulativo fornisce circa hello equivalente 200 unità di velocità effettiva. È possibile ridimensionare la capacità verso l'alto o verso il basso in tutto hello mese toomeet esigenze aggiungendo o rimuovendo per. piano dedicato Hello è univoco, in quanto è possibile che si verifichi un caricamento più pratico da hello gli hub di eventi prodotto team tooget hello distribuzione flessibile che è adatta alle proprie esigenze. 

## <a name="next-steps"></a>Passaggi successivi
Contattare il rappresentante Microsoft o il supporto Microsoft tooget ulteriori dettagli capacità dedicato hub di eventi. È possibile visualizzare altre informazioni sugli hub di eventi visitando hello seguenti collegamenti:

Per informazioni dettagliate sui prezzi, visitare hello seguenti collegamenti:

- [Tariffe di Hub eventi dedicato](https://azure.microsoft.com/pricing/details/event-hubs/). È anche possibile contattare il rappresentante Microsoft o i dettagli aggiuntivi di supporto Microsoft tooget sulla capacità dedicato hub eventi.
- Hello [domande frequenti sull'hub di eventi](event-hubs-faq.md) contiene informazioni sui prezzi e le risposte alcune domande frequenti sugli hub di eventi. 
