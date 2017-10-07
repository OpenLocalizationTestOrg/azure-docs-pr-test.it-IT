---
title: aaaGuide per l'utilizzo di PolyBase in SQL Data Warehouse | Documenti Microsoft
description: Linee guida e consigli per l'uso di PolyBase in scenari di SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>Guida per l'uso di PolyBase in SQL Data Warehouse
Questa guida offre informazioni pratiche per l'uso di PolyBase in SQL Data Warehouse.

tooget introduzione, vedere hello [caricano dati con PolyBase] [ Load data with PolyBase] esercitazione.

## <a name="rotating-storage-keys"></a>Rotazione delle chiavi di archiviazione
Da ora tootime è l'archiviazione blob toochange hello accesso tooyour chiave per motivi di sicurezza.

Hello più elegante tooperform modo che questa attività è toofollow un processo noto come "rotazione delle chiavi di hello". Si sarà notato che siano due chiavi di archiviazione per l'account di archiviazione blob. Si tratta in modo che è possibile eseguire la transizione

Ruotare le chiavi dell'account di archiviazione di Azure è un processo semplice tre passaggio

1. Creare seconda credenziali con ambito database basata sulla chiave di accesso di archiviazione secondaria hello
2. Creare una seconda origine dati esterna in base a questa nuova credenziale
3. Eliminare e creare tabelle esterne di hello verso toohello nuova origine dati esterna

Quando è stata eseguita la migrazione di tutte le tabelle esterne toohello nuova origine dati esterna, quindi è possibile eseguire hello eseguire la pulizia delle attività:

1. Eliminare prima origine dati esterna
2. Credenziali basata sulla chiave di accesso di archiviazione primaria hello con ambito database prima di rilascio
3. Accedere ad Azure e rigenerare la chiave di accesso primaria hello pronto per hello successivo

## <a name="query-azure-blob-storage-data"></a>Eseguire query sui dati di archiviazione BLOB di Azure
Le query su tabelle esterne è sufficiente utilizzano il nome di tabella hello come se fosse una tabella relazionale.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Una query su una tabella esterna può avere esito negativo con errore hello *"Query interrotta--è stata raggiunta la soglia massima di rifiuti di hello durante la lettura da un'origine esterna"*. Indica che i dati esterni contengono record *sporchi* . Un record di dati viene considerato come 'danneggiato' se i dati effettivi hello tipi/numero di colonne non corrispondono a definizioni di colonna hello della tabella esterna hello o se non è conforme il formato di file esterno specificato toohello dati hello. toofix, verificare che la tabella esterna e le definizioni di formato di file esterno siano corrette e che le definizioni di toothese è conforme ai dati esterni. Nel caso in cui un subset di record di dati esterni vengono modificati, è possibile scegliere tooreject questi record per le query utilizzando le opzioni di rifiuto hello CREATE EXTERNAL TABLE DDL.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Caricare dati dall'archiviazione BLOB di Azure
In questo esempio carica i dati dal database Data Warehouse tooSQL di archiviazione blob di Azure.

L'archiviazione dei dati direttamente rimuove il tempo di trasferimento dati hello per le query. L'archiviazione dei dati con un indice columnstore consente di migliorare le prestazioni delle query per le query di analisi da backup too10x.

In questo esempio utilizza i dati di tooload istruzione CREATE TABLE AS SELECT hello. nuova tabella Hello eredita le colonne di hello denominate query hello. Eredita i tipi di dati hello di tali colonne dalla definizione della tabella esterna hello.

CREATE TABLE AS SELECT è un efficiente elevata istruzione Transact-SQL che carica i dati di hello in parallelo tooall hello calcolo i nodi del proprio SQL Data Warehouse.  Questa è stata sviluppata per il motore di elaborazione parallela massiva (. MPP) hello nel sistema di piattaforma Analitica ed è ora in SQL Data Warehouse.

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

Vedere [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].

## <a name="create-statistics-on-newly-loaded-data"></a>Creare statistiche sui dati appena caricati
SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.  Ordine tooget hello prestazioni migliori dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento hello o si verificano modifiche sostanziali in dati hello.  Per una spiegazione dettagliata delle statistiche, vedere hello [statistiche] [ Statistics] argomento nel gruppo di sviluppare hello degli argomenti.  Di seguito è riportato un esempio di come statistiche toocreate sulla tabella hello caricati in questo esempio.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>Esportazione di archiviazione blob di dati tooAzure
Questa sezione illustra la modalità di archiviazione blob dati tooexport tooAzure SQL Data Warehouse. Questo esempio Usa CREATE EXTERNAL TABLE AS SELECT che è un elevata ad alte prestazioni di Transact-SQL istruzione tooexport hello dati in parallelo da tutti i nodi di calcolo di hello.

Hello seguente viene creata una tabella esterna Weblogs2014 utilizzando le definizioni delle colonne e dati da dbo. Tabella di blog. definizione della tabella esterna Hello viene archiviato in SQL Data Warehouse e i risultati di hello dell'istruzione SELECT hello sono esportato toohello "/ / log2014/archiviare" directory nel contenitore blob hello specificato dall'origine dati hello. Hello dati vengono esportati nel formato di file di testo specificato hello.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>Isolare il caricamento degli utenti
Vi è spesso un toohave necessità più utenti che possono caricare dati in un data Warehouse SQL. Poiché hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] richiede autorizzazioni di controllo del database di hello, si finirà con più utenti con accesso di controllo su tutti gli schemi. toolimit, è possibile utilizzare l'istruzione DENY controllo hello.

Esempio: si supponga che esistano gli schemi di database schema_A per reparto A e schema_B per reparto B e di consentire agli utenti di database utente_A e utente _B di effettuare caricamenti PolyBase rispettivamente in reparto A e B. A entrambi gli utenti sono state concesse le autorizzazioni di database CONTROL.
creatori di Hello dello schema A e B ora bloccare i relativi schemi utilizzando l'istruzione DENY:

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 Con questa operazione, user_A ed user_B dovrebbe ora essere bloccato da hello dello schema di altro reparto.
 


## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su tooSQL lo spostamento di dati Data Warehouse, vedere hello [Cenni preliminari sulla migrazione di dati][data migration overview].

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
