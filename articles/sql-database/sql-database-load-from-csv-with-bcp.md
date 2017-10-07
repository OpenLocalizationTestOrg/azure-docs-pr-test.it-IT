---
title: file di dati di aaaLoad da file CSV nel Database di SQL Azure (bcp) | Documenti Microsoft
description: Per una dimensione dei dati di piccole dimensioni, utilizza bcp tooimport dati in Database SQL di Azure.
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
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Caricare dati da CSV in un database SQL di Azure (file flat)
È possibile utilizzare hello bcp utilità della riga di comando tooimport dati da un file CSV nel Database di SQL Azure.

## <a name="before-you-begin"></a>Prima di iniziare
### <a name="prerequisites"></a>Prerequisiti
hello toocomplete i passaggi in questo articolo, è necessario:

* Un server logico e un database SQL di Azure
* utilità della riga di comando bcp Hello installato
* utilità della riga di comando sqlcmd Hello installato

È possibile scaricare le utilità bcp e sqlcmd hello da hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dati in formato ASCII o UTF-16
Se si sta provando questa esercitazione con i propri dati, i dati devono toouse hello ASCII o UTF-16 codifica poiché bcp non supportano UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Creare una tabella di destinazione
Definire una tabella nel Database SQL come tabella di destinazione hello. colonne di Hello nella tabella hello devono corrispondere toohello dati in ogni riga del file di dati.

toocreate una tabella, aprire un prompt dei comandi e utilizzare hello toorun sqlcmd.exe comando seguente:

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

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Caricare i dati di hello
dati hello tooload, aprire un prompt dei comandi ed eseguire hello comando seguente, sostituendo valori hello per il nome del Server, nome di Database, nome utente e Password con le proprie informazioni di.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Utilizzare questo comando tooverify hello di dati è stati caricati correttamente

```bcp
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

## <a name="next-steps"></a>Passaggi successivi
toomigrate un database di SQL Server, vedere [la migrazione di database di SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
