---
title: dati di esempio aaaLoad in SQL Data Warehouse | Documenti Microsoft
description: Caricare i dati di esempio in SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a>Caricare i dati di esempio in SQL Data Warehouse
Seguire questi tooload semplici passaggi e i database di esempio Adventure Works hello di query. Questi script innanzitutto utilizzano sqlcmd toorun SQL che verranno create tabelle e viste. Dopo avere create le tabelle, gli script hello utilizzerà dati tooload bcp.  Se si dispone già sqlcmd e bcp installato, vedere i collegamenti seguenti troppo[installare bcp] [ install bcp] e troppo[installare sqlcmd][install sqlcmd].

## <a name="load-sample-data"></a>Caricare dati di esempio
1. Scaricare hello [script di esempio Adventure Works per SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] file zip.
2. Estrarre i file hello dalla directory tooa zip scaricato nel computer locale.
3. Modificare aw_create.bat file hello estratto e impostare hello seguenti variabili presenti all'inizio di hello del file hello.  Non essere tooleave che spazi tra hello "=" e il parametro hello.  Di seguito sono riportati alcuni esempi dell'aspetto che le modifiche potrebbero assumere.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. Da un prompt di Windows, eseguire aw_create.bat hello modificato.  Assicurarsi che trovano nella directory hello in cui è salvata la versione modificata di aw_create.bat.
   Questo script consentirà di eseguire le operazioni seguenti:
   
   * Eliminare le tabelle o le visualizzazioni Adventure Works già esistenti nel database
   * Creare viste e tabelle di Adventure Works hello
   * Caricare tutte le tabelle Adventure Works tramite bcp
   * Convalidare i conteggi delle righe per ogni tabella di Adventure Works hello
   * Raccogliere le statistiche per ogni colonna di ogni tabella Adventure Works

## <a name="query-sample-data"></a>Eseguire query sui dati di esempio
Dopo aver caricato alcuni dati di esempio in SQL Data Warehouse, è possibile eseguire rapidamente alcune query.  toorun una query, la connessione a database di Adventure Works tooyour appena creati nel data Warehouse di SQL Azure con Visual Studio e SSDT, come descritto in hello [query con Visual Studio] [ query with Visual Studio] documento.

Esempio di semplice selezionare istruzione tooget tutte le informazioni di hello dei dipendenti hello:

```sql
SELECT * FROM DimEmployee;
```

Esempio di una query più complessa utilizzando costrutti, ad esempio GROUP BY toolook alla quantità totale di hello per tutte le vendite ogni giorno:

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Esempio di un'istruzione SELECT con una toofilter della clausola WHERE gli ordini da prima di una determinata data:

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

SQL Data Warehouse supporta quasi tutti i costrutti T-SQL supportati da SQL Server.  Eventuali differenze sono illustrate nella documentazione relativa alla [migrazione del codice][migrate code].

## <a name="next-steps"></a>Passaggi successivi
Ora che hai era un tootry possibilità alcune query con dati di esempio, estrarre come troppo[sviluppare][develop], [caricare][load], o [ eseguire la migrazione] [ migrate] tooSQL Data Warehouse.

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
