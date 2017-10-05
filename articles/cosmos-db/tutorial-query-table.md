---
title: Procedura per l'esecuzione di query sui dati tabella in Azure Cosmos DB | Microsoft Docs
description: Informazioni per l'esecuzione di query sui dati tabella in Azure Cosmos DB
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
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="b089a-104">Azure Cosmos DB: procedura per l'esecuzione di query sui dati della tabella con l'API Table (anteprima)</span><span class="sxs-lookup"><span data-stu-id="b089a-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="b089a-105">L'[API Table](table-introduction.md) di Azure Cosmos DB (anteprima) supporta l'esecuzione di query OData e [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) sui dati chiave/valore (tabella).</span><span class="sxs-lookup"><span data-stu-id="b089a-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="b089a-106">Questo articolo illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="b089a-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b089a-107">Esecuzione di query sui dati con l'API Table</span><span class="sxs-lookup"><span data-stu-id="b089a-107">Querying data with the Table API</span></span>

<span data-ttu-id="b089a-108">Le query di questo articolo usano la tabella di esempio `People`:</span><span class="sxs-lookup"><span data-stu-id="b089a-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="b089a-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="b089a-109">PartitionKey</span></span> | <span data-ttu-id="b089a-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="b089a-110">RowKey</span></span> | <span data-ttu-id="b089a-111">Email</span><span class="sxs-lookup"><span data-stu-id="b089a-111">Email</span></span> | <span data-ttu-id="b089a-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="b089a-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b089a-113">Harp</span><span class="sxs-lookup"><span data-stu-id="b089a-113">Harp</span></span> | <span data-ttu-id="b089a-114">Walter</span><span class="sxs-lookup"><span data-stu-id="b089a-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="b089a-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="b089a-115">425-555-0101</span></span> |
| <span data-ttu-id="b089a-116">Smith</span><span class="sxs-lookup"><span data-stu-id="b089a-116">Smith</span></span> | <span data-ttu-id="b089a-117">Ben</span><span class="sxs-lookup"><span data-stu-id="b089a-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="b089a-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="b089a-118">425-555-0102</span></span> |
| <span data-ttu-id="b089a-119">Smith</span><span class="sxs-lookup"><span data-stu-id="b089a-119">Smith</span></span> | <span data-ttu-id="b089a-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="b089a-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="b089a-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="b089a-121">425-555-0104</span></span> | 

<span data-ttu-id="b089a-122">Poiché Azure Cosmos DB è compatibile con le API di archiviazione delle tabelle di Azure, vedere [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) (Esecuzione di query su tabelle ed entità) per informazioni dettagliate su come eseguire una query con l'API Tabella.</span><span class="sxs-lookup"><span data-stu-id="b089a-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="b089a-123">Per altre informazioni sulle funzionalità Premium offerte da Azure Cosmos DB, vedere [Azure Cosmos DB: API Table ](table-introduction.md) e [Sviluppare con l'API Table in .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b089a-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b089a-124">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b089a-124">Prerequisites</span></span>

<span data-ttu-id="b089a-125">Per il funzionamento di queste query è necessario disporre di un account Azure Cosmos DB e nel contenitore devono essere presenti dati di entità.</span><span class="sxs-lookup"><span data-stu-id="b089a-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="b089a-126">Questi requisiti non sono disponibili?</span><span class="sxs-lookup"><span data-stu-id="b089a-126">Don't have any of those?</span></span> <span data-ttu-id="b089a-127">Completare la [Guida introduttiva di 5 minuti](https://aka.ms/acdbtnetqs) o l'[esercitazione per sviluppatori](https://aka.ms/acdbtabletut) per creare un account e popolare il database.</span><span class="sxs-lookup"><span data-stu-id="b089a-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="b089a-128">Query su PartitionKey e RowKey</span><span class="sxs-lookup"><span data-stu-id="b089a-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="b089a-129">Poiché le proprietà PartitionKey e RowKey costituiscono la chiave primaria di un'entità, è possibile usare la sintassi speciale seguente per identificare l'entità:</span><span class="sxs-lookup"><span data-stu-id="b089a-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="b089a-130">**Query**</span><span class="sxs-lookup"><span data-stu-id="b089a-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="b089a-131">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="b089a-131">**Results**</span></span>

| <span data-ttu-id="b089a-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="b089a-132">PartitionKey</span></span> | <span data-ttu-id="b089a-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="b089a-133">RowKey</span></span> | <span data-ttu-id="b089a-134">Email</span><span class="sxs-lookup"><span data-stu-id="b089a-134">Email</span></span> | <span data-ttu-id="b089a-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="b089a-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b089a-136">Harp</span><span class="sxs-lookup"><span data-stu-id="b089a-136">Harp</span></span> | <span data-ttu-id="b089a-137">Walter</span><span class="sxs-lookup"><span data-stu-id="b089a-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="b089a-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="b089a-138">425-555-0104</span></span> |

<span data-ttu-id="b089a-139">In alternativa, è possibile specificare queste proprietà come parte dell'opzione `$filter`, come illustrato nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="b089a-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="b089a-140">Si noti che i nomi delle proprietà chiave e i valori costanti distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b089a-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="b089a-141">Entrambe le proprietà PartitionKey e RowKey sono di tipo String.</span><span class="sxs-lookup"><span data-stu-id="b089a-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="b089a-142">Eseguire una query usando un filtro OData</span><span class="sxs-lookup"><span data-stu-id="b089a-142">Query by using an OData filter</span></span>
<span data-ttu-id="b089a-143">Quando si crea una stringa di filtro, tenere presente queste regole:</span><span class="sxs-lookup"><span data-stu-id="b089a-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="b089a-144">Usare gli operatori logici definiti dalla specifica del protocollo OData per confrontare una proprietà con un valore.</span><span class="sxs-lookup"><span data-stu-id="b089a-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="b089a-145">Si noti che non è possibile confrontare una proprietà con un valore dinamico.</span><span class="sxs-lookup"><span data-stu-id="b089a-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="b089a-146">Un lato dell'espressione deve essere una costante.</span><span class="sxs-lookup"><span data-stu-id="b089a-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="b089a-147">Il nome della proprietà, l'operatore e il valore costante devono essere separati da spazi con codifica URL.</span><span class="sxs-lookup"><span data-stu-id="b089a-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="b089a-148">Uno spazio con codifica URL è come `%20`.</span><span class="sxs-lookup"><span data-stu-id="b089a-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="b089a-149">Viene effettuata la distinzione tra maiuscole e minuscole per tutte le parti della stringa di filtro.</span><span class="sxs-lookup"><span data-stu-id="b089a-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="b089a-150">Il valore costante deve essere dello stesso tipo di dati della proprietà affinché il filtro restituisca risultati validi.</span><span class="sxs-lookup"><span data-stu-id="b089a-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="b089a-151">Per altre informazioni sui tipi di proprietà supportati, vedere [Informazioni sul modello di dati del servizio tabelle](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="b089a-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="b089a-152">La query di esempio illustra come filtrare in base alla proprietà PartitionKey Email usando un `$filter` ODATA.</span><span class="sxs-lookup"><span data-stu-id="b089a-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="b089a-153">**Query**</span><span class="sxs-lookup"><span data-stu-id="b089a-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="b089a-154">Per altre informazioni su come creare espressioni filtro per vari tipi di dati sono disponibili in [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities) (Esecuzione di query su tabelle ed entità).</span><span class="sxs-lookup"><span data-stu-id="b089a-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="b089a-155">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="b089a-155">**Results**</span></span>

| <span data-ttu-id="b089a-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="b089a-156">PartitionKey</span></span> | <span data-ttu-id="b089a-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="b089a-157">RowKey</span></span> | <span data-ttu-id="b089a-158">Email</span><span class="sxs-lookup"><span data-stu-id="b089a-158">Email</span></span> | <span data-ttu-id="b089a-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="b089a-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b089a-160">Ben</span><span class="sxs-lookup"><span data-stu-id="b089a-160">Ben</span></span> |<span data-ttu-id="b089a-161">Smith</span><span class="sxs-lookup"><span data-stu-id="b089a-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="b089a-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="b089a-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="b089a-163">Eseguire una query utilizzando LINQ</span><span class="sxs-lookup"><span data-stu-id="b089a-163">Query by using LINQ</span></span> 
<span data-ttu-id="b089a-164">È anche possibile eseguire query con LINQ, che consente di tradurle nelle corrispondenti espressioni di query OData.</span><span class="sxs-lookup"><span data-stu-id="b089a-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="b089a-165">L'esempio seguente mostra come compilare le query usando .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="b089a-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b089a-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b089a-166">Next steps</span></span>

<span data-ttu-id="b089a-167">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b089a-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b089a-168">È stato appreso come eseguire query usando l'API Table (anteprima)</span><span class="sxs-lookup"><span data-stu-id="b089a-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="b089a-169">È ora possibile passare all'esercitazione successiva per imparare a distribuire i dati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="b089a-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b089a-170">Distribuire i dati a livello globale</span><span class="sxs-lookup"><span data-stu-id="b089a-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
