---
title: Copia ripetibile in Azure Data Factory | Microsoft Docs
description: "Informazioni su come evitare duplicati, anche se una sezione che copia i dati viene eseguita più volte."
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
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="c0d16-103">Copia ripetibile in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c0d16-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c0d16-104">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="c0d16-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="c0d16-105">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="c0d16-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c0d16-106">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="c0d16-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c0d16-107">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="c0d16-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c0d16-108">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="c0d16-109">Gli esempi seguenti sono per Azure SQL, ma sono applicabili a qualsiasi archivio dati che supporti set di dati rettangolari.</span><span class="sxs-lookup"><span data-stu-id="c0d16-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="c0d16-110">Potrebbe essere necessario modificare il **tipo** di origine e la proprietà **query** (ad esempio, query invece di sqlReaderQuery) per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="c0d16-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="c0d16-111">In genere, durante la lettura da archivi relazionali, si preferisce leggere solo i dati corrispondenti a tale sezione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="c0d16-112">Un modo per eseguire questa operazione è usare le variabili di sistema WindowStart e WindowEnd disponibili in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c0d16-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="c0d16-113">Per altre informazioni su variabili e funzioni di Azure Data Factory consultare l'articolo [Azure Data Factory - Funzioni e variabili di sistema](data-factory-functions-variables.md) seguente.</span><span class="sxs-lookup"><span data-stu-id="c0d16-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="c0d16-114">Esempio:</span><span class="sxs-lookup"><span data-stu-id="c0d16-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="c0d16-115">Questa query legge i dati che rientrano nell'intervallo di durata della sezione (WindowStart-> WindowEnd) della tabella MyTable.</span><span class="sxs-lookup"><span data-stu-id="c0d16-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="c0d16-116">Inoltre la riesecuzione di questa sezione garantirà sempre la lettura degli stessi dati.</span><span class="sxs-lookup"><span data-stu-id="c0d16-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="c0d16-117">In altri casi, si consiglia di leggere l'intera tabella e definire sqlReaderQuery come segue:</span><span class="sxs-lookup"><span data-stu-id="c0d16-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="c0d16-118">Scrittura ripetibile in SqlSink</span><span class="sxs-lookup"><span data-stu-id="c0d16-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="c0d16-119">Quando si copiano dati in un **database di SQL Server/SQL di Azure** da altri archivi dati, è necessario mantenere criteri di ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="c0d16-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="c0d16-120">Quando si copiano dati in un database SQL Server/SQL di Azure, per impostazione predefinita l'attività di copia accoda i dati alla tabella di sink.</span><span class="sxs-lookup"><span data-stu-id="c0d16-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="c0d16-121">Ad esempio, si copiano dati da un file con estensione CSV (valori delimitati da virgole) contenente due record per la tabella seguente in un Database SQL di Azure o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c0d16-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="c0d16-122">Quando viene eseguita una sezione, i due record vengono copiati nella tabella di SQL.</span><span class="sxs-lookup"><span data-stu-id="c0d16-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="c0d16-123">Si supponga di aver trovato degli errori nel file di origine e di aver aggiornato la quantità di Down Tube da 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="c0d16-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="c0d16-124">Se si esegue nuovamente la sezione di dati per quel periodo manualmente, saranno disponibili due nuovi record accodati al database di SQL Server/SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d16-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="c0d16-125">Questo esempio presuppone che in nessuna delle colonne della tabella sia presente il vincolo di chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="c0d16-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="c0d16-126">Per evitare questo comportamento, è necessario specificare la semantica UPSERT usando uno dei due meccanismi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0d16-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="c0d16-127">Meccanismo 1: uso di sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="c0d16-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="c0d16-128">È possibile usare la proprietà **sqlWriterCleanupScript** per cancellare i dati dalla tabella sink prima di inserire i dati durante l'esecuzione di una sezione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="c0d16-129">Quando viene eseguita una sezione, lo script di pulizia viene eseguito prima per eliminare i dati che corrispondono alla sezione della tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="c0d16-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="c0d16-130">Tramite l'attività di copia i dati vengono quindi inseriti nella tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="c0d16-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="c0d16-131">Se la sezione viene eseguita di nuovo, la quantità viene aggiornata in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c0d16-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="c0d16-132">Si supponga, ad esempio, che il record Flat Washer venga rimosso dal file con estensione csv originale.</span><span class="sxs-lookup"><span data-stu-id="c0d16-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="c0d16-133">Se la sezione viene eseguita nuovamente, si ottiene il risultato seguente:</span><span class="sxs-lookup"><span data-stu-id="c0d16-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="c0d16-134">L'attività di copia ha eseguito lo script di pulizia per eliminare i dati corrispondenti alla sezione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="c0d16-135">Quindi, ha letto l'input dal file con estensione CSV (che conteneva solo un record) e lo ha inserito nella tabella.</span><span class="sxs-lookup"><span data-stu-id="c0d16-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="c0d16-136">Meccanismo 2: uso di sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="c0d16-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c0d16-137">Attualmente sliceIdentifierColumnName non è supportato per Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c0d16-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="c0d16-138">Il secondo meccanismo per ottenere la ripetibilità prevede la disponibilità di una colonna dedicata (sliceIdentifierColumnName) nella tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="c0d16-139">Questa colonna viene usata da Data factory di Azure per garantire che l'origine e la destinazione rimangano sincronizzate.</span><span class="sxs-lookup"><span data-stu-id="c0d16-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="c0d16-140">Questo approccio può essere usato solo quando è disponibile una certa flessibilità nella modifica o nella definizione dello schema della tabella SQL di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="c0d16-141">La colonna viene usata da Azure Data Factory per scopi di ripetibilità e nel corso del processo Azure Data Factory non apporterà alcuna modifica allo schema della tabella.</span><span class="sxs-lookup"><span data-stu-id="c0d16-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="c0d16-142">Per applicare questo approccio, è possibile seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c0d16-142">Way to use this approach:</span></span>

1. <span data-ttu-id="c0d16-143">Definire una colonna di tipo **binario (32)** nella tabella SQL di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="c0d16-144">in cui non sia presente alcun vincolo.</span><span class="sxs-lookup"><span data-stu-id="c0d16-144">There should be no constraints on this column.</span></span> <span data-ttu-id="c0d16-145">Ai fini di questo esempio, la colonna viene denominata AdfSliceIdentifier.</span><span class="sxs-lookup"><span data-stu-id="c0d16-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="c0d16-146">Tabella di origine:</span><span class="sxs-lookup"><span data-stu-id="c0d16-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="c0d16-147">Tabella di destinazione:</span><span class="sxs-lookup"><span data-stu-id="c0d16-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="c0d16-148">Usarla nell'attività di copia come segue:</span><span class="sxs-lookup"><span data-stu-id="c0d16-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="c0d16-149">Azure Data Factory popolerà la colonna in base alle proprie esigenze affinché l'origine e la destinazione risultino sincronizzate.</span><span class="sxs-lookup"><span data-stu-id="c0d16-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="c0d16-150">I valori della colonna non possono essere usati al di fuori di questo contesto.</span><span class="sxs-lookup"><span data-stu-id="c0d16-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="c0d16-151">Analogamente al meccanismo 1, l'attività di copia cancella automaticamente i dati della sezione specificata dalla tabella SQL di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="c0d16-152">Vengono quindi inseriti i dati dall'origine nella tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c0d16-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c0d16-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0d16-153">Next steps</span></span>
<span data-ttu-id="c0d16-154">Rivedere gli articoli seguenti sul connettore per gli esempi JSON completi:</span><span class="sxs-lookup"><span data-stu-id="c0d16-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="c0d16-155">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="c0d16-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="c0d16-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c0d16-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="c0d16-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c0d16-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)