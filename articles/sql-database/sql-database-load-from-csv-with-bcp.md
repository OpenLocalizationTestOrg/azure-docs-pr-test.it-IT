---
title: Caricare dati da un file CSV al database SQL di Azure (bcp) | Microsoft Docs
description: Per dati di piccole dimensioni, usa bcp per importare dati nel database SQL di Azure.
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 84bebab7763bb21f73880a6c8b367a62b0c137d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Caricare dati da CSV in un database SQL di Azure (file flat)
È possibile usare l'utilità della riga di comando bcp per importare dati da un file CSV in un database SQL di Azure.

## <a name="before-you-begin"></a>Prima di iniziare
### <a name="prerequisites"></a>Prerequisiti
Per seguire la procedura descritta in questo articolo, sono necessari:

* Un server logico e un database SQL di Azure
* Utilità della riga di comando bcp installata
* Utilità della riga di comando sqlcmd installata

È possibile scaricare le utilità bcp e sqlcmd dall'[Area download Microsoft][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dati in formato ASCII o UTF-16
Se si prova a eseguire questa esercitazione con dati personalizzati, è necessario che i dati usino la codifica ASCII o UTF-16, perché bcp non supporta UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Creare una tabella di destinazione
Definire una tabella nel database SQL come tabella di destinazione. Le colonne della tabella devono corrispondere ai dati in ogni riga del file di dati.

Per creare una tabella, aprire un prompt dei comandi e usare sqlcmd.exe per eseguire i comandi seguenti:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a>2. Creare un file di dati di origine
Aprire il Blocco note, copiare le righe di dati seguenti in un nuovo file di testo e quindi salvare il file nella directory temporanea locale, C:\Temp\DimDate2.txt. I dati hanno formato ASCII.

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

(Facoltativo) Per esportare i dati personalizzati da un database di SQL Server, aprire un prompt dei comandi ed eseguire il comando seguente. Sostituire TableName, ServerName, DatabaseName, Username e Password con le informazioni personalizzate.

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a>3. Caricare i dati
Per caricare i dati, aprire un prompt dei comandi ed eseguire il comando seguente, sostituendo i valori per nome server, nome database, nome utente e password con le informazioni personalizzate.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Usare questo comando per verificare che i dati siano stati caricati correttamente.

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

I risultati dovrebbero avere l'aspetto seguente:

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

## <a name="next-steps"></a>Passaggi successivi
Per eseguire la migrazione di un database SQL Server, vedere [Migrazione di un database SQL Server al database SQL nel cloud](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
