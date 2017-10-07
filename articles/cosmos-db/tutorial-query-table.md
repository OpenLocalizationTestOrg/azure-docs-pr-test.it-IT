---
title: aaaHow tooquery dati della tabella nel database di Azure Cosmos? | Microsoft Docs
description: Ulteriori dati della tabella nel database di Azure Cosmos tooquery
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="fc2e2-104">Azure Cosmos DB: Come dati della tabella tooquery utilizzando hello tabella API (anteprima)?</span><span class="sxs-lookup"><span data-stu-id="fc2e2-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="fc2e2-105">Hello Azure Cosmos DB [tabella API](table-introduction.md) (anteprima) supporta OData e [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) query su dati chiave/valore (tabella).</span><span class="sxs-lookup"><span data-stu-id="fc2e2-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="fc2e2-106">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="fc2e2-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="fc2e2-107">Eseguire query sui dati con tabella API hello</span><span class="sxs-lookup"><span data-stu-id="fc2e2-107">Querying data with hello Table API</span></span>

<span data-ttu-id="fc2e2-108">le query in questo articolo Hello utilizzano seguendo l'esempio hello `People` tabella:</span><span class="sxs-lookup"><span data-stu-id="fc2e2-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="fc2e2-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="fc2e2-109">PartitionKey</span></span> | <span data-ttu-id="fc2e2-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="fc2e2-110">RowKey</span></span> | <span data-ttu-id="fc2e2-111">Email</span><span class="sxs-lookup"><span data-stu-id="fc2e2-111">Email</span></span> | <span data-ttu-id="fc2e2-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="fc2e2-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc2e2-113">Harp</span><span class="sxs-lookup"><span data-stu-id="fc2e2-113">Harp</span></span> | <span data-ttu-id="fc2e2-114">Walter</span><span class="sxs-lookup"><span data-stu-id="fc2e2-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="fc2e2-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="fc2e2-115">425-555-0101</span></span> |
| <span data-ttu-id="fc2e2-116">Smith</span><span class="sxs-lookup"><span data-stu-id="fc2e2-116">Smith</span></span> | <span data-ttu-id="fc2e2-117">Ben</span><span class="sxs-lookup"><span data-stu-id="fc2e2-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="fc2e2-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="fc2e2-118">425-555-0102</span></span> |
| <span data-ttu-id="fc2e2-119">Smith</span><span class="sxs-lookup"><span data-stu-id="fc2e2-119">Smith</span></span> | <span data-ttu-id="fc2e2-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="fc2e2-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="fc2e2-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="fc2e2-121">425-555-0104</span></span> | 

<span data-ttu-id="fc2e2-122">Poiché Azure Cosmos DB è compatibile con le API di archiviazione Azure Table hello, vedere [esecuzione di query su tabelle ed entità] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) per informazioni dettagliate su come tooquery utilizzando hello Tabella API.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="fc2e2-123">Per ulteriori informazioni sulle funzionalità premium hello che offre Azure Cosmos DB, vedere [DB Cosmos Azure: tabella API](table-introduction.md) e [sviluppare con API di tabelle in .NET hello](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fc2e2-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fc2e2-124">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fc2e2-124">Prerequisites</span></span>

<span data-ttu-id="fc2e2-125">Per questi toowork query, è necessario dispone di un account Azure Cosmos DB e disporre di dati di entità nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="fc2e2-126">Questi requisiti non sono disponibili?</span><span class="sxs-lookup"><span data-stu-id="fc2e2-126">Don't have any of those?</span></span> <span data-ttu-id="fc2e2-127">Hello completo [Guida introduttiva di cinque minuti](https://aka.ms/acdbtnetqs) o hello [esercitazione developer](https://aka.ms/acdbtabletut) toocreate un account e popolare il database.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="fc2e2-128">Query su PartitionKey e RowKey</span><span class="sxs-lookup"><span data-stu-id="fc2e2-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="fc2e2-129">Poiché le proprietà PartitionKey e RowKey hello formano la chiave primaria di un'entità, è possibile utilizzare hello seguenti entità di una sintassi speciale tooidentify hello:</span><span class="sxs-lookup"><span data-stu-id="fc2e2-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="fc2e2-130">**Query**</span><span class="sxs-lookup"><span data-stu-id="fc2e2-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="fc2e2-131">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="fc2e2-131">**Results**</span></span>

| <span data-ttu-id="fc2e2-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="fc2e2-132">PartitionKey</span></span> | <span data-ttu-id="fc2e2-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="fc2e2-133">RowKey</span></span> | <span data-ttu-id="fc2e2-134">Email</span><span class="sxs-lookup"><span data-stu-id="fc2e2-134">Email</span></span> | <span data-ttu-id="fc2e2-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="fc2e2-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc2e2-136">Harp</span><span class="sxs-lookup"><span data-stu-id="fc2e2-136">Harp</span></span> | <span data-ttu-id="fc2e2-137">Walter</span><span class="sxs-lookup"><span data-stu-id="fc2e2-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="fc2e2-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="fc2e2-138">425-555-0104</span></span> |

<span data-ttu-id="fc2e2-139">In alternativa, è possibile specificare queste proprietà come parte di hello `$filter` opzione, come illustrato nella seguente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="fc2e2-140">Si noti che i nomi di proprietà chiave hello e valori costanti tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="fc2e2-141">Sia hello PartitionKey e RowKey proprietà sono di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="fc2e2-142">Eseguire una query usando un filtro OData</span><span class="sxs-lookup"><span data-stu-id="fc2e2-142">Query by using an OData filter</span></span>
<span data-ttu-id="fc2e2-143">Quando si crea una stringa di filtro, tenere presente queste regole:</span><span class="sxs-lookup"><span data-stu-id="fc2e2-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="fc2e2-144">Usare hello operatori logici definiti dalla specifica del protocollo OData toocompare un valore della proprietà tooa hello.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="fc2e2-145">Si noti che non è possibile confrontare un valore di proprietà tooa dinamico.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="fc2e2-146">Un lato dell'espressione hello deve essere una costante.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="fc2e2-147">valore costante, operatore e il nome di proprietà Hello devono essere separati da spazi con codifica URL.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="fc2e2-148">Uno spazio con codifica URL è come `%20`.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="fc2e2-149">Tutte le parti della stringa di filtro hello maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="fc2e2-150">valore costante Hello deve essere di hello del tipo di dati stesso come proprietà hello affinché hello filtro tooreturn valido risultati.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="fc2e2-151">Per ulteriori informazioni sui tipi di proprietà supportati, vedere [hello comprensione modello di dati del servizio tabelle](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="fc2e2-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="fc2e2-152">Ecco una query di esempio che illustra come toofilter da hello PartitionKey e le proprietà di posta elettronica utilizzando un OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="fc2e2-153">**Query**</span><span class="sxs-lookup"><span data-stu-id="fc2e2-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="fc2e2-154">Per ulteriori informazioni su come tooconstruct espressioni per vari tipi di dati di filtro, vedere [query su tabelle ed entità](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="fc2e2-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="fc2e2-155">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="fc2e2-155">**Results**</span></span>

| <span data-ttu-id="fc2e2-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="fc2e2-156">PartitionKey</span></span> | <span data-ttu-id="fc2e2-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="fc2e2-157">RowKey</span></span> | <span data-ttu-id="fc2e2-158">Email</span><span class="sxs-lookup"><span data-stu-id="fc2e2-158">Email</span></span> | <span data-ttu-id="fc2e2-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="fc2e2-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc2e2-160">Ben</span><span class="sxs-lookup"><span data-stu-id="fc2e2-160">Ben</span></span> |<span data-ttu-id="fc2e2-161">Smith</span><span class="sxs-lookup"><span data-stu-id="fc2e2-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="fc2e2-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="fc2e2-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="fc2e2-163">Eseguire una query utilizzando LINQ</span><span class="sxs-lookup"><span data-stu-id="fc2e2-163">Query by using LINQ</span></span> 
<span data-ttu-id="fc2e2-164">È anche possibile eseguire una query utilizzando LINQ, che converte le espressioni di query OData corrispondente toohello.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="fc2e2-165">Di seguito è riportato un esempio di come query toobuild utilizzando hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="fc2e2-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a><span data-ttu-id="fc2e2-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc2e2-166">Next steps</span></span>

<span data-ttu-id="fc2e2-167">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="fc2e2-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc2e2-168">Appreso come tooquery utilizzando hello tabella API (anteprima)</span><span class="sxs-lookup"><span data-stu-id="fc2e2-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="fc2e2-169">È ora possibile procedere come toolearn esercitazione successiva toohello toodistribute i dati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc2e2-170">Distribuire i dati a livello globale</span><span class="sxs-lookup"><span data-stu-id="fc2e2-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
