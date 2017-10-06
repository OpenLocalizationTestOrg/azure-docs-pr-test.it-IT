---
title: aaaScaling out con il Database SQL di Azure | Documenti Microsoft
description: "Software come un sviluppatori del servizio (SaaS) può creare facilmente elastico, database scalabili in hello cloud utilizzando questi strumenti"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Aumentare il numero di istanze con il database SQL di Azure
È possibile ridimensionare il database di SQL Azure mediante hello **Database elastico** strumenti. Questi strumenti e funzionalità consentono di utilizzare hello virtualmente illimitata del database delle risorse di **Database SQL di Azure** toocreate soluzioni per carichi di lavoro transazionali e soprattutto il Software come applicazioni di servizio (SaaS). Funzionalità di Database elastiche sono costituite da seguente hello:

* [Libreria client di Database elastica](sql-database-elastic-database-client-library.md): libreria client hello è una funzionalità che consentono di toocreate e gestione database partizionati.  Vedere [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).
* [Strumento divisione-unione del database elastico](sql-database-elastic-scale-overview-split-and-merge.md): consente di spostare dati tra database partizionati. Ciò è utile per lo spostamento dei dati da un multi-tenant database tooa single-tenant database (o viceversa). Vedere [Esercitazione relativa allo strumento divisione-unione del database elastico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [I processi di Database elastici](sql-database-elastic-jobs-overview.md) (anteprima): utilizzare processi toomanage un numero elevato di database SQL di Azure. Consente di eseguire facilmente operazioni amministrative, ad esempio le modifiche dello schema, la gestione delle credenziali, gli aggiornamenti dei dati di riferimento, la raccolta dei dati sulle prestazioni o la raccolta di dati di telemetria tenant (cliente) utilizzando i processi.
* [Query di Database elastico](sql-database-elastic-query-overview.md) (anteprima): consente query toorun Transact-SQL che si estende su più database. In questo modo gli strumenti tooreporting di connessione, ad esempio Excel, Power BI, Tableau, e così via.
* [Transazioni elastiche](sql-database-elastic-transactions-overview.md): questa funzionalità consente transazioni toorun che si estendono su più database nel Database di SQL Azure. Le transazioni di database elastici sono disponibili per le applicazioni .NET tramite ADO .NET e integrate con hello familiarità esperienza di programmazione utilizzando hello [classi System. Transaction](https://msdn.microsoft.com/library/system.transactions.aspx).

grafico Hello riportato di seguito è illustrata un'architettura che include hello **le funzionalità di Database elastico** nella raccolta tooa relazione di database.

In questo grafico, i colori del database hello rappresentano gli schemi. Database con hello stessa condivisione di colori hello stesso schema.

1. Un set di **database SQL di Azure** è ospitato in Azure tramite l'architettura di partizionamento orizzontale.
2. Hello **libreria client di Database elastico** è impostato toomanage utilizzati una partizione.
3. Un subset dei database hello vengono inseriti in un **pool elastico**. Vedere l'articolo su [che cos'è un pool](sql-database-elastic-pool.md).
4. Un **Processo di database elastico** esegue gli script T-SQL pianificati o ad-hoc in tutti i database.
5. Hello **strumento di merge di divisione** toomove utilizzati dati da una partizione tooanother.
6. Hello **query di Database elastico** consente toowrite una query che si estende a tutti i database nel set di partizioni hello.
7. **Transazioni elastiche** consente transazioni toorun che si estendono su più database. 

![Strumenti di database elastici][1]

## <a name="why-use-hello-tools"></a>Perché utilizzare strumenti hello?
Il raggiungimento dell’elasticità e della scalabilità delle applicazioni cloud è stato semplice per le VM e l'archiviazione BLOB in quanto è bastato aggiungere o sottrarre le unità nonché aumentare la potenza. Tuttavia, resta una sfida per l’elaborazione dei dati con stato in database relazionali. Sfide emerse in questi scenari:

* Espansione e riduzione di capacità per la parte di un database relazionale hello del carico di lavoro.
* Gestione degli hotspot che potrebbero verificarsi interessando un subset specifico di dati, quali ad esempio clienti finali (tenant) particolarmente impegnati.

In genere, gli scenari simili sono stati risolti dotando applicazione hello toosupport server di database su larga scala. Tuttavia, questa opzione è limitata nel cloud hello in tutta l'elaborazione avviene su hardware di base predefiniti. Invece, la distribuzione dei dati e di elaborazione attraverso molti database strutturato in modo identico (un modello di scalabilità orizzontale noto come "partizionamento orizzontale") fornisce un'alternativa tootraditional approcci di scalabilità verticale sia in termini di costi ed elasticità.

## <a name="horizontal-and-vertical-scaling"></a>Scalabilità orizzontale e verticale
Hello seguente figura hello dimensioni orizzontali e verticali della scalabilità, che sono semplici hello i database elastici hello possono essere ridimensionati.

![Scalabilità orizzontale e verticale][2]

Scalabilità orizzontale si riferisce tooadding o la rimozione di database di ordine tooadjust capacità o prestazioni. Detta anche “scaling out”. Partizionamento orizzontale, in cui i dati vengono partizionati tra una raccolta di database in modo identico strutturati, è un comune tooimplement modo orizzontale scalabilità.  

La scalabilità verticale fa riferimento tooincreasing o diminuire il livello di prestazioni hello di un singolo database, questa è nota anche come "scalabilità verticale".

La maggior parte delle applicazioni di database su scala cloud utilizzano una combinazione di questi due strategie. Ad esempio, un'applicazione Software come un servizio può utilizzare orizzontale scala tooprovision nuovi clienti finali e scalabilità tooallow toogrow o compattazione le risorse del database fine-di ciascun cliente in base alle esigenze del carico di lavoro hello verticale.

* Scalabilità orizzontale viene gestita mediante hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md).
* La scalabilità verticale viene eseguita con livello di servizio hello toochange cmdlet PowerShell di Azure, oppure inserendo i database in un pool elastico.

## <a name="sharding"></a>Partizionamento orizzontale
*Partizionamento orizzontale* è una tecnica toodistribute grandi quantità di dati strutturati in modo identico in un numero di database indipendenti. È molto usato dagli sviluppatori cloud che creano offerte Software as a Service (SAAS) per clienti finali o aziende. Questi clienti finali sono spesso tooas cui "tenant". Il partizionamento orizzontale può essere necessario per vari motivi:  

* quantità totale di Hello di dati è troppo grande toofit entro i limiti di hello di un singolo database
* velocità effettiva delle transazioni Hello di hello carico di lavoro complessivo è superiore alle capacità di un singolo database hello
* Può essere necessario isolare fisicamente i tenant, quindi predisporre database separati per ogni tenant
* Diverse sezioni di un database potrebbe essere necessario tooreside in aree geografiche diverse per la conformità, prestazioni o per motivi di natura geopolitiche.

In altri scenari, ad esempio l'inserimento di dati dai dispositivi distribuiti, partizionamento orizzontale può essere utilizzato toofill un set di database che sono organizzate temporaneamente. Ad esempio, un database separato può essere dedicato tooeach giorno o settimana. In tal caso, la chiave di partizionamento orizzontale hello può essere una data di hello che rappresentano numero intero (presente in tutte le righe delle tabelle partizionate hello) e il recupero delle informazioni per un intervallo di date di query deve essere indirizzata da subset di toohello applicazione hello dei database relativi all'intervallo hello in domanda.

Partizionamento orizzontale funziona meglio quando tutte le transazioni in un'applicazione possono essere limitato tooa singolo valore di una chiave di partizionamento orizzontale. Che garantisce che tutte le transazioni locali tooa specifico database.

## <a name="multi-tenant-and-single-tenant"></a>Multi-tenant e single-tenant
Alcune applicazioni usano l'approccio più semplice hello di creazione di un database separato per ogni tenant. Si tratta di hello **il modello di partizionamento orizzontale single-tenant** che fornisce risorse scalabilità con granularità hello del tenant di hello, possibilità di backup/ripristino e isolamento. Con il partizionamento orizzontale single-tenant, ogni database è associato un valore di ID tenant specifico (o valore chiave cliente), ma tale chiave devono sempre essere presente nei dati hello stesso. È hello tooroute responsabilità dell'applicazione ogni richiesta toohello appropriata del database - e libreria client hello può semplificare l'operazione.

![Single-tenant e multi-tenant][4]

Altri scenari prevedono di riunire più tenant all'interno dei database, anziché isolarli in database separati. Si tratta di una tipica **modello di partizionamento orizzontale di multi-tenant** - e dovuta fatti hello che un'applicazione gestisce un numero elevato di tenant molto piccoli. Nel partizionamento orizzontale di multi-tenant, le righe di hello nelle tabelle di database hello sono che tutti progettati toocarry una chiave che identifica l'ID o il partizionamento orizzontale chiave del tenant di hello. Nuovamente, il livello di applicazione hello è responsabile per il database appropriato toohello richiesta di un tenant di routing e questo può essere supportato dalla libreria client di database elastico hello. Inoltre, la sicurezza a livello di riga può essere utilizzato toofilter quali righe di ogni tenant può accedere alle - per informazioni dettagliate, vedere [applicazioni multi-tenant con strumenti di database elastico e la sicurezza a livello di riga](sql-database-elastic-tools-multi-tenant-row-level-security.md). Ridistribuzione dei dati nei database potrebbe essere necessaria con il modello di partizionamento orizzontale di multi-tenant hello e questa operazione è facilitata dallo strumento di unione di menu combinato di database elastico hello. toolearn ulteriori informazioni sui modelli di progettazione per le applicazioni SaaS con i pool elastici, vedere [modelli di progettazione per le applicazioni SaaS multi-tenant con Database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>Spostare i dati da più database toosingle tenancy
Quando si crea un'applicazione SaaS, è tipico toooffer potenziali clienti una versione di valutazione di hello software. In questo caso, è conveniente toouse un database multi-tenant per i dati di hello. Tuttavia, quando un potenziale cliente diventa un cliente reale, è consigliabile utilizzare un database single-tenant, poiché garantisce prestazioni migliori. Se il cliente hello è stato creato dati durante il periodo di valutazione di hello, utilizzare hello [strumento di merge di divisione](sql-database-elastic-scale-overview-split-and-merge.md) dati hello toomove dal database di hello toohello multi-tenant nuovo single-tenant.

## <a name="next-steps"></a>Passaggi successivi
Per un'app di esempio che illustra la libreria client di hello, vedere [Introduzione agli strumenti di database elastico](sql-database-elastic-scale-get-started.md).

tooconvert esistente database strumenti hello toouse, vedere [esistenti di eseguire la migrazione di database tooscale-out](sql-database-elastic-convert-to-use-elastic-tools.md).

vedere le specifiche di hello toosee del pool elastico hello, [prezzo e considerazioni sulle prestazioni per un pool elastico](sql-database-elastic-pool.md), oppure creare un nuovo pool con [pool elastici](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

