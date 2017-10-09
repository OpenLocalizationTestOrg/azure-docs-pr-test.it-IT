---
title: aaaDefinine e gestire lo stato in Azure microservizi | Documenti Microsoft
description: Come toodefine e gestire lo stato del servizio in Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>Stato del servizio
**Stato del servizio** fa riferimento toohello in memoria o su dati su disco che un servizio richiede toofunction. Include, ad esempio, le strutture di dati hello e le variabili membro servizio hello legge e scrive toodo lavoro. A seconda della modalità progettazione di un servizio hello, può anche includere file o altre risorse che sono archiviati su disco. File di un database, ad esempio, hello utilizzerebbe toostore registri delle transazioni e di dati.

Come un servizio di esempio, si consideri una calcolatrice. Questo servizio di calcolatrice di base accetta due numeri per restituirne la somma. L'esecuzione di questo calcolo non implica alcuna variabile membro o altre informazioni.

Si consideri ora hello calcolatrice stessa, ma con un metodo aggiuntivo per l'archiviazione e la restituzione ultima somma di hello è calcolato. Il servizio è ora con stato. Informazioni sullo stato significa che contiene uno stato che scrive toowhen calcola la somma di nuovo e legge da quando si chiede somma calcolata di tooreturn hello ultimo.

In Azure Service Fabric, primo servizio hello viene chiamato un servizio senza stato. secondo servizio Hello viene chiamato un servizio con stato.

## <a name="storing-service-state"></a>Archiviazione dello stato del servizio
Lo stato può essere esternalizzato o con percorso condiviso con codice di hello che sta modificando lo stato di hello. Esternalizzazione di stato è in genere eseguita con un database esterno o altri dati di archiviano che viene eseguito in computer diversi tramite rete hello o fuori del processo su hello nello stesso computer. In questo esempio, la calcolatrice archivio dati hello potrebbe essere un database SQL o un'istanza dell'archivio tabelle di Azure. Somma di hello toocompute ogni richiesta esegue un aggiornamento per i dati e richieste toohello servizio tooreturn hello valore generano valore corrente di hello recuperati dall'archivio hello. 

Lo stato può anche essere condiviso con codice hello che modifica lo stato di hello. I servizi con stato in Service Fabric vengono in genere creati usando questo modello. Service Fabric fornisce hello infrastruttura tooensure che questo stato è altamente disponibile, coerente e durevole e che i servizi di hello creati in questo modo può essere facilmente scalato.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sui concetti di Service Fabric, vedere hello seguenti articoli:

* [Disponibilità dei servizi di Service Fabric](service-fabric-availability-services.md)
* [Scalabilità dei servizi di Service Fabric](service-fabric-concepts-scalability.md)
* [Partizionamento dei servizi di Service Fabric](service-fabric-concepts-partitioning.md)
* [Reliable Services di Service Fabric](service-fabric-reliable-services-introduction.md)
