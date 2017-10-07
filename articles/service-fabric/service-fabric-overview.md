---
title: aaaOverview dell'infrastruttura di servizio in Azure | Documenti Microsoft
description: "Panoramica dell'infrastruttura di servizio, in cui le applicazioni sono costituite da molti microservizi tooprovide scalabilità e resilienza. Service Fabric è una piattaforma di sistemi distribuiti utilizzato toobuild scalabile, affidabile e facilmente applicazioni gestite per i cloud hello."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Panoramica di Azure Service Fabric
Azure Service Fabric è una piattaforma di sistemi distribuiti che rende facile toopackage, distribuire e gestire contenitori e microservizi scalabili e affidabili. Service Fabric risolve inoltre hello problematiche legate lo sviluppo e la gestione delle applicazioni native cloud. Gli sviluppatori e gli amministratori non devono più occuparsi di risolvere complessi problemi di infrastruttura e possono concentrarsi sull'implementazione di carichi di lavoro cruciali e impegnativi, con la certezza di assicurare scalabilità, affidabilità e gestibilità. Service Fabric rappresenta una piattaforma di prossima generazione hello per creare e gestire questi aziendale, livello 1, le applicazioni a livello di cloud in esecuzione nei contenitori.

Questo breve video presenta Service Fabric e i microservizi: <center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Applicazioni costituite da microservizi 
Service Fabric consente toobuild e gestire applicazioni scalabili e affidabili composte microservizi che esegue a densità elevata in un pool condiviso di macchine, ovvero cui tooas un cluster. Fornisce un toobuild runtime sofisticati, lightweight distribuito, microservizi scalabili, senza stato e informazioni sullo stato in esecuzione nei contenitori. Fornisce inoltre tooprovision funzionalità di gestione completa dell'applicazione, distribuire, monitorare, aggiornamento/patch ed eliminare le applicazioni distribuite, inclusi i servizi nei contenitori.

Service Fabric viene attualmente usato in numerosi servizi Microsoft, tra cui database SQL di Azure, Azure Cosmos DB, Cortana, Microsoft Power BI, Microsoft Intune, Hub eventi di Azure, Hub IoT di Azure, Dynamics 365, Skype for Business e molti servizi di base di Azure.

Service Fabric è toocreate personalizzata native servizi cloud in grado di iniziare, in base alle esigenze e aumento delle dimensioni di scala toomassive con centinaia o migliaia di computer.

Gli attuali servizi su scala Internet vengono compilati attraverso microservizi. costituiti ad esempio da gateway di protocollo, profili utente, carrelli acquisti, elaborazione dell'inventario, code e cache. Service Fabric è una piattaforma di microservizi che assegna a ogni microservizio (o contenitore) un nome univoco, con o senza stato.

Service Fabric fornisce completa runtime e del ciclo di vita gestione funzionalità tooapplications che sono costituite da questi microservizi. Esso ospita microservizi all'interno di contenitori che vengono distribuiti e tra i cluster di Service Fabric hello. Spostamento di macchine virtuali toocontainers rende possibile un aumento dell'ordine di grandezza approssimativo densità. Analogamente, un altro ordine di grandezza densità diventa possibile quando si spostano da contenitori toomicroservices in questi contenitori. Un singolo cluster di database SQL di Azure, ad esempio, è costituito da centinaia di computer che eseguono decine di migliaia di contenitori in cui vengono ospitati complessivamente centinaia di migliaia di database. Ogni database è un microservizio di Service Fabric con stato. 

Per ulteriori informazioni sull'approccio microservizi hello, leggere [perché un'applicazione di microservizi approccio toobuilding?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Orchestrazione e distribuzione di contenitori
Service Fabric è un [agente di orchestrazione dei contenitori](service-fabric-cluster-resource-manager-introduction.md) che distribuisce microservizi in un cluster di computer. Microservizi possono essere sviluppata in molti modi di utilizzare hello [modelli di programmazione di Service Fabric](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [qualsiasi codice di propria scelta](service-fabric-deploy-existing-app.md). Inoltre, è possibile combinare entrambi i servizi nei processi e servizi in contenitori hello stessa applicazione. Se si desidera troppo[distribuire e gestire i contenitori](service-fabric-containers-overview.md), Service Fabric è la soluzione ottimale come un agente di orchestrazione del contenitore.

## <a name="any-os-any-cloud"></a>Qualsiasi sistema operativo, qualsiasi ambiente cloud
Service Fabric può essere eseguito ovunque. È possibile creare cluster di Service Fabric in molti ambienti, tra cui Azure o in locale, in Windows Server o su Linux, nonché in altri cloud pubblici. Inoltre, l'ambiente di sviluppo hello in hello SDK è **identici** toohello ambiente di produzione, con nessun emulatore coinvolto. In altre parole, ciò che viene eseguito nel cluster di sviluppo locale consente di distribuire i cluster toohello in altri ambienti.

![Piattaforma Service Fabric][Image1]

Per ulteriori informazioni sulla creazione di cluster locale, leggere [creazione di un cluster in Windows Server o Linux](service-fabric-deploy-anywhere.md) o per la creazione di un cluster Azure [tramite il portale di Azure hello](service-fabric-cluster-creation-via-portal.md).

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Microservizi con e senza stato per Service Fabric
Service Fabric consente applicazioni toobuild costituiti microservizi o contenitori. Uno stato modificabile all'esterno di una richiesta e la risposta dal servizio hello non conservano microservizi senza stati (ad esempio i gateway di protocollo e il proxy web). I ruoli di lavoro di Servizi cloud di Azure sono un esempio di servizio senza stato. Informazioni sullo stato microservizi (ad esempio gli account utente, database, i dispositivi, carrelli della spesa e code) mantengono uno stato modificabile, autorevole oltre hello richiesta e la risposta. Le attuali applicazioni su scala Internet sono costituite da una combinazione di microservizi con e senza stato. 

Una chiave differentation con Service Fabric è incentrato sulla generazione di servizi con stati, con hello [modelli di programmazione predefiniti ](service-fabric-choose-framework.md) o con i servizi con stati nei contenitori. Hello [scenari applicativi](service-fabric-application-scenarios.md) vengono descritti gli scenari di hello in cui vengono utilizzati i servizi con stato.


## <a name="application-lifecycle-management"></a>Gestione del ciclo di vita delle applicazioni
Service Fabric fornisce supporto per ciclo di vita dell'applicazione completo hello e CI/CD delle applicazioni cloud come Container. Questo ciclo di vita consente lo sviluppo di distribuzione, gestione quotidiana e la rimozione delle autorizzazioni tooeventual di manutenzione.

Funzionalità di gestione del ciclo di vita dell'applicazione di Service Fabric consentono ad amministratori di applicazioni e tooprovision di flussi di lavoro semplice, bassa tocco toouse operatori IT, distribuire, patch e monitorare le applicazioni. Questi flussi di lavoro predefiniti di ridurre notevolmente carico hello applicazioni tookeep operatori IT continuamente disponibile.

La maggior parte delle applicazioni è costituita da una combinazione di microservizi con e senza stato, da contenitori e da altri runtime o file eseguibili distribuiti insieme. Con i tipi sicuri sulle applicazioni hello, Service Fabric consente hello una distribuzione di più istanze dell'applicazione. Ogni istanza viene gestita e aggiornata in modo indipendente. Aspetto ancora più importante, Service Fabric può distribuire contenitori o file eseguibili di qualsiasi tipo e renderli affidabili. Service Fabric, ad esempio, può distribuire .NET, ASP.NET Core, Node.js, contenitori Windows, contenitori Linux, macchine virtuali Java, script, Angular o qualsiasi altro elemento costitutivo dell'applicazione.

Service Fabric è integrato con vari strumenti di integrazione continua e distribuzione continua, ad esempio [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html) e [Octopus Deploy](https://octopus.com/), e può essere usato con qualsiasi altro strumento di integrazione continua e distribuzione continua.

Per altre informazioni sulla gestione del ciclo di vita delle applicazioni, vedere l'articolo [Ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md). Per altre informazioni su come toodeploy qualsiasi codice, vedere [distribuire un eseguibile guest](service-fabric-deploy-existing-app.md).

## <a name="key-capabilities"></a>Funzionalità principali
Usando Service Fabric è possibile:

* Distribuire i Data Center tooAzure o tooon locale che esegue Windows o Linux con zero modifiche al codice. Scrivere una sola volta e quindi distribuire in un punto qualsiasi del cluster di Service Fabric tooany.
* Sviluppare applicazioni scalabili sono composti di microservizi utilizzando modelli di programmazione di Service Fabric hello, contenitori o qualsiasi codice.
* Sviluppare microservizi con o senza stato altamente affidabili. Semplificare la progettazione dell'applicazione hello tramite microservizi con stato. 
* Utilizzare hello novel Reliable Actors modello toocreate cloud gli oggetti di programmazione con lo stato e codice autonomo.
* Distribuire e orchestrare contenitori, tra cui contenitori Windows e Linux. Service Fabric è un agente di orchestrazione dei contenitori con stato e con funzione di riconoscimento dei dati.
* Distribuire applicazioni in pochi secondi e a densità elevata, con centinaia o migliaia di applicazioni o contenitori per ogni computer.
* Distribuire diverse versioni di hello stessa applicazione side-by-side e l'aggiornamento di ogni applicazione in modo indipendente.
* Gestire hello del ciclo di vita delle applicazioni senza tempo di inattività, inclusi gli aggiornamenti di rilievo e non di interruzione.
* Scalabilità orizzontale o aumentare il numero di hello di nodi in un cluster. Quando si modifica il numero di nodi, viene automaticamente modificato anche il numero di applicazioni.
* Monitorare e diagnosticare l'integrità di hello delle applicazioni e impostare i criteri per l'esecuzione di operazioni di ripristino automatico.
* Guardare bilanciamento delle risorse hello orchestrano ridistribuzione hello delle applicazioni in cluster hello. Service Fabric ripristino in caso di errori e consente di ottimizzare la distribuzione di hello di carico in base alle risorse disponibili.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni:
  * [Motivo per cui un microservizi approccio toobuilding applicazioni?](service-fabric-overview-microservices.md)
  * [Panoramica della terminologia](service-fabric-technical-overview.md)
* Configurazione dell' [ambiente di sviluppo](service-fabric-get-started.md)  
* Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
