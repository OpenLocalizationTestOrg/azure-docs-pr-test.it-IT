---
title: Guida alla progettazione di archiviazione tabella aaaAzure | Documenti Microsoft
description: Progettare tabelle scalabili ed efficienti in Archiviazione tabelle di Azure
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: bbac5e83fe994c1ba1408dd43367fbcfca6a2148
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Guida alla progettazione della tabella di archiviazione di Azure: Progettazione scalabile e Tabelle ad alte prestazioni 
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign scalabile e ad alte prestazioni tabelle è necessario considerare diversi fattori, ad esempio prestazioni, scalabilità e costi. Se è stato creato in precedenza gli schemi per i database relazionali, queste considerazioni sarà tooyou familiare, ma sono presenti alcune somiglianze tra modello di archiviazione del servizio tabelle di Azure hello e i modelli relazionali, esistono anche molti importanti differenze. In genere queste differenze determinano inevitabilmente un toovery diverse progettazioni che potrebbero essere poco plausibile o errato toosomeone familiarità con i database relazionali, ma cui effettuare una scelta appropriata se si sta progettando per un archivio chiave-valore NoSQL, ad esempio hello del servizio tabelle di Azure. Molte delle differenze di progettazione del rifletterà hello fatto che il servizio di tabella hello toosupport progettato le applicazioni a livello di cloud che possono contenere anche su miliardi di entità (righe nella terminologia dei database relazionali) dei dati o per i set di dati che devono essere supportati molto elevato volumi di transazioni: pertanto, è necessario toothink in modo diverso sulla modalità di archiviazione dei dati e comprendere il funzionamento di hello del servizio tabelle. Archivio dati NoSQL ben progettato è possibile abilitare tooscale la soluzione maggiore (e a un costo inferiore) rispetto a una soluzione che utilizza un database relazionale. Questa guida illustra proprio questi argomenti.  

## <a name="about-hello-azure-table-service"></a>Su hello del servizio tabelle di Azure
In questa sezione illustra alcune hello le funzionalità principali di servizio tabelle hello che sono particolarmente rilevanti toodesigning per prestazioni e scalabilità. Se si tooAzure nuova archiviazione e del servizio tabelle hello, leggere prima [tooMicrosoft introduzione di archiviazione di Azure](storage-introduction.md) e [Introduzione all'archiviazione tabelle di Azure usando .NET](storage-dotnet-how-to-use-tables.md) prima di leggere il resto di hello del articolo. Sebbene hello di questa guida è attiva hello del servizio tabelle, che include alcuni discussione di hello coda di Azure e i servizi Blob e come è possibile utilizzare insieme hello del servizio tabelle in una soluzione.  

Novità del servizio tabelle hello? Come previsto dal nome hello, hello del servizio tabelle utilizza i dati di toostore un formato tabulare. Nella terminologia standard hello, ogni riga della tabella hello rappresenta un'entità e archivio colonne hello hello varie proprietà di tale entità. Ogni entità dispone di una coppia di chiavi toouniquely identificarlo e una colonna timestamp che hello del servizio tabelle utilizza tootrack dell'ultimo aggiornamento entità hello (ciò avviene automaticamente e non è possibile sovrascrivere manualmente hello timestamp con un valore arbitrario). Hello del servizio tabelle utilizza questo timestamp ultima modifica (LMT) toomanage la concorrenza ottimistica.  

> [!NOTE]
> operazioni API REST del servizio tabelle Hello inoltre restituiranno un **ETag** valore da cui deriva il timestamp di ultima modifica di hello (LMT). In questo documento si utilizzerà hello termini ETag e LMT indifferentemente perché fanno riferimento toohello stessi dati sottostanti.  
> 
> 

Hello riportato di seguito toostore di progettazione una semplice tabella entità dipendente e reparto. Molti degli esempi di hello illustrati più avanti in questa guida si basano su questo progetto semplice.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td>Marketing</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Don</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Jun</td>
<td>Cao</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>Department</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Marketing</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Sales</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Ken</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


Finora, questa è molto simile tooa tabella in un database relazionale con le differenze principali di hello viene hello colonne obbligatorie e hello toostore possibilità entità più tipi in hello stessa tabella. Inoltre, ogni hello proprietà definite dall'utente, ad esempio **FirstName** o **Age** ha un tipo di dati, ad esempio integer o string, solo come una colonna in un database relazionale. Anche se a differenza di un database relazionale, hello significa servizio di tabella che non deve avere una proprietà di natura senza schema hello hello stesso tipo di dati per ogni entità. tipi di dati complessi toostore in una singola proprietà, è necessario utilizzare un formato serializzato come JSON o XML. Per ulteriori informazioni sui tipi di dati di hello tabella servizio supportato, ad esempio, gli intervalli di date supportato, le regole di denominazione e vincoli relativi alle dimensioni, vedere [hello comprensione modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Come si vedrà, la scelta di **PartitionKey** e **RowKey** è fondamentale toogood progettazione della tabella. Ogni entità archiviata in una tabella deve avere una combinazione univoca di **PartitionKey** e **RowKey**. Come con chiavi in una tabella di database relazionale, hello **PartitionKey** e **RowKey** valori indicizzati toocreate un indice cluster che consente le ricerche veloci; hello del servizio tabelle, tuttavia, non viene creato alcun gli indici secondari, pertanto questi sono hello solo due indicizzati proprietà (alcuni dei modelli di hello descritti di seguito mostra come è possibile aggirare questa limitazione apparente).  

Una tabella è costituita da una o più partizioni, e come si vedrà, molte di hello progettazione decisioni verrà intorno alla scelta di un oggetto utilizzabile **PartitionKey** e **RowKey** toooptimize la soluzione. Una soluzione può essere costituita da una sola tabella contenente tutte le entità organizzate in partizioni, ma normalmente una soluzione comprende più tabelle. Tabelle consentono di toologically organizzare le entità e consentono di gestire dati di accesso toohello mediante access control list, è possibile eliminare un'intera tabella utilizzando una singola operazione di archiviazione.  

### <a name="table-partitions"></a>Partizioni della tabella
nome dell'account Hello, il nome di tabella e **PartitionKey** identificano insieme partizione hello all'interno del servizio di archiviazione hello in cui il servizio di tabella hello archivia entità hello. Oltre a far parte di hello allo schema per le entità di indirizzamento, le partizioni definiscono un ambito per le transazioni (vedere [gruppi di entità](#entity-group-transactions) sotto) e form di base hello di scalabilità di servizio tabelle hello. Per altre informazioni sulle partizioni, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md).  

Nel servizio tabelle hello, un singolo nodo servizi uno o più partizioni di completare e hello servizio scale dal bilanciamento del carico in modo dinamico le partizioni tra i nodi. Se un nodo è in condizioni di carico, è possibile del servizio tabelle hello *dividere* intervallo hello delle partizioni elaborate dal nodo in nodi diversi; quando diminuisce il traffico, è possibile servizio hello *unione* partizione hello compreso tra nodi non interattiva in un singolo nodo.  

Per ulteriori informazioni su hello servizio tabelle dettagli interni di hello e in particolare come servizio hello gestisce le partizioni, vedere il documento hello [archiviazione di Microsoft Azure: A elevata disponibilità servizio di archiviazione Cloud con verifica coerenza sicuro](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>Transazioni dei gruppi di entità
In hello del servizio tabelle, gruppi di entità (EGTs) sono un meccanismo solo integrato hello per l'esecuzione di aggiornamenti atomici in più entità. EGTs sono anche cui tooas *batch transazioni* nella parte della documentazione. EGTs può essere utilizzato solo per le entità archiviate in hello stessa partizione (condivisione hello stessa chiave di partizione in una determinata tabella), pertanto ogni volta che è necessario un comportamento transazionale atomico in più entità, è necessario tooensure le entità presenti hello stessa partizione. Questo è spesso un motivo per mantenere più tipi di entità in hello stessa tabella (e di partizione) e non utilizzare più tabelle per i tipi di entità diversa. Una sola EGT può agire al massimo su 100 entità.  Se si inviano più EGTs simultanee per l'elaborazione è importante tooensure tali EGTs non funzionano per le entità che sono comuni tra EGTs come in caso contrario, l'elaborazione può essere ritardato.

EGTs introduce inoltre un compromesso potenziali per tooevaluate nella progettazione: utilizzo di più partizioni aumenterà scalabilità hello dell'applicazione in quanto Azure offre maggiori opportunità per il bilanciamento del carico delle richieste tra i nodi, ma ciò potrebbe limitare hello possibilità di transazioni atomiche applicazione tooperform e mantenere la coerenza assoluta per i dati. Inoltre, vi sono obiettivi di scalabilità specifici a livello di hello di una partizione che potrebbe limitare la velocità effettiva hello delle transazioni, è probabile che per un singolo nodo: per ulteriori informazioni sulle destinazioni di scalabilità hello per gli account di archiviazione di Azure e tabella hello servizio, vedere [Azure obiettivi di scalabilità e prestazioni](storage-scalability-targets.md). Nelle sezioni successive di questa guida discutere sulle diverse strategie che consentono di gestire i compromessi come e viene illustrato il modo migliore toochoose la chiave di partizione in base ai requisiti specifici di hello dell'applicazione client di progettazione.  

### <a name="capacity-considerations"></a>Considerazioni sulla capacità
Hello nella tabella seguente sono incluse alcune delle toobe di valori di chiave hello conoscere quando si progetta una soluzione di servizio di tabella:  

| Capacità totale di un account di archiviazione di Azure | 500 TB |
| --- | --- |
| Numero di tabelle in un account di archiviazione di Azure |Limitato solo dalla capacità di hello hello dell'account di archiviazione |
| Numero di partizioni in una tabella |Limitato solo dalla capacità di hello hello dell'account di archiviazione |
| Numero di entità in una partizione |Limitato solo dalla capacità di hello hello dell'account di archiviazione |
| Dimensioni di una singola entità |Backup MB too1 con un massimo di 255 proprietà (inclusi hello **PartitionKey**, **RowKey**, e **Timestamp**) |
| Dimensioni di hello **PartitionKey** |Una stringa di dimensioni too1 KB |
| Dimensioni di hello **RowKey** |Una stringa di dimensioni too1 KB |
| Dimensioni di una transazione di gruppi di entità |Una transazione può includere al massimo 100 entità e payload hello deve essere minore di 4 MB. Una transazione EGT può aggiornare una sola entità per volta. |

Per ulteriori informazioni, vedere [hello comprensione modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx).  

### <a name="cost-considerations"></a>Considerazioni sul costo
Archiviazione tabelle è relativamente poco costosa, ma è consigliabile includere le stime dei costi per la quantità di informazioni sull'utilizzo e hello entrambe le capacità di transazioni come parte di una valutazione di una soluzione che utilizza il servizio tabella hello. Tuttavia, in molti scenari l'archiviazione dati denormalizzati o duplicati in hello tooimprove ordine prestazioni o la scalabilità della soluzione è tootake un approccio valido. Per altre informazioni sui prezzi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/).  

## <a name="guidelines-for-table-design"></a>Linee guida per la progettazione di tabelle
Questi elenchi riepilogano alcune linee guida fondamentali di hello che è necessario tenere presenti quando si progettano le tabelle e verrà risolverli in modo più dettagliato più avanti in questa Guida. Queste linee guida sono molto diverse da linee guida hello in genere è necessario seguire per la progettazione di database relazionale.  

La progettazione del toobe di soluzioni di servizio tabella *leggere* efficiente:

* ***Progettazione per le query nelle applicazioni con intensa attività di lettura.*** Quando si progettano le tabelle, considerare le query di hello (soprattutto hello la latenza quelle riservate) che verrà eseguita prima di pianificare la modalità si aggiornerà le entità. Ciò comporta in genere una soluzione efficiente e ad alte prestazioni.  
* ***Specificare PartitionKey e RowKey nelle query.*** *Scegliere query* , ad esempio si tratta di query sul servizio tabella più efficiente hello.  
* ***Prendere in considerazione l'archiviazione di copie duplicate delle entità.*** Archiviazione tabelle è economica opportuno considerare l'archiviazione hello stessa entità più volte (con chiavi diverse) tooenable query più efficienti.  
* ***Considerare la denormalizzazione dei dati.*** L’archiviazione delle tabelle è economica, dunque è opportuno considerare la denormalizzazione dei dati. Ad esempio, archiviare le entità di riepilogo in modo che le query sui dati aggregati sufficiente tooaccess una singola entità.  
* ***Usare valori chiave composti.*** sono Hello solo le chiavi sono **PartitionKey** e **RowKey**. Ad esempio, utilizzare i valori di chiave composta tooenable accesso con chiave alternativo percorsi tooentities.  
* ***Usare la proiezione di query.*** È possibile ridurre la quantità hello di dati che vengono trasferite in rete hello utilizzando le query che selezionano solo i campi di hello che è necessario.  

La progettazione del toobe di soluzioni di servizio tabella *scrivere* efficiente:  

* ***Non creare partizioni critiche.*** Scegliere le chiavi che consentono di toospread le richieste tra più partizioni in qualsiasi momento.  
* ***Evitare picchi di traffico.*** Smooth traffico hello in un periodo di tempo ragionevole ed evitare picchi di traffico.
* ***Non creare necessariamente una tabella separata per ogni tipo di entità.*** Quando si richiedono transazioni atomiche tra tipi di entità, è possibile archiviare più di questi tipi di entità nella stessa partizione hello hello stessa tabella.
* ***Prendere in considerazione la velocità effettiva massima hello che è necessario ottenere.*** È necessario essere a conoscenza di obiettivi di scalabilità hello per hello del servizio tabelle e garantire che il progetto non è tooexceed li.  

Questa guida contiene esempi in cui vengono messi in pratica tutti questi principi.  

## <a name="design-for-querying"></a>Progettazione per le query
Soluzioni di servizio di tabella possono essere letti con utilizzo intensivo, con un utilizzo elevato di scrittura o una combinazione di due hello. In questa sezione è incentrata sulla toobear operazioni hello in considerazione quando si progetta il toosupport servizio tabella operazioni di lettura in modo efficiente. Una progettazione che supporta in modo efficiente le operazioni di lettura è in genere efficiente anche nelle operazioni di scrittura. Tuttavia, esistono ulteriori considerazioni toobear presente quando progettazione toosupport scrittura, illustrato nella sezione successiva hello, [progettazione per la modifica dei dati](#design-for-data-modification).

Un buon punto di partenza per la progettazione del tooenable di soluzioni di servizio tabella tooread dati in modo efficiente sono tooask "quali sono le query verranno i dati dell'applicazione necessario tooexecute tooretrieve hello che necessari dal servizio tabelle hello?"  

> [!NOTE]
> Con hello del servizio tabelle, è importante tooget hello progettazione corretto inizio perché è difficile e costoso toochange posticipato. Ad esempio, in un database relazionale è spesso tooaddress possibili problemi di prestazioni semplicemente aggiungendo indici database esistente tooan: non è un'opzione con hello del servizio tabelle.  
> 
> 

Questa sezione vengono illustrati i problemi di chiave hello che è necessario risolvere quando si progettano le tabelle per l'esecuzione di query. Hello argomenti trattati in questa sezione includono:

* [Come la scelta di PartitionKey e RowKey compromette le prestazioni delle query](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [Scelta di un valore PartitionKey appropriato](#choosing-an-appropriate-partitionkey)
* [Ottimizzazione delle query per hello del servizio tabelle](#optimizing-queries-for-the-table-service)
* [Ordinamento dati nel servizio tabelle hello](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>Come la scelta di PartitionKey e RowKey compromette le prestazioni delle query
Hello esempi seguenti presuppongono servizio tabella hello è l'archiviazione delle entità employee con hello seguente struttura (la maggior parte degli esempi di hello omettere hello **Timestamp** proprietà per maggiore chiarezza):  

| *Nome colonna* | *Tipo di dati* |
| --- | --- |
| **PartitionKey** (nome del reparto) |String |
| **RowKey** (ID dipendente) |String |
| **FirstName** |String |
| **LastName** |String |
| **Age** |Integer |
| **EmailAddress** |String |

Hello precedente sezione [Panoramica del servizio tabelle di Azure](#overview) descrive alcune delle hello le funzionalità principali di hello del servizio tabelle di Azure che influiscono direttamente sulla progettazione per la query. In tal modo hello seguenti linee guida generali per la progettazione di query sul servizio di tabella. Si noti che la sintassi di filtro hello utilizzata negli esempi di hello riportato di seguito è da hello tabella API REST del servizio, per ulteriori informazioni, vedere [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

* Oggetto ***punto Query*** è hello toouse di ricerca più efficiente ed è consigliata toobe usati per ricerche di volumi elevati o ricerche che richiedono la latenza più bassa. Tale query può utilizzare in modo molto efficiente hello indici toolocate una singola entità specificando entrambi hello **PartitionKey** e **RowKey** valori. Ad esempio, $filter=(PartitionKey eq 'Sales') e (RowKey eq '2')  
* In secondo luogo è un ***Query di intervallo*** che utilizza hello **PartitionKey** e i filtri su un intervallo di **RowKey** valori tooreturn più di un'entità. Hello **PartitionKey** valore identifica una partizione specifica e hello **RowKey** valori identificano un subset di entità hello in tale partizione. Ad esempio, $filter=PartitionKey eq 'Sales' e RowKey ge 'S' e RowKey lt 'T'  
* Terzo migliore è un ***partizione analisi*** che utilizza hello **PartitionKey** e filtri in un'altra proprietà non chiave e che possono restituire più di un'entità. Hello **PartitionKey** valore identifica una partizione specifica e i valori delle proprietà di hello select per un subset di entità hello in tale partizione. Ad esempio: $filter=PartitionKey eq 'Sales' e LastName eq 'Smith'  
* Oggetto ***Table Scan*** non include hello **PartitionKey** ed è molto efficiente perché viene eseguita la ricerca di tutte le partizioni di hello che costituiscono la tabella a sua volta per tutte le entità corrispondenti. Verrà eseguita una scansione di tabella indipendentemente dal fatto che il filtro Usa hello **RowKey**. Ad esempio: $filter = LastName eq 'Jones'  
* Le query che restituiscono più entità le ordinano in base a **PartitionKey** e **RowKey**. entità hello ricorrere tooavoid client hello, scegliere un **RowKey** che definisce hello più comuni di ordinamento.  

Si noti che l'utilizzo un "**o**" toospecify un filtro basato su **RowKey** valori dei risultati in una scansione di partizione e non viene considerato come una query di intervallo. Pertanto, è consigliabile evitare query che utilizzano filtri ad esempio: $filter = PartitionKey eq "Sales" e (RowKey '121' o RowKey eq '322')  

Per esempi di codice lato client che usano query efficienti tooexecute di hello libreria Client di archiviazione, vedere:  

* [Esegue una query di punto utilizzando hello libreria Client di archiviazione](#executing-a-point-query-using-the-storage-client-library)
* [Recupero di più entità usando LINQ](#retrieving-multiple-entities-using-linq)
* [Proiezione lato server](#server-side-projection)  

Per esempi di codice sul lato client in grado di gestire più entità tipi archiviati in hello stessa tabella, vedere:  

* [Uso di tipi di entità eterogenei](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>Scelta di un valore PartitionKey appropriato
La scelta di **PartitionKey** deve bilanciare hello necessità tooenables hello ricorso EGTs (tooensure coerenza) su hello requisito toodistribute le entità tra più partizioni (tooensure una soluzione scalabile).  

A un'estremità, è possibile archiviare tutte le entità in una singola partizione, ma ciò potrebbe limitare la scalabilità hello della soluzione e potrebbe impedire servizio tabella hello in grado di tooload-bilanciamento delle richieste. In hello altra estremità, è possibile archiviare un'entità per ogni partizione, che potrebbe essere estremamente scalabile e che consente di hello tabella tooload bilanciamento delle richieste, ma che potrebbe impedire l'utilizzo di gruppi di entità.  

L'obiettivo ideale **PartitionKey** uno che consente di eseguire query efficienti toouse e tooensure partizioni sufficienti che è la soluzione è scalabile. Di solito le entità dispongono una proprietà apposita che le distribuisce in un numero sufficiente di partizioni.

> [!NOTE]
> Ad esempio, in un sistema che archivia le informazioni sugli utenti o i dipendenti, l'ID utente può essere un valore PartitionKey valido. È possibile diverse entità che utilizzano un ID utente specificato come chiave di partizione hello. Ogni entità che archivia i dati su un utente è raggruppata in una singola partizione e quindi queste entità sono accessibili tramite gruppi di entità, mantenendo la scalabilità elevata.
> 
> 

Esistono ulteriori considerazioni nella scelta di **PartitionKey** relative toohow verrà inserire, aggiornare ed eliminare entità: vedere la sezione hello [progettazione per la modifica dei dati](#design-for-data-modification) sotto.  

### <a name="optimizing-queries-for-hello-table-service"></a>Ottimizzazione delle query per hello del servizio tabelle
Hello del servizio tabelle vengono indicizzati automaticamente le entità utilizzando hello **PartitionKey** e **RowKey** valori in un solo indice cluster, pertanto hello motivo che punto query sono hello toouse più efficiente . Tuttavia, non sono presenti indici diverso da quello in indice cluster hello hello **PartitionKey** e **RowKey**.

Molte progettazioni devono soddisfare ricerca tooenable requisiti di entità in base a più criteri. ad esempio trovare le entità dipendente in base a indirizzo di posta elettronica, ID dipendente o cognome. Hello in seguito nella sezione hello modelli [modelli di progettazione tabella](#table-design-patterns) risolvere questi tipi di requisiti e una descrizione delle modalità di utilizzo intorno fatti hello del servizio tabelle hello non fornisce indici secondari:  

* [Modello di indice secondario intra-partition](#intra-partition-secondary-index-pattern) -archiviazione di più copie di ogni entità mediante diverse **RowKey** valori (in hello stessa partizione) tooenable veloci ed efficienti ricerche e ordinamento alternativo gli ordini tramite diversi **RowKey** valori.  
* [Modello di indice secondario partizione tra](#inter-partition-secondary-index-pattern) : archiviazione di più copie di ogni entità utilizzando i diversi valori RowKey in partizioni distinte o in tabelle separate tooenable veloce e ricerche efficienti e ordinamento alternativo gli ordini con diversi **RowKey** valori.  
* [Modello di entità indice](#index-entities-pattern) -Gestisci entità tooenable efficienti ricerche che restituiscono elenchi di entità.  

### <a name="sorting-data-in-hello-table-service"></a>Ordinamento dati nel servizio tabelle hello
Hello del servizio tabelle restituisce entità ordinate in ordine crescente in base **PartitionKey** e quindi per **RowKey**. Queste chiavi sono i valori stringa e tooensure che i valori numerici ordinare in modo corretto, è necessario convertirli in lunghezza fissata tooa e li riempire con zeri. Ad esempio, se hello valore di id dipendente è utilizzare come hello **RowKey** è un valore intero, è necessario convertire l'id dipendente **123** troppo**00000123**.  

Molte applicazioni hanno requisiti toouse dati ordinati in ordine diverso: ordinamento, ad esempio, i dipendenti in base al nome o creando un join di Data. Hello in seguito nella sezione hello modelli [modelli di progettazione tabella](#table-design-patterns) come tooalternate di ordinamento per le entità di indirizzi:  

* [Modello di indice secondario intra-partition](#intra-partition-secondary-index-pattern) -archiviazione di più copie di ogni entità utilizzando i diversi valori RowKey (in hello stessa partizione) tooenable veloci ed efficienti ricerche e ordinamento alternativo gli ordini con diversi valori RowKey.  
* [Modello di indice secondario partizione tra](#inter-partition-secondary-index-pattern) : archiviazione di più copie di ogni entità con diversi valori RowKey in partizioni distinte in tabelle separate tooenable veloce e ricerche efficienti e ordinamento alternativo gli ordini con RowKey diversi valori.
* [Modello della parte finale del log](#log-tail-pattern) -hello recuperare  *n*  le entità aggiunte più di recente tooa partizione utilizzando un **RowKey** valore che ordina in data inversa e l'ordine temporale.  

## <a name="design-for-data-modification"></a>Progettazione per la modifica dei dati
In questa sezione è incentrata sulle considerazioni relative alla progettazione di hello per l'ottimizzazione di inserimenti, aggiornamenti ed eliminazioni. In alcuni casi, è necessario ottimizzare per l'esecuzione di query sui progetti che ottimizza per la modifica dei dati, come avviene nelle progettazioni per i database relazionali (anche se per la gestione di tecniche di hello hello progettazione le progettazioni conciliare hello tooevaluate vantaggi e svantaggi sono diversi in un database relazionale). Hello sezione [modelli di progettazione tabella](#table-design-patterns) vengono descritti alcuni modelli di progettazione dettagliata per hello del servizio tabelle e vengono evidenziate alcune questi vantaggi e svantaggi. In pratica si vedrà che molte progettazioni ottimizzate per le query delle entità vanno bene anche per la modifica delle entità.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Ottimizzazione delle prestazioni di hello di inserimento, aggiornamento ed eliminazione
tooupdate o eliminare un'entità, è necessario essere in grado di tooidentify usando hello **PartitionKey** e **RowKey** valori. In questo senso, la scelta di **PartitionKey** e **RowKey** per la modifica di entità deve seguire simile criteri tooyour scelta toosupport scegliere query dal momento che le entità tooidentify come più efficiente possibile. Non si desidera un inefficiente partizione o tabella analisi toolocate un'entità in hello toodiscover ordine toouse **PartitionKey** e **RowKey** valori, è necessario tooupdate oppure eliminarla.  

Hello in seguito nella sezione hello modelli [modelli di progettazione tabella](#table-design-patterns) indirizzo l'ottimizzazione delle prestazioni di hello o l'inserimento, aggiornamento e le operazioni di eliminazione:  

* [Eliminazione di volumi elevati con un modello](#high-volume-delete-pattern) -eliminazione hello attiva di un volume elevato di entità mediante l'archiviazione di tutte le entità hello per l'eliminazione simultanea nella propria tabella separata, ma eliminare entità hello eliminando hello tabella.  
* [Modello serie di dati](#data-series-pattern) -archivio dati completo serie in un numero di hello toominimize singola entità richieste di effettuate.  
* [Modello di entità Wide](#wide-entities-pattern) -utilizzare come entità logiche più entità fisiche toostore con più di 252 proprietà.  
* [Modello di entità di grandi dimensioni](#large-entities-pattern) -utilizza valori di proprietà di grandi dimensioni toostore archiviazione blob.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>Verifica della coerenza nelle entità archiviate
altri fattori chiave che influenza la scelta di chiavi per l'ottimizzazione delle modifiche dei dati è Hello come tooensure coerenza con le transazioni atomiche. È possibile utilizzare solo un toooperate EGT in entità archiviate in hello stessa partizione.  

Hello in seguito nella sezione hello modelli [modelli di progettazione tabella](#table-design-patterns) la gestione della coerenza di indirizzi:  

* [Modello di indice secondario intra-partition](#intra-partition-secondary-index-pattern) -archiviazione di più copie di ogni entità mediante diverse **RowKey** valori (in hello stessa partizione) tooenable veloci ed efficienti ricerche e ordinamento alternativo gli ordini tramite diversi **RowKey** valori.  
* [Modello di indice secondario partizione tra](#inter-partition-secondary-index-pattern) : archiviazione di più copie di ogni entità utilizzando i diversi valori RowKey in partizioni distinte o in tabelle separate tooenable veloce e ricerche efficienti e ordinamento alternativo gli ordini con diversi **RowKey** valori.  
* [Modello per transazioni con coerenza finale](#eventually-consistent-transactions-pattern) - Abilita un comportamento di coerenza finale tra i limiti della partizione o i limiti del sistema di archiviazione usando le code di Azure.
* [Modello di entità indice](#index-entities-pattern) -Gestisci entità tooenable efficienti ricerche che restituiscono elenchi di entità.  
* [Modello denormalizzazione](#denormalization-pattern) -combinare i dati relativi insieme in una singola entità tooenable tooretrieve tutti hello è necessario con una query con singolo punto dati.  
* [Modello serie di dati](#data-series-pattern) -archivio dati completo serie in un numero di hello toominimize singola entità richieste di effettuate.  

Per informazioni sui gruppi di entità, vedere la sezione hello [gruppi di entità](#entity-group-transactions).  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>Verifica della capacità della progettazione per modifiche efficienti di facilitare query efficienti
In molti casi, una progettazione per i risultati di query efficienti modifiche efficiente, ma è sempre necessario valutare se hello caso dello scenario specifico. Alcuni dei modelli di hello nella sezione hello [modelli di progettazione tabella](#table-design-patterns) in modo esplicito, valutare i compromessi tra l'esecuzione di query e modifica di entità e tenere sempre in numero di hello conto di ogni tipo di operazione.  

Hello in seguito nella sezione hello modelli [modelli di progettazione tabella](#table-design-patterns) indirizzo compromessi tra la progettazione di query efficienti e la progettazione per la modifica dei dati efficiente:  

* [Modello di chiave composta](#compound-key-pattern) -utilizzare composta **RowKey** tooenable valori toolookup un client relativi dati con un singolo punto di query.  
* [Modello della parte finale del log](#log-tail-pattern) -hello recuperare  *n*  le entità aggiunte più di recente tooa partizione utilizzando un **RowKey** valore che ordina in data inversa e l'ordine temporale.  

## <a name="encrypting-table-data"></a>Crittografia dei dati di tabella
Libreria Client di archiviazione Azure .NET supporta crittografia stringa proprietà dell'entità per l'inserimento di Hello e sostituire operazioni. crittografato Hello sono archiviate nel servizio hello come proprietà binarie e vengono convertiti toostrings indietro dopo la decrittografia.    

Per le tabelle, inoltre i criteri di crittografia toohello, gli utenti devono specificare toobe proprietà hello crittografati. Questa operazione può essere eseguita specificando un attributo [EncryptProperty] \(per le entità POCO che derivano da TableEntity) o un resolver di crittografia nelle opzioni di richiesta. Un resolver di crittografia è un delegato che accetta una chiave di partizione, una chiave di riga e un nome di proprietà e restituisce un valore booleano che indica se tale proprietà deve essere crittografata. Durante la crittografia, la libreria client di hello utilizzerà questo toodecide informazioni se una proprietà deve essere crittografata durante la scrittura di transito toohello. delegato di Hello fornisce anche la possibilità di hello di logica per la modalità di crittografia delle proprietà. (Ad esempio, se X, quindi crittografa la proprietà A; in caso contrario crittografa le proprietà A e B). Si noti che è necessario non tooprovide queste informazioni durante la lettura o di una query sulle entità.

Si noti che l'unione non è attualmente supportata. Poiché un subset delle proprietà è stato crittografato in precedenza usando una chiave diversa, semplicemente l'unione di nuove proprietà hello e l'aggiornamento dei metadati hello comporterà la perdita di dati. L'unione di uno, è necessario rendere servizio aggiuntivo chiama entità preesistente di hello tooread dal servizio hello o utilizzando una nuova chiave per ogni proprietà, che non sono adatti per motivi di prestazioni.     

Per informazioni sulla crittografia dei dati di tabella, vedere [Crittografia lato client e insieme di credenziali delle chiavi di Azure per Archiviazione di Microsoft Azure](storage-client-side-encryption.md).  

## <a name="modelling-relationships"></a>Modellazione di relazioni
Compilazione di modelli di dominio è un passaggio fondamentale nella progettazione di hello dei sistemi complessi. In genere, usare hello modellazione processo tooidentify entità e relazioni hello tra di esse come un modo toounderstand hello dominio aziendale e indicano progettazione hello del sistema. Questa sezione viene illustrato come è possibile convertire i tipi relazione comuni hello trovato nel dominio modelli toodesigns per hello del servizio tabelle. il processo di Hello di mapping da un tooa modello di dati logico fisico basato su modello dati NoSQL-è molto diverso da quella utilizzata quando si progetta un database relazionale. Progettazione di database relazionali presuppone che in genere un processo di normalizzazione dei dati ottimizzato per ridurre al minimo di ridondanza e una funzionalità di query dichiarativa che astrae hello come implementazione del funzionamento di database hello.  

### <a name="one-to-many-relationships"></a>Relazioni uno a molti
Le relazioni uno a molti tra gli oggetti del dominio aziendale sono molto frequenti: ad esempio, un reparto ha più dipendenti. Esistono diverse relazioni uno-a-molti di tooimplement modi hello del servizio tabelle ogni con i vantaggi e svantaggi che possono essere rilevanti toohello particolare scenario.  

Considerare l'esempio hello di una grande azienda multinazionale con decine di migliaia di servizi e le entità dipendente in ogni reparto ha molti dipendenti e ogni dipendente come associata a un reparto specifico. Un approccio consiste reparto separato toostore e le entità dipendente come i seguenti:  

![][1]

Questo esempio mostra una relazione uno-a-molti implicita tra tipi di hello basati su hello **PartitionKey** valore. Ogni reparto può avere più dipendenti.  

In questo esempio viene inoltre un'entità di reparto e le entità correlate dipendente in hello stessa partizione. È possibile scegliere anche gli account di archiviazione per i tipi di entità diversa hello, tabelle o partizioni diverse toouse.  

Un approccio alternativo è toodenormalize le entità dipendente solo dati e l'archivio dati denormalizzati reparto, come illustrato nell'esempio seguente hello. In questo scenario specifico, questo approccio denormalizzato potrebbe non essere hello migliore se si hanno requisito toobe toochange in grado di hello i dettagli su un responsabile del reparto perché toodo ciò è necessario tooupdate ogni dipendente nel reparto hello.  

![][2]

Per ulteriori informazioni, vedere hello [modello denormalizzazione](#denormalization-pattern) più avanti in questa Guida.  

Hello nella tabella seguente sono riepilogate hello vantaggi e svantaggi di ognuno di hello approcci descritti in precedenza per l'archiviazione di dipendente ed entità reparto che hanno una relazione uno-a-molti. È necessario considerare anche la frequenza con cui si prevede che tooperform diverse operazioni: può essere accettabile toohave una struttura che include un'operazione costosa se tale operazione viene eseguita solo raramente.  

<table>
<tr>
<th>Approccio</th>
<th>Vantaggi</th>
<th>Svantaggi</th>
</tr>
<tr>
<td>Tipi di entità distinti, stessa partizione, stessa tabella</td>
<td>
<ul>
<li>È possibile aggiornare un'entità reparto con un'unica operazione.</li>
<li>Se si dispone di un requisito toomodify un'entità di reparto, è possibile utilizzare una coerenza toomaintain EGT ogni volta che si aggiornamenti, inserimenti ed eliminazioni un'entità employee. ad esempio se si mantiene un conteggio dei dipendenti per ogni reparto.</li>
</ul>
</td>
<td>
<ul>
<li>Potrebbe essere necessario tooretrieve sia un dipendente e un'entità di reparto per alcune attività di client.</li>
<li>Operazioni di archiviazione si verificano in hello stessa partizione. Con volumi di transazioni elevati, potrebbe risultarne un hotspot.</li>
<li>È possibile spostare un reparto di nuovo tooa dipendente utilizzando un EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Tipi di entità distinti, partizioni o tabelle o account di archiviazione diversi</td>
<td>
<ul>
<li>È possibile aggiornare un'entità reparto o un'entità dipendente con un'unica operazione.</li>
<li>Volumi elevati di transazioni, favorisce la diffusione hello carico tra più partizioni.</li>
</ul>
</td>
<td>
<ul>
<li>Potrebbe essere necessario tooretrieve sia un dipendente e un'entità di reparto per alcune attività di client.</li>
<li>Non è possibile utilizzare EGTs toomaintain coerenza quando si aggiorna, inserimenti ed eliminazioni un dipendente e aggiornamento di un reparto. ad esempio quando si aggiorna un conteggio dipendenti in un'entità reparto.</li>
<li>È possibile spostare un reparto di nuovo tooa dipendente utilizzando un EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Denormalizzazione in un solo tipo di entità</td>
<td>
<ul>
<li>È possibile recuperare tutte le informazioni di hello che è necessario con una singola richiesta.</li>
</ul>
</td>
<td>
<ul>
<li>Se sono necessarie informazioni di reparto tooupdate (ciò richiederebbe si tooupdate tutti i dipendenti hello in un reparto) può essere costoso toomaintain coerenza.</li>
</ul>
</td>
</tr>
</table>

Come si sceglie tra queste opzioni e che di professionisti hello e gli svantaggi sono i più importanti, dipende gli scenari dell'applicazione specifici. Ad esempio, la frequenza con cui modificare le entità reparto; tutte le query dipendente necessario hello reparto informazioni; come chiudere sei toohello limiti di scalabilità su partizioni o account di archiviazione?  

### <a name="one-to-one-relationships"></a>Relazioni uno a uno
I modelli di dominio possono includere relazioni uno a uno tra le entità. Se è necessario tooimplement una relazione uno a uno in hello del servizio tabelle, è necessario scegliere come toolink hello due entità correlate quando è necessario tooretrieve entrambi. Questo collegamento può essere implicita, in base a una convenzione di valori di chiave hello o esplicita tramite l'archiviazione di un collegamento nel formato hello **PartitionKey** e **RowKey** valori in ogni tooits entità entità correlata. Per una discussione su se è consigliabile archiviare hello le entità correlate in hello stessa partizione, vedere la sezione hello [uno-a-molti relazioni](#one-to-many-relationships).  

Si noti che esistono inoltre considerazioni sull'implementazione che si potrebbero generare relazioni uno a uno tooimplement nel servizio tabelle hello:  

* Gestione di entità di grandi dimensioni (per altre informazioni, vedere [Modello di entità di grandi dimensioni](#large-entities-pattern)).  
* Implementazione di controlli di accesso. Per altre informazioni, vedere [Controllo dell'accesso con le firme di accesso condiviso](#controlling-access-with-shared-access-signatures).  

### <a name="join-in-hello-client"></a>Creare un join nel client hello
Anche se esistono relazioni toomodel modi in hello del servizio tabelle, non si dimenticare che i due motivi principali hello per l'utilizzo del servizio tabelle hello siano scalabilità e prestazioni. Se che si sono modellazione molte relazioni che compromettono le prestazioni di hello e la scalabilità della soluzione, è necessario richiedere manualmente che se è necessario toobuild tutti hello relazioni tra i dati nella struttura della tabella. È possibile toosimplify in grado di hello progettazioni e migliorare hello scalabilità e prestazioni della soluzione, se si consente l'applicazione client di eseguire tutti i join necessari.  

Ad esempio, se si dispongono di tabelle di piccole dimensioni contenenti dati che vengono modificati spesso, quindi è possibile recuperare i dati una volta e memorizzarlo nella cache sul client hello. Ciò consente di evitare round trip ripetuti tooretrieve hello stessi dati. Negli esempi di hello esaminata in questa Guida, hello set reparti in un'organizzazione di piccole dimensioni è probabilmente toobe di piccole dimensioni e modificare raramente rende un ottimo candidato per l'applicazione client è possibile scaricare una volta i dati e della cache come cercare dati.  

### <a name="inheritance-relationships"></a>Relazioni di ereditarietà
Se l'applicazione client utilizza un set di classi che fanno parte di un'entità di business toorepresent relazione di ereditarietà, è possibile mantenere facilmente le entità nel servizio tabelle hello. Ad esempio, potrebbe essere hello seguente insieme di classi definite nell'applicazione client in cui **persona** è una classe astratta.

![][3]

È possibile rendere persistenti le istanze di due classi concrete hello in hello del servizio tabelle utilizzando una singola tabella di persona con entità in un aspetto simile al seguente:  

![][4]

Per ulteriori informazioni sull'utilizzo di più tipi di entità nella stessa tabella nel codice client hello, vedere la sezione hello [utilizzo dei tipi di entità eterogenee](#working-with-heterogeneous-entity-types) più avanti in questa Guida. Questo fornisce esempi di come toorecognize hello il tipo di entità nel codice client.  

## <a name="table-design-patterns"></a>Modelli di progettazione tabella
Nelle sezioni precedenti, sono state illustrate alcune discussioni dettagliate su come toooptimize tabella progettate per entrambi il recupero dei dati di entità tramite query e per l'inserimento, aggiornamento ed eliminazione di dati di entità. Questa sezione descrive alcuni modelli adatti all'uso con le soluzioni di servizio tabelle. Inoltre, si noterà come praticamente è possibile risolvere alcuni dei problemi di hello e compromessi generati in precedenza in questa Guida. Hello diagramma seguente vengono riepilogate le relazioni di hello tra modelli diversi di hello:  

![][5]

mappa di schema Hello sopra sono evidenziate alcune relazioni tra modelli (blu) e anti-pattern (arancione) che sono documentati in questa Guida. Ovviamente esistono molti altri modelli utili. Ad esempio, uno dei principali scenari di hello per il servizio tabelle è hello toouse [materializzata vista modello](https://msdn.microsoft.com/library/azure/dn589782.aspx) da hello [comando Query Responsibility Segregation (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) modello.  

### <a name="intra-partition-secondary-index-pattern"></a>Modello per indice secondario intrapartizione
Archiviazione di più copie di ogni entità mediante diverse **RowKey** valori (in hello stessa partizione) tooenable veloci ed efficienti ricerche e ordinamento alternativo gli ordini con diversi **RowKey** valori. Gli aggiornamenti tra copie possono essere mantenuti coerenti usando transazioni EGT.  

#### <a name="context-and-problem"></a>Contesto e problema
Hello del servizio tabelle vengono indicizzati automaticamente le entità utilizzando hello **PartitionKey** e **RowKey** valori. In questo modo un tooretrieve applicazione client di un'entità in modo efficiente utilizzando questi valori. Ad esempio, utilizzando una struttura della tabella hello illustrato di seguito, un'applicazione client consente tooretrieve di query un punto di un'entità di singolo dipendente utilizzando il nome di reparto hello e id dipendente hello (hello **PartitionKey** e  **RowKey** valori). Un client può anche recuperare entità ordinate per ID dipendente in ogni reparto.

![][6]

Se si desidera anche toobe in grado di toofind un'entità dipendente in base al valore di hello di un'altra proprietà, ad esempio indirizzo di posta elettronica, è necessario utilizzare un livello di efficienza minore toofind di analisi partizione una corrispondenza. Questo avviene perché il servizio tabelle hello non fornisce indici secondari. Inoltre, non è toorequest alcuna opzione un elenco di dipendenti in un ordine diverso rispetto a **RowKey** ordine.  

#### <a name="solution"></a>Soluzione
toowork intorno mancanza hello di indici secondari, è possibile archiviare più copie di ogni entità con ciascuna copia con un altro **RowKey** valore. Se si archivia un'entità con strutture hello illustrate di seguito, è possibile recuperare in modo efficiente l'entità dipendente in base all'id dipendente o di indirizzo di posta elettronica. i valori del prefisso per hello Hello **RowKey**, "empid_" e "email_" consentono di tooquery per un singolo dipendente o un intervallo di dipendenti con un intervallo di indirizzi di posta elettronica o gli ID dipendente.  

![][7]

Hello seguenti due criteri di filtro (una ricerca con id dipendente e una ricerca con indirizzo di posta elettronica) entrambi specifica query punto:  

* $filter=(PartitionKey eq 'Sales') e (RowKey eq 'empid_000223)  
* $filter=(PartitionKey eq 'Sales') e (RowKey eq 'email_jonesj@contoso.com')  

Se si esegue una query per un intervallo di entità dipendente, è possibile specificare un intervallo ordinato in ordine di id dipendente o un intervallo ordinato in ordine di indirizzo di posta elettronica eseguendo una query per le entità con prefisso appropriato di hello in hello **RowKey**.  

* utilizzano tutti i dipendenti hello nel reparto vendite hello con un id dipendente in hello intervallo 000100 too000199 toofind: $filter = (PartitionKey eq 'Sales') e (ge RowKey 'empid_000100') e (le RowKey 'empid_000199')  
* toofind tutti hello impiegati nel reparto vendite hello con un indirizzo di posta elettronica a partire da hello rappresentato dalla lettera 'a' utilizzo: $filter = (PartitionKey eq 'Sales') e (ge RowKey 'email_a') (RowKey lt 'email_b') e  
  
  Si noti che la sintassi di filtro hello utilizzata negli esempi di hello sopra è da hello tabella API REST del servizio, per ulteriori informazioni, vedere [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* Archiviazione tabelle è relativamente conveniente toouse pertanto hello costi aggiuntivi della memorizzazione dei dati duplicati non deve essere un problema. È tuttavia sempre valutare il costo di hello di progettazione in base ai requisiti di archiviazione previste e aggiungere le entità duplicate le query di hello toosupport che l'applicazione client viene eseguita solo.  
* Poiché l'entità di indice secondario hello sono archiviate nella stessa partizione come entità originale hello hello, è necessario assicurarsi che non superi obiettivi di scalabilità hello per una singola partizione.  
* È possibile mantenere le entità duplicate coerenti tra loro tramite EGTs tooupdate hello due copie dell'entità hello in modo atomico. Ciò implica che è necessario archiviare tutte le copie di un'entità in hello stessa partizione. Per ulteriori informazioni, vedere la sezione hello [utilizzando transazioni di gruppi di entità](#entity-group-transactions).  
* valore utilizzato per hello Hello **RowKey** deve essere univoco per ogni entità. Provare a usare valori di chiave composti.  
* Spaziatura interna di valori numerici in hello **RowKey** (ad esempio, id dipendente hello 000223), consente di correggere l'ordinamento e filtro in base a intervallo di valori.  
* Non è necessariamente necessario tooduplicate tutte le proprietà di hello dell'entità. Ad esempio, se hello query di entità di ricerca hello hello tramite posta elettronica di indirizzi in hello **RowKey** mai necessario età hello del dipendente, queste entità potrebbe avere hello seguente struttura:

![][8]

* È in genere migliore toostore duplicazione dei dati e garantire che è possibile recuperare tutti i dati di hello è necessario con una singola query, toouse toolocate di una query rispetto a un'entità e un altro hello toolookup i dati necessari.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando l'applicazione client deve tooretrieve entità utilizzando un'ampia gamma di chiavi diverse, quando il client deve entità tooretrieve in diversi tipi di ordinamento e in cui è possibile identificare ogni entità utilizzando un'ampia gamma di valori univoci. Tuttavia, è necessario assicurarsi che non superi i limiti di scalabilità di hello partizione quando si eseguono ricerche di entità utilizzando diversi hello **RowKey** valori.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Modello per indice secondario interpartizione](#inter-partition-secondary-index-pattern)
* [Modello per chiave composta](#compound-key-pattern)
* [Transazioni dei gruppi di entità](#entity-group-transactions)
* [Uso di tipi di entità eterogenei](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>Modello per indice secondario intrapartizione
Archiviazione di più copie di ogni entità mediante diverse **RowKey** valori partizioni distinte o ricerche veloci ed efficienti tooenable di tabelle distinte e tipi di ordinamento alternativo utilizzando diversi **RowKey**valori.  

#### <a name="context-and-problem"></a>Contesto e problema
Hello del servizio tabelle vengono indicizzati automaticamente le entità utilizzando hello **PartitionKey** e **RowKey** valori. In questo modo un tooretrieve applicazione client di un'entità in modo efficiente utilizzando questi valori. Ad esempio, utilizzando una struttura della tabella hello illustrato di seguito, un'applicazione client consente tooretrieve di query un punto di un'entità di singolo dipendente utilizzando il nome di reparto hello e id dipendente hello (hello **PartitionKey** e  **RowKey** valori). Un client può anche recuperare entità ordinate per ID dipendente in ogni reparto.  

![][9]

Se si desidera anche toobe in grado di toofind un'entità dipendente in base al valore di hello di un'altra proprietà, ad esempio indirizzo di posta elettronica, è necessario utilizzare un livello di efficienza minore toofind di analisi partizione una corrispondenza. Questo avviene perché il servizio tabelle hello non fornisce indici secondari. Inoltre, non è toorequest alcuna opzione un elenco di dipendenti in un ordine diverso rispetto a **RowKey** ordine.  

Si è prevedono un volume molto elevato di transazioni su queste entità e si desidera rischio hello toominimize hello del servizio tabelle, la limitazione delle richieste del client.  

#### <a name="solution"></a>Soluzione
toowork intorno mancanza hello di indici secondari, è possibile archiviare più copie di ogni entità con ciascuna copia utilizzando diversi **PartitionKey** e **RowKey** valori. Se si archivia un'entità con strutture hello illustrate di seguito, è possibile recuperare in modo efficiente l'entità dipendente in base all'id dipendente o di indirizzo di posta elettronica. i valori del prefisso per hello Hello **PartitionKey**, "empid_" e "email_" consentono di tooidentify quale indice si desidera toouse per una query.  

![][10]

Hello seguenti due criteri di filtro (una ricerca con id dipendente e una ricerca con indirizzo di posta elettronica) entrambi specifica query punto:  

* $filter=(PartitionKey 'empid_Sales') e (RowKey eq '000223')
* $filter=(PartitionKey eq 'email_Sales') e (RowKey eq 'jonesj@contoso.com')  

Se si esegue una query per un intervallo di entità dipendente, è possibile specificare un intervallo ordinato in ordine di id dipendente o un intervallo ordinato in ordine di indirizzo di posta elettronica eseguendo una query per le entità con prefisso appropriato di hello in hello **RowKey**.  

* tutti i dipendenti di hello toofind hello reparto vendite con un id dipendente nell'intervallo di hello **000100** troppo**000199** ordinati employee id ordine utilizzato: $filter = (PartitionKey eq ' empid_Sales') e (ge RowKey ' 000100') e (le RowKey '000199')  
* toofind utilizzare ordine indirizzo di posta elettronica tutti i dipendenti hello reparto vendite hello con un indirizzo di posta elettronica che inizia con 'a' ordinato in: $filter = (PartitionKey eq ' email_Sales') e (ge RowKey 'a') e (RowKey lt 'b')  

Si noti che la sintassi di filtro hello utilizzata negli esempi di hello sopra è da hello tabella API REST del servizio, per ulteriori informazioni, vedere [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* È possibile mantenere le entità duplicate alla fine coerente tra loro tramite hello [modello alla fine coerente transazioni](#eventually-consistent-transactions-pattern) le entità di toomaintain hello indice primario e secondario.  
* Archiviazione tabelle è relativamente conveniente toouse pertanto hello costi aggiuntivi della memorizzazione dei dati duplicati non deve essere un problema. È tuttavia sempre valutare il costo di hello di progettazione in base ai requisiti di archiviazione previste e aggiungere le entità duplicate le query di hello toosupport che l'applicazione client viene eseguita solo.  
* valore utilizzato per hello Hello **RowKey** deve essere univoco per ogni entità. Provare a usare valori di chiave composti.  
* Spaziatura interna di valori numerici in hello **RowKey** (ad esempio, id dipendente hello 000223), consente di correggere l'ordinamento e filtro in base a intervallo di valori.  
* Non è necessariamente necessario tooduplicate tutte le proprietà di hello dell'entità. Ad esempio, se hello query di entità di ricerca hello hello tramite posta elettronica di indirizzi in hello **RowKey** mai necessario età hello del dipendente, queste entità potrebbe avere hello seguente struttura:
  
  ![][11]
* È in genere migliore toostore duplicazione dei dati e assicurarsi che è possibile recuperare tutti i dati di hello che è necessario con una singola query di toouse toolocate di una query un'entità mediante hello indice secondario e un altro toolookup hello dati necessari nell'indice primario hello.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando l'applicazione client deve tooretrieve entità utilizzando un'ampia gamma di chiavi diverse, quando il client deve entità tooretrieve in diversi tipi di ordinamento e in cui è possibile identificare ogni entità utilizzando un'ampia gamma di valori univoci. Utilizzare questo modello quando si desidera tooavoid superamento dei limiti di scalabilità di hello partizione quando si eseguono ricerche di entità utilizzando diversi hello **RowKey** valori.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Modello per transazioni con coerenza finale](#eventually-consistent-transactions-pattern)  
* [Modello per indice secondario intrapartizione](#intra-partition-secondary-index-pattern)  
* [Modello per chiave composta](#compound-key-pattern)  
* [Transazioni dei gruppi di entità](#entity-group-transactions)  
* [Uso di tipi di entità eterogenei](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>Modello per transazioni con coerenza finale
abilita un comportamento di coerenza finale tra i limiti della partizione o i limiti del sistema di archiviazione usando le code di Azure.  

#### <a name="context-and-problem"></a>Contesto e problema
EGTs Abilita transazioni atomiche in più entità che condividono hello stessa chiave di partizione. Per motivi di scalabilità e prestazioni, è possibile decidere toostore entità che hanno requisiti di coerenza in partizioni distinte o in un sistema di archiviazione distinti: in questo caso, non è possibile utilizzare EGTs toomaintain coerenza. Ad esempio, potrebbe essere una requisito toomaintain la coerenza eventuale tra:  

* Entità archiviate in due partizioni diverse nella stessa tabella, in tabelle diverse, in diversi account di archiviazione hello.  
* Un'entità archiviati nel servizio tabelle hello e un blob archiviato in hello servizio Blob.  
* Un'entità archiviata nel servizio tabelle hello e un file in un file system.  
* Un'entità archiviare nel servizio tabelle hello ancora indicizzato tramite il servizio di ricerca di Azure hello.  

#### <a name="solution"></a>Soluzione
Usando le code di Azure, è possibile implementare una soluzione che offre coerenza finale tra due o più partizioni o sistemi di archiviazione.
tooillustrate questo approccio, si supponga di avere un requisito toobe tooarchive in grado di dipendente le entità precedenti. Queste entità sono raramente oggetto di query e devono essere escluse da tutte le attività associate ai dipendenti correnti. tooimplement questo requisito si archiviano i dipendenti attivi in hello **corrente** tabella e i dipendenti precedenti hello **archivio** tabella. Archiviazione di un dipendente richiede entità hello toodelete hello **corrente** tabella e aggiungere hello entità toohello **archivio** tabella, ma è possibile utilizzare un tooperform EGT queste due operazioni. rischio hello tooavoid che un errore causa tooappear un'entità in entrambe o nessuna delle due tabelle, l'operazione di archiviazione hello deve essere alla fine coerente. Hello diagramma sequenza seguente descrive i passaggi di hello in questa operazione. Dettaglio è disponibile per i percorsi delle eccezioni in seguito il testo hello.  

![][12]

Un client avvia l'operazione di archiviazione hello inserendo un messaggio in una coda di Azure, in questo dipendente di esempio tooarchive #456. Un ruolo di lavoro viene eseguito il polling della coda di hello per i nuovi messaggi. Quando ne viene trovato uno, legge il messaggio hello e lascia una copia nascosta nella coda di hello. ruolo di lavoro Hello successivamente recupera una copia dell'entità hello dal hello **corrente** tabella, inserisce una copia in hello **archivio** tabella e quindi Elimina hello originale da hello **corrente**tabella. Infine, se non sono presenti errori nei passaggi precedenti hello, ruolo di lavoro hello Elimina messaggio nascosto hello dalla coda di hello.  

In questo esempio, il passaggio 4 inserisce dipendente hello hello **archivio** tabella. È possibile aggiungere il blob tooa dipendente di hello nel servizio Blob hello o un file in un file system.  

#### <a name="recovering-from-failures"></a>Ripristino da errori
È importante che le operazioni nei passaggi di hello **4** e **5** deve essere *idempotente* nel caso in cui il ruolo di lavoro hello deve toorestart operazione di archiviazione hello. Se si utilizza servizio tabella hello, per passaggio **4** è necessario utilizzare un'operazione "inserire o sostituire", per passaggio **5** si consiglia di utilizzare un "eliminare se esiste" operazione nella libreria client hello in uso. Se si sta usando un altro sistema di archiviazione, è consigliabile usare un'operazione idempotente appropriata.  

Se il ruolo di lavoro hello mai completata passaggio **6**, quindi dopo un messaggio hello di timeout viene visualizzato nuovamente nella coda di hello prepararla per hello lavoro ruolo tootry tooreprocess. ruolo di lavoro Hello può controllare quante volte è stato letto un messaggio in coda hello e, se necessario, è un messaggio "non elaborabile" per l'analisi mediante l'invio tooa flag separare coda. Per ulteriori informazioni sulla lettura dei messaggi in coda e il controllo hello conteggio rimozione dalla coda, vedere [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).  

Alcuni errori da servizi di tabella e coda hello sono gli errori temporanei e l'applicazione client deve includere toohandle logica di ripetizione adatto li.  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* Questa soluzione non prevede l'isolamento delle transazioni. Ad esempio, un client può leggere hello **corrente** e **archivio** tabelle quando il ruolo di lavoro hello è tra i vari passaggi **4** e **5**e vedere un visualizzazione non coerente dei dati hello. Si noti che i dati di hello sarà coerenti alla fine.  
* È necessario assicurarsi che i passaggi 4 e 5 sono idempotenti in coerenza finale tooensure di ordine.  
* È possibile ridimensionare la soluzione hello utilizzando più code e istanze del ruolo di lavoro.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando si desidera che la coerenza eventuale tooguarantee tra le entità presenti in tabelle o partizioni diverse. Consente di estendere questo modello tooensure la coerenza eventuale per le operazioni del servizio tabelle hello e servizio Blob hello e altre origini dati non correlati all'archiviazione Azure, ad esempio database o hello file system.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Transazioni dei gruppi di entità](#entity-group-transactions)  
* [Unione o sostituzione](#merge-or-replace)  

> [!NOTE]
> Se l'isolamento delle transazioni è importante tooyour soluzione, è consigliabile riprogettare le tabelle tooenable è toouse EGTs.  
> 
> 

### <a name="index-entities-pattern"></a>Modello per entità di indice
Gestire le entità tooenable efficienti ricerche che restituiscono elenchi di entità.  

#### <a name="context-and-problem"></a>Contesto e problema
Hello del servizio tabelle vengono indicizzati automaticamente le entità utilizzando hello **PartitionKey** e **RowKey** valori. In questo modo un tooretrieve applicazione client un'entità in modo efficiente utilizzando una query del punto. Ad esempio, utilizzando una struttura della tabella hello illustrato di seguito, un'applicazione client può recuperare in modo efficiente un'entità employee singole utilizzando il nome di reparto hello e id dipendente hello (hello **PartitionKey** e **RowKey** ).  

![][13]

Se si desidera anche tooretrieve in grado di toobe un elenco di entità dipendente in base hello valore di un'altra proprietà non è univoco, ad esempio cognome, è necessario utilizzare una partizione meno efficiente analisi toofind corrispondenze anziché un indice toolook li backup direttamente. Questo avviene perché il servizio tabelle hello non fornisce indici secondari.  

#### <a name="solution"></a>Soluzione
ricerca tooenable in base al cognome con struttura entità hello illustrato sopra, è necessario mantenere elenchi di ID dipendente. Se si desidera che le entità di tooretrieve hello dipendente con un determinato cognome, ad esempio Jones, è necessario innanzitutto individuare elenco hello di ID dipendente per i dipendenti con Jones come cognome e quindi recuperare tali entità employee. Sono disponibili tre opzioni principali per l'archiviazione di elenchi di hello di ID dipendente:  

* Usare l'archiviazione BLOB.  
* Creare le entità di indice nella stessa partizione come entità employee hello hello.  
* Creare entità di indice in una tabella o una partizione separata.  

<u>Opzione 1: usare l'archiviazione BLOB</u>  

Per la prima opzione hello, creare un blob per ogni nome ultimo univoco in ogni archivio blob un elenco di hello **PartitionKey** (reparto) e **RowKey** valori (id dipendente) per i dipendenti che hanno questo ultimo nome. Quando si aggiunge o elimina un dipendente, è necessario assicurarsi che il contenuto di hello del blob rilevanti hello è alla fine coerente con l'entità dipendente hello.  

<u>Opzione &#2;:</u> entità Crea indice hello stessa partizione  

Per la seconda opzione hello, utilizzare le entità di indice che memorizzano hello dati seguenti:  

![][14]

Hello **EmployeeIDs** proprietà contiene un elenco di ID dipendente per i dipendenti con cognome hello archiviati in hello **RowKey**.  

Hello seguito viene illustrato il processo di hello da seguire quando si aggiunge un nuovo dipendente se si utilizza l'opzione secondo hello. In questo esempio, si sta aggiungendo un dipendente con Id 000152 e un cognome Jones nel reparto vendite hello:  

1. Recuperare hello indice entità con un **PartitionKey** "Sales" e hello valore **RowKey** valore "Jones". Salvare hello ETag della toouse entità nel passaggio 2.  
2. Creare una transazione di gruppo di entità (ovvero, un'operazione batch) che inserisce l'entità employee nuovo hello (**PartitionKey** valore "Sales" e **RowKey** valore "000152"), e gli aggiornamenti hello entità indice ( **PartitionKey** valore "Sales" e **RowKey** valore "Jones") tramite l'aggiunta di hello nuovo dipendente id toohello elenco nel campo EmployeeIDs hello. Per informazioni sulle transazioni di gruppi di entità, vedere la sezione [Transazioni di gruppi di entità](#entity-group-transactions).  
3. Se transazione di gruppo di entità hello non riesce a causa di un errore di concorrenza ottimistica (un altro utente ha modificato solo hello indice entità), è necessario toostart al passaggio 1 nuovamente.  

Se si utilizza hello seconda opzione, è possibile utilizzare un toodeleting approccio simile, un dipendente. Modifica il cognome del dipendente è leggermente più complessa, poiché sarà necessaria una transazione di gruppo di entità che aggiorna tre entità tooexecute: hello entità employee, l'entità di indice hello per cognome precedente hello ed entità indice hello per cognome nuovo hello. È necessario recuperare ogni entità prima di apportare modifiche nell'ordine valori ETag di hello tooretrieve che è possibile utilizzare gli aggiornamenti di hello tooperform la concorrenza ottimistica.  

Hello seguito viene illustrato il processo di hello da seguire quando è necessario toolook backup di tutti i dipendenti con un determinato cognome in un reparto hello se si utilizza l'opzione secondo hello. In questo esempio, ci rivolgiamo backup di tutti i dipendenti con cognome Jones nel reparto vendite hello hello:  

1. Recuperare hello indice entità con un **PartitionKey** "Sales" e hello valore **RowKey** valore "Jones".  
2. Analizzare l'elenco di hello ID nel campo EmployeeIDs hello di dipendenti.  
3. Se sono necessarie ulteriori informazioni su ciascuno di questi dipendenti (ad esempio gli indirizzi di posta elettronica), ognuna delle entità employee hello utilizzando recuperare **PartitionKey** valore "Sales" e **RowKey** i valori elenco di Hello di dipendenti ottenuto nel passaggio 2.  

<u>Opzione 3:</u> creare entità di indice in una tabella o una partizione separata  

Per la terza opzione hello, utilizzare le entità di indice che memorizzano hello dati seguenti:  

![][15]

Hello **EmployeeIDs** proprietà contiene un elenco di ID dipendente per i dipendenti con cognome hello archiviati in hello **RowKey**.  

Con l'opzione terzo hello, è possibile utilizzare EGTs toomaintain coerenza perché sono entità indice hello in una partizione separata dall'entità employee hello. È necessario assicurarsi che le entità di indice hello sono alla fine coerente con l'entità dipendente hello.  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* Questa soluzione richiede almeno due query tooretrieve corrispondenti entità: uno tooquery hello indice tooobtain hello elenco entità di **RowKey** valori e quindi esegue una query tooretrieve ogni entità nell'elenco di hello.  
* Dato che una singola entità è una dimensione massima di 1 MB, opzione #2 e l'opzione #3 nella soluzione hello presuppone elenco hello di ID dipendente per un determinato cognome non è mai maggiore di 1 MB. Se hello elenco di ID dipendente toobe probabilmente maggiore di 1 MB di dimensioni, utilizzare l'opzione #1 e archiviare i dati dell'indice hello nell'archiviazione blob.  
* Se si utilizza l'opzione #2 (tramite EGTs toohandle aggiunta e l'eliminazione di dipendenti e modifica il cognome del dipendente) è necessario valutare se il volume di hello di transazioni raggiungeranno limiti di scalabilità hello in una determinata partizione. In caso di hello, considerare una soluzione alla fine coerente (opzione &#1; o #3) che usa code toohandle hello update richieste e consente di toostore le entità di indice in una partizione separata dall'entità employee hello.  
* Opzione #2 in questa soluzione si presuppone che si desidera ripristinare toolook in base al cognome in un reparto: ad esempio, si desidera un elenco di dipendenti con un cognome Jones nel reparto vendite hello tooretrieve. Se si desidera toobe toolook in grado di backup di tutti i dipendenti il cui cognome Jones intera organizzazione hello hello, utilizzare l'opzione &#1; o #3.
* È possibile implementare una soluzione basata su coda che offre la coerenza eventuale (vedere hello [modello alla fine coerente transazioni](#eventually-consistent-transactions-pattern) per altri dettagli).  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando si desidera un set di entità che condividono un valore di proprietà comuni, ad esempio tutti i dipendenti con cognome hello Jones toolookup.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Modello per chiave composta](#compound-key-pattern)  
* [Modello per transazioni con coerenza finale](#eventually-consistent-transactions-pattern)  
* [Transazioni dei gruppi di entità](#entity-group-transactions)  
* [Uso di tipi di entità eterogenei](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>Modello di denormalizzazione
Combinare i dati correlati in una singola entità di tooenable tooretrieve tutti hello è necessario con una query con singolo punto dati.  

#### <a name="context-and-problem"></a>Contesto e problema
In un database relazionale, è in genere possibile normalizzare la duplicazione dei tooremove dati risultanti in query che recuperano dati da più tabelle. Se si esegue la normalizzazione dei dati in tabelle di Azure, è necessario apportare più round trip da hello client toohello server tooretrieve i dati correlati. Ad esempio, con la struttura di tabella hello illustrato di seguito è necessario due round trip tooretrieve hello dettagli un reparto: entità reparto di hello uno toofetch che include l'id del responsabile hello e i dettagli di gestione quindi un'altra richiesta toofetch hello in un dipendente entità.  

![][16]

#### <a name="solution"></a>Soluzione
Invece di archiviare dati hello in due entità separate, denormalizzare dati hello e conservare una copia dei dettagli del gestore hello in entità reparto hello. ad esempio:  

![][17]

Con entità reparto archiviate con queste proprietà, è ora possibile recuperare tutti i dettagli di hello che necessarie su un reparto utilizzando una query del punto.  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* Archiviare alcuni dati due volte comporta un aumento dei costi. miglioramento delle prestazioni (risultante dal servizio di archiviazione di un numero inferiore richieste toohello) in genere Hello supera l'incremento marginale hello dei costi di archiviazione (e il costo dell'offset parzialmente con una riduzione del numero di hello di transazioni si richiedono i dettagli di hello toofetch di un reparto).  
* È necessario mantenere la coerenza di hello di due entità hello che archiviano informazioni sui Manager. È possibile gestire il problema di coerenza hello utilizzando EGTs tooupdate più entità in una singola transazione atomica: in questo caso, vengono archiviati entità reparto hello ed entità employee hello responsabile del reparto hello in hello stessa partizione.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando è spesso necessario toolook le informazioni correlate. Questo modello consente di ridurre il numero di hello di query, per che il client deve effettuare tooretrieve hello i dati che necessari.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Modello per chiave composta](#compound-key-pattern)  
* [Transazioni dei gruppi di entità](#entity-group-transactions)  
* [Uso di tipi di entità eterogenei](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>Modello per chiave composta
Utilizzare composta **RowKey** tooenable valori toolookup un client relativi dati con un singolo punto di query.  

#### <a name="context-and-problem"></a>Contesto e problema
In un database relazionale, è piuttosto naturale toouse join nelle query tooreturn relative parti del client toohello dati in una singola query. Ad esempio, è possibile utilizzare hello employee id toolook un elenco di entità correlate che contengono le prestazioni ed esaminare i dati per il dipendente.  

Si supponga che l'entità dipendente vengono archiviati nel servizio tabelle hello utilizzando hello seguente struttura:  

![][18]

È inoltre necessario toostore dati cronologici relativi tooreviews e prestazioni per ogni dipendente hello anno ha lavorato per l'organizzazione e necessario tooaccess in grado di toobe queste informazioni per anno. Un'opzione è toocreate un'altra tabella che contiene le entità con hello seguente struttura:  

![][19]

Si noti che con questo approccio si potrebbero decidere tooduplicate alcune informazioni (ad esempio nome e cognome) hello nuova entità tooenable si tooretrieve i dati con una singola richiesta. Tuttavia, non è possibile garantire la coerenza sicura perché non è possibile utilizzare un due entità hello tooupdate EGT in modo atomico.  

#### <a name="solution"></a>Soluzione
Archiviare un nuovo tipo di entità nella tabella originale con entità hello seguente struttura:  

![][20]

Si noti come hello **RowKey** è ora una chiave composta costituita da id dipendente hello e anno hello dati revisione hello che consente di tooretrieve hello delle prestazioni del dipendente ed esaminare i dati con una singola richiesta per una singola entità.  

Hello di esempio seguente viene illustrato come recuperare tutti i dati di revisione hello per un dipendente specifico (ad esempio employee 000123 nel reparto vendite hello):  

$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* È consigliabile utilizzare un carattere separatore appropriato che rende facile tooparse hello **RowKey** valore: ad esempio, **000123_2012**.  
* Questa entità vengono inoltre archiviati nella stessa partizione delle altre entità che contengono dati correlati per hello hello stesso dipendente, pertanto è possibile utilizzare EGTs toomaintain la coerenza assoluta.
* È necessario considerare la frequenza si richiederà hello dati toodetermine se questo modello è appropriato.  Ad esempio, se è necessario accedere hello raramente data di revisione e hello principale i dati dei dipendenti spesso che deve essere conservato come entità separate.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando è necessario toostore uno o più entità correlate ai cui si eseguono query frequentemente.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Transazioni dei gruppi di entità](#entity-group-transactions)  
* [Uso di tipi di entità eterogenei](#working-with-heterogeneous-entity-types)  
* [Modello per transazioni con coerenza finale](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>Modello della parte finale del log
Recuperare hello  *n*  le entità aggiunte più di recente tooa partizione utilizzando un **RowKey** valore che ordina in data inversa e l'ordine temporale.  

#### <a name="context-and-problem"></a>Contesto e problema
Un requisito comune è in grado di tooretrieve entità hello creato di recente, ad esempio hello dieci più recente di rimborso spese inviata da un dipendente. Supporto di una query nella tabella un **$top** hello tooreturn operazione di query prima  *n*  entità da un set: non vi è nessuna query equivalente operazione tooreturn hello ultimi n entità in un set.  

#### <a name="solution"></a>Soluzione
Le entità hello archivio utilizzando un **RowKey** che naturalmente Ordina in senso inverso data/ora ordine utilizzando in modo che la voce più recente di hello è sempre hello presente nella tabella hello.  

Ad esempio, tooretrieve in grado di toobe hello dieci più recente di rimborso spese inviata da un dipendente, è possibile utilizzare un valore di apice inverso derivato da hello data/ora corrente. Hello c# esempio seguente viene illustrato un modo toocreate un valore di "invertito segni di graduazione" appropriato per un **RowKey** che ordina da hello più recente toohello meno recente:  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

È possibile ottenere il valore del tempo data toohello tramite hello seguente codice:  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

query di tabella Hello è simile al seguente:  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* È necessario aggiungere il valore di apice inverso hello con zeri iniziali valore di stringa hello tooensure Ordina come previsto.  
* È necessario essere consapevoli di obiettivi di scalabilità hello a livello di hello di una partizione. Fare attenzione a non creare partizioni critiche.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando è necessario tooaccess entità in ordine inverso di data/ora o quando è necessario più di recente hello tooaccess aggiunto le entità.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Anti-modello prepend/append](#prepend-append-anti-pattern)  
* [Recupero di entità](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>Modello di eliminazione volume elevato
Abilitare l'eliminazione di hello di un volume elevato di entità mediante l'archiviazione di tutte le entità hello per l'eliminazione simultanea nella tabella propria separata. eliminare le entità hello tabella hello.  

#### <a name="context-and-problem"></a>Contesto e problema
Molte applicazioni eliminare i dati obsoleti che non necessita più dell'applicazione client di toobe tooa disponibile o che un'applicazione hello è archiviato il supporto di archiviazione tooanother. È in genere identificare tali dati da una data: ad esempio, si dispone di un record di toodelete requisito di tutte le richieste di accesso di più di 60 giorni.  

Uno schema possibili è toouse hello data e ora della richiesta di accesso hello in hello **RowKey**:  

![][21]

Questo approccio evita hotspot partizione perché un'applicazione hello può inserire ed eliminare entità di account di accesso per ogni utente in una partizione separata. Tuttavia, questo approccio può essere costoso e molto tempo se si dispone di un numero elevato di entità perché è necessario innanzitutto tooperform una scansione di tabella in ordine tooidentify tutti hello entità toodelete e quindi è necessario eliminare ogni entità precedente. Si noti che è possibile ridurre il numero di hello di round trip toohello server necessarie toodelete hello precedente entità suddividendo in batch più richieste di eliminazione in EGTs.  

#### <a name="solution"></a>Soluzione
Usare una tabella separata per ogni giorno di tentativi di accesso. Quando si inseriscono entità e l'eliminazione di entità precedente è ora sufficiente una domanda di eliminazione di una tabella di ogni giorno, è possibile utilizzare progettazione entità hello sopra hotspot tooavoid (una singola operazione di archiviazione) invece di ricerca e all'eliminazione di centinaia di migliaia di entità di singoli account di accesso ogni giorno.  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* Il progetto supporta altri modi in cui l'applicazione utilizzerà dati hello, ad esempio la ricerca di entità specifica, il collegamento con altri dati o generare informazioni di aggregazione?  
* La progettazione consente di evitare hotspot durante l'inserimento di nuove entità?  
* Prevedere un ritardo se si desidera tooreuse hello stesso nome di tabella dopo l'eliminazione. È meglio i nomi di tabella univoco di utilizzare tooalways.  
* È probabile che alcune la limitazione delle richieste quando si usa una nuova tabella mentre hello del servizio tabelle apprende i modelli di accesso hello e distribuisce le partizioni hello tra i nodi. È necessario considerare la frequenza con cui è necessario toocreate nuove tabelle.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando si dispone di un volume elevato di entità che è necessario eliminare in hello contemporaneamente.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Transazioni dei gruppi di entità](#entity-group-transactions)
* [Modifica di entità](#modifying-entities)  

### <a name="data-series-pattern"></a>Modello di serie di dati
Archivio dati completo serie in un numero di hello toominimize singola entità richieste di effettuate.  

#### <a name="context-and-problem"></a>Contesto e problema
Uno scenario comune è per un'applicazione toostore una serie di dati che è in genere necessario tooretrieve tutti contemporaneamente. L'applicazione potrebbe ad esempio, registrare il numero di messaggi di messaggistica immediata ogni dipendente invia ogni ora e quindi utilizzare questa tooplot informazioni il numero di messaggi inviati da ogni utente in hello 24 ore precedenti. Uno schema potrebbe essere toostore 24 entità per ogni dipendente:  

![][22]

Con questa struttura, si possono individuare e aggiornare hello entità tooupdate per ogni dipendente, ogni volta che un'applicazione hello deve tooupdate valore del conteggio messaggio hello. Tuttavia, tooretrieve hello informazioni tooplot un grafico delle attività di hello per hello 24 ore precedenti, è necessario recuperare 24 entità.  

#### <a name="solution"></a>Soluzione
Utilizzare hello seguente struttura con un numero di messaggi hello toostore proprietà separata per ogni ora:  

![][23]

Con questa struttura, è possibile utilizzare un numero di messaggi hello tooupdate operazione di merge per un dipendente per un'ora specifica. A questo punto, è possibile recuperare tutte le informazioni di hello occorre grafico hello tooplot usando una richiesta per una singola entità.  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* Se la serie di dati completo non è sufficiente una singola entità (un'entità può avere proprietà too252), utilizzare un archivio di dati alternativi, ad esempio un blob.  
* Se si dispone di più client contemporaneamente l'aggiornamento di un'entità, sarà necessario hello toouse **ETag** tooimplement la concorrenza ottimistica. Se si dispone di molti client, potrebbe verificarsi un conflitto elevato.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando è necessario tooupdate e recuperare una serie di dati associata a una singola entità.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Modello di entità di grandi dimensioni](#large-entities-pattern)  
* [Unione o sostituzione](#merge-or-replace)  
* [Il modello alla fine coerente transazioni](#eventually-consistent-transactions-pattern) (se si archiviano serie di dati hello in un blob)  

### <a name="wide-entities-pattern"></a>Modello di entità di grandi dimensioni
Utilizzare come entità logiche più entità fisiche toostore con più di 252 proprietà.  

#### <a name="context-and-problem"></a>Contesto e problema
Una singola entità può disporre di proprietà non deve superare 252 (escluse le proprietà del sistema obbligatorio hello) e non è possibile archiviare più di 1 MB di dati in totale. In un database relazionale, è in genere ottenuto round eventuali limiti di dimensioni hello di una riga aggiunta una nuova tabella e a imporre una relazione 1 a 1 tra di essi.  

#### <a name="solution"></a>Soluzione
Utilizzo del servizio tabelle hello, è possibile archiviare più entità toorepresent un oggetto di business di grandi dimensioni con più di 252 proprietà. Ad esempio, se si desidera toostore hello numero di messaggi immediati inviati da ogni dipendente per hello ultimi 365 giorni, è possibile utilizzare hello seguito progettazione che usa due entità con schemi diversi:  

![][24]

Se è necessario toomake una modifica che richiede l'aggiornamento sia tookeep entità li sincronizzati con l'altro è possibile utilizzare un EGT. In caso contrario, è possibile utilizzare un numero di messaggi di unione singola operazione tooupdate hello per un giorno specifico. tooretrieve tutti hello dati per un singolo dipendente, è necessario recuperare entrambe le entità, che è possibile eseguire con due richieste efficiente di utilizzano sia un **PartitionKey** e **RowKey** valore.  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* Recupero di un'entità logica completa richiede almeno due transazioni di archiviazione: entità fisica uno tooretrieve.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando è necessario toostore entità la cui dimensione o il numero di proprietà supera i limiti di hello per una singola entità in hello servizio tabelle.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Transazioni dei gruppi di entità](#entity-group-transactions)
* [Unione o sostituzione](#merge-or-replace)

### <a name="large-entities-pattern"></a>Modello di entità di grandi dimensioni
Utilizzare valori di proprietà di grandi dimensioni toostore archiviazione blob.  

#### <a name="context-and-problem"></a>Contesto e problema
Una singola entità non può memorizzare più di 1 MB di dati in totale. Se una o più delle proprietà di archiviare i valori che determinano questo valore di dimensione totale di hello di tooexceed l'entità, è possibile archiviare l'intera entità hello in hello del servizio tabelle.  

#### <a name="solution"></a>Soluzione
Se l'entità supera 1 MB di dimensioni perché una o più proprietà contengono una grande quantità di dati, è possibile archiviare i dati nel servizio Blob hello e quindi archiviare indirizzo hello del blob hello in una proprietà nell'entità hello. Ad esempio, è possibile archiviare foto hello di un dipendente nell'archiviazione blob e archiviare una foto toohello collegamento in hello **foto** proprietà dell'entità dipendente:  

![][25]

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* la coerenza eventuale toomaintain tra entità hello in hello del servizio tabelle e dati hello hello servizio Blob, utilizzare hello [modello alla fine coerente transazioni](#eventually-consistent-transactions-pattern) toomaintain le entità.
* Recupero di un'entità completa richiede almeno due transazioni di archiviazione: un'entità di hello tooretrieve e hello un tooretrieve blob di dati.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Utilizzare questo modello quando è necessario toostore entità la cui dimensione supera i limiti di hello per una singola entità nel servizio tabelle hello.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Modello per transazioni con coerenza finale](#eventually-consistent-transactions-pattern)  
* [Modello di entità di grandi dimensioni](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>Anti-modello prepend/append
Aumentare la scalabilità quando si dispone di un volume elevato di inserimenti distribuendo hello inserimenti tra più partizioni.  

#### <a name="context-and-problem"></a>Contesto e problema
Anteponendo o l'aggiunta di entità di entità tooyour archiviati in genere comporta l'aggiunta di nuove entità toohello innanzitutto un'applicazione hello o l'ultima partizione di una sequenza di partizioni. In questo caso, tutti gli inserimenti hello in qualsiasi momento vengono eseguite nella stessa partizione, la creazione di un'area sensibile che impedisce che il bilanciamento del carico del servizio tabelle hello inserisce in più nodi hello e causando la scalabilità dell'applicazione toohit hello destinazioni per partizione. Ad esempio, se si dispone di un'applicazione che accedono a risorse e rete registri dai dipendenti, quindi potrebbe causare una struttura di entità, come illustrato di seguito hello partizione dell'ora corrente diventi un punto di accesso se il volume di hello delle transazioni raggiunge l'obiettivo di scalabilità hello per una singola partizione:  

![][26]

#### <a name="solution"></a>Soluzione
Hello struttura entità alternativa seguente consente di evitare un'area sensibile in qualsiasi partizione specifica come i log eventi dell'applicazione hello:  

![][27]

Si noti con questo esempio come entrambi hello **PartitionKey** e **RowKey** sono chiavi composte. Hello **PartitionKey** Usa reparto hello e registrazione di hello toodistribute id dipendente tra più partizioni.  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide di hello come tooimplement questo modello:  

* Fa hello chiave struttura alternativa che evita la creazione di partizioni di frequente operazioni di inserimento in modo efficiente query per il supporto hello rende l'applicazione client?  
* Il volume previsto di transazioni significa che sono probabilmente tooreach obiettivi di scalabilità hello per una singola partizione e di essere limitate dal servizio di archiviazione hello?  

#### <a name="when-toouse-this-pattern"></a>Quando toouse questo modello
Evitare hello accodare o anteporre anti-pattern quando il volume di transazioni è probabilmente tooresult di limitazione dal servizio di archiviazione hello quando si accede a una partizione a caldo.  

#### <a name="related-patterns-and-guidance"></a>Modelli correlati e informazioni aggiuntive
Hello modelli e le indicazioni seguenti possono anche essere importanti quando si implementa il pattern di:  

* [Modello per chiave composta](#compound-key-pattern)  
* [Modello della parte finale del log](#log-tail-pattern)  
* [Modifica di entità](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>Anti-modello dei dati di log
In genere, è consigliabile utilizzare hello servizio Blob anziché hello dati del log toostore servizio tabella.  

#### <a name="context-and-problem"></a>Contesto e problema
Caso di utilizzo comune per i dati di log sono tooretrieve una selezione di voci di log per un intervallo di data/ora specifico: ad esempio, si desidera toofind tutti hello messaggi di errore e critico che ha registrato l'applicazione dal 15:04 / 15:06 in una data specifica. Non si desidera toouse hello data e ora della partizione hello hello log messaggio toodetermine si salva entità log: che i risultati in una partizione di frequente perché in qualsiasi momento, tutte le entità di log hello condivideranno hello stesso **PartitionKey** valore (vedere la sezione hello [accodare o anteporre anti-pattern](#prepend-append-anti-pattern)). Ad esempio, hello segue lo schema dell'entità per un messaggio di log comporta una partizione di frequente perché un'applicazione hello scrive tutti i messaggi di log partizione toohello per hello data e ora:  

![][28]

In questo esempio hello **RowKey** include hello data e ora di hello log messaggio tooensure che i messaggi di log vengono archiviati in ordine di data/ora e un id di messaggio nel caso in cui più messaggi di log condividono hello stessa data e ora.  

Un altro approccio consiste toouse un **PartitionKey** che assicura che un'applicazione hello scrive i messaggi in un intervallo di partizioni. Ad esempio, se origine hello del messaggio registro hello fornisce un modo toodistribute messaggi in più partizioni, è possibile utilizzare hello segue lo schema dell'entità:  

![][29]

Tuttavia, il problema di hello con questo schema è che tooretrieve tutti i messaggi di log per un periodo di tempo specifico è necessario eseguire la ricerca di hello ogni partizione nella tabella hello.

#### <a name="solution"></a>Soluzione
Hello precedente sezione evidenziata hello problema di toouse hello voci di log toostore servizio tabella e due, insoddisfacenti suggerito, progettazioni. Una soluzione ha portata tooa a caldo di partizione con il rischio di hello di una riduzione delle prestazioni di scrittura di messaggi di log. Hello altre soluzioni ha restituito le prestazioni delle query a causa di hello requisito tooscan ogni partizione in hello tabella tooretrieve log i messaggi per un periodo di tempo specifico. Archiviazione BLOB offre una soluzione migliore per questo tipo di scenario e si tratta di Azure come archiviazione Analitica archivia hello log i dati vengono raccolti.  

Questa sezione descrive come archiviazione Analitica archivia i dati del log nell'archiviazione blob come un'illustrazione di questi dati toostoring approccio che si esegue una query in genere dall'intervallo.  

Analisi archiviazione archivia i messaggi di log in un formato delimitato in più BLOB. formato delimitato Hello semplifica per un client dati hello tooparse dell'applicazione nel messaggio hello del registro.  

Archiviazione Analitica utilizza una convenzione di denominazione per i blob che permette di blob hello di toolocate (o BLOB) che contengono messaggi hello del registro che sta cercando. Ad esempio, un blob denominato "queue/2014/07/31/1800/000001.log" contiene i messaggi di log correlati toohello servizio di Accodamento per ora hello a partire da 18:00 del 31 luglio 2014. Hello "000001" indica che questo è il primo file di log hello per questo periodo. Archiviazione Analitica registra inoltre innanzitutto hello timestamp di hello e ultimo log i messaggi archiviati nel file hello come parte dei metadati del blob hello. Hello API per consente di archiviazione blob individuare i BLOB in un contenitore in base a un prefisso del nome: toolocate tutti i BLOB contenenti coda hello registrare i dati per ora hello a partire da 18:00, è possibile usare hello prefisso "coda/2014/07/31/1800."  

Archiviazione Analitica buffer internamente i messaggi di log e quindi aggiorna periodicamente blob appropriato hello o crea uno nuovo con l'ultimo batch di hello di voci di log. Questo riduce il numero di hello servizio blob toohello deve eseguire operazioni di scrittura.  

Se si implementa una soluzione simile nella propria applicazione, è necessario considerare come toomanage hello compromesso tra l'affidabilità (scrittura ogni archiviazione tooblob voce di log in questo caso) e i costi e scalabilità (memorizzazione nel buffer gli aggiornamenti dell'applicazione e memorizzarli tooblob archiviazione in batch).  

#### <a name="issues-and-considerations"></a>Considerazioni e problemi
Considerare i seguenti punti quando si decide la modalità di registrazione dei dati toostore hello:  

* Se si crea una progettazione di tabella che consente di evitare potenziali partizioni critiche, è possibile che non si possa accedere ai dati di log in modo efficiente.  
* tooprocess registrare i dati, un client deve spesso tooload numero di record.  
* Nonostante i dati di log siano spesso strutturati, l'archiviazione BLOB può essere una soluzione migliore.  

### <a name="implementation-considerations"></a>Considerazioni sull'implementazione
In questa sezione vengono illustrati alcuni toobear considerazioni hello in considerazione quando si implementa il pattern hello descritto nelle sezioni precedenti hello. La maggior parte di questa sezione utilizza esempi scritti in c# che utilizzano la libreria Client di archiviazione (versione 4.3.0 in fase di scrittura di hello) hello.  

### <a name="retrieving-entities"></a>Recupero di entità
Come illustrato nella sezione hello [progettazione per l'esecuzione di query](#design-for-querying), query più efficiente hello è un punto. Tuttavia, in alcuni scenari potrebbe essere tooretrieve più entità. Questa sezione descrive alcune entità di tooretrieving approcci comuni utilizzando hello libreria Client di archiviazione.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Esegue una query di punto utilizzando hello libreria Client di archiviazione
tooexecute delle modalità più semplice una query del punto di Hello è hello toouse **recuperare** operazione di tabella, come illustrato nell'hello seguente frammento di codice c# che recupera un'entità con un **PartitionKey** del valore "Sales" e un  **RowKey** del valore "212":  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

Si noti come entità hello è previsto in questo esempio viene recuperato toobe di tipo **EmployeeEntity**.  

#### <a name="retrieving-multiple-entities-using-linq"></a>Recupero di più entità usando LINQ
È possibile recuperare più entità usando LINQ con la libreria client di archiviazione e specificando una query con una clausola **where** . tooavoid una scansione di tabella, è necessario includere sempre hello **PartitionKey** valore hello dove clausola e se possibile hello **RowKey** valore tooavoid scansioni di tabella e di partizione. Hello del servizio tabelle supporta un set limitato di toouse (maggiore di, maggiore o uguale a, minore di, minore o uguale, uguale e non uguale) gli operatori di confronto in hello dove clausola. Hello seguente frammento di codice c# consente di individuare tutti i dipendenti hello il cui cognome inizia con "B" (presupponendo che hello **RowKey** archivi hello cognome) nel reparto vendite hello (presupponendo che hello **PartitionKey** Archivia il nome di reparto hello):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

Si noti come query hello specifica sia un **RowKey** e **PartitionKey** tooensure ottenere prestazioni migliori.  

Hello nell'esempio di codice seguente viene illustrata una funzionalità equivalente utilizzando l'API fluent hello (per ulteriori informazioni sulle API fluent in generale, vedere [le procedure consigliate per la progettazione di un'API intuitiva](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> esempio Hello nidifica più **CombineFilters** tooinclude metodi hello tre condizioni di filtro.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>Recupero di un numero elevato di entità da una query
Una query ottimale restituisce una singola entità in base a un valore **PartitionKey** e a un valore **RowKey**. Tuttavia, in alcuni scenari potrebbe essere un requisito tooreturn molte entità da hello stessa partizione o anche dal numero di partizioni.  

In questi scenari, è consigliabile testare sempre completamente hello delle prestazioni dell'applicazione.  

Una query sul servizio tabella hello può restituire un massimo di 1.000 entità contemporaneamente e può essere eseguita per un massimo di cinque secondi. Se il set di risultati hello contiene più di 1.000 entità, se hello query non viene completata entro cinque secondi, o se la query hello supera il limite di partizione hello, hello del servizio tabelle restituisce un tooenable token di continuazione hello hello toorequest di applicazione client set successivo di entità. Per altre informazioni sul funzionamento dei token di continuazione, vedere [Timeout e paginazione delle query](http://msdn.microsoft.com/library/azure/dd135718.aspx).  

Se si utilizza hello libreria Client di archiviazione, può automaticamente gestire i token di continuazione per l'utente che restituisca le entità da hello del servizio tabelle. Hello c# codice riportato di seguito utilizzando hello libreria Client di archiviazione automaticamente gestisce i token di continuazione del servizio tabelle hello li restituisce in una risposta:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

codice c# seguente Hello gestisce i token di continuazione in modo esplicito:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

Tramite i token di continuazione in modo esplicito, è possibile controllare quando l'applicazione recupera successivo segmento di dati di hello. Ad esempio, se l'applicazione client consente agli utenti toopage tramite le entità hello archiviati in una tabella, un utente può decidere non toopage tramite tutte le entità hello recuperati dalla query di hello quindi l'applicazione solo utilizzato successivamente un hello tooretrieve token di continuazione segmento quando hello utente ha terminato il paging di tutte le entità hello nel segmento corrente hello. Questo approccio offre diversi vantaggi:  

* Consente di quantità di hello toolimit di tooretrieve dati dal servizio tabelle hello e che si sposta sulla rete hello.  
* In questo modo si tooperform IO asincroni in .NET.  
* Consente di archiviazione di token toopersistent tooserialize hello continuazione in modo è possibile continuare in caso di hello di un arresto anomalo dell'applicazione.  

> [!NOTE]
> Un token di continuazione in genere restituisce un segmento contenente al massimo 1.000 entità. Ciò avviene anche hello se si limita il numero di hello di voci di una query restituisce utilizzando **richiedere** tooreturn hello primo n entità che soddisfano i criteri di ricerca: servizio tabella hello può restituire un segmento contenente meno di n entità lungo con un tooenable token di continuazione è tooretrieve hello entità rimanenti.  
> 
> 

Hello codice c# seguente viene illustrato come numero di hello toomodify di entità restituito all'interno di un segmento:  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>Proiezione lato server
Una singola entità può avere le proprietà too255 e di dimensioni too1 MB. Quando si esegue una query tabella hello e recuperare le entità, si potrebbe non essere necessario tutte le proprietà di hello e possibile evitare il trasferimento dei dati inutilmente (toohelp ridurre la latenza e costo). È possibile utilizzare le proprietà di hello solo tootransfer proiezione sul lato server che è necessario. Hello riportato di seguito è recupera solo hello **posta elettronica** proprietà (insieme a **PartitionKey**, **RowKey**, **Timestamp**e  **ETag**) dalle entità hello selezionata dalla query hello.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

Si noti come hello **RowKey** valore è disponibile anche se non è stato incluso nell'elenco di hello di tooretrieve di proprietà.  

### <a name="modifying-entities"></a>Modifica di entità
Libreria Client di archiviazione Hello consente toomodify le entità archiviate nel servizio di tabella hello da inserimento, eliminazione e aggiornamento di entità. È possibile utilizzare EGTs toobatch più insert, update e le operazioni di eliminazione numero hello tooreduce insieme di round trip necessari e migliorare le prestazioni di hello della soluzione.  

Si noti che le eccezioni generate quando hello libreria Client di archiviazione viene eseguito un EGT in genere includono indice hello dell'entità di hello che ha provocato hello batch toofail. Ciò è utile quando si esegue il debug di codice che usa le transazioni EGT.  

È inoltre opportuno considerare l'influenza della progettazione sul modo in cui l'applicazione gestisce le operazioni di concorrenza e aggiornamento.  

#### <a name="managing-concurrency"></a>Gestione della concorrenza
Per impostazione predefinita, il servizio di tabella hello implementa i controlli di concorrenza ottimistica a livello di hello di singole entità per **inserire**, **Merge**, e **eliminare** operazioni, Sebbene sia possibile per un messaggi hello del client tooforce tabella toobypass servizio questi controlli. Per ulteriori informazioni sulle modalità di gestione della concorrenza del servizio tabelle hello, vedere [gestione della concorrenza in archiviazione di Microsoft Azure](storage-concurrency.md).  

#### <a name="merge-or-replace"></a>Unione o sostituzione
Hello **sostituire** metodo hello **TableOperation** classe sostituisce sempre un'entità completa hello, hello del servizio tabelle. Se non si include una proprietà nella richiesta di hello quando tale proprietà è presente in entità hello archiviato, richiesta hello rimuove proprietà hello archiviate entità. Se non si desidera tooremove una proprietà in modo esplicito da un'entità archiviata, è necessario includere tutte le proprietà nella richiesta di hello.  

È possibile utilizzare hello **Merge** metodo hello **TableOperation** quantità hello tooreduce di classe di dati che si invia servizio tabelle toohello quando si desidera tooupdate un'entità. Hello **Merge** metodo sostituisce qualsiasi proprietà nell'entità hello archiviato con i valori delle proprietà di entità hello incluse nella richiesta di hello, ma lascia invariati qualsiasi proprietà hello archiviati entità che non sono inclusi nella richiesta di hello. Ciò è utile se si dispone di entità di grandi dimensioni ed è solo necessario tooupdate un piccolo numero di proprietà in una richiesta.  

> [!NOTE]
> Hello **sostituire** e **Merge** metodi hanno esito negativo se hello entità non esiste. In alternativa, è possibile utilizzare hello **InsertOrReplace** e **InsertOrMerge** metodi che creano una nuova entità se non esiste.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>Uso di tipi di entità eterogenei
Hello del servizio tabelle è un *senza schema* archivio tabelle che significa che una singola tabella possa archiviare le entità di più tipi che fornisce una notevole flessibilità nella progettazione. Hello seguente esempio viene illustrata una tabella di archiviazione sia dipendente ed entità reparto:  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Si noti che ogni entità deve disporre comunque dei valori **PartitionKey**, **RowKey** e **Timestamp**, ma può avere qualsiasi set di proprietà. Inoltre, non è hello tooindicate tipo di un'entità, a meno che non si sceglie toostore tali informazioni in un punto. Sono disponibili due opzioni per identificare il tipo di entità hello:  

* Anteporre hello entità tipo toohello **RowKey** (o eventualmente hello **PartitionKey**). Ad esempio, **EMPLOYEE_000123** o **DEPARTMENT_SALES** come valori **RowKey**.  
* Utilizzare un tipo di entità di proprietà separata toorecord hello come illustrato nella tabella hello riportata di seguito.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>department</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

prima opzione Hello, anteponendo hello entità tipo toohello **RowKey**, è utile se è possibile che due entità di tipo diverso potrebbe avere hello stesso valore della chiave. Inoltre, raggruppa entità dello stesso tipo insieme nella partizione hello hello.  

le tecniche descritte in questa sezione Hello sono particolarmente rilevanti toohello discussione [le relazioni di ereditarietà](#inheritance-relationships) più indietro in questa Guida, nella sezione hello [modellazione relazioni](#modelling-relationships).  

> [!NOTE]
> È consigliabile includere un numero di versione nel hello tipo valore tooenable client applicazioni tooevolve POCO oggetti entità e utilizzare versioni diverse.  
> 
> 

Hello resto di questa sezione vengono descritte alcune delle funzionalità di hello hello libreria Client di archiviazione che semplificano l'utilizzo di più tipi di entità in hello stessa tabella.  

#### <a name="retrieving-heterogeneous-entity-types"></a>Recupero di tipi di entità eterogenei
Se si utilizza hello libreria Client di archiviazione, sono disponibili tre opzioni per l'utilizzo di più tipi di entità.  

Se si conosce il tipo di hello dell'entità hello archiviato con uno specifico **RowKey** e **PartitionKey** valori, è possibile specificare il tipo di entità hello quando si recupera entità hello, come illustrato negli esempi di hello due precedenti che consentono di recuperare le entità di tipo **EmployeeEntity**: [esegue una query di punto utilizzando hello libreria Client di archiviazione](#executing-a-point-query-using-the-storage-client-library) e [il recupero di più entità utilizzando LINQ](#retrieving-multiple-entities-using-linq).  

seconda opzione Hello è hello toouse **DynamicTableEntity** tipo (un contenitore di proprietà) anziché un tipo di entità POCO concreto (questa opzione può anche migliorare le prestazioni poiché non esiste alcuna necessità tooserialize e deserializzare troppo entità hello. Tipi di rete). Dopo il codice c# potenzialmente Hello recupera più entità di tipo diverso dalla tabella hello, ma restituisce tutte le entità come **DynamicTableEntity** istanze. Viene quindi utilizzato hello **EntityType** tipo hello toodetermine di proprietà di ogni entità:  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

Si noti che tooretrieve altre proprietà, è necessario utilizzare hello **TryGetValue** metodo hello **proprietà** proprietà di hello **DynamicTableEntity** classe.  

Una terza opzione è toocombine utilizzando hello **DynamicTableEntity** tipo e un **EntityResolver** istanza. In questo modo è tooresolve toomultiple POCO tipi hello stessa query. In questo esempio hello **EntityResolver** delegato utilizza hello **EntityType** toodistinguish proprietà tra i tipi di hello due entità che hello restituite dalla query. Hello **risolvere** metodo utilizza hello **resolver** delegato tooresolve **DynamicTableEntity** istanze troppo**TableEntity** istanze.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>Modifica dei tipi di entità eterogenei
Tipo di hello tooknow di toodelete un'entità non è necessario e si desidera conoscere sempre tipo hello di un'entità per l'inserimento. Tuttavia, è possibile utilizzare **DynamicTableEntity** digitare tooupdate un'entità senza conoscerne il tipo e senza utilizzare una classe di entità POCO. Hello nell'esempio di codice seguente recupera una singola entità e controlla hello **EmployeeCount** proprietà esiste prima dell'aggiornamento.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>Controllo dell'accesso con le firme di accesso condiviso
È possibile utilizzare toomodify applicazioni client di firma di accesso condiviso (SAS) token tooenable (e di query) entità tabella direttamente senza hello necessario tooauthenticate direttamente con il servizio tabella hello. In genere, sono disponibili tre vantaggi principali toousing SAS nell'applicazione:  

* Non è necessario toodistribute lo spazio di archiviazione account tooan chiave di piattaforma non protetta (ad esempio, un dispositivo mobile) in ordine tooallow tooaccess tale dispositivo e modificare le entità nel servizio tabelle hello.  
* È possibile trasferire una parte del lavoro hello che web e ruoli di lavoro di eseguire la gestione dei dispositivi tooclient entità, ad esempio computer degli utenti finali e i dispositivi mobili.  
* È possibile assegnare un vincolata e set di client tooa autorizzazioni (ad esempio per consentire l'accesso in sola lettura le risorse toospecific) limitate nel tempo.  

Per ulteriori informazioni sull'utilizzo di token di firma di accesso condiviso con hello del servizio tabelle, vedere [tramite firme di accesso condiviso (SAS)](storage-dotnet-shared-access-signature-part-1.md).  

Tuttavia, è comunque necessario generare token SAS hello che concedono l'entità toohello applicazione nel servizio tabelle hello un client: è necessario farlo in un ambiente che dispone di proteggere l'accesso alle chiavi dell'account di archiviazione tooyour. In genere, si utilizza un web o lavoro ruolo toogenerate hello SAS token e inviarli toohello le applicazioni client che devono accedere tooyour entità. Poiché non esiste ancora un overhead coinvolti nella generazione e il recapito tooclients i token di firma di accesso condiviso, è consigliabile tooreduce ottimale questo overhead, specialmente negli scenari con volumi elevati.  

È possibile toogenerate un token di firma di accesso condiviso che concede l'accesso tooa subset di entità hello in una tabella. Per impostazione predefinita, si crea un token di firma di accesso condiviso per un'intera tabella, ma è anche possibile toospecify che tooeither di accesso grant token SAS hello un intervallo di **PartitionKey** valori o un intervallo di **PartitionKey** e  **RowKey** valori. È possibile scegliere toogenerate i token di firma di accesso condiviso per i singoli utenti del sistema in modo che il token di firma di accesso condiviso di ciascun utente solo consente loro di accedere tootheir entità personalizzate in hello servizio tabelle.  

### <a name="asynchronous-and-parallel-operations"></a>Operazioni asincrone e parallele
A condizione che le richieste vengano distribuite in più partizioni, è possibile migliorare la velocità effettiva e la velocità di risposta del client usando le query parallele o asincrone.
Ad esempio, si potrebbero avere due o più istanze del ruolo di lavoro che accedono alle tabelle in parallelo. È possibile disporre di ruoli di lavoro singole responsabili particolare set di partizioni o semplicemente avere più istanze del ruolo di lavoro, ogni possibile tooaccess tutti hello partizioni in una tabella.  

All'interno di un'istanza del client, è possibile migliorare la velocità effettiva effettuando operazioni di archiviazione in modo asincrono. Libreria Client di archiviazione Hello rende modifiche e query asincrona toowrite semplice. Ad esempio, è possibile iniziare con metodo sincrono hello che recupera tutte le entità hello in una partizione, come illustrato nel seguente codice c# di hello:  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

È possibile modificare questo codice facilmente query hello con cui viene eseguito in modo asincrono come indicato di seguito:  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

In questo esempio asincrono, è possibile visualizzare le modifiche seguenti di hello dalla versione sincrona hello:  

* firma del metodo Hello include ora hello **async** modificatore e restituisce un **attività** istanza.  
* Anziché chiamare hello **ExecuteSegmented** tooretrieve risultati del metodo, hello metodo ora chiamate hello **ExecuteSegmentedAsync** hello metodo e viene utilizzato **await** modificatore tooretrieve comporta in modo asincrono.  

un'applicazione Hello client può chiamare questo metodo più volte (con valori diversi per hello **reparto** parametro), e ogni query verrà eseguita in un thread separato.  

Si noti che non è una versione asincrona di hello **Execute** metodo hello **TableQuery** classe perché hello **IEnumerable** interfaccia non supporta asincrona enumerazione.  

È inoltre possibile inserire, aggiornare ed eliminare entità in modo asincrono. Hello esempio c# seguente viene illustrato un metodo sincrono, semplice di tooinsert o sostituita un'entità dipendente:  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

È possibile modificare questo codice facilmente in modo che aggiornamento hello eseguito in modo asincrono come indicato di seguito:  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

In questo esempio asincrono, è possibile visualizzare le modifiche seguenti di hello dalla versione sincrona hello:  

* firma del metodo Hello include ora hello **async** modificatore e restituisce un **attività** istanza.  
* Anziché chiamare hello **Execute** entità hello tooupdate del metodo, hello metodo ora chiamate hello **ExecuteAsync** hello metodo e viene utilizzato **await** tooretrieve modificatore risultati in modo asincrono.  

un'applicazione Hello client può chiamare più metodi asincroni come questa, e ogni chiamata al metodo verrà eseguita in un thread separato.  

### <a name="credits"></a>Credits
Desideriamo hello toothank segue i membri del team di Azure per il loro contributo hello: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Shah Vinay Serdar Ozler nonché Tom Hollander da DX Microsoft. 

Desideriamo anche hello toothank seguente MVP di Microsoft per i commenti e suggerimenti utili durante i cicli di revisione: Igor Papirov e Edward Bakker.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

