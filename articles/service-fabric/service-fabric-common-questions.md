---
title: domande aaaCommon su Microsoft Azure Service Fabric | Documenti Microsoft
description: Domande frequenti su Service Fabric e relative risposte
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Domande frequenti su Service Fabric

Esistono molte domande frequenti sulle caratteristiche e sulle modalità di uso di Service Fabric. In questo documento vengono illustrate molte di queste domande comuni e le relative risposte.

## <a name="cluster-setup-and-management"></a>Configurazione e gestione del cluster

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>È possibile creare un cluster che si estenda a più aree di Azure o ai miei data center?

Sì. 

core Hello tecnologia di clustering Service Fabric può essere utilizzato toocombine macchine in esecuzione ovunque nel mondo hello, in modo che abbiano rete connettività tooeach altri. La compilazione e l'esecuzione di questo tipo di cluster possono essere tuttavia complicate.

Se si è interessati in questo scenario, è consigliabile tooget in contatto tramite hello [elenco di problemi di Service Fabric Github](https://github.com/azure/service-fabric-issues) o tramite il supporto tecnico clienti in altro materiale sussidiario tooobtain ordine. il team di Service Fabric Hello sta spiegazioni aggiuntive tooprovide, linee guida e consigli per questo scenario. 

Tooconsider alcune operazioni: 

1. Hello risorsa cluster di Service Fabric in Azure è oggi regionale, come sono set di scalabilità della macchina virtuale hello tale cluster hello si basa su. Ciò significa che nell'evento hello di un errore internazionale è possibile perdere cluster hello di hello possibilità toomanage tramite Gestione risorse di Azure hello o hello portale di Azure. Questa situazione può verificarsi anche se hello cluster rimane in esecuzione e sarà in grado di toointeract con esso direttamente. Inoltre, Azure attualmente non offre hello possibilità toohave una singola rete virtuale che può essere utilizzata in aree geografiche. Ciò significa che richiede un cluster con più aree in Azure [indirizzi IP pubblici per ogni macchina virtuale nel set di scalabilità di macchine Virtuali hello](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) o [gateway VPN di Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md). Queste opzioni rete hanno effetti diversi nella progettazione di applicazioni di livello toosome i costi e prestazioni, in modo che un'attenta analisi e la pianificazione è necessario prima posizione di un ambiente di questo tipo.
2. Hello manutenzione, la gestione e monitoraggio di tali macchine può diventare complicati, soprattutto quando estese su _tipi_ degli ambienti, ad esempio tra provider di cloud diversi o tra risorse locali e Azure . Prestare attenzione tooensure che viene aggiornato, il monitoraggio, gestione e diagnostica viene riconosciuta per cluster hello e applicazioni hello prima di eseguire i carichi di lavoro in un tale ambiente. Se si ha già grande esperienza di risoluzione di questi problemi in Azure o nei propri Data center, è possibile che si possano applicare queste stesse soluzioni durante la compilazione o l'esecuzione del cluster di Service Fabric. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>I nodi di Service Fabric ricevono automaticamente aggiornamenti del sistema operativo?

Non oggi, ma è anche una richiesta comune che Azure intende toodeliver.

In hello provvisorio, abbiamo [fornita un'applicazione](service-fabric-patch-orchestration-application.md) che i sistemi operativi hello sotto i nodi di Service Fabric rimangono patch e backup toodate.

challenge Hello con aggiornamenti del sistema operativo è in genere che richiedono il riavvio del computer hello, che comporta una perdita temporanea della disponibilità. Di per sé che non è un problema, poiché Service Fabric verrà reindirizzata automaticamente il traffico per tali nodi tooother servizi. Tuttavia, se gli aggiornamenti del sistema operativo non vengono coordinati cluster hello, è potenzialmente hello che molti nodi verso il basso in una sola volta. Tali riavvii simultanei possono causare la perdita totale di disponibilità per un servizio o, perlomeno, per una partizione specifica (per un servizio con stato).

In futuro hello, contiamo criteri di aggiornamento toosupport un sistema operativo che sono completamente automatizzato e coordinato tra i domini di aggiornamento, verificare che la disponibilità viene mantenuta nonostante i riavvii e altri errori imprevisti.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>È possibile usare set di scalabilità di macchine virtuali di grandi dimensioni nel cluster di Service Fabric? 

**Risposta breve**: no. 

**Tempo di risposta** : anche se i set di scalabilità macchina virtuale di grandi dimensioni hello consentono tooscale un macchina virtuale del set di scalabilità fino a 1000 istanze della macchina virtuale, tale scopo, utilizzare hello dei gruppi di posizionamento (PGs). Domini di errore (Fd) e domini di aggiornamento (UD) sono solo coerenti all'interno di un servizio dell'infrastruttura Usa posizionamento gruppo decisioni di posizionamento toomake domini di errore e domini di aggiornamento delle istanze di repliche o del servizio del servizio. Poiché hello domini di errore e domini di aggiornamento sono confrontabili solo all'interno di un gruppo di posizionamento SF può essere utilizzato. Ad esempio, se VM1 in PG1 con una topologia di FD = 0 e VM9 in PG2 con una topologia di FD = 4, non significa che VM1 e VM2 si trovano in due rack Hardware diverso, pertanto SF non è possibile utilizzare i valori hello FD nelle decisioni di selezione host case toomake.

Esistono altri problemi con il set di scalabilità di grandi dimensioni di macchina virtuale, ad esempio mancanza di hello di livello 4 di supporto del bilanciamento del carico. Fare riferimento toofor [informazioni dettagliate sulla grande set di scalabilità](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>Che cos'è una dimensione minima di hello di un cluster di Service Fabric? Perché non può essere di dimensioni minori?

Hello dimensione supportata minima per un cluster di Service Fabric che esegue i carichi di lavoro è cinque nodi. Per scenari di sviluppo e test, sono supportati cluster a tre nodi.

Questi valori minimi esistono perché il cluster di Service Fabric hello esegue un set di servizi di sistema con stato, tra cui servizio di denominazione hello e gestione failover hello. Questi servizi, tenere traccia di quali servizi sono stati distribuiti toohello cluster e in cui sono ospitati attualmente, dipendono dalla coerenza assoluta. La coerenza assoluta, a sua volta dipende da hello possibilità tooacquire un *quorum* per qualsiasi aggiornamento specificato toohello stato di tali dei servizi, in cui un quorum rappresenta una maggioranza strict di repliche di hello (N/2 + 1) per un determinato servizio.

Detto questo, esaminiamo alcune possibili configurazioni di cluster:

**Un nodo**: questa opzione non fornisce la disponibilità elevata poiché la perdita di hello del nodo singolo di hello per qualsiasi motivo significa perdita di hello dell'intero cluster hello.

**Due nodi**: un quorum per un servizio distribuito tra due nodi (N = 2) è 2 (2/2 + 1 = 2). Quando una singola replica viene persa, è Impossibile toocreate un quorum. Dato che per aggiornare un servizio è necessario portare temporaneamente offline una replica, questa non è una configurazione utile.

**Tre nodi**: con tre nodi (N = 3), hello requisito toocreate un quorum è ancora due nodi (3/2 + 1 = 2). Ciò significa che è possibile perdere un singolo nodo e mantenere comunque il quorum.

configurazione di Hello tre nodi del cluster è supportata per sviluppo/test perché è possibile in modo sicuro eseguire aggiornamenti e mantenute in seguito a errori di nodo singolo, fino a quando essi non vengono eseguite contemporaneamente. Per i carichi di lavoro, è necessario essere resilienti toosuch errori simultanei, quindi cinque nodi sono obbligatori.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>È possibile disattivare il cluster costi toosave notte/i fine settimana?

Generalmente, no. Service Fabric archivia lo stato su dischi locali, temporanei, vale a dire che se tooa spostato diversi host macchina virtuale hello è hello dati non vengono spostati con esso. In condizioni normali, che non è un problema come nuovo nodo hello viene portata backup toodate da altri nodi. Tuttavia, se si arresta tutti i nodi e riavviarle in un secondo momento, è possibile che la maggior parte dei nodi hello avviare nei nuovi host e rendere hello sistema non è possibile toorecover significativa.

Se si desidera toocreate cluster per il test dell'applicazione prima della distribuzione, è consigliabile creare in modo dinamico tali cluster come parte del [integrazione continua/continua pipeline di distribuzione](service-fabric-set-up-continuous-integration.md).


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>Come aggiornare il sistema operativo (ad esempio da Windows Server 2012 tooWindows Server 2016)

Mentre si sta lavorando oggi, una migliore esperienza utente è responsabile per l'aggiornamento di hello. È necessario aggiornare l'immagine del sistema operativo hello in hello macchine virtuali di hello una macchina virtuale del cluster alla volta. 

## <a name="container-support"></a>Supporto dei contenitori

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>Perché sono i contenitori che vengono distribuiti tooSF Impossibile tooresolve DNS risolve?

Il problema è stato segnalato nei cluster versione 5.6.204.9494 

**Attenuazione** : seguire [questo documento](service-fabric-dnsservice.md) tooenable hello DNS del servizio service fabric nel cluster.

**Correggere** : versione del cluster aggiornamento tooa supportato che è superiore a 5.6.204.9494, quando è disponibile. Se il cluster è impostato tooautomatic aggiornamenti, quindi cluster hello verrà aggiornato automaticamente toohello versione che si è verificato questo problema risolto.

  
## <a name="application-design"></a>Progettazione di applicazioni

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>Che cos'è dati tooquery modo migliori di hello tra partizioni di un insieme affidabile?

Raccolte affidabili sono in genere [partizionata](service-fabric-concepts-partitioning.md) tooenable con scalabilità maggiore produttività e prestazioni. Ciò significa che lo stato di hello per un determinato servizio può essere distribuito in 10s o 100s macchine. tooperform operazioni sul set di dati completo, sono disponibili alcune opzioni:

- Creare un servizio che esegue una query di tutte le partizioni di un altro servizio toopull nei dati hello necessario.
- Creare un servizio che possa ricevere dati da tutte le partizioni di un altro servizio.
- Periodicamente il push dei dati dall'archivio esterno di tooan ogni servizio. Questo approccio è appropriato se stai eseguendo query di hello non fanno parte della logica di business principale.


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>Che cos'è dati tooquery modo migliori di hello in my attori?

Gli attori sono progettate toobe unità indipendenti dello stato e calcolo, pertanto non è consigliabile tooperform ampie query dello stato actor in fase di esecuzione. Se si dispone di un tooquery necessario tra il set completo di hello dello stato dell'actor, considerare uno:

- Sostituendo i servizi actor con i servizi reliable con stati, in modo che il numero di hello di rete richieste toogather tutti i dati da hello numero attori toohello di partizioni nel servizio.
- Progettazione al push tooperiodically attori relativo archivio esterno tooan di stato per le query più semplice. Come in precedenza, questo approccio è realizzabile solo se si sta eseguendo query di hello non sono necessari per il comportamento di runtime.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>Quanti dai è possibile archiviare in una raccolta Reliable Collections?

Servizi affidabili sono in genere partizionati, in modo quantità hello che è possibile archiviare è limitato solo dalle hello numero dei computer che sono presenti cluster hello e quantità hello di memoria disponibile in tali computer.

Ad esempio, si supponga di avere una raccolta Reliable Collections in un servizio con 100 partizioni e 3 replica, con archiviati oggetti di dimensioni pari a 1 KB di media. Si supponga quindi di disporre di un cluster di 10 macchine con 16 GB di memoria per macchina. Per semplicità e toobe molto conservativa, si supponga che hello del sistema operativo e i servizi di sistema, il runtime di Service Fabric hello e i servizi utilizzano 6gb di che, se si lascia 10gb disponibili per ogni computer, o 100gb per i cluster di hello.

Tenendo presente che ciascun oggetto deve essere archiviato tre volte (una primaria e due repliche), si avrà una memoria sufficiente per circa 35 milioni di oggetti nella raccolta, con funzionamento a piena capacità. Tuttavia, è consigliabile essere resilienti toohello perdita simultaneo di un dominio di errore e un dominio di aggiornamento, che rappresenta circa 1/3 della capacità e consentirebbe di ridurre tooroughly numero hello 23 milioni.

Si noti che questo calcolo presuppone inoltre:

- Tale distribuzione hello dei dati tra partizioni hello è approssimativamente uniforme o che si sta segnalando carico metriche toohello gestione delle risorse Cluster. Per impostazione predefinita, Service Fabric bilancia il carico in base al numero di repliche. Nell'esempio precedente, che dovrà inserire 10 repliche primarie e secondarie 20 su ogni nodo nel cluster hello. Che funziona bene per un carico viene distribuito uniformemente tra le partizioni di hello. Se il carico non è in realtà, deve segnalare carico hello Gestione risorse può pack insieme le repliche più piccole e consentire più grande tooconsume repliche maggiore quantità di memoria di un singolo nodo.

- Servizio affidabile hello in questione è solo uno stato archiviazione hello cluster hello. Poiché è possibile distribuire cluster tooa a più servizi, è necessario toobe attenzione risorse hello che ognuno sarà anche necessario toorun e gestire il proprio stato.

- Tale cluster hello stesso non stia aumentando o la compattazione. Se si aggiungono altre macchine, Service Fabric verrà ribilanciare la capacità di repliche tooleverage hello aggiuntive fino a quando non numero hello di macchine supera il numero di hello di partizioni nel servizio, poiché non può estendersi a una replica di singole macchine. Al contrario, se si riducono le dimensioni di hello del cluster di hello rimuovendo le macchine, le repliche verranno compressa più rigoroso di minore capacità globale.

### <a name="how-much-data-can-i-store-in-an-actor"></a>Quanti dati è possibile archiviare in un attore?

Come per i servizi affidabili, quantità hello di dati che è possibile archiviare in un servizio actor è limitato solo dalle hello spazio totale su disco e memoria disponibile tra i nodi del cluster hello. Tuttavia, singoli soggetti risultano più efficaci quando vengono utilizzati tooencapsulate una piccola quantità di logica di business associati e stato. Come regola generale, un singolo attore dovrebbe avere uno stato misurabile in kilobyte.

## <a name="other-questions"></a>Altre domande

### <a name="how-does-service-fabric-relate-toocontainers"></a>Correlazione di toocontainers Service Fabric

I contenitori offrono un modo semplice toopackage services e le relative dipendenze in modo che possano eseguire in modo coerente in tutti gli ambienti e può funzionare in modo isolato su un singolo computer. Service Fabric offre un modo toodeploy e gestione dei servizi, tra cui [servizi che sono state incluse in un contenitore](service-fabric-containers-overview.md).

### <a name="are-you-planning-tooopen-source-service-fabric"></a>Se si sta pianificando origine tooopen Service Fabric?

Si prevede servizi affidabili di tooopen origine hello e altri framework attori affidabile su GitHub e accetteranno i progetti di toothose i contributi della community. Segui hello [blog Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/) per altri dettagli come sta annunciati.

Hello non sono attualmente alcuna fase di esecuzione di piani tooopen origine hello Service Fabric.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui concetti chiave e sulle procedure consigliate di Service Fabric](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
