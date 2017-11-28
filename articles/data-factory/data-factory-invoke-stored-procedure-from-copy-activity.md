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
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="8362d-103">Chiamare una stored procedure da un'attività di copia in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8362d-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="8362d-104">Quando si copiano dati in [SQL Server](data-factory-sqlserver-connector.md) o [Database SQL di Azure](data-factory-azure-sql-connector.md), è possibile configurare hello **SqlSink** in attività di copia tooinvoke una stored procedure.</span><span class="sxs-lookup"><span data-stu-id="8362d-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="8362d-105">È opportuno toouse hello stored procedure tooperform eventuali elaborazioni aggiuntive (l'unione di colonne, la ricerca di valori, l'inserimento in più tabelle, e così via) sono necessario prima di inserire dati nella tabella di destinazione toohello.</span><span class="sxs-lookup"><span data-stu-id="8362d-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="8362d-106">Questa funzionalità sfrutta [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="8362d-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="8362d-107">Hello seguente esempio mostra come tooinvoke una stored procedure in SQL Server di database da una pipeline di Data Factory (attività di copia):</span><span class="sxs-lookup"><span data-stu-id="8362d-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="8362d-108">Set di dati di output JSON</span><span class="sxs-lookup"><span data-stu-id="8362d-108">Output dataset JSON</span></span>
<span data-ttu-id="8362d-109">Nel set di dati output hello JSON, impostare hello **tipo** a: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="8362d-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="8362d-110">Impostarlo troppo**AzureSqlTable** toouse con un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="8362d-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="8362d-111">valore per Hello **tableName** proprietà deve corrispondere il nome di hello del primo parametro di procedura hello archiviato.</span><span class="sxs-lookup"><span data-stu-id="8362d-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="8362d-112">Sezione SqlSink nel file JSON dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="8362d-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="8362d-113">Definire hello **SqlSink** sezione nell'attività di copia hello JSON, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8362d-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="8362d-114">tooinvoke una stored procedure durante l'inserimento di dati in database sink/destinazione hello, specificare i valori per entrambe **SqlWriterStoredProcedureName** e **SqlWriterTableType** proprietà.</span><span class="sxs-lookup"><span data-stu-id="8362d-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="8362d-115">Per una descrizione di queste proprietà, vedere [SqlSink sezione nell'articolo di connettore SQL Server hello](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="8362d-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="8362d-116">Definizione della stored procedure</span><span class="sxs-lookup"><span data-stu-id="8362d-116">Stored procedure definition</span></span> 
<span data-ttu-id="8362d-117">Nel database, definire procedure hello archiviato con stesso nome come hello **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="8362d-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="8362d-118">Hello stored procedure gestisce i dati di input dall'archivio dati di origine hello e inserisce i dati in una tabella nel database di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="8362d-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="8362d-119">nome di Hello del primo parametro della stored procedure di hello deve corrispondere tableName hello definiti nel set di dati hello JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="8362d-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="8362d-120">Definizione del tipo di tabella</span><span class="sxs-lookup"><span data-stu-id="8362d-120">Table type definition</span></span>
<span data-ttu-id="8362d-121">Nel database, definire il tipo di tabella hello con stesso nome come hello **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="8362d-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="8362d-122">schema di Hello hello del tipo di tabella deve corrispondere schema hello del set di dati input hello.</span><span class="sxs-lookup"><span data-stu-id="8362d-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="8362d-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8362d-123">Next steps</span></span>
<span data-ttu-id="8362d-124">Esaminare i seguenti articoli connettore che, per completare gli esempi JSON hello:</span><span class="sxs-lookup"><span data-stu-id="8362d-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="8362d-125">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="8362d-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="8362d-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8362d-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
