---
title: Copia aaaRepeatable nella Data Factory di Azure | Documenti Microsoft
description: "Informazioni su come tooavoid duplicati anche se una sezione che copia i dati viene eseguita più volte."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Copia ripetibile in Azure Data Factory

## <a name="repeatable-read-from-relational-sources"></a>Lettura ripetibile da origini relazionali
Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.  
 
> [!NOTE]
> Hello negli esempi seguenti sono per SQL Azure ma sono applicabili tooany archivio di dati che supporta i set di dati rettangolare. È possibile hello tooadjust **tipo** di origine e hello **query** proprietà (ad esempio: query anziché sqlReaderQuery) per i dati di hello archiviare.   

In genere, durante la lettura dagli archivi relazionali, dati tooread solo hello toothat sezione corrispondente. Toodo un modo sarebbe così utilizzando hello WindowStart e WindowEnd le variabili di sistema disponibili in Azure Data Factory. Ulteriori informazioni sulle variabili hello e funzioni in Azure Data Factory qui in hello [Data Factory di Azure - funzioni e variabili di sistema](data-factory-functions-variables.md) articolo. Esempio: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
Questa query legge i dati che rientrano nell'intervallo di durata della sezione hello (WindowEnd WindowStart ->) dalla tabella hello MyTable. Eseguire di nuovo di questa sezione sempre anche assicurarsi che hello stessi dati vengono letti. 

In altri casi, è preferibile l'intera tabella di tooread hello e può definire hello sqlReaderQuery come segue:

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>Scrittura REPEATABLE tooSqlSink
Quando si copiano dati troppo**Azure SQL di SQL Server** da altri archivi dati, è necessario ripetibilità tookeep in considerazione tooavoid risultati imprevisti. 

Quando si copiano dati tooAzure Database SQL o SQL Server, attività di copia hello Accoda tabella di dati toohello sink per impostazione predefinita. Ad esempio, si copiano dati da un formato CSV (valori delimitati da virgole) file che contiene due record toohello in un Database di Azure SQL o SQL Server nella tabella seguente. Quando viene eseguita una sezione, hello due record sono toohello copiate nella tabella SQL. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Si supponga trovati errori nel file di origine e la quantità di hello di Tube verso il basso da 2 too4 aggiornata. Se si esegue nuovamente la sezione dati hello durante tale periodo manualmente, sono disponibili due nuovi record accodato tooAzure Database SQL o SQL Server. In questo esempio si presuppone che nessuna delle colonne hello hello tabella il vincolo di chiave primaria di hello.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid questo comportamento, è necessario semantica UPSERT toospecify utilizzando uno dei seguenti due meccanismi hello:

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Meccanismo 1: uso di sqlWriterCleanupScript
È possibile utilizzare hello **sqlWriterCleanupScript** tooclean proprietà backup dei dati dalla tabella sink hello prima di inserire dati hello durante l'esecuzione di una sezione. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Quando viene eseguita una sezione, script di pulizia hello viene eseguito prima dati toodelete corrispondente sezione toohello dalla tabella SQL hello. attività di copia Hello quindi inserisce dati hello tabella SQL. Se viene eseguito di nuovo la sezione hello, quantità hello viene aggiornato come desiderato.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Si supponga che hello record rondellapiatta viene rimosso da file csv originale hello. Quindi rieseguire sezione hello produrrebbe hello seguente risultato: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

esecuzione dell'attività di copia Hello hello pulizia dati dello script toodelete hello corrispondente per tale sezione. Quindi leggere l'input di hello da file csv hello (contenute quindi un solo record) e viene inserita nella tabella hello. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Meccanismo 2: uso di sliceIdentifierColumnName
> [!IMPORTANT]
> Attualmente sliceIdentifierColumnName non è supportato per Azure SQL Data Warehouse. 

ripetibilità di tooachieve Hello secondo meccanismo consiste nel disporre di una colonna dedicata (sliceIdentifierColumnName) nella destinazione hello tabella. Questa colonna verrà usata dalla Data Factory di Azure tooensure hello origine e destinazione la sincronizzazione. Questo approccio funziona quando è disponibile una flessibilità nella modifica o la definizione di schema di tabella SQL di destinazione hello. 

Questa colonna viene utilizzata da Data Factory di Azure per scopi di ripetibilità e nel processo di hello Azure Data Factory non apporta qualsiasi schema cambia toohello tabella. Modo toouse questo approccio:

1. Definire una colonna di tipo **binary (32)** nella destinazione hello tabella SQL. in cui non sia presente alcun vincolo. Ai fini di questo esempio, la colonna viene denominata AdfSliceIdentifier.


    Tabella di origine:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Tabella di destinazione: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Utilizzarlo nell'attività di copia hello come segue:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Azure Data Factory popola questa colonna in base alle necessità tooensure hello origine e destinazione mantenere la sincronizzazione. non utilizzare i valori Hello della colonna all'esterno di questo contesto. 

Toomechanism simile 1, l'attività di copia puliscono automaticamente i dati di hello per hello dato slice dalla destinazione hello tabella SQL. Vengono quindi inseriti i dati dall'origine nella tabella di destinazione toohello. 

## <a name="next-steps"></a>Passaggi successivi
Esaminare i seguenti articoli connettore che, per completare gli esempi JSON hello: 

- [Database SQL di Azure](data-factory-azure-sql-connector.md)
- [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)