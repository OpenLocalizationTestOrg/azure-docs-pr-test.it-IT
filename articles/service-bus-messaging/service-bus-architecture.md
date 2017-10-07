---
title: messaggio del Bus di servizio aaaAzure panoramica dell'architettura di elaborazione | Documenti Microsoft
description: Descrive l'architettura di elaborazione di messaggi hello del Bus di servizio di Azure.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>Architettura del bus di servizio
Questo articolo descrive l'architettura di elaborazione di messaggi hello del Bus di servizio di Azure.

## <a name="service-bus-scale-units"></a>Unità di scala del bus di servizio
Il bus di servizio è organizzato in base a *unità di scala*. Un'unità di scala è un'unità di distribuzione che contiene tutti i componenti necessari hello esecuzione di un servizio. Ogni area distribuisce una o più unità di scala del bus di servizio.

Uno spazio dei nomi del Bus di servizio è l'unità di scala tooa mappato. unità di scala Hello gestisce tutti i tipi di entità del Bus di servizio (code, argomenti, sottoscrizioni). Un'unità di scala del Bus di servizio è costituito da hello seguenti componenti:

* **Un set di nodi del gateway.** I nodi del gateway autenticano le richieste in ingresso. Ogni nodo del gateway ha un indirizzo IP pubblico.
* **Un set di nodi del broker di messaggistica.** I nodi del broker di messaggistica elaborano le richieste relative alle entità di messaggistica.
* **Un archivio del gateway.** archivio gateway Hello contiene i dati di hello per ogni entità per cui è definito in questa unità di scala. archivio gateway Hello è implementato su un database SQL Azure.
* **Più archivi di messaggistica.** Archivi di messaggistica contengono messaggi hello di tutte le code, argomenti e sottoscrizioni che sono definite in questa unità di scala. Contiene anche tutti i dati di sottoscrizione. A meno che non [il partizionamento delle entità di messaggistica](service-bus-partitioning.md) è abilitato, è una coda o argomento archivio di messaggistica tooone mappato. Le sottoscrizioni vengono archiviate in hello stesso archivio di messaggistica come l'argomento padre. Ad eccezione di Service Bus [messaggistica Premium](service-bus-premium-messaging.md), archivi di messaggistica hello vengono implementati nel database di SQL Azure.

## <a name="containers"></a>Contenitori
A ciascuna entità di messaggistica viene assegnato un contenitore specifico. Un contenitore è un costrutto logico che utilizza un solo toostore archivio messaggistica tutti i dati per questo contenitore. Ogni contenitore viene assegnato tooa nodo broker di messaggistica. In genere, esistono più contenitori che nodi del broker di messaggistica. Pertanto, ogni nodo del broker di messaggistica carica più contenitori. distribuzione di Hello del nodo broker di contenitori tooa messaggistica è organizzata in modo che tutti i nodi broker di messaggistica vengono caricati in modo uniforme. Se le modifiche al modello di carico hello (ad esempio, uno di hello contenitori ottiene molto occupati) o se un nodo broker di messaggistica diventa temporaneamente non disponibile, hello contenitori vengono ridistribuiti tra hello nodi broker di messaggistica.

## <a name="processing-of-incoming-messaging-requests"></a>Elaborazione delle richieste di messaggistica in ingresso
Quando un client invia un tooService richiesta Bus, servizio di bilanciamento del carico di Azure hello instrada tooany dei nodi gateway hello. nodo gateway Hello autorizza la richiesta di hello. Se la richiesta hello relativo a un'entità di messaggistica (coda, argomento o sottoscrizione), il nodo di gateway hello cerca entità hello nell'archivio gateway hello e determina in quali hello archivio messaggistica entità si trova. Cerca quindi il nodo broker di messaggistica è attualmente la manutenzione di questo contenitore e invia hello richiesta toothat nodo broker di messaggistica. Hello nodo broker di messaggistica Elabora richiesta hello e gli aggiornamenti di stato dell'entità hello nell'archivio di contenitore hello. Hello quindi il nodo broker di messaggistica invia hello risposta toohello indietro nodo gateway, che invia un client di back-toohello risposta appropriata che hello emesso la richiesta originale.

![Elaborazione delle richieste di messaggistica in ingresso](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>Passaggi successivi
Ora che si è lette una panoramica dell'architettura di Service Bus, hello seguenti collegamenti per ulteriori informazioni, visitare:

* [Panoramica della messaggistica del bus di servizio](service-bus-messaging-overview.md)
* [Dati fondamentali del bus di servizio](service-bus-fundamentals-hybrid-solutions.md)
* [Una soluzione di messaggistica accodata che usa le code del bus di servizio](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


