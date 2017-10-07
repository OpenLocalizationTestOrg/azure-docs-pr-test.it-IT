---
title: dati aaaLoad da SQL Server in Azure SQL Data Warehouse (bcp) | Documenti Microsoft
description: Per una dimensione dei dati di piccole dimensioni, utilizza bcp tooexport file tooflat di SQL Server e di importazione hello dati direttamente in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>Caricare dati da SQL Server in Azure SQL Data Warehouse (file flat)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Per set di dati di piccole dimensioni, è possibile utilizzare dati di tooexport hello bcp utilità della riga di comando di SQL Server e quindi caricarlo direttamente tooAzure SQL Data Warehouse.

In questa esercitazione si userà bcp per eseguire queste operazioni:

* Esportare una tabella da SQL Server tramite bcp hello comando (o creare un file di esempio semplice)
* Importare la tabella hello tooSQL un file flat del Data Warehouse.
* Creare le statistiche sui dati di hello caricato.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>Prima di iniziare
### <a name="prerequisites"></a>Prerequisiti
toostep di questa esercitazione, è necessario:

* Un database di SQL Data Warehouse
* utilità della riga di comando bcp Hello installato
* utilità della riga di comando sqlcmd Hello installato

È possibile scaricare le utilità bcp e sqlcmd hello da hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dati in formato ASCII o UTF-16
Se si sta provando questa esercitazione con i propri dati, i dati devono toouse hello ASCII o UTF-16 codifica poiché bcp non supportano UTF-8. 

PolyBase supporta UTF-8 ma non supporta ancora UTF-16. Si noti che se si desidera toocombine bcp con PolyBase occorre tootransform hello dati tooUTF-8 dopo la relativa esportazione da SQL Server. 

## <a name="1-create-a-destination-table"></a>1. Creare una tabella di destinazione
Definire una tabella in SQL Data Warehouse che fungerà da tabella di destinazione hello carico hello. colonne di Hello nella tabella hello devono corrispondere toohello dati in ogni riga del file di dati.

toocreate una tabella, aprire un prompt dei comandi e utilizzare hello toorun sqlcmd.exe comando seguente:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a>2. Creare un file di dati di origine
Aprire Blocco note e copiare hello seguenti righe di dati in un nuovo file di testo e quindi salvare il file tooyour locale directory temporanea, C:\Temp\DimDate2.txt. I dati hanno formato ASCII.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

(Facoltativo) tooexport i propri dati da un database di SQL Server, aprire un prompt dei comandi ed eseguire hello comando seguente. Sostituire TableName, ServerName, DatabaseName, Username e Password con le informazioni personalizzate.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Caricare i dati di hello
dati hello tooload, aprire un prompt dei comandi ed eseguire hello comando seguente, sostituendo valori hello per il nome del Server, nome di Database, nome utente e Password con le proprie informazioni di.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

Utilizzare questo comando tooverify hello di dati è stati caricati correttamente

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

risultati Hello dovrebbero essere simile al seguente:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

## <a name="4-create-statistics"></a>4. Creare le statistiche
SQL Data Warehouse non supporta ancora la creazione automatica o l'aggiornamento automatico delle statistiche. tooget hello migliori prestazioni di query, è importante toocreate statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento hello o dopo le modifiche sostanziali vengono eseguiti in dati hello. Per una spiegazione dettagliata delle statistiche, vedere [Statistiche][Statistics]. 

Comando che segue di esecuzione hello toocreate statistiche in una tabella appena caricata.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. Esportare i dati da SQL Data Warehouse
Per una divertente, è possibile esportare i dati di hello caricati nuovamente fuori SQL Data Warehouse.  tooexport comando Hello è hello esattamente come l'esportazione da SQL Server.

Tuttavia, sussiste una differenza nei risultati di hello. Poiché i dati di hello viene archiviati in posizioni distribuite all'interno di SQL Data Warehouse, quando si esportano dati ogni nodo di calcolo scrive file di output toohello di dati. ordine di Hello dei dati di hello nel file di output di hello è toobe probabilmente diverso da quello hello dei dati di hello nel file di input hello.

### <a name="export-a-table-and-compare-exported-results"></a>Esportare una tabella e confrontare i risultati esportati
toosee hello dati esportati, aprire un prompt dei comandi ed eseguire il comando utilizzando i parametri definiti dall'utente. NomeServer è il nome di hello del Server SQL Azure logico.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
È possibile verificare i dati è stati esportati correttamente aprendo hello nuovo file hello. dati Hello nel file hello devono corrispondere sotto il testo hello, ma verranno probabilmente essere ordinati in un ordine diverso:

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-hello-results-of-a-query"></a>Esportare i risultati di una query hello
È possibile utilizzare hello **queryout** funzione dei risultati di hello bcp tooexport di una query, anziché esportare l'intera tabella hello. 

## <a name="next-steps"></a>Passaggi successivi
Per una panoramica sul caricamento, vedere [Caricare i dati in SQL Data Warehouse][Load data into SQL Data Warehouse].
Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].
Per altre informazioni sulla creazione di una tabella in SQL Data Warehouse, vedere [Panoramica delle tabelle][Table Overview] o la sintassi di [CREATE TABLE][CREATE TABLE syntax].

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
