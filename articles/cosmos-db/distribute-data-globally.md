---
title: dati aaaDistribute globale con Azure Cosmos DB | Documenti Microsoft
description: Informazioni sulla replica geografica a livello globale, sul failover e sul ripristino dei dati usando i database globali di Azure Cosmos DB, un servizio database multimodello distribuito a livello globale.
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>Come dati toodistribute globale con Azure Cosmos DB
Azure è ovunque, offre una copertura globale in oltre 30 aree geografiche ed è in continua espansione. Con la propria presenza in tutto il mondo, è una funzionalità di hello differenziata che Azure offre agli sviluppatori di tooits hello toobuild possibilità, distribuire e gestire facilmente le applicazioni distribuite globalmente. 

[Azure Cosmos DB](../cosmos-db/introduction.md) è il servizio di database multimodello distribuito a livello globale di Microsoft per applicazioni cruciali. DB Cosmos Azure fornisce chiavi in mano distribuzione globale, [scalabilità elastica di velocità effettiva e l'archiviazione](../cosmos-db/partition-data.md) latenze millisecondo in tutto il mondo, a una cifra a percentile 99th hello, [cinque livelli di coerenza ben definito ](consistency-levels.md)e garantisce la disponibilità elevata, tutti i backup da [SLA leader del settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB Cosmos [automaticamente i dati di indici](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) senza toodeal con la gestione dello schema e indice. Si tratta di un database multimodello che supporta modelli di dati di documenti, coppie chiave-valore, grafi e colonne. Come servizio cloud intuitivo, Azure Cosmos DB è progettato con attenzione con distribuzione multi-tenancy e globale da hello messa a terra.

**Una singola raccolta di Azure Cosmos DB partizionata e distribuita tra più aree di Azure**

![Raccolta di Azure Cosmos DB partizionata e distribuita tra tre aree](./media/distribute-data-globally/global-apps.png)

Durante lo sviluppo di Azure Cosmos DB, è emerso che non era possibile aggiungere la distribuzione globale a posteriori, perché non è una funzionalità che si può integrare su un sistema di database basato su "singolo sito". funzionalità di Hello offerte da un database distribuito a livello globale estendersi oltre che di emergenza tradizionali recovery (ripristino di emergenza geografico) offerti dai database "singolo sito". Il database basati su singolo sito che offrono la funzionalità di ripristino di emergenza con ridondanza geografica rappresentano un sottoinsieme limitato dei database distribuiti a livello globale. 

Con distribuzione globale del database di Azure Cosmos pronte all'uso, gli sviluppatori non è necessario toobuild i propri scaffolding di replica mediante l'utilizzo di un modello di Lambda hello (ad esempio, [DynamoDB AWS replica](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) nel log del database hello o da In questo "scritture double" in più aree. Non è consigliabile questi approcci, perché è Impossibile tooensure correttezza di questi approcci e fornire i contratti di servizio audio. 

In questo articolo viene illustrata una panoramica delle funzionalità di distribuzione globale di Azure Cosmos DB Viene inoltre descritto tooproviding approccio univoco del database di Azure Cosmos complete contratti di servizio. 

## <a id="EnableGlobalDistribution"></a>Abilitazione della distribuzione globale chiavi in mano
DB Cosmos Azure fornisce seguente hello funzionalità tooenable si tooeasily scrivere applicazioni su larga scala pianeta. Queste funzionalità sono disponibili tramite la risorsa del database di hello Azure Cosmos basato su provider [API REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) nonché hello portale di Azure.

### <a id="RegionalPresence"></a>Presenza in tutte le aree 
La presenza geografica di Azure è in continuo aumento, grazie alla disponibilità di un crescente numero di [nuove aree](https://azure.microsoft.com/regions/). Per impostazione predefinita, Azure Cosmos DB è disponibile in tutte le nuove aree di Azure. Ciò consente un'area geografica con l'account di database di Azure Cosmos DB tooassociate appena Azure verrà visualizzata la nuova area del hello per le aziende.

**Per impostazione predefinita, Azure Cosmos DB è disponibile in tutte le aree di Azure**

![Azure Cosmos DB è disponibile in tutte le aree di Azure](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>Associazione di un numero di aree illimitato all'account del database Azure Cosmos DB
Azure DB Cosmos consente tooassociate qualsiasi numero di aree di Azure con il database di Azure Cosmos account del database. Di fuori di restrizioni recinto (ad esempio, Cina, Germania), non sono previste limitazioni per il numero di hello delle aree che possono essere associati all'account di database di Azure Cosmos DB. Hello seguente illustrazione mostra un toospan account configurato database nelle aree di Azure 25.  

**Account del database Azure Cosmos DB di un tenant che si estende su 25 aree di Azure**

![Account del database Azure Cosmos DB che si estende su 25 aree di Azure](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>Geofencing basato su criteri
Azure DB Cosmos è progettato toohave basata su criteri recinto funzionalità. Geo-fencing è tooensure un importante componente restrizioni governance e conformità dei dati e potrebbe impedire l'associazione di un'area specifica con l'account. Esempi di recinto includono (ma non sono limitati a), dell'ambito delle aree di toohello distribuzione globale all'interno di un cloud sovrani (ad esempio Cina e Germania) o in un limite di imposizione per enti pubblici (ad esempio, Australia). criteri di Hello vengono controllati mediante hello metadati della sottoscrizione Azure.

### <a id="DynamicallyAddRegions"></a>Aggiunta e rimozione di aree in modo dinamico
Azure DB Cosmos consente tooadd (associazione) o rimuovere (annullare l'associazione) account del database tooyour aree in qualsiasi momento (vedere [figura precedente](#UnlimitedRegionsPerAccount)). Per la replica dei dati tra partizioni in parallelo, Azure Cosmos DB assicura che quando una nuova area torna online, Azure Cosmos DB sia disponibile entro 30 minuti in un punto qualsiasi in HelloWorld per backup di questo servizio too100. 

### <a id="FailoverPriorities"></a>Priorità di failover
toocontrol esatta sequenza degli internazionali failover quando si verifica un'interruzione in più paesi, Azure Cosmos DB consente le aree toovarious priorità hello tooassociate associate hello database account (vedere la seguente illustrazione hello). DB Cosmos Azure garantisce che in ordine di priorità hello specificato si verifica una sequenza di failover automatico di hello. Per altre informazioni su failover regionali, vedere [Failover a livello di area automatici per la continuità aziendale in Azure Cosmos DB](regional-failover.md).

**Un tenant di Azure Cosmos DB possibile configurare l'ordine di priorità di failover hello (riquadro a destra) per le aree associate a un account di database**

![Configurazione delle priorità di failover con Azure Cosmos DB](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>Impostazione dinamica delle aree "offline"
Azure DB Cosmos consente tootake database account offline in un'area specifica e quindi riportarla online in un secondo momento. Le aree contrassegnato come offline non attivamente partecipare alla replica e non fanno parte della sequenza di failover hello. In questo modo è hello toofreeze ultima conosciuto immagine di database appropriata in uno dei hello leggere aree prima tooyour applicazione degli aggiornamenti in sequenza potenzialmente rischiosa.

### <a id="ConsistencyLevels"></a>Più modelli di coerenza ben definiti per i database con replica a livello globale
Azure Cosmos DB espone [più livelli di coerenza ben definiti](consistency-levels.md) supportati da contratti di servizio. È possibile scegliere un modello di verifica coerenza specifiche (elenco hello disponibili delle opzioni) a seconda del carico di lavoro hello e scenari. 

### <a id="TunableConsistency"></a>Livelli di coerenza regolabili per i database con replica a livello globale
DB Cosmos Azure consente di eseguire l'override tooprogrammatically e ridurre scelta di coerenza predefinita hello nei singoli per ogni richiesta, in fase di esecuzione. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>Aree di lettura e scrittura configurabili in modo dinamico
Azure DB Cosmos consente aree hello tooconfigure (associate al database hello) per "lettura", "scrittura" o "in lettura/scrittura" aree. 

### <a id="ElasticallyScaleThroughput"></a>Scalabilità elastica della velocità effettiva tra aree di Azure
È possibile ridimensionare in modo elastico una raccolta di Azure Cosmos DB eseguendo il provisioning della velocità effettiva a livello di codice. velocità effettiva di Hello è aree hello tooall applicato hello collection viene distribuito in.

### <a id="GeoLocalReadsAndWrites"></a>Letture e scritture nell'area locale specifica
vantaggi Hello di un database distribuito a livello globale sono toooffer dati toohello accesso a bassa latenza in qualsiasi punto della HelloWorld. Azure Cosmos DB offre garanzie di bassa latenza di livello p99 per varie operazioni su database. Garantisce che tutte le letture siano indirizzati toohello area più vicina lettura locale. viene utilizzato tooserve una richiesta di lettura, l'area del quorum hello toohello locale in cui viene eseguita hello leggere; Hello vale toohello scritture. Un'operazione di scrittura viene riconosciuto solo dopo che la maggior parte delle repliche commit in modo durevole scrittura hello in locale, ma non viene gestita in remoto repliche tooacknowledge hello scritture. Inserire in modo diverso, il protocollo di replica hello di Azure Cosmos DB opera presupposto hello che hello in lettura e scrittura quorum sono sempre locali toohello lettura e scrivere aree, rispettivamente, nella quale richiesta hello viene eseguita.

### <a id="ManualFailover"></a>Avvio manuale del failover a livello di area
DB Cosmos Azure consente il failover hello tootrigger di hello toovalidate di hello database account *terminare tooend* proprietà disponibilità di un'intera applicazione hello (oltre a database hello). Poiché entrambi hello sicurezza e proprietà liveness di elezione di rilevamento e la linea guida errore hello è garantita, Azure Cosmos DB garantisce *perdita di dati zero* per un'operazione di failover manuale avviato dal tenant.

### <a id="AutomaticFailover"></a>Failover automatico
Azure Cosmos DB supporta il failover automatico in caso di una o più interruzioni di servizio a livello di area. Durante un failover a livello di area, Azure Cosmos DB mantiene i contratti di servizio per latenza di lettura, disponibilità di tempo di attività, coerenza e velocità effettiva. DB Cosmos Azure fornisce un limite superiore alla durata hello di toocomplete di operazione un failover automatico. Si tratta di finestra hello della potenziale perdita di dati durante l'interruzione dell'alimentazione locale hello.

### <a id="GranularFailover"></a>Progettato per varie granularità di failover
Attualmente hello automatica e le funzionalità di failover manuale sono esposti con granularità hello dell'account database hello. Si noti che internamente Azure Cosmos DB sono progettato toooffer *automatica* failover a livello di granularità di un database, raccolta o anche una partizione (di una raccolta di proprietario di un intervallo di chiavi). 

### <a id="MultiHomingAPIs"></a>API multihosting in Azure Cosmos DB
Azure DB Cosmos consente toointeract con database hello utilizzando logico (indipendente dall'area) o fisico endpoint (specifico dell'area). L'utilizzo di endpoint logico assicura che un'applicazione hello possibile in modo trasparente multihomed in caso di failover. Hello endpoint fisico, quest'ultimo, fornire un controllo accurato toohello applicazione tooredirect legge e scrive toospecific aree.

È possibile trovare informazioni sulla modalità di lettura delle preferenze per hello tooconfigure [API DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md), [API Graph](../cosmos-db/tutorial-global-distribution-graph.md), [tabella API](../cosmos-db/tutorial-global-distribution-table.md), e [MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)nelle rispettive collegato articoli.

### <a id="TransparentSchemaMigration"></a>Migrazione di indici e di schemi del database trasparente e coerente 
Azure Cosmos DB è completamente [indipendente dallo schema](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). progettazione di univoco Hello del relativo motore di database consente di tooautomatically e tutti i dati di hello inserisce senza richiedere gli indici secondari da parte dell'utente o schema di indice in modo sincrono. In questo modo si tooiterate l'applicazione distribuita a livello globale rapidamente senza doversi preoccupare di migrazione dello schema e indice del database o il coordinamento delle implementazioni multifase applicazione delle modifiche dello schema. DB Cosmos Azure garantisce che tutti i criteri di tooindexing le modifiche apportati in modo esplicito dall'utente non risultato nella riduzione delle prestazioni o disponibilità.  

### <a id="ComprehensiveSLAs"></a>Contratti di servizio completi (oltre la sola disponibilità elevata)
Come servizio di database distribuita a livello globale, Azure Cosmos DB offre un contratto di servizio ben definito per **perdita di dati**, **disponibilità**, **latenza P99**, **velocità effettiva**  e **coerenza** per database hello nel suo complesso, indipendentemente dal numero di hello delle regioni associati hello database.  

## <a id="LatencyGuarantees"></a>Garanzie di latenza
Hello dei principali vantaggi offerti un servizio di database distribuiti in modo globale come Azure Cosmos DB sono toooffer dati tooyour accesso a bassa latenza in qualsiasi punto della HelloWorld. Azure Cosmos DB offre garanzie di bassa latenza di livello p99 per varie operazioni su database. protocollo di replica Hello che utilizza Azure Cosmos DB assicura che hello operazioni di database (in teoria, legge e scrive) vengono sempre eseguiti in toothat locale di area hello del client hello. latenza Hello per che SLA di Azure Cosmos DB include P99 letture, scritture indicizzate (modo sincrono) sia una query per vari formati di richiesta e risposta. garanzie di latenza Hello per le scritture includono commit quorum maggioranza dei durevoli nel data center locale hello.

### <a id="LatencyAndConsistency"></a>Relazione tra latenza e coerenza 
Per una servizio distribuito a livello globale toooffer coerenza assoluta in un'installazione distribuita a livello globale, è necessario toosynchronously hello replicare scritture sincrone o eseguire operazioni di lettura tra più aree: velocità di hello di chiaro e hello stabiliscono l'affidabilità di rete WAN la coerenza assoluta comporta latenze elevate e la bassa disponibilità delle operazioni di database. Di conseguenza, in ordine toooffer garantito bassa latenza P99 e disponibilità 99.99, servizio hello necessario impiegare la replica asincrona. Questo a sua volta richiede che il servizio hello deve offrire anche [oggetti scelti coerenza ben definiti, relaxed](consistency-levels.md) : meno sicuro (toooffer bassa latenza e disponibilità garanzie) e idealmente più avanzato rispetto a (coerenza "finale" toooffer un modello di programmazione intuitivo).

DB Cosmos Azure assicura che un'operazione di lettura non è necessario toocontact repliche tra più aree toodeliver hello specifico livello garanzia di coerenza. Analogamente, assicura che un'operazione di scrittura non restare bloccata mentre hello dati vengono replicati tra tutte le aree di hello (ad esempio operazioni di scrittura sono in modo asincrono replicate tra le aree). Per gli account del database in più aree sono disponibili più livelli di coerenza media. 

### <a id="LatencyAndAvailability"></a>Relazione tra latenza e disponibilità 
La latenza e disponibilità sono hello due lati hello moneta stesso. Si parla di latenza dell'operazione di hello stabile e disponibilità, in faccia hello di errori. Dal punto di vista dell'applicazione hello, non è distinguibile da un database che non è disponibile un'operazione di database in esecuzione lenta. 

una latenza elevata toodistinguish dalla mancata disponibilità, Azure Cosmos DB fornisce un limite massimo assoluto sulla latenza di varie operazioni di database. Se l'operazione sul database hello richiede più tempo toocomplete limite superiore di hello, Azure Cosmos DB restituisce un errore di timeout. Hello SLA sulla disponibilità di Azure Cosmos DB garantisce che i timeout hello vengono conteggiate rispetto a disponibilità hello contratto di servizio. 

### <a id="LatencyAndThroughput"></a>Relazione tra latenza e velocità effettiva
Con Azure Cosmos DB non è necessario scegliere tra latenza e velocità effettiva. Rispetta hello contratto di servizio per entrambi una latenza P99 e offrire velocità effettiva di hello che è stato effettuato il provisioning. 

## <a id="ConsistencyGuarantees"></a>Garanzie di coerenza
Durante la hello [modello coerenza assoluta](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) hello oro standard di programmabilità, si tratta di prezzo ripida hello ad alta latenza (nello stato stazionario) e perdita di disponibilità (in faccia hello di errori). 

DB Cosmos Azure offre un tooreason tooyou modello programmazione ben definito sulla coerenza dei dati replicati. Ordinare tooenable si toobuild multihomed applicazioni, i modelli di coerenza hello esposti da Azure Cosmos DB sono indipendenti dal area toobe progettato e non dipendono area hello da dove vengono servite hello letture e scritture. 

Contratto di servizio di Azure Cosmos DB coerenza garantisce che 100% delle richieste di lettura soddisfare la garanzia di coerenza hello per il livello di coerenza hello richiesto dall'utente (hello coerenza livello predefinito nell'account di database hello o valore hello sottoposto a override in una richiesta di hello ). Una richiesta di lettura viene considerata toohave soddisfatti hello coerenza contratto di servizio, se vengono soddisfatte tutte le garanzie di coerenza hello associate a livello di coerenza hello. Hello nella tabella seguente vengono acquisiti garanzie di coerenza hello che corrispondono a livelli di coerenza toospecific offerti da Azure Cosmos DB.

**Garanzie di coerenza associate ai livelli di coerenza specifici in Azure Cosmos DB** 

<table>
    <tr>
        <td><strong>Livello di coerenza</strong></td>
        <td><strong>Caratteristiche di coerenza</strong></td>
        <td><strong>Contratto di servizio</strong></td>
    </tr>
    <tr>
        <td rowspan="3">sessione</td>
        <td>Lettura delle proprie scritture</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Lettura monotonica</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefisso coerente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">Obsolescenza associata</td>
        <td>Lettura monotonica (all'interno di un'area)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefisso coerente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Decadimento ristretto &lt; K,T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefisso coerente</td>
        <td>Prefisso coerente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Assoluta</td>
        <td>Linearizzabile</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>Relazione tra coerenza e disponibilità
Hello [risultato impossibilità](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) di hello [teorema di CAP](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) dimostra che non è infatti possibile hello sistema tooremain disponibili e la coerenza di linearizable offerta in faccia hello di errori. il servizio di database Hello deve scegliere toobe CP o Asia - Pacifico sistemi CP evitare disponibilità a favore di coerenza linearizable mentre i sistemi di hello PA evitare [coerenza linearizable](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) a favore di disponibilità. Azure DB Cosmos non viola mai hello richiesto a livello di coerenza, rendendo formalmente un sistema CP. Tuttavia, in pratica la coerenza non è una proposta di tutto o niente, sono disponibili più modelli di coerenza ben definiti lungo spettro di hello la coerenza tra la coerenza eventuale e linearizable. Nel database Cosmos di Azure, si è tentato tooidentify numerosi hello ridotti i modelli di coerenza con un modello di programmazione intuitivo e applicabilità mondo reale. Azure DB Cosmos passa compromessi coerenza disponibilità hello offrendo 99.99 contratti di servizio di disponibilità insieme a [più ridotti i livelli di coerenza ancora ben definito](consistency-levels.md). 

### <a id="ConsistencyAndAvailability"></a>Relazione tra coerenza e latenza
Il Prof. Daniel Abadi ha proposto una variante più completa del teorema CAP denominata [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf), che tiene in considerazione i compromessi tra latenza e coerenza in stato stabile. Indicante che lo stato stabile, il sistema di database hello è necessario scegliere tra la coerenza e latenza. Con più modelli di tipo relaxed coerenza (supportati da replica asincrona e locale lettura, scrittura quorum), Azure Cosmos DB garantisce che tutte le letture e scritture siano toohello locale lettura e scrivono aree rispettivamente.  In questo modo Azure Cosmos toooffer bassa latenza garantisce all'interno di area hello per livelli di coerenza hello.  

### <a id="ConsistencyAndThroughput"></a>Relazione tra coerenza e velocità effettiva
Poiché l'implementazione di hello di un modello di verifica coerenza specifiche dipende dalla scelta hello di un [tipo di quorum](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), velocità effettiva di hello varia anche in base alla scelta di hello di verifica di coerenza. Ad esempio, in Azure Cosmos DB hello velocità effettiva con fortemente coerente letture è toothat circa la metà di letture alla fine coerente. 
 
**Relazione della capacità di lettura per un livello di coerenza specifico in Azure Cosmos DB** 

![Relazione tra coerenza e velocità effettiva](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>Garanzie di velocità effettiva 
Azure DB Cosmos consente tooscale velocità effettiva (nonché, archiviazione), elastico in aree geografiche diverse in base alla richiesta di hello. 

**Una singola raccolta di Azure Cosmos DB partizionata (su tre partizioni) e quindi distribuita su tre aree di Azure**

![Raccolte di Azure Cosmos DB partizionate e distribuite](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Una raccolta di Azure Cosmos DB viene distribuita usando due dimensioni, all'interno di un'area e in più aree. Ecco come: 

* All'interno di una singola area, la scalabilità di una raccolta di Azure Cosmos DB viene garantita tramite l'aumento di partizioni di risorse. Ogni partizione di risorsa gestisce un set di chiavi e offre coerenza assoluta e disponibilità elevata grazie alla replica della macchina a stati tra un set di repliche. DB Cosmos Azure è un sistema di resource governati completamente in una partizione delle risorse è responsabile per il recapito relativa condivisione di velocità effettiva per budget hello di tooit risorse di sistema. Hello il ridimensionamento di una raccolta di Azure Cosmos DB è completamente trasparente: Azure Cosmos DB gestisce le partizioni di risorsa hello e suddivide e di unirla in base alle esigenze. 
* Ognuna delle partizioni di risorsa hello viene quindi distribuito in più aree. Le partizioni di risorse proprietario hello stesso set di chiavi tra set di partizioni diverse aree form (vedere [figura precedente](#ThroughputGuarantees)).  Partizioni di risorse all'interno di un set di partizioni vengono coordinate tramite la replica nello stato macchina tra hello più aree. In base al livello di coerenza hello configurato, le partizioni di hello risorse all'interno di un set di partizioni vengono configurate in modo dinamico tramite diverse topologie (ad esempio, a stella, margherita, struttura ad albero e così via.). 

Grazie a gestione delle partizioni ad alte, il bilanciamento del carico e la governance delle risorse strict, Azure Cosmos DB consente velocità effettiva di scala tooelastically tra più aree di Azure per una raccolta di Azure Cosmos DB. Velocità effettiva la modifica in una raccolta è un'operazione di runtime nel database di Azure Cosmos - come con altre operazioni di database che DB Cosmos Azure garantisce hello un assoluto limite superiore sulla latenza per la velocità effettiva hello toochange di richiesta. Ad esempio, hello seguente illustrazione mostra insieme a un cliente con provisioning elastico velocità effettiva (compreso fra 1 milione a 10M - richieste/sec in due aree) in base alle esigenze di hello.
 
**Raccolta di un cliente con provisioning elastico della velocità effettiva (compresa tra 1 milione e 10 milioni di richieste al secondo)**

![Provisioning elastico della velocità effettiva di Azure Cosmos DB](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>Relazione tra velocità effettiva e coerenza 
Analoga alla [Relazione tra coerenza e velocità effettiva](#ConsistencyAndThroughput).

### <a id="ThroughputAndAvailability"></a>Relazione tra velocità effettiva e disponibilità
Azure DB Cosmos toomaintain la disponibilità quando continua hello modifiche velocità effettiva toohello. DB Cosmos Azure gestisce in modo trasparente le partizioni (ad esempio split, merge, operazioni di clonazione) e assicura che le operazioni di hello non influire negativamente sulle prestazioni o disponibilità, mentre un'applicazione hello elastico aumenta o diminuisce la velocità effettiva. 

## <a id="AvailabilityGuarantees"></a>Garanzie di disponibilità
DB Cosmos Azure offre una disponibilità 99,99% del contratto di servizio per ognuno dei hello operazioni piano dati e il controllo. Come descritto in precedenza, le garanzie di disponibilità di Azure Cosmos DB includono un limite superiore assoluto di latenza per ogni operazione del piano dati e controllo. le garanzie di disponibilità Hello sono assenza e non cambia con il numero di hello delle aree geografica distanza tra le aree. Le garanzie di disponibilità si applicano sia al failover manuale sia a quello automatico. DB Cosmos Azure offre API multihosting trasparente che garantiscono che l'applicazione può operare su endpoint logici e instradare in modo trasparente hello richieste toohello nuova area in caso di failover. Inserire in modo diverso, l'applicazione non è necessario toobe ridistribuzione in caso di failover regionale e disponibilità hello contratti di servizio vengono mantenute.

### <a id="AvailabilityAndConsistency"></a>Relazione tra disponibilità e coerenza, latenza e velocità effettiva
La relazione tra disponibilità e coerenza, latenza e velocità effettiva è descritta nelle sezioni [Relazione tra coerenza e disponibilità](#ConsistencyAndAvailability), [Relazione tra latenza e disponibilità](#LatencyAndAvailability) e [Relazione tra velocità effettiva e disponibilità](#ThroughputAndAvailability). 

## <a id="GuaranteesAgainstDataLoss"></a>Garanzie e comportamento del sistema per la "perdita di dati"
In Azure Cosmos DB la disponibilità elevata di ogni partizione (di una raccolta) è determinata da un numero di repliche distribuite tra un minimo di 10 e un massimo di 20 domini di errore. Tutte le scritture sono in modo sincrono e durevole commit da un quorum maggioranza delle repliche prima che vengano riconosciuti toohello client. La replica asincrona è coordinata tra partizioni distribuite in più aree. Azure Cosmos DB garantisce che non si verifichi alcuna perdita di dati per un failover manuale avviato dal tenant. Durante il failover automatico, Azure Cosmos DB garantisce un limite superiore di hello configurato delimitata intervallo obsolescenza nella finestra di perdita di dati hello come parte del relativo contratto di servizio.

## <a id="CustomerFacingSLAMetrics"></a>Metriche del contratto di servizio per il cliente
Azure Cosmos DB espone in modo trasparente le metriche di velocità effettiva, latenza, coerenza e la disponibilità di hello. Queste metriche sono accessibili tramite il portale di Azure (vedere la figura seguente) hello e livello di codice. È anche possibile impostare avvisi per varie soglie usando Azure Application Insights.
 
**Le metriche di disponibilità, latenza, velocità effettiva e la coerenza sono disponibili in modo trasparente tooeach tenant**

![Metriche del contratto di servizio di Azure Cosmos DB visibili per il cliente](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>Passaggi successivi
* replica globale tooimplement dell'account di Azure Cosmos DB usando hello Azure portale, vedere [come replica di database globale Azure Cosmos DB tooperform tramite hello Azure portal](tutorial-global-distribution-documentdb.md).
* toolearn sulla tooimplement architetture multimaster con Azure Cosmos DB, vedere [architetture database multimaster con Azure Cosmos DB](multi-region-writers.md).
* toolearn ulteriori informazioni sugli come failover automatico e manuale di lavoro in Azure Cosmos DB, vedere [internazionali i failover nel database di Azure Cosmos](regional-failover.md).

## <a id="References"></a>Riferimenti
1. Eric Brewer. [Towards Robust Distributed Systems](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) (Verso sistemi distribuiti affidabili)
2. Eric Brewer. [Estremità dodici anni in un secondo momento, il cui hello regole sono state modificate](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert, Lynch. - [Brewer&#39;s Conjecture and Feasibility of Consistent, Available, Partition Tolerant Web Services](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) (Ipotesi e fattibilità dei servizi Web con coerenza, disponibilità e tolleranza di errore)
4. Daniel Abadi. [Consistency Tradeoffs in Modern Distributed Database Systems Design](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf) (Compromessi sulla coerenza nella progettazione di sistemi di database distribuiti moderni)
5. Martin Kleppmann. [Please stop calling databases CP or AP](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html) (Non definire più i database come CP (coerenza e tolleranza di partizione) o AP (disponibilità e tolleranza di partizione))
6. Peter Bailis et al. [Probabilistic Bounded Staleness (PBS) for Practical Partial Quorums](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf) (Decadimento ristretto probabilistico per quorum parziali pratici)
7. Naor e Wool. [Load, Capacity and Availability in Quorum Systems](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf) (Carico, capacità e disponibilità nei sistemi di quorum)
8. Herlihy e Wing. [Lineralizability: A correctness condition for concurrent objects](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) (Linearizzabilità: una condizione di correttezza per gli oggetti simultanei)
9. [Contratto di servizio Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
