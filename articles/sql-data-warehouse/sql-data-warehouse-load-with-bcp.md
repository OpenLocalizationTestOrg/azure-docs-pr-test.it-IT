---
title: dati di tooload aaaUse bcp in SQL Data Warehouse | Documenti Microsoft
description: Informazioni su quali bcp e come toouse per scenari di data warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a>Caricare i dati con BCP
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

**[bcp] [ bcp]**  è un'utilità di caricamento bulk della riga di comando che consente di toocopy dati tra SQL Server, i file di dati e SQL Data Warehouse. Usare bcp tooimport un numero elevato di righe in tabelle di SQL Data Warehouse o tooexport dati dalle tabelle di SQL Server nei file di dati. Tranne quando sono usati con l'opzione queryout hello, bcp richiede alcuna conoscenza di Transact-SQL.

bcp è un modo semplice e rapido toomove più piccoli set di dati dentro e fuori da un database di SQL Data Warehouse. quantità esatta di Hello di dati che sono consigliabile tooload/estrazione tramite bcp variano di rete nella connessione toohello data center di Azure.  In genere, le tabelle delle dimensioni possono essere caricate ed estratte facilmente con bcp, tuttavia bcp non è consigliato per il caricamento o l'estrazione di grandi volumi di dati.  Polybase è hello consigliato strumento per il caricamento e l'estrazione di grandi volumi di dati come un processo migliore sfruttando l'architettura di elaborazione parallela massiva hello di SQL Data Warehouse.

Con bcp è possibile:

* Utilizzare una semplice utilità da riga di comando tooload di dati in SQL Data Warehouse.
* Utilizzare un semplice utilità da riga di comando tooextract dati da SQL Data Warehouse.

In questa esercitazione verranno illustrate le attività seguenti:

* Importazione di dati in una tabella utilizzando bcp hello nella finestra di comando
* Esportare i dati da un piano di hello tabella abbonamento comando

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a>Prerequisiti
toostep di questa esercitazione, è necessario:

* Un database di SQL Data Warehouse
* utilità della riga di comando bcp Hello installato
* utilità della riga di comando SQLCMD installato Hello

> [!NOTE]
> È possibile scaricare le utilità bcp e sqlcmd hello da hello [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>Importare i dati in SQL Data Warehouse
In questa esercitazione, verrà di creare una tabella in Azure SQL Data Warehouse e di importare dati nella tabella hello.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>Passaggio 1: Creare una tabella in Azure SQL Data Warehouse
Da un prompt dei comandi, utilizzare sqlcmd toorun hello seguente query toocreate una tabella nell'istanza:

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

> [!NOTE]
> Vedere [Cenni preliminari su tabella] [ Table Overview] o [sintassi CREATE TABLE] [ CREATE TABLE syntax] per ulteriori informazioni sulla creazione di una tabella in SQL Data Warehouse e hello  opzioni disponibili nella clausola WITH hello.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>Passaggio 2: Creare un file di dati di origine
Aprire Blocco note e copiare hello seguenti righe di dati in un nuovo file di testo e quindi salvare il file tooyour locale directory temporanea, C:\Temp\DimDate2.txt.

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

> [!NOTE]
> È importante tooremember che bcp.exe non supporta la codifica file hello UTF-8. Usare i file ASCII o con codifica UTF-16 quando si usa bcp.exe.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>Passaggio 3: Connettersi e importare i dati hello
Utilizzo di bcp, è possibile connettersi e importare i dati di hello tramite hello seguente comando sostituendo hello i valori appropriati:

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

È possibile verificare i dati sono stati caricati eseguendo la seguente query utilizzando sqlcmd hello hello:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Deve essere restituito hello seguenti risultati:

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

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Passaggio 4: creare le statistiche sui dati appena caricati
SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico. Ordine tooget hello prestazioni migliori dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento hello o si verificano modifiche sostanziali in dati hello. Per una spiegazione dettagliata delle statistiche, vedere hello [statistiche] [ Statistics] argomento nel gruppo di sviluppare hello degli argomenti. Di seguito è riportato un esempio di come statistiche toocreate sulla tabella hello caricati in questo esempio

Hello seguendo le istruzioni CREATE STATISTICS sqlcmd al prompt dei comandi eseguire:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>Esportare i dati da SQL Data Warehouse
In questa esercitazione verrà creato un file di dati da una tabella in SQL Data Warehouse. Si esporterà i dati di hello creato in precedenza tooa nuovo file di dati denominato DimDate2_export.txt.

### <a name="step-1-export-hello-data"></a>Passaggio 1: Esportare i dati di hello
Utilità bcp hello, è possibile connettersi ed esportare dati utilizzando hello seguente comando sostituendo hello i valori appropriati:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
È possibile verificare i dati è stati esportati correttamente aprendo hello nuovo file hello. dati Hello nel file hello devono corrispondere testo hello riportato di seguito:

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

> [!NOTE]
> A causa di natura toohello dei sistemi distribuiti, ordine dei dati hello potrebbe non essere hello uguali tra i database di SQL Data Warehouse. Un'altra opzione consiste hello toouse **queryout** funzione di bcp toowrite una query estrarre anziché di esportare l'intera tabella hello.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Per una panoramica sul caricamento, vedere [Caricare i dati in SQL Data Warehouse][Load data into SQL Data Warehouse].
Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].

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
