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
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="8d9eb-103">Copia ripetibile in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8d9eb-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="8d9eb-104">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="8d9eb-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="8d9eb-105">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="8d9eb-106">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8d9eb-107">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="8d9eb-108">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="8d9eb-109">Hello negli esempi seguenti sono per SQL Azure ma sono applicabili tooany archivio di dati che supporta i set di dati rettangolare.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="8d9eb-110">È possibile hello tooadjust **tipo** di origine e hello **query** proprietà (ad esempio: query anziché sqlReaderQuery) per i dati di hello archiviare.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="8d9eb-111">In genere, durante la lettura dagli archivi relazionali, dati tooread solo hello toothat sezione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="8d9eb-112">Toodo un modo sarebbe così utilizzando hello WindowStart e WindowEnd le variabili di sistema disponibili in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="8d9eb-113">Ulteriori informazioni sulle variabili hello e funzioni in Azure Data Factory qui in hello [Data Factory di Azure - funzioni e variabili di sistema](data-factory-functions-variables.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="8d9eb-114">Esempio:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="8d9eb-115">Questa query legge i dati che rientrano nell'intervallo di durata della sezione hello (WindowEnd WindowStart ->) dalla tabella hello MyTable.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="8d9eb-116">Eseguire di nuovo di questa sezione sempre anche assicurarsi che hello stessi dati vengono letti.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="8d9eb-117">In altri casi, è preferibile l'intera tabella di tooread hello e può definire hello sqlReaderQuery come segue:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="8d9eb-118">Scrittura REPEATABLE tooSqlSink</span><span class="sxs-lookup"><span data-stu-id="8d9eb-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="8d9eb-119">Quando si copiano dati troppo**Azure SQL di SQL Server** da altri archivi dati, è necessario ripetibilità tookeep in considerazione tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="8d9eb-120">Quando si copiano dati tooAzure Database SQL o SQL Server, attività di copia hello Accoda tabella di dati toohello sink per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="8d9eb-121">Ad esempio, si copiano dati da un formato CSV (valori delimitati da virgole) file che contiene due record toohello in un Database di Azure SQL o SQL Server nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="8d9eb-122">Quando viene eseguita una sezione, hello due record sono toohello copiate nella tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="8d9eb-123">Si supponga trovati errori nel file di origine e la quantità di hello di Tube verso il basso da 2 too4 aggiornata.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="8d9eb-124">Se si esegue nuovamente la sezione dati hello durante tale periodo manualmente, sono disponibili due nuovi record accodato tooAzure Database SQL o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="8d9eb-125">In questo esempio si presuppone che nessuna delle colonne hello hello tabella il vincolo di chiave primaria di hello.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="8d9eb-126">tooavoid questo comportamento, è necessario semantica UPSERT toospecify utilizzando uno dei seguenti due meccanismi hello:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="8d9eb-127">Meccanismo 1: uso di sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8d9eb-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="8d9eb-128">È possibile utilizzare hello **sqlWriterCleanupScript** tooclean proprietà backup dei dati dalla tabella sink hello prima di inserire dati hello durante l'esecuzione di una sezione.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="8d9eb-129">Quando viene eseguita una sezione, script di pulizia hello viene eseguito prima dati toodelete corrispondente sezione toohello dalla tabella SQL hello.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="8d9eb-130">attività di copia Hello quindi inserisce dati hello tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="8d9eb-131">Se viene eseguito di nuovo la sezione hello, quantità hello viene aggiornato come desiderato.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="8d9eb-132">Si supponga che hello record rondellapiatta viene rimosso da file csv originale hello.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="8d9eb-133">Quindi rieseguire sezione hello produrrebbe hello seguente risultato:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="8d9eb-134">esecuzione dell'attività di copia Hello hello pulizia dati dello script toodelete hello corrispondente per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="8d9eb-135">Quindi leggere l'input di hello da file csv hello (contenute quindi un solo record) e viene inserita nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="8d9eb-136">Meccanismo 2: uso di sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="8d9eb-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8d9eb-137">Attualmente sliceIdentifierColumnName non è supportato per Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="8d9eb-138">ripetibilità di tooachieve Hello secondo meccanismo consiste nel disporre di una colonna dedicata (sliceIdentifierColumnName) nella destinazione hello tabella.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="8d9eb-139">Questa colonna verrà usata dalla Data Factory di Azure tooensure hello origine e destinazione la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="8d9eb-140">Questo approccio funziona quando è disponibile una flessibilità nella modifica o la definizione di schema di tabella SQL di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="8d9eb-141">Questa colonna viene utilizzata da Data Factory di Azure per scopi di ripetibilità e nel processo di hello Azure Data Factory non apporta qualsiasi schema cambia toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="8d9eb-142">Modo toouse questo approccio:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="8d9eb-143">Definire una colonna di tipo **binary (32)** nella destinazione hello tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="8d9eb-144">in cui non sia presente alcun vincolo.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-144">There should be no constraints on this column.</span></span> <span data-ttu-id="8d9eb-145">Ai fini di questo esempio, la colonna viene denominata AdfSliceIdentifier.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="8d9eb-146">Tabella di origine:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="8d9eb-147">Tabella di destinazione:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="8d9eb-148">Utilizzarlo nell'attività di copia hello come segue:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="8d9eb-149">Azure Data Factory popola questa colonna in base alle necessità tooensure hello origine e destinazione mantenere la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="8d9eb-150">non utilizzare i valori Hello della colonna all'esterno di questo contesto.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="8d9eb-151">Toomechanism simile 1, l'attività di copia puliscono automaticamente i dati di hello per hello dato slice dalla destinazione hello tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="8d9eb-152">Vengono quindi inseriti i dati dall'origine nella tabella di destinazione toohello.</span><span class="sxs-lookup"><span data-stu-id="8d9eb-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8d9eb-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8d9eb-153">Next steps</span></span>
<span data-ttu-id="8d9eb-154">Esaminare i seguenti articoli connettore che, per completare gli esempi JSON hello:</span><span class="sxs-lookup"><span data-stu-id="8d9eb-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="8d9eb-155">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="8d9eb-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="8d9eb-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8d9eb-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="8d9eb-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8d9eb-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)