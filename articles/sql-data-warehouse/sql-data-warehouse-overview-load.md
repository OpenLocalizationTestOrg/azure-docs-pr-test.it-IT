---
title: dati aaaLoad in Azure SQL Data Warehouse | Documenti Microsoft
description: "Informazioni su scenari comuni di hello per i dati durante il caricamento in SQL Data Warehouse. Questi includono l'uso di PolyBase, dell’archiviazione BLOB di Azure, di file flat e l’invio dei dischi. È anche possibile usare strumenti di terze parti."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Caricare i dati in Azure SQL Data Warehouse
Un riepilogo delle opzioni di scenario hello e consigli per il caricamento dei dati in SQL Data Warehouse.

parte di più difficile Hello di caricamento dei dati è in genere preparazione dei dati hello carico hello. Azure semplifica il caricamento con l'archiviazione blob di Azure come archivio dati comuni per la maggior parte dei servizi di hello e usando Azure Data Factory tooorchestrate lo spostamento di dati e la comunicazione tra hello servizi di Azure. Questi processi sono integrati con la tecnologia PolyBase che utilizza l'elaborazione parallela massiva dati tooload (. MPP) in parallelo dall'archiviazione blob di Azure in SQL Data Warehouse. 

Per esercitazioni in cui vengono caricati database di esempio, vedere [Caricare i dati di esempio in SQL Data Warehouse][Load sample databases].

## <a name="load-from-azure-blob-storage"></a>Caricare i dati dall’archiviazione BLOB di Azure
Hello più veloce modo tooimport dati in SQL Data Warehouse sono toouse dati tooload PolyBase dall'archiviazione blob di Azure. PolyBase utilizza SQL Data Warehouse elaborazione parallela massiva dati tooload della progettazione (. MPP) in parallelo dall'archiviazione blob di Azure. toouse PolyBase, è possibile utilizzare i comandi T-SQL o una pipeline di Data Factory di Azure.

### <a name="1-use-polybase-and-t-sql"></a>1. Usare PolyBase e T-SQL
Riepilogo del processo di caricamento:

1. Spostare l'archiviazione blob di dati tooAzure o archivio Azure Data Lake e archiviarlo nel file di testo.
2. Configurare gli oggetti esterni nel percorso di hello toodefine SQL Data Warehouse e il formato dei dati hello
3. Eseguire una data di hello tooload comando T-SQL in parallelo in una nuova tabella di database.

<!-- 5. Schedule and run a loading job. --> 

Per un'esercitazione, vedere [caricare dati da tooSQL di archiviazione blob di Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="2-use-azure-data-factory"></a>2. Usare Azure Data Factory
Per un toouse modo più semplice PolyBase, è possibile creare una pipeline di Data Factory di Azure che utilizza dati di PolyBase tooload dall'archiviazione blob di Azure in SQL Data Warehouse. Si tratta di tooconfigure veloce, poiché non è necessario oggetti T-SQL di toodefine hello. Se è necessario dati esterni di hello tooquery senza eseguirne l'importazione, è possibile utilizzare T-SQL. 

Riepilogo del processo di caricamento:

1. Spostare l'archiviazione blob di dati tooAzure e archiviarlo nel file di testo. Azure Data Factory attualmente non supporta la connettività ADLS con PolyBase.
2. Creare una pipeline di Data Factory di Azure tooingest hello dati. Utilizzare l'opzione PolyBase hello.
4. Pianificare ed eseguire pipeline hello.

Per un'esercitazione, vedere [caricare dati da tooSQL di archiviazione blob di Azure Data Warehouse (Data Factory di Azure)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].

## <a name="load-from-sql-server"></a>Caricare i dati da SQL Server
tooload tooSQL di SQL Server Data Warehouse è possibile utilizzare Integration Services (SSIS), trasferimento di file flat o spedire i dischi tooMicrosoft. Continuare a leggere toosee un riepilogo dei diverso durante il caricamento dei processi e i collegamenti tootutorials hello.

tooplan una migrazione completa di dati da tooSQL di SQL Server Data Warehouse, vedere hello [Cenni preliminari sulla migrazione][Migration overview]. 

### <a name="use-integration-services-ssis"></a>Usare SQL Server Integration Services (SSIS)
Se si usa già tooload di pacchetti di Integration Services (SSIS) in SQL Server, è possibile aggiornare il toouse pacchetti SQL Server come origine di hello e SQL Data Warehouse come destinazione di hello. Questa è un'operazione rapida e semplice toodo, ed è una buona scelta se non si stia tentando toomigrate il caricamento elaborare dati toouse già presenti nel cloud hello. compromesso di Hello è carico hello risulterà più lenta rispetto all'utilizzo di PolyBase poiché questo SSIS non esegue il carico hello in parallelo.

Riepilogo del processo di caricamento:

1. Modificare l'istanza di SQL Server Integration Services pacchetto toopoint toohello per origine hello e database di SQL Data Warehouse hello per destinazione hello.
2. Eseguire la migrazione del tooSQL dello schema del Data Warehouse, se non esiste già.
3. Modifica associazione hello nei pacchetti di utilizzare solo i tipi di dati di hello sono supportati da SQL Data Warehouse.
4. Pianificare ed eseguire il pacchetto di hello.

Per un'esercitazione, vedere [caricare dati da SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].

### <a name="use-azcopy-recommended-for--10-tb-data"></a>Usare AZCopy (scelta consigliata per i dati < 10 TB)
Se la dimensione dei dati è < 10 TB, è possibile esportare dati hello dai file tooflat di SQL Server, copiare l'archiviazione di blob tooAzure file hello e quindi utilizzare i dati di PolyBase tooload hello in SQL Data Warehouse

Riepilogo del processo di caricamento:

1. Usare hello bcp utilità della riga di comando tooexport dati da file tooflat di SQL Server.
2. Utilizzare i dati di hello AZCopy utilità della riga di comando toocopy dall'archiviazione blob tooAzure di file flat.
3. Utilizzare tooload PolyBase in SQL Data Warehouse.

Per un'esercitazione, vedere [caricare dati da tooSQL di archiviazione blob di Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="use-bcp"></a>Usare bcp
Se si dispone di una piccola quantità di dati è possibile utilizzare bcp tooload direttamente in Azure SQL Data Warehouse.

Riepilogo del processo di caricamento:

1. Usare hello bcp utilità della riga di comando tooexport dati da file tooflat di SQL Server.
2. Utilizzare bcp tooload da flat i file di dati direttamente tooSQL Data Warehouse.

Per un'esercitazione, vedere [caricare dati da SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].

### <a name="use-importexport-recommended-for--10-tb-data"></a>Usare il servizio Importazione/Esportazione (scelta consigliata per i dati > 10 TB)
Se la dimensione dei dati è > 10 TB e si desidera toomove è tooAzure, si consiglia di utilizzare il disco di servizio di spedizione [importazione/esportazione][Import/Export]. 

Riepilogo del processo di caricamento

1. Utilizzare hello bcp utilità della riga di comando tooexport dati dai file di SQL Server tooflat su dischi trasferibili.
2. Hello spedire i dischi tooMicrosoft.
3. Microsoft carica i dati di hello in SQL Data Warehouse

## <a name="load-from-hdinsight"></a>Caricare da HDInsight
SQL Data Warehouse supporta il caricamento di dati da HDInsight tramite PolyBase. il processo di Hello è hello stesso come il caricamento dei dati dall'archiviazione Blob di Azure - utilizzo dati di PolyBase tooconnect tooHDInsight tooload. 

### <a name="1-use-polybase-and-t-sql"></a>1. Usare PolyBase e T-SQL
Riepilogo del processo di caricamento:

1. Spostare i dati tooHDInsight e archiviarlo nel file di testo, ORC o Parquet formato.
2. In SQL Data Warehouse toodefine hello percorso e il formato dei dati di hello, configurare gli oggetti esterni.
3. Eseguire una data di hello tooload comando T-SQL in parallelo in una nuova tabella di database.

Per un'esercitazione, vedere [caricare dati da tooSQL di archiviazione blob di Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

## <a name="recommendations"></a>Raccomandazioni
Molti partner Microsoft dispongono di soluzioni di caricamento. toofind altre informazioni, vedere un elenco dei nostri [partner delle soluzioni][solution partners]. 

Se i dati provenienti da un'origine non relazionali e si desidera tooload in SQL Data Warehouse è necessario tootransform in righe e colonne prima di caricarli. i dati di Hello trasformato non devono toobe archiviati in un database, possono essere archiviato nei file di testo.

Creare statistiche sui dati appena caricati. SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.  Ordine tooget hello prestazioni migliori dalle query, è importante innanzitutto caricano toocreate statistiche per tutte le colonne di tutte le tabelle dopo hello o si verificano modifiche sostanziali in dati hello.  Per informazioni dettagliate, vedere [Managing statistics on tables in SQL Data Warehouse][Statistics](Gestione delle statistiche nelle tabelle in SQL Data Warehouse).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori suggerimenti per lo sviluppo, vedere hello [Cenni preliminari sullo sviluppo][development overview].

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
