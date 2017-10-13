---
title: Aumento del numero di istanze con il database SQL di Azure | Documentazione Microsoft
description: Gli sviluppatori di Software come Servizio (Saas) possono facilmente creare database elastici e scalabili nel cloud utilizzando questi strumenti
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
ms.openlocfilehash: 5bb6d17ffd047ae91476c52750f293414d1dfdd5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Aumentare il numero di istanze con il database SQL di Azure
È possibile aumentare facilmente il numero di istante dei database SQL di Azure con gli strumenti dei **database elastici** . Questi strumenti e funzionalità consentono di usare le risorse di database virtualmente illimitate di **Database SQL di Azure** per creare soluzioni per carichi di lavoro transazionali e soprattutto applicazioni SaaS (Software as a Service). Le funzioni di database elastico sono costituite dai seguenti elementi:

* [Libreria client dei database elastici](sql-database-elastic-database-client-library.md): la libreria client è una funzionalità che consente di creare e gestire i database partizionati.  Vedere [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).
* [Strumento divisione-unione del database elastico](sql-database-elastic-scale-overview-split-and-merge.md): consente di spostare dati tra database partizionati. Ciò è utile per lo spostamento di dati da un database multi-tenant in un database single-tenant (o viceversa). Vedere [Esercitazione relativa allo strumento divisione-unione del database elastico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [Processi di database elastico](sql-database-elastic-jobs-overview.md) (anteprima): utilizzare i processi per gestire un numero elevato di database SQL di Azure. Consente di eseguire facilmente operazioni amministrative, ad esempio le modifiche dello schema, la gestione delle credenziali, gli aggiornamenti dei dati di riferimento, la raccolta dei dati sulle prestazioni o la raccolta di dati di telemetria tenant (cliente) utilizzando i processi.
* [Query di database elastico](sql-database-elastic-query-overview.md) (anteprima): consente di eseguire una query Transact-SQL che si estende in più database. Tale query consente una connessione a strumenti di report, ad esempio Excel, PowerBI, Tableau e così via.
* [Transazioni di database elastico](sql-database-elastic-transactions-overview.md): questa funzionalità consente di eseguire transazioni estese a più database nel database SQL di Azure. Le transazioni di database elastico sono disponibili per le applicazioni .NET tramite ADO .NET e si integrano con i tipi di programmazione più diffusi grazie alle classi [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx).

Nel grafico seguente è illustrata un'architettura che include le **funzionalità dei database elastici** in relazione a una raccolta di database.

In questo grafico, i colori del database rappresentano gli schemi. I database con lo stesso colore condividono gli stessi schemi.

1. Un set di **database SQL di Azure** è ospitato in Azure tramite l'architettura di partizionamento orizzontale.
2. La **libreria client di database elastici** viene utilizzata per gestire un set di partizioni.
3. Un subset dei database viene inserito in un **pool elastico**. Vedere l'articolo su [che cos'è un pool](sql-database-elastic-pool.md).
4. Un **Processo di database elastico** esegue gli script T-SQL pianificati o ad-hoc in tutti i database.
5. Lo **strumento di suddivisione-unione** viene utilizzato per spostare i dati da una partizione a un’altra.
6. La **query di database elastico** consente di scrivere una query che si estende a tutti i database nel set di partizioni.
7. **Transazioni di database elastico** è una funzionalità che consente di eseguire transazioni che si estendono su più database. 

![Strumenti di database elastici][1]

## <a name="why-use-the-tools"></a>Perché usare gli strumenti?
Il raggiungimento dell’elasticità e della scalabilità delle applicazioni cloud è stato semplice per le VM e l'archiviazione BLOB in quanto è bastato aggiungere o sottrarre le unità nonché aumentare la potenza. Tuttavia, resta una sfida per l’elaborazione dei dati con stato in database relazionali. Sfide emerse in questi scenari:

* Aumento e riduzione della capacità per la parte del carico di lavoro relativa al database relazionale.
* Gestione degli hotspot che potrebbero verificarsi interessando un subset specifico di dati, quali ad esempio clienti finali (tenant) particolarmente impegnati.

In genere, questi scenari sono stati affrontati effettuando investimenti in server di database di scala maggiore per supportare l'applicazione. Questa opzione offre però possibilità limitate negli ambienti cloud, in cui l'intera elaborazione viene eseguita su appositi componenti hardware predefiniti. Invece, la distribuzione dei dati e l’elaborazione in molti database strutturati in modo identico (un modello di scalabilità orizzontale noto come "partizionamento orizzontale") fornisce un'alternativa agli approcci tradizionali di scalabilità verticale sia in termini di costi che di elasticità.

## <a name="horizontal-and-vertical-scaling"></a>Scalabilità orizzontale e verticale
Nella figura seguente vengono illustrate le dimensioni orizzontali e verticali della scalabilità, che sono i metodi di base in cui possono essere ridimensionati i database elastici.

![Scalabilità orizzontale e verticale][2]

Per scalabilità orizzontale si intende l’aggiunta o la rimozione di database per regolare le prestazioni complessive o la capacità. Detta anche “scaling out”. Il partizionamento orizzontale, in cui i dati vengono partizionati in una raccolta di database strutturati in modo identico, è un approccio comune per implementare la scalabilità orizzontale .  

Per scalabilità verticale si intende l’aumento o la riduzione del livello delle prestazioni di un singolo database ed è nota anche come "scaling up".

La maggior parte delle applicazioni di database su scala cloud utilizzano una combinazione di questi due strategie. Un'applicazione di software come servizio può, ad esempio, utilizzare la scalabilità orizzontale per eseguire il provisioning di nuovi clienti finali e la scalabilità verticale per consentire l’espansione o la riduzione delle risorse del database di ogni cliente finale in base alle esigenze del carico di lavoro.

* La scalabilità orizzontale è gestita tramite la [Libreria client di database elastici](sql-database-elastic-database-client-library.md).
* La scalabilità verticale viene eseguita con i cmdlet di Azure PowerShell per modificare il livello di servizio o posizionando i database in un pool elastico.

## <a name="sharding"></a>Partizionamento orizzontale
*Partizionamento orizzontale* è una tecnica per distribuire grandi quantità di dati strutturati in modo identico tra più database indipendenti. È molto usato dagli sviluppatori cloud che creano offerte Software as a Service (SAAS) per clienti finali o aziende. Questi clienti finali vengono spesso definiti "tenant". Il partizionamento orizzontale può essere necessario per vari motivi:  

* La quantità totale di dati è troppo elevata per un singolo database
* La velocità effettiva delle transazioni del carico di lavoro complessivo supera le capacità di un singolo database
* Può essere necessario isolare fisicamente i tenant, quindi predisporre database separati per ogni tenant
* È possibile che sezioni diverse di un database risiedano in aree geografiche diverse per motivi di conformità, di prestazioni o geopolitici.

In altri scenari, ad esempio l'inserimento di dati da dispositivi distribuiti, il partizionamento orizzontale può essere usato per riempire un set di database organizzati secondo una logica temporale. Ad esempio, è possibile destinare un database separato a ogni giorno o settimana. In tal caso, la chiave di partizionamento orizzontale può essere un integer che rappresenta la data (presente in tutte le righe delle tabelle partizionate) e l'applicazione deve instradare le query che recuperano informazioni per un intervallo di date al subset di database che coprono l'intervallo in questione.

Il partizionamento orizzontale rappresenta la scelta ottimale quando tutte le transazioni in un'applicazione possono essere limitate a un singolo valore di una chiave di partizionamento orizzontale. Questo garantisce che tutte le transazioni saranno locali rispetto a uno specifico database.

## <a name="multi-tenant-and-single-tenant"></a>Multi-tenant e single-tenant
Alcune applicazioni usano l'approccio più semplice di creare un database separato per ogni tenant. Questo è il **modello di partizionamento orizzontale per singolo tenant** , che offre isolamento, funzionalità di backup e ripristino e scalabilità delle risorse in base alla granularità del tenant. Con il partizionamento orizzontale per singolo tenant, ogni database è associato a uno specifico valore di ID tenant (o valore di chiave del cliente), ma tale chiave non deve essere necessariamente presente nei dati. È responsabilità dell'applicazione indirizzare ogni richiesta al database appropriato e la libreria client può semplificare questa operazione.

![Single-tenant e multi-tenant][4]

Altri scenari prevedono di riunire più tenant all'interno dei database, anziché isolarli in database separati. Si tratta di un **modello di partizionamento orizzontale multi-tenant** tipico e la scelta di un modello di questo tipo può essere dovuta al fatto che un'applicazione gestisce un numero elevato di tenant di dimensioni molto limitate. Nel partizionamento orizzontale multi-tenant, tutte le righe delle tabelle di database sono progettate per contenere una chiave che identifica l'ID tenant o una chiave di partizionamento orizzontale. Anche in questo caso, il livello applicazione è responsabile dell'instradamento delle richieste del tenant al database appropriato e questo può essere supportato dalla libreria client dei database elastici. Inoltre, la sicurezza a livello di riga può essere utilizzata per filtrare le righe a cui ogni tenant può accedere: per informazioni dettagliate, vedere [Applicazioni multi-tenant con strumenti di database elastici e sicurezza a livello di riga](sql-database-elastic-tools-multi-tenant-row-level-security.md). Con lo schema di partizionamento orizzontale multi-tenant potrebbe essere necessaria la ridistribuzione dei dati tra database e questa operazione è facilitata dallo strumento di suddivisione-unione dei database elastici. Per altre informazioni sui modelli di progettazione per le applicazioni SaaS mediante pool elastici, vedere [Modelli di progettazione per applicazioni SaaS multi-tenant con database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-to-single-tenancy-databases"></a>Spostare i dati da database a più tenancy a database a singolo tenancy
Quando si crea un'applicazione SaaS, in genere ai clienti potenziali viene offerta una versione di valutazione del software. In questo caso, è conveniente utilizzare un database multi-tenant per i dati. Tuttavia, quando un potenziale cliente diventa un cliente reale, è consigliabile utilizzare un database single-tenant, poiché garantisce prestazioni migliori. Se il cliente ha creato dati durante il periodo di valutazione, utilizzare lo [strumento di suddivisione-unione](sql-database-elastic-scale-overview-split-and-merge.md) per spostare i dati dal database multi-tenant al nuovo database single-tenant.

## <a name="next-steps"></a>Passaggi successivi
Per un'app di esempio che illustra la libreria client, vedere [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).

Per convertire i database esistenti e usare gli strumenti, vedere l'articolo sulla [migrazione dei database esistenti per aumentare il numero di istanze](sql-database-elastic-convert-to-use-elastic-tools.md).

Per visualizzare le specifiche del pool elastico, vedere [Considerazioni di prezzo e prestazioni per un pool elastico](sql-database-elastic-pool.md) oppure creare un nuovo pool con [pool elastici](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

