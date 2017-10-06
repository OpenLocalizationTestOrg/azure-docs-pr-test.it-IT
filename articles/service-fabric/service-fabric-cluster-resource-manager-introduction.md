---
title: hello aaaIntroducing servizio di gestione delle risorse Cluster dell'infrastruttura | Documenti Microsoft
description: Toohello un'introduzione, gestione delle risorse Cluster dell'infrastruttura del servizio.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>Introduzione della gestione delle risorse cluster hello Service Fabric
In genere la gestione dei sistemi IT o i servizi online deve dedicare le macchine fisiche o virtuali toothose specifici servizi specifici o sistemi. I servizi erano progettati come livelli. Era presente un livello "web" e un livello "dati" o "archiviazione". Applicazioni sarebbe necessario un livello di messaggistica in cui le richieste propagate avanti e indietro, oltre a un set di macchine dedicato toocaching. Ogni livello o un tipo di carico di lavoro aveva tooit dedicato di computer specifici: database hello ottenuto poche macchine tooit dedicato, server web hello alcuni. Se un particolare tipo di carico di lavoro causato macchine hello in cui si trovava toorun troppo frequente, è aggiunto altre macchine con livello di configurazione toothat stesso. Tuttavia, non tutti i carichi di lavoro può essere adattati facilmente - particolare con livello di dati hello viene in genere sostituito macchine con computer più grandi. Semplice. Se un computer non è riuscita, la parte di hello complessiva dell'applicazione è stata eseguita capacità inferiore fino a quando non è stato possibile ripristinare la macchina hello. Ancora piuttosto semplice, anche se non necessariamente divertente.

A questo punto tuttavia hello world del servizio e l'architettura software è stato modificato. È più comune l'adozione di una progettazione di scalabilità orizzontale da parte delle applicazioni. La creazione di applicazioni con contenitori o microservizi (o entrambi) è comune. Anche se è ancora possibile avere solo pochi computer, questi non eseguono una sola istanza di un carico di lavoro. Si può anche essere in esecuzione più carichi di lavoro diversi hello contemporaneamente. Ci sono dozzine di tipi di servizi diversi e nessuno usa le risorse di un intero computer. Sono presenti anche centinaia di istanze diverse di questi servizi. Ciascuna istanza denominata dispone di una o più istanze o repliche per la disponibilità elevata. A seconda delle dimensioni di hello di questi carichi di lavoro e alla disponibilità sono, potrebbe essere necessario con centinaia o migliaia di computer. 

Improvvisamente gestione dell'ambiente non è così semplice come la gestione dei tipi di toosingle dedicato macchine alcuni dei carichi di lavoro. I server virtuali e non dispone più nomi (si sono passati modelli mentali da [toocattle animali](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) dopo che tutti). La configurazione è minore sulle macchine hello e ulteriori informazioni sui servizi hello autonomamente. Hardware dedicato tooa singola istanza di un carico di lavoro è in gran parte di hello precedente. I servizi stessi sono diventati piccoli sistemi distribuiti che si dividono in più parti più piccole di hardware.

Poiché l'app non è più una serie di monoliti distribuiti in più livelli, è ora possibile molti toodeal combinazioni più con. Chi decide quali e quanti tipi di carichi di lavoro possono essere eseguiti su quale hardware? Carichi di lavoro funzionano bene in hello stesso hardware e che sono in conflitto? Quando un computer smette di funzionare cosa era in funzione in quel momento? Chi è responsabile di assicurarsi che il carico di lavoro venga rimesso in funzione? Attesa per il backup di hello computer (virtuale)? toocome o i carichi di lavoro automaticamente il failover tooother macchine e continuare l'esecuzione? È necessario l'intervento dell'utente? Come si gestiscono gli aggiornamenti in questo ambiente?

Come gli sviluppatori e gli operatori di gestione in questo ambiente, verrà toowant Guida gestione questa complessità. Oggetto assunzione binge e complessità hello toohide con utenti probabilmente non è la risposta corretta hello, che cosa è eseguito?

## <a name="introducing-orchestrators"></a>Introduzione agli agenti di orchestrazione
Un "Orchestrator" è il termine generale di hello per un componente software che consente agli amministratori di gestire questi tipi di ambienti. Orchestrators sono componenti di hello che accettano nelle richieste, ad esempio "Vorrei cinque copie di questo servizio in esecuzione nell'ambiente." Provare toomake hello corrispondenza hello desiderato stato dell'ambiente, indipendentemente da quanto accade.

Sono gli agenti di orchestrazione e non gli esseri umani che entrano in gioco quando un computer si arresta o un flusso di lavoro si blocca per qualche motivo non previsto. La maggior parte degli agenti di orchestrazione non si limita a gestire gli errori. Gli agenti infatti dispongono di altre funzionalità come la gestione di nuove distribuzioni, degli aggiornamenti e del consumo e la governance di risorse. Orchestrators tutti sono fondamentalmente sulla gestione di uno stato di configurazione nell'ambiente di hello desiderato. Si desidera toobe in grado di tootell agente di orchestrazione ciò che si desidera e fare in modo hello pesante. Aurora su Mesos, Docker Datacenter/Docker Swarm, Kubernetes e Service Fabric sono tutti esempi di agenti di orchestrazione. Questi orchestrators vengono sviluppati attivamente toomeet hello esigenze dei carichi di lavoro reale negli ambienti di produzione. 

## <a name="orchestration-as-a-service"></a>Orchestrazione come servizio
Gestione delle risorse Cluster Hello è componente del sistema hello che gestisce l'orchestrazione nell'infrastruttura del servizio. processo di gestione risorse del Cluster di Hello è suddivisa in tre parti:

1. Applicazione di regole
2. Ottimizzazione dell'ambiente
3. Contribuire con altri processi

toosee sul funzionamento del gestore delle risorse Cluster hello, guardare hello seguente video Microsoft Virtual Academy:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>Che cosa non è
Nelle applicazioni tradizionali di livello N è sempre presente un [Load Balancer](https://en.wikipedia.org/wiki/Load_balancing_(computing)). In genere si tratta di un servizio di bilanciamento del carico di rete (NLB) o un servizio di bilanciamento del carico dell'applicazione (ALB) a seconda di dove rimasta in stack di rete hello. Alcuni servizi di bilanciamento del carico sono basati su hardware, come BigIP F5, mentre altri sono software, ad Bilanciamento carico di rete di Microsoft. In altri ambienti si userà qualcosa di simile a HAProxy, nginx, Istio o Envoy in questo ruolo. In queste architetture, il processo di hello del bilanciamento del carico è tooensure ai carichi di lavoro di ricezione (approssimativamente) hello stessa quantità di lavoro. Le strategie per il bilanciamento del carico sono variate. Alcuni servizi di bilanciamento del invierebbe ogni server di diversi tooa chiamata diverso. Altri fornivano persistenza o visibilità elevata delle sessioni. Bilanciamento del carico più avanzate utilizza stima carico effettivo o tooroute reporting una chiamata in base al costo previsto e il carico di lavoro corrente.

Bilanciamento del carico di rete o tooensure router ha tentato di messaggio che hello livello web/di lavoro è rimasto approssimativamente bilanciato. Strategie per il bilanciamento del livello dati hello erano diversi e dipende da meccanismo di archiviazione dati hello. Bilanciamento del carico di livello dati hello basato sul partizionamento orizzontale dei dati, la memorizzazione nella cache, gestite viste, stored procedure e altri meccanismi di specifiche dell'archivio.

Anche se alcune delle strategie seguenti sono interessanti, hello servizio di gestione delle risorse Cluster dell'infrastruttura non è un valore come un servizio di bilanciamento del carico di rete o una cache. Un servizio di bilanciamento del carico di rete consente di bilanciare i front-end suddividendo il traffico di essi. Hello gestione delle risorse Cluster dell'infrastruttura del servizio dispone di una strategia diversa. Fondamentalmente, Service Fabric sposta *servizi* toowhere rendono più appropriate, è previsto il traffico di hello o caricare toofollow. Ad esempio, è possibile spostare toonodes servizi che sono attualmente freddo perché i servizi di hello che esistono non siano eseguendo la quantità di lavoro. nodi Hello potrebbero essere ad accesso sporadico, poiché servizi hello che erano presenti sono stati eliminati o spostati in un' posizione. Ad esempio, hello gestione delle risorse Cluster potrebbe inoltre spostare un servizio da un computer. Ad esempio macchina hello sta toobe aggiornato o è sottoposto a overload a causa di picco tooa consumo dai servizi di hello in esecuzione su di esso. Alernatively, requisiti di risorse del servizio hello potrebbero essere aumentate. In questo toocontinue macchina in esecuzione, di conseguenza non ci siano risorse sufficienti. 

Poiché gestione delle risorse Cluster hello è responsabile dello spostamento dei servizi correlati, contiene un toowhat di set di confronto diverse funzionalità disponibili in un bilanciamento del carico di rete. Questo avviene perché i bilanciamenti del carico di rete recapitare toowhere il traffico di rete sono già servizi, anche se tale posizione non è ideale per l'esecuzione hello servizio stesso. Servizio di gestione delle risorse Cluster dell'infrastruttura di Hello utilizza fondamentalmente diverse strategie per assicurare che risorse hello hello cluster vengono utilizzate in modo efficiente.

## <a name="next-steps"></a>Passaggi successivi
- Per informazioni sul flusso hello di architettura e le informazioni all'interno di gestione delle risorse Cluster hello, estrarre [in questo articolo](service-fabric-cluster-resource-manager-architecture.md)
- Hello gestione delle risorse Cluster dispone di numerose opzioni per la descrizione del cluster di hello. toofind ulteriori informazioni sulle metriche, consultare questo articolo in [che descrive un cluster di Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- Per altre informazioni sulla configurazione dei servizi vedere [Informazioni sulla configurazione dei servizi](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Le metriche sono la modalità di gestione di consumo e la capacità in cluster hello in hello gestore di risorse Cluster dell'infrastruttura del servizio. altre informazioni sulle metriche e come tooconfigure li estrarre toolearn [questo articolo](service-fabric-cluster-resource-manager-metrics.md)
- Gestione delle risorse Cluster Hello funziona con capacità di gestione dell'infrastruttura del servizio. lettura toofind le informazioni che l'integrazione, [in questo articolo](service-fabric-cluster-resource-manager-management-integration.md)
- toofind out sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, controllare l'articolo hello [bilanciamento del carico](service-fabric-cluster-resource-manager-balancing.md)
