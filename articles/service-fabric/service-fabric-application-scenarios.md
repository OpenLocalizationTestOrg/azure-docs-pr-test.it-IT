---
title: aaaApplication scenari e progettazione | Documenti Microsoft
description: Panoramica delle categorie di applicazioni cloud nell'infrastruttura di servizi. Illustra la progettazione di applicazioni con servizi con e senza stato.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>Scenari di applicazione di Service Fabric
Azure Service Fabric offre una piattaforma affidabile e flessibile che consente di toowrite ed eseguire molti tipi di servizi e applicazioni aziendali. Queste applicazioni e microservizi possono essere con stato o senza stato e sono bilanciato su risorse tra le macchine virtuali toomaximize efficienza. l'architettura univoca di Service Fabric Hello consente tooperform in prossimità di analisi dei dati in tempo reale, il calcolo in memoria, le transazioni parallele e nelle applicazioni di elaborazione di eventi. È possibile aumentare o ridurre facilmente il numero di applicazioni a seconda dei requisiti di risorse.

piattaforma Service Fabric Hello in Azure è ideale per hello seguenti categorie di applicazioni:

* **Servizi a disponibilità elevata**: i servizi di Service Fabric garantiscono un failover veloce tramite la creazione di più repliche secondarie del servizio. Se un nodo, un processo o un singolo servizio si arresta a causa di toohardware o altri errori, una delle repliche secondarie hello è tooa innalzate di livello la replica primaria con una minima perdita di servizio.
* **Servizi scalabili**: possono essere partizionati singoli servizi, consentendo di stato toobe su cluster hello di scalabilità. Inoltre, singoli servizi possono essere creati e rimossi in tempo reale di hello. Possono essere facilmente e rapidamente scalabilità da alcune istanze su alcuni nodi toothousands di istanze su molti nodi e quindi ridimensionata nuovamente, a seconda delle esigenze di risorse. È possibile utilizzare questi servizi di Service Fabric toobuild e gestire i relativi cicli di vita completo.
* **Calcolo sui dati non statici**: Service Fabric consente dati toobuild, input/output e le applicazioni con stato con utilizzo intensivo di calcolo. Service Fabric consente la collocazione di hello di elaborazione (calcolo) e i dati nelle applicazioni. In genere, quando l'applicazione richiede accesso toodata, è la latenza di rete associata a un livello di cache o l'archiviazione di dati esterni. Con i servizi con stato di Service Fabric la latenza viene eliminata e questo consente operazioni di lettura e scrittura più efficienti. Si supponga, ad esempio, di avere un'applicazione che esegue la selezione delle raccomandazioni quasi in tempo reale per i clienti, con un requisito di tempo di round trip inferiore a 100 millisecondi. caratteristiche di latenza e prestazioni Hello dei servizi di Service Fabric (in cui il calcolo hello della selezione di raccomandazione è collocati insieme ai dati hello e regole) fornisce un utente toohello esperienza reattiva confrontato con l'implementazione standard di hello modello di avere toofetch hello i dati necessari da un archivio remoto.  
* **Applicazioni interattive basate sulla sessione**: Service Fabric si rivela utile se le applicazioni, ad esempio un gioco online o la messaggistica istantanea, richiedono operazioni di lettura e scrittura con bassa latenza. Service Fabric consente si toobuild queste applicazioni con state interattivo senza la necessità di toocreate un archivio separato o cache, come richiesto per le applicazioni senza state. Questo aumenta la latenza e può introdurre problemi di coerenza.
* **Analitica dei dati e flussi di lavoro**: hello veloce letture e scritture di Service Fabric consentono alle applicazioni in modo affidabile devono elaborare gli eventi o flussi di dati. Service Fabric consente inoltre alle applicazioni che descrivono la pipeline di elaborazione, in cui i risultati devono essere passati e affidabile in toohello successiva fase senza perdita di elaborazione. Sono inclusi sistemi transazionali e finanziari, in cui le garanzie di coerenza e calcolo dei dati sono essenziali.
* **Raccolta dati, elaborazione e IoT**: poiché Service Fabric gestisce su larga scala e presenta una latenza bassa tramite i servizi con stati, è ideale per l'elaborazione dati in milioni di dispositivi in cui sono dati hello per i dispositivi hello e calcolo hello un percorso condiviso.
Numerosi clienti hanno realizzato sistemi IoT usando Service Fabric, ad esempio [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), [Schneider Electric](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) e [Mesh Systems](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/).

## <a name="application-design-case-studies"></a>Case study sulla progettazione delle applicazioni
Un numero di case study che mostrano come Service Fabric è usato toodesign applicazioni viene pubblicato su hello [blog del team di Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) hello e [sito soluzioni microservizi](https://azure.microsoft.com/solutions/microservice-applications/).

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>Progettare applicazioni costituite da microservizi con e senza stato
La compilazione di applicazioni con ruoli di lavoro del servizio cloud di Azure è un esempio di servizio senza stato. Al contrario, con stati microservizi mantengono dello stato autorevole oltre hello richiesta e la risposta. In questo modo la disponibilità elevata e la coerenza dello stato di hello tramite le API semplici che forniscono garanzie di eseguito dalla replica transazionale. Servizi di informazioni sullo stato dell'infrastruttura servizio di semplificare l'elevata disponibilità, portarla tooall tipi di applicazioni, non solo i database e altri archivi dati. Si tratta di un progresso naturale. Le applicazioni sono stati già spostati dall'utilizzo di database relazionali esclusivamente per i database di disponibilità elevata tooNoSQL. Ora stesse applicazioni hello possono avere loro stato "attivo" e i dati gestiti all'interno di essi per ottenere un miglioramento delle prestazioni aggiuntivi senza compromettere l'affidabilità, la coerenza o disponibilità.

Quando si compilano applicazioni composto microservizi, in genere è una combinazione di applicazioni web senza stato (ASP.NET, Node.js e così via) la chiamata in servizi di livello intermedio di business e senza stato, tutti distribuiti in hello stesso cluster di Service Fabric utilizzando i comandi di distribuzione di Service Fabric hello. Ognuno di questi servizi è indipendente utilizzo considerare tooscale, affidabilità e delle risorse, migliorando la flessibilità per lo sviluppo e del ciclo di vita di gestione.

Informazioni sullo stato microservizi semplificano progettazioni di applicazioni perché rimuoverle necessità hello per le code aggiuntive hello e memorizza nella cache che è stati in genere necessario tooaddress hello requisiti di disponibilità e la latenza delle applicazioni semplicemente senza state. Poiché i servizi con stati sono naturalmente latenza bassa e a disponibilità elevata, ciò significa che non esistono meno toomanage lo spostamento di parti dell'applicazione nel suo complesso. diagrammi di Hello seguenti illustrano le differenze di hello tra la progettazione di un'applicazione che è senza stata e uno stato. Sfruttando hello [servizi affidabili](service-fabric-reliable-services-introduction.md) e [Reliable Actors](service-fabric-reliable-actors-introduction.md) modelli di programmazione, i servizi con stati ridurre la complessità dell'applicazione durante il raggiungimento di velocità effettiva elevata e bassa latenza.

## <a name="an-application-built-using-stateless-services"></a>Applicazione creata con servizi senza stato
![Applicazione che usa un servizio senza stato][Image1]

## <a name="an-application-built-using-stateful-services"></a>Applicazione creata con servizi con stato
![Applicazione che usa un servizio senza stato][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi

* In attesa troppo[case study](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* Leggere informazioni sui [casi di studio dei clienti](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)
* Altre informazioni su [modelli e scenari](service-fabric-patterns-and-scenarios.md)

* Introduzione a servizi di compilazione e senza stati con hello Service Fabric [servizi affidabili](service-fabric-reliable-services-quick-start.md) e [attori affidabili](service-fabric-reliable-actors-get-started.md) modelli di programmazione.
* Vedere anche hello seguenti argomenti:
  * [Informazioni sui microservizi](service-fabric-overview-microservices.md)
  * [Definire e gestire lo stato del servizio](service-fabric-concepts-state.md)
  * [Disponibilità dei servizi di Service Fabric](service-fabric-availability-services.md)
  * [Scalabilità dei servizi di Service Fabric](service-fabric-concepts-scalability.md)
  * [Partizionare i servizi di Service Fabric](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
