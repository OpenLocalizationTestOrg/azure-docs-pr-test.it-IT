---
title: "stored procedure da attività di copia di Azure Data Factory di aaaInvoke | Documenti Microsoft"
description: "Informazioni su come attività di copia tooinvoke una stored procedure nel Database SQL di Azure o SQL Server da una Data Factory di Azure."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Chiamare una stored procedure da un'attività di copia in Azure Data Factory
Quando si copiano dati in [SQL Server](data-factory-sqlserver-connector.md) o [Database SQL di Azure](data-factory-azure-sql-connector.md), è possibile configurare hello **SqlSink** in attività di copia tooinvoke una stored procedure. È opportuno toouse hello stored procedure tooperform eventuali elaborazioni aggiuntive (l'unione di colonne, la ricerca di valori, l'inserimento in più tabelle, e così via) sono necessario prima di inserire dati nella tabella di destinazione toohello. Questa funzionalità sfrutta [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx). 

Hello seguente esempio mostra come tooinvoke una stored procedure in SQL Server di database da una pipeline di Data Factory (attività di copia):  

## <a name="output-dataset-json"></a>Set di dati di output JSON
Nel set di dati output hello JSON, impostare hello **tipo** a: **SqlServerTable**. Impostarlo troppo**AzureSqlTable** toouse con un database SQL di Azure. valore per Hello **tableName** proprietà deve corrispondere il nome di hello del primo parametro di procedura hello archiviato.  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a>Sezione SqlSink nel file JSON dell'attività di copia
Definire hello **SqlSink** sezione nell'attività di copia hello JSON, come indicato di seguito. tooinvoke una stored procedure durante l'inserimento di dati in database sink/destinazione hello, specificare i valori per entrambe **SqlWriterStoredProcedureName** e **SqlWriterTableType** proprietà. Per una descrizione di queste proprietà, vedere [SqlSink sezione nell'articolo di connettore SQL Server hello](data-factory-sqlserver-connector.md#sqlsink).

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a>Definizione della stored procedure 
Nel database, definire procedure hello archiviato con stesso nome come hello **SqlWriterStoredProcedureName**. Hello stored procedure gestisce i dati di input dall'archivio dati di origine hello e inserisce i dati in una tabella nel database di destinazione hello. nome di Hello del primo parametro della stored procedure di hello deve corrispondere tableName hello definiti nel set di dati hello JSON (Marketing).

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>Definizione del tipo di tabella
Nel database, definire il tipo di tabella hello con stesso nome come hello **SqlWriterTableType**. schema di Hello hello del tipo di tabella deve corrispondere schema hello del set di dati input hello.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>Passaggi successivi
Esaminare i seguenti articoli connettore che, per completare gli esempi JSON hello: 

- [Database SQL di Azure](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
