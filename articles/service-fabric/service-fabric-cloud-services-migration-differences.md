---
title: aaaDifferences tra l'infrastruttura dei servizi e i servizi Cloud | Documenti Microsoft
description: Informazioni generali per la migrazione di applicazioni di servizi Cloud tooService dell'infrastruttura.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a>Informazioni sulle differenze di hello tra servizi Cloud e infrastruttura a servizio prima della migrazione di applicazioni.
Microsoft Azure Service Fabric è una piattaforma di applicazione di prossima generazione cloud hello per le applicazioni distribuite altamente scalabili e altamente affidabile. Introduce molte nuove funzionalità per la creazione di pacchetti, la distribuzione, l'aggiornamento e la gestione di applicazioni cloud distribuite. 

Si tratta di un'applicazione toomigrating Guida introduttiva di servizi Cloud tooService dell'infrastruttura. La guida è incentrata soprattutto sulle differenze a livello di architettura e progettazione tra Servizi cloud e Service Fabric.

## <a name="applications-and-infrastructure"></a>Applicazioni e infrastruttura
Una differenza fondamentale tra servizi Cloud e di Service Fabric è relazione hello tra le macchine virtuali, i carichi di lavoro e applicazioni. In questo caso un carico di lavoro è definito come codice hello scrivere tooperform un'attività specifica o fornire un servizio.

* **Servizi cloud viene usato per la distribuzione di applicazioni come macchine virtuali.** codice Hello che scritto è fortemente accoppiata tooa istanza della macchina virtuale, ad esempio un ruolo Web o lavoratore. un carico di lavoro in servizi Cloud toodeploy è toodeploy uno o VM più istanze di tale carico di lavoro hello esecuzione. Non essendoci una separazione tra applicazioni e VM, non esiste una definizione formale di applicazione. Un'applicazione può essere considerata come un set di istanze del ruolo di lavoro o Web all'interno di una distribuzione di Servizi cloud o come un'intera distribuzione di Servizi cloud. In questo esempio un'applicazione viene illustrata come un set di istanze del ruolo.

![Applicazioni e topologia di Servizi cloud][1]

* **Service Fabric è sulla distribuzione applicazioni tooexisting macchine virtuali o computer che esegue Service Fabric in Windows o Linux.** servizi di Hello che è scrivere sono completamente separati dall'infrastruttura, che viene estratto dalla piattaforma dell'applicazione di Service Fabric hello, un'applicazione può essere distribuito toomultiple ambienti sottostante hello. Un carico di lavoro nell'infrastruttura del servizio è denominato "servizio" e uno o più servizi sono raggruppati in un'applicazione definito formalmente che viene eseguito sulla piattaforma dell'applicazione di Service Fabric hello. Più applicazioni possono essere distribuito tooa singolo cluster di Service Fabric.

![Applicazioni e topologia di Service Fabric][2]

Lo stesso Service Fabric è un livello della piattaforma di applicazioni eseguito in Windows o Linux, mentre Servizi cloud è un sistema per la distribuzione di macchine virtuali gestite di Azure con carichi di lavoro collegati.
modello di applicazione di Service Fabric Hello presenta numerosi vantaggi:

* Tempi di distribuzione rapidi. La creazione di istanze di macchina virtuale può richiedere tempi lunghi. Nell'infrastruttura del servizio, le macchine virtuali sono distribuite solo una volta tooform un cluster che ospita hello piattaforma Service Fabric. Da quel momento in poi, pacchetti di applicazioni possono essere distribuito toohello cluster molto rapidamente.
* Hosting ad alta densità. In Servizi cloud una macchina virtuale con ruolo di lavoro ospita un carico di lavoro. Nell'infrastruttura del servizio, le applicazioni sono separate da macchine virtuali di hello che eseguirli, pertanto che è possibile distribuire un numero elevato di applicazioni tooa pochissimi macchine virtuali, che può ridurre il costo complessivo per distribuzioni più grandi.
* Hello Service Fabric piattaforma possono essere eseguite dovunque che dispone di computer Windows Server o Linux, se si tratta di Azure o in locale. piattaforma di Hello fornisce un livello di astrazione dell'infrastruttura sottostante hello che consentono di eseguire l'applicazione in diversi ambienti. 
* Gestione delle applicazioni distribuite. Service Fabric è una piattaforma che non solo gli host di applicazioni distribuite, ma anche consente di gestire l'intero ciclo di vita in modo indipendente da hello ospita macchina virtuale o del ciclo di vita del computer.

## <a name="application-architecture"></a>Architettura dell'applicazione
Hello architettura di un'applicazione di servizi Cloud in genere include numerose dipendenze di servizio esterno, ad esempio il Bus di servizio, tabelle di Azure e archiviazione Blob, SQL, Redis e altri toomanage hello stato e i dati di un'applicazione e la comunicazione tra Web e i ruoli di lavoro in una distribuzione di servizi Cloud. Un esempio di applicazione di Servizi cloud completa può avere un aspetto simile al seguente:  

![Architettura di Servizi cloud][9]

Applicazioni di Service Fabric possono anche scegliere toouse hello stessi servizi esterni in un'applicazione completa. Utilizzando questo esempio di architettura di servizi Cloud, percorso di migrazione più semplice di hello da servizi Cloud tooService dell'infrastruttura è tooreplace hello servizi Cloud distribuzione solo con un'applicazione di Service Fabric, mantenendo hello architettura complessiva hello stesso. Hello Web e ruoli di lavoro possono essere tooService porting dell'infrastruttura di servizi senza stati con modifiche minime al codice.

![Architettura di Service Fabric dopo una migrazione semplice][10]

In questa fase, deve continuare sistema hello toowork hello stesso come in precedenza. Sfruttando le funzionalità con stato di Service Fabric, è possibile internalizzare gli archivi stati esterni come servizi con stato, se applicabile. Questo è più complessa rispetto a una semplice migrazione di servizi Web e ruoli di lavoro tooService infrastruttura senza stati, poiché richiede la scrittura di servizi personalizzati che forniscono l'applicazione di una funzionalità equivalente tooyour servizi esterni hello non è stato modificato. Hello i vantaggi di questa operazione includono: 

* Rimozione delle dipendenze esterne 
* Unificazione hello distribuzione, gestione e i modelli di aggiornamento. 

Un'architettura di esempio risultante dall'internalizzazione di questi servizi può avere un aspetto simile al seguente:

![Architettura di Service Fabric dopo una migrazione completa][11]

## <a name="communication-and-workflow"></a>Comunicazioni e flusso di lavoro
La maggior parte delle applicazioni di Servizi Cloud è costituita da più di un livello. Analogamente, un'applicazione di Service Fabric è costituita da più di un servizio, in genere molti servizi. Due modelli di comunicazione comuni sono la comunicazione diretta e quella tramite una risorsa di archiviazione esterna permanente.

### <a name="direct-communication"></a>Comunicazione diretta
Con la comunicazione diretta i livelli possono comunicare direttamente tramite l'endpoint esposto da ogni livello. In ambienti senza stati, ad esempio servizi Cloud, questo significa che la selezione di un'istanza di un ruolo VM, in modo casuale o carico round robin toobalance e connessione di endpoint tooits direttamente.

![Comunicazione diretta di Servizi cloud][5]

 La comunicazione diretta è un modello di comunicazione comune in Service Fabric. Hello chiave differenza tra servizi Cloud e infrastruttura di servizio è in servizi Cloud si connette tooa macchina virtuale, mentre in Service Fabric è connettersi tooa del servizio. Questa è una distinzione importante per due motivi:

* Servizi di Service Fabric non sono macchine virtuali associate toohello che ospitano. servizi può spostarsi all'interno del cluster hello e sono in effetti, toomove previsto intorno per diversi motivi: risorse bilanciamento del carico failover, gli aggiornamenti dell'applicazione e dell'infrastruttura e vincoli di posizionamento o di carico. Ciò significa che l'indirizzo di un'istanza del servizio può cambiare in qualsiasi momento. 
* Una macchina virtuale in Service Fabric può ospitare più servizi, ognuno con un endpoint univoco.

Service Fabric fornisce un meccanismo di individuazione del servizio, denominato hello servizio di denominazione, che può essere utilizzato tooresolve indirizzi degli endpoint dei servizi. 

![Comunicazione diretta di Service Fabric][6]

### <a name="queues"></a>Code
Un meccanismo di comunicazione comune tra livelli in ambienti senza stati, ad esempio servizi Cloud è un toodurably coda di archiviazione esterna toouse archiviare le attività di lavoro da un livello tooanother. Uno scenario comune è un livello web che invia i processi tooan coda di Azure o Bus di servizio in cui le istanze del ruolo di lavoro possono rimuovere dalla coda ed elaborare i processi di hello.

![Comunicazione con coda di Servizi cloud][7]

Hello stesso modello di comunicazione può essere utilizzato in Service Fabric. Può essere utile durante la migrazione di un tooService di applicazione di servizi Cloud dell'infrastruttura esistente. 

![Comunicazione diretta di Service Fabric][8]

## <a name="next-steps"></a>Passaggi successivi
Hello percorso di migrazione più semplice da servizi Cloud tooService Fabric è tooreplace solo hello distribuzione di servizi Cloud con un'applicazione di Service Fabric, mantenendo hello architettura complessiva dell'applicazione approssimativamente hello stesso. Hello articolo seguente viene fornita una Guida convert toohelp un tooa ruolo lavoro Web o di servizio senza stato Service Fabric.

* [Migrazione semplice: convertire un tooa ruolo lavoro Web o di servizio senza stato Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
