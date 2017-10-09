---
title: aaaAvailability dei servizi di Service Fabric | Documenti Microsoft
description: Descrive il rilevamento degli errori, il failover e il ripristino dei servizi
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Disponibilità dei servizi di Service Fabric
Questo articolo contiene una panoramica sul modo in cui Service Fabric gestisce la disponibilità di un servizio.

## <a name="availability-of-service-fabric-stateless-services"></a>Disponibilità dei servizi di Service Fabric senza stato
I servizi Service Fabric di Azure possono essere con o senza stato. Un servizio senza stato è un servizio di applicazione che non dispone di alcuna [stato locale](service-fabric-concepts-state.md) che deve toobe altamente disponibile o affidabile.

La creazione di un servizio senza stato richiede la definizione di un `InstanceCount`. numero di istanze di Hello definisce il numero di hello di istanze della logica dell'applicazione del servizio senza stato hello che deve essere in esecuzione nel cluster hello. Aumentare il numero di hello istanze è hello consigliato modo di scalabilità orizzontale di un servizio senza stato.

Quando un'istanza di servizio denominato stateless ha esito negativo, viene creata una nuova istanza su un nodo nel cluster hello idoneo. Ad esempio, un'istanza del servizio senza stato potrebbe non riuscire in Node1 ed essere ricreata in Node5.

## <a name="availability-of-service-fabric-stateful-services"></a>Disponibilità dei servizi di Service Fabric con stato
Un servizio con stato dispone di uno stato associato. In Service Fabric un servizio con stato è modellato come set di repliche. Ogni replica è un'istanza in esecuzione di codice hello del servizio hello che dispone anche di una copia dello stato di hello per quel servizio. Operazioni di lettura e scrittura vengono eseguite in una replica (denominata hello primario). Modifiche toostate da operazioni di scrittura sono *replicati* toohello altre repliche nel set di repliche hello (denominato repliche secondarie attive) e applicata. 

Può esistere solo una replica primaria, ma possono esistere più repliche secondarie attive. numero di Hello di repliche attive secondarie è configurabile e un elevato numero di repliche è in grado di tollerare un maggior numero di errori hardware e software simultaneo.

Se la replica primaria hello diventa inattiva, Service Fabric esegue hello secondario attivo repliche hello nuova replica primaria. Questa replica secondaria attiva ha già una versione di hello aggiornamento dello stato di hello (tramite *replica*), e può continuare l'elaborazione di ulteriore lettura e operazioni di scrittura.

Questo concetto, di una replica da un database primario o secondario attivo, è noto come hello ruolo della Replica.

### <a name="replica-roles"></a>Ruoli di replica
ruolo di Hello di una replica è toomanage utilizzati hello di ciclo di vita dello stato di hello gestito da tale replica. Una replica con ruolo primario gestisce le richieste di lettura. Hello primario gestisce anche tutte le richieste di scrittura aggiornando lo stato e la replica delle modifiche hello. Queste modifiche vengono applicata toohello repliche secondarie attive nel set di repliche hello. il processo di Hello di un concetto di secondario attivo è le modifiche dello stato tooreceive hello replica primaria è replicato e aggiornare la visualizzazione dello stato di hello.

> [!NOTE]
> Modelli di programmazione di livello superiore, ad esempio [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [servizi affidabili](service-fabric-reliable-services-introduction.md) nascondere il concetto di hello del ruolo di replica da Developer Edition hello. In attori, nozione hello del ruolo è necessaria, mentre in servizi di cui si è in gran parte semplificato per la maggior parte degli scenari.
>

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sui concetti di Service Fabric, vedere hello seguenti articoli:

- [Scalabilità dei servizi di Service Fabric](service-fabric-concepts-scalability.md)
- [Partizionamento dei servizi di Service Fabric](service-fabric-concepts-partitioning.md)
- [Definizione e gestione dello stato](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)
