---
title: aaaLearn sulle operazioni di Azure SQL Data Warehouse | Documenti Microsoft
description: "L'elasticità di SQL Data Warehouse consente di aumentare, ridurre o sospendere la potenza di calcolo usando una scala scorrevole di unità data warehouse (DWU). Questo articolo illustra le metriche di hello data warehouse e come interagiscono tooDWUs. "
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 8be5ff6b14ab907e2b0a7eb55e0e2f4139aca8b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-workload"></a>Carico di lavoro del data warehouse
Un carico di lavoro data warehouse si riferisce tooall di operazioni di hello di in un data warehouse. il carico di lavoro di Hello data warehouse comprende l'intero processo di caricamento dati nel warehouse hello, analisi e creazione di report per data warehouse di hello, la gestione dei dati nel data warehouse di hello ed esportazione dei dati dal data warehouse di hello di hello. Hello profondità e larghezza di questi componenti sono spesso proporzionati con livello di maturità hello del data warehouse di hello.

## <a name="new-toodata-warehousing"></a>Nuovo toodata warehouse?
Un data warehouse è una raccolta di dati che vengono caricati da una o più dati di origini e tooperform utilizzati attività di business intelligence, ad esempio l'analisi dei dati e creazione di report.

Data warehouse sono caratterizzati dalle query in un'analisi di un numero maggiore di righe, ampi intervalli di dati e possono restituire risultati di dimensioni relativamente grandi per scopi di hello di analisi e creazione report. I data warehouse sono anche caratterizzati da caricamenti di dati relativamente estesi anziché da inserimenti, aggiornamenti o eliminazioni a livello di transazione di piccole dimensioni.

* Un data warehouse raggiunge prestazioni migliori quando hello dati vengono archiviati in modo che consente di ottimizzare le query che richiedono un numero elevato di righe tooscan o ampi intervalli di dati. Questo tipo di analisi funziona meglio quando l'archiviazione e la ricerca nelle colonne, anziché dalle righe dei dati di hello.

> [!NOTE]
> l'indice columnstore in memoria Hello, che usa l'archiviazione delle colonne, fornisce i guadagni di compressione too10x e 100 x miglioramento delle prestazioni di query su alberi binari tradizionale per le query di analitica e di reporting. Gli indici columnstore vengono considerate come hello standard per l'archiviazione e l'analisi dei dati di grandi dimensioni in un data warehouse.
> 
> 

* Un data warehouse ha requisiti diversi rispetto a un sistema ottimizzato per l'elaborazione di transazioni online (OLTP). Hello sistema OLTP ha molte inserimento, aggiornamento e le operazioni di eliminazione. Queste operazioni di ricerca toospecific righe nella tabella hello. Tabella ricerche risultare migliori se hello dati vengono archiviati in un modo di riga per riga. dati Hello possono essere ordinati rapidamente la ricerca con una divisione e impera approccio definito una ricerca binaria di struttura ad albero o albero b.

## <a name="data-loading"></a>Caricamento dei dati
Il caricamento dei dati è una parte importante del carico di lavoro di hello data warehouse. Le aziende hanno in genere un sistema OLTP occupato che tiene traccia delle modifiche per tutto il giorno hello quando i clienti generano transazioni aziendali. Periodicamente, spesso durante la notte durante una finestra di manutenzione, le operazioni di hello vengono spostate o copiati toohello data warehouse di. Una volta hello dati nel data warehouse di hello, gli analisti possono eseguire l'analisi e prendere decisioni aziendali sui dati hello.

* In genere, il processo di hello di caricamento viene chiamato ETL di estrazione, trasformazione e caricamento. In genere i dati devono toobe trasformato in modo che sia coerente con altri dati nel data warehouse di hello. Le aziende in precedenza, usare le trasformazioni hello tooperform server ETL dedicate. A questo punto, con l'elaborazione parallela massiva veloce è possibile caricare innanzitutto i dati in SQL Data Warehouse e quindi eseguire le trasformazioni di hello. Questo processo viene chiamato di estrazione, carico e trasformare (ELT) e sta diventando un nuovo standard per il carico di lavoro di hello data warehouse.

> [!NOTE]
> Con SQL Server 2016 è ora possibile eseguire l'analisi in tempo reale su una tabella OLTP. Ciò non sostituisce hello necessità per una toostore di data warehouse e analizzare i dati, ma fornisce un'analisi tooperform del modo in tempo reale.
> 
> 

### <a name="reporting-and-analysis-queries"></a>Query di reporting e analisi
Le query di reporting e analisi vengono spesso classificate come di piccole, medie e grandi dimensioni in base al numero di criteri, ma in genere si basano sul tempo. Nella maggior parte dei data warehouse è presente un carico di lavoro misto costituito da una combinazione di query a esecuzione rapida e query a esecuzione prolungata. In ogni caso, è importante toodetermine questa combinazione e toodetermine la frequenza (oraria, giornaliera, fine mese, trimestre-end e così via). È importante toounderstand che hello query miste del carico di lavoro, insieme a concorrenza, lead tooproper pianificazione della capacità per un data warehouse.

* Pianificazione della capacità può essere un'attività complessa per un carico di lavoro di query miste, soprattutto quando è necessario un data warehouse di lead time lunghi ora tooadd capacità toohello. SQL Data Warehouse rimuove urgenza hello della pianificazione della capacità, poiché è possibile aumentare e ridurre le capacità di calcolo in qualsiasi momento e dall'archiviazione e capacità di calcolo vengono ridimensionati in modo indipendente.

### <a name="data-management"></a>Gestione dati
La gestione dei dati è importante, specialmente quando si conosce che potrebbe divenire insufficiente spazio su disco in hello prossimo futuro. Data warehouse dividono in genere dati hello in intervalli significativi, che vengono archiviati come partizioni in una tabella. Tutti i prodotti basato su SQL Server consentono di spostare le partizioni da e verso la tabella hello. Questo consente di cambio di partizione si sposta precedente costosa archiviazione tooless dati e mantenere disponibili dati più recenti hello archiviazione online.

* Gli indici columnstore supportano le tabelle partizionate. Per questi indici, le tabelle partizionate vengono usate per la gestione e l'archiviazione dei dati. Per le tabelle archiviate riga per riga, le partizioni hanno un peso maggiore sulle prestazioni delle query.  
* PolyBase svolge un ruolo importante nella gestione dati. Usando PolyBase, è necessario tooHadoop dati meno recenti di hello opzione tooarchive o archiviazione blob di Azure.  Questo offre molte delle opzioni poiché dati hello sono ancora online.  Potrebbe richiedere più tempo tooretrieve dati da Hadoop, ma il compromesso di hello del tempo di recupero potrebbe superano hello costo di archiviazione.

### <a name="exporting-data"></a>Esportazione dei dati
Un modo toomake sono disponibili dati per report e analisi sono toosend dati hello dati warehouse tooservers dedicato per l'esecuzione di report e analisi. Tali server sono denominati data mart. Ad esempio, è possibile pre-elaborare i dati del report e quindi esportarla dal server di hello data warehouse toomany mondo hello, toomake viene reso disponibile per i clienti e gli analisti.

* Per la generazione di report, ogni notte è stato possibile popolare server di report di sola lettura con uno snapshot dei dati giornaliera hello. In questo modo maggiore larghezza di banda per i clienti, riducendo l'esigenza di risorse di calcolo di hello nel data warehouse di hello. Da un aspetto di sicurezza, i data mart consentono numero hello tooreduce di utenti che dispongono del data warehouse toohello di accesso.
* Per analitica, è possibile creare un cubo di analisi nel data warehouse di hello ed eseguire analisi di data warehouse di hello, o pre-elaborare i dati ed esportarlo toohello computer analysis server per un'ulteriore analitica.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere esaminato su SQL Data Warehouse, consultare come tooquickly [creare un Data Warehouse SQL] [ create a SQL Data Warehouse] e [caricare dati di esempio][load sample data].

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
