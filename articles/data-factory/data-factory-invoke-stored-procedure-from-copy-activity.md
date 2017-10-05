---
title: "Chiamare una stored procedure da un'attività di copia di Azure Data Factory | Documentazione Microsoft"
description: "Informazioni su come chiamare una stored procedure nel Database SQL di Azure o in SQL Server da un'attività di copia di Azure Data Factory."
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
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="b5edf-103">Chiamare una stored procedure da un'attività di copia in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b5edf-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="b5edf-104">Quando si copiano dati in [SQL Server](data-factory-sqlserver-connector.md) o nel [Database SQL di Azure](data-factory-azure-sql-connector.md), è possibile configurare **SqlSink** nell'attività di copia per chiamare una stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5edf-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="b5edf-105">Si consiglia di usare la stored procedure per eseguire eventuali elaborazioni aggiuntive (unione di colonne, ricerca di valori, inserimento in più tabelle e così via) è necessario prima inserire i dati nella tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b5edf-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="b5edf-106">Questa funzionalità sfrutta [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5edf-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="b5edf-107">L'esempio seguente illustra come chiamare una stored procedure in un database di SQL Server da una pipeline di data factory (attività di copia):</span><span class="sxs-lookup"><span data-stu-id="b5edf-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="b5edf-108">Set di dati di output JSON</span><span class="sxs-lookup"><span data-stu-id="b5edf-108">Output dataset JSON</span></span>
<span data-ttu-id="b5edf-109">Nel set di dati di output JSON impostare **type** su **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="b5edf-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="b5edf-110">Impostarlo su **AzureSqlTable** per usarlo con un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5edf-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="b5edf-111">Il valore per la proprietà **tableName** deve corrispondere al nome del primo parametro della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5edf-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="b5edf-112">Sezione SqlSink nel file JSON dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="b5edf-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="b5edf-113">Definire la sezione **SqlSink** nel file JSON dell'attività di copia come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b5edf-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="b5edf-114">Per chiamare una stored procedure durante l'inserimento di dati nel sink o nel database di destinazione, specificare i valori per entrambe le proprietà **SqlWriterStoredProcedureName** e **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="b5edf-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="b5edf-115">Per le descrizioni di queste proprietà, vedere [la sezione SqlSink dell'articolo sul connettore di SQL Server](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="b5edf-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="b5edf-116">Definizione della stored procedure</span><span class="sxs-lookup"><span data-stu-id="b5edf-116">Stored procedure definition</span></span> 
<span data-ttu-id="b5edf-117">Nel database definire la stored procedure con lo stesso nome di **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="b5edf-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="b5edf-118">La stored procedure gestisce i dati di input dall'archivio dati di origine e inserisce i dati in una tabella nel database di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b5edf-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="b5edf-119">Il nome del primo parametro della stored procedure deve corrispondere al tableName definito nel set di dati JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="b5edf-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="b5edf-120">Definizione del tipo di tabella</span><span class="sxs-lookup"><span data-stu-id="b5edf-120">Table type definition</span></span>
<span data-ttu-id="b5edf-121">Nel database definire il tipo di tabella con lo stesso nome di **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="b5edf-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="b5edf-122">Lo schema del tipo di tabella deve corrispondere allo schema del set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="b5edf-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="b5edf-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5edf-123">Next steps</span></span>
<span data-ttu-id="b5edf-124">Rivedere gli articoli seguenti sul connettore per gli esempi JSON completi:</span><span class="sxs-lookup"><span data-stu-id="b5edf-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="b5edf-125">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="b5edf-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="b5edf-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b5edf-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
