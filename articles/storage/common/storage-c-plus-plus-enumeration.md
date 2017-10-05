---
title: Elencare le risorse di archiviazione di Azure con la libreria client di archiviazione per C++ | Documentazione Microsoft
description: "Imparare a utilizzare le API elencate nella libreria Client di archiviazione di Microsoft Azure per C++ per enumerare contenitori, BLOB, code, tabelle ed entità."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: 9844412739f4f6f95416f81347f0f2eeeca62bea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="013e9-103">Elenco delle risorse di archiviazione di Azure in C++</span><span class="sxs-lookup"><span data-stu-id="013e9-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="013e9-104">Elenco operazioni fondamentali per numerosi scenari di sviluppo con la risorsa di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="013e9-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="013e9-105">In questo articolo viene descritto come enumerare in modo più efficiente gli oggetti in archiviazione di Azure utilizzando l'elenco interfacce API fornito nella libreria client di archiviazione di Microsoft Azure per C++.</span><span class="sxs-lookup"><span data-stu-id="013e9-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="013e9-106">Questa guida fa riferimento alla libreria client di Archiviazione di Azure per la versione 2.x di C++, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="013e9-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="013e9-107">La libreria Client di archiviazione fornisce un'ampia gamma di metodi per elencare o effettuare una query degli oggetti nel servizio di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="013e9-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="013e9-108">In questo articolo vengono affrontati i seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="013e9-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="013e9-109">Contenitori di elenco in un account</span><span class="sxs-lookup"><span data-stu-id="013e9-109">List containers in an account</span></span>
* <span data-ttu-id="013e9-110">Elencare i BLOB in un contenitore o una directory blob virtuale</span><span class="sxs-lookup"><span data-stu-id="013e9-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="013e9-111">Elenco delle code in un account</span><span class="sxs-lookup"><span data-stu-id="013e9-111">List queues in an account</span></span>
* <span data-ttu-id="013e9-112">Elenco di tabelle in un account</span><span class="sxs-lookup"><span data-stu-id="013e9-112">List tables in an account</span></span>
* <span data-ttu-id="013e9-113">Entità di query in una tabella</span><span class="sxs-lookup"><span data-stu-id="013e9-113">Query entities in a table</span></span>

<span data-ttu-id="013e9-114">Ognuno di questi metodi viene visualizzato utilizzando diversi overload per scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="013e9-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="013e9-115">Asincrono o sincrono</span><span class="sxs-lookup"><span data-stu-id="013e9-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="013e9-116">Poiché la libreria client di archiviazione per C++ viene compilata sopra la [libreria REST C++](https://github.com/Microsoft/cpprestsdk), le operazioni asincrone sono intrinsecamente supportate tramite [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="013e9-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="013e9-117">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="013e9-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="013e9-118">Operazioni sincrone incapsulano le corrispondenti operazioni asincrone:</span><span class="sxs-lookup"><span data-stu-id="013e9-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="013e9-119">Se si lavora con più applicazioni o servizi di threading, è consigliabile utilizzare direttamente l'API asincrona anziché creare un thread per chiamare le API sincrone, poiché quest’ultima operazione influisce notevolmente sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="013e9-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="013e9-120">Elenco segmentato</span><span class="sxs-lookup"><span data-stu-id="013e9-120">Segmented listing</span></span>
<span data-ttu-id="013e9-121">La scalabilità di archiviazione cloud richiede un elenco segmentato.</span><span class="sxs-lookup"><span data-stu-id="013e9-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="013e9-122">Ad esempio, è possibile avere più di un milione di BLOB in un contenitore di blob di Azure o più di un miliardo di entità in una tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="013e9-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="013e9-123">Non sono numeri teorici, ma casi di utilizzo di clienti reali.</span><span class="sxs-lookup"><span data-stu-id="013e9-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="013e9-124">Pertanto non è pratico elencare tutti gli oggetti in un'unica risposta.</span><span class="sxs-lookup"><span data-stu-id="013e9-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="013e9-125">Al contrario, è possibile elencare gli oggetti utilizzando la paginazione.</span><span class="sxs-lookup"><span data-stu-id="013e9-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="013e9-126">Ogni elenco API ha un overload *segmentato* .</span><span class="sxs-lookup"><span data-stu-id="013e9-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="013e9-127">La risposta per un'operazione elenco segmentato include:</span><span class="sxs-lookup"><span data-stu-id="013e9-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="013e9-128"><i>_segment</i>che contiene il set di risultati restituiti per una singola chiamata all'elenco API.</span><span class="sxs-lookup"><span data-stu-id="013e9-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="013e9-129">*continuation_token* che viene passato alla chiamata successiva per ottenere la pagina successiva dei risultati.</span><span class="sxs-lookup"><span data-stu-id="013e9-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="013e9-130">Quando non sono presenti ulteriori risultati da restituire, il token di continuazione è nullo.</span><span class="sxs-lookup"><span data-stu-id="013e9-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="013e9-131">Ad esempio, una chiamata tipica per ottenere un elenco di tutti i BLOB in un contenitore può essere simile al seguente frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="013e9-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="013e9-132">Il codice è disponibile nei nostri [esempi](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="013e9-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="013e9-133">Si noti che il numero di risultati restituiti in una pagina può essere controllato dal parametro*max_results* nell'overload di ogni API, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="013e9-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="013e9-134">Se non si specifica il parametro *max_results*, il valore massimo predefinito di 5000 risultati viene restituito in un'unica pagina.</span><span class="sxs-lookup"><span data-stu-id="013e9-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="013e9-135">Si noti anche che una query sull'archiviazione di tabelle di Azure può non restituire alcun record o record di numero inferiore al valore del parametro *max_results* specificato, anche se il token di continuazione non è vuoto.</span><span class="sxs-lookup"><span data-stu-id="013e9-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="013e9-136">Una delle cause potrebbe essere il fatto che la query non può essere completata in cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="013e9-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="013e9-137">Fino a quando il token di continuazione non è vuoto, la query dovrebbe continuare e il codice non dovrebbe presupporre le dimensioni dei risultati del segmento.</span><span class="sxs-lookup"><span data-stu-id="013e9-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="013e9-138">Il modello di codifica consigliato per la maggior parte degli scenari è l’elenco segmentato, che fornisce lo stato di avanzamento esplicito di elenco o di una query e informazioni su come il servizio risponde a ciascuna richiesta.</span><span class="sxs-lookup"><span data-stu-id="013e9-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="013e9-139">In particolare per le applicazioni o i servizi C++, il controllo a basso livello dello stato dell'elenco può aiutare a controllare memoria e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="013e9-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="013e9-140">Elenco greedy</span><span class="sxs-lookup"><span data-stu-id="013e9-140">Greedy listing</span></span>
<span data-ttu-id="013e9-141">Le versioni precedenti della libreria Client di archiviazione per C++ (versioni 0.5.0 anteprima e versioni precedenti) includevano API ad elenco non segmentato per tabelle e code, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="013e9-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="013e9-142">Questi metodi sono stati implementati come wrapper di API segmentate.</span><span class="sxs-lookup"><span data-stu-id="013e9-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="013e9-143">Per ogni risposta dell’elenco segmentato, il codice aggiungeva i risultati a un vettore e restituiva tutti i risultati dopo l’analisi dei contenitori completi.</span><span class="sxs-lookup"><span data-stu-id="013e9-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="013e9-144">Questo approccio potrebbe funzionare quando l'account o la tabella di archiviazione contiene un numero limitato di oggetti.</span><span class="sxs-lookup"><span data-stu-id="013e9-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="013e9-145">Tuttavia, con un aumento del numero di oggetti, la quantità di memoria necessaria potrebbe aumentare a dismisura, poiché tutti i risultati rimangono in memoria.</span><span class="sxs-lookup"><span data-stu-id="013e9-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="013e9-146">Un'operazione di elenco può richiedere molto tempo, durante il quale il chiamante non dispone di alcuna informazione sul relativo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="013e9-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="013e9-147">Questi API a elenco greedy nell’SDK non esistono in C#, Java o nell’ambiente JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="013e9-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="013e9-148">Per evitare i potenziali problemi relativi  all’utilizzo di queste API greedy, esse sono state rimosse nella versione 0.6.0 anteprima.</span><span class="sxs-lookup"><span data-stu-id="013e9-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="013e9-149">Se il codice chiama tali API greedy:</span><span class="sxs-lookup"><span data-stu-id="013e9-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="013e9-150">È quindi necessario modificare il codice per utilizzare l'elenco segmentato API:</span><span class="sxs-lookup"><span data-stu-id="013e9-150">Then you should modify your code to use the segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="013e9-151">Specificando il parametro *max_results* del segmento, è possibile bilanciare numero di richieste e uso della memoria per soddisfare le considerazioni sulle prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="013e9-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="013e9-152">Se si usano anche API a elenco segmentato, ma si memorizzano i dati in una raccolta locale in stile "greedy", è consigliabile effettuare il refactoring del codice per gestire l'archiviazione dei dati in una raccolta locale facendo attenzione alla scalabilità.</span><span class="sxs-lookup"><span data-stu-id="013e9-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="013e9-153">Elenco Lazy</span><span class="sxs-lookup"><span data-stu-id="013e9-153">Lazy listing</span></span>
<span data-ttu-id="013e9-154">Benché l’elenco greedy generi potenziali problemi, è conveniente non avere troppi oggetti nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="013e9-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="013e9-155">Se si usa anche C# o Oracle Java SDK, è necessario conoscere il modello di programmazione enumerabile, che offre un elenco in stile lazy, in cui i dati in un determinato offset vengono recuperati solo se necessario.</span><span class="sxs-lookup"><span data-stu-id="013e9-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="013e9-156">In C++, il modello basato sull’iteratore offre inoltre un approccio simile.</span><span class="sxs-lookup"><span data-stu-id="013e9-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="013e9-157">Un'API tipica ad elenco lazy, che usa **list_blobs** come esempio, è simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="013e9-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="013e9-158">Un frammento di codice tipico che utilizza il modello di elenco lazy è simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="013e9-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="013e9-159">Si noti che l’elenco lazy è disponibile solo in modalità sincrona.</span><span class="sxs-lookup"><span data-stu-id="013e9-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="013e9-160">Un elenco lazy rispetto a un elenco greedy, recupera i dati solo quando necessario.</span><span class="sxs-lookup"><span data-stu-id="013e9-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="013e9-161">Nascosto, recupera dati dall’archiviazione di Azure solo quando l'iteratore successivo si sposta nel segmento successivo.</span><span class="sxs-lookup"><span data-stu-id="013e9-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="013e9-162">Pertanto, l'utilizzo della memoria è controllato con una dimensione limitata e l'operazione è veloce.</span><span class="sxs-lookup"><span data-stu-id="013e9-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="013e9-163">Le API ad elenco lazy sono incluse nella libreria client di archiviazione per C++ nella versione 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="013e9-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="013e9-164">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="013e9-164">Conclusion</span></span>
<span data-ttu-id="013e9-165">In questo articolo, abbiamo parlato di diversi overload per elencare le API per vari oggetti nella libreria Client di archiviazione per C++.</span><span class="sxs-lookup"><span data-stu-id="013e9-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="013e9-166">Per riepilogare:</span><span class="sxs-lookup"><span data-stu-id="013e9-166">To summarize:</span></span>

* <span data-ttu-id="013e9-167">Le API asincrone sono fortemente consigliate in più scenari di threading.</span><span class="sxs-lookup"><span data-stu-id="013e9-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="013e9-168">L’elenco segmentato è consigliabile per la maggior parte degli scenari.</span><span class="sxs-lookup"><span data-stu-id="013e9-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="013e9-169">L’elenco lazy viene fornito nella libreria in qualità di wrapper conveniente negli scenari sincroni.</span><span class="sxs-lookup"><span data-stu-id="013e9-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="013e9-170">L’elenco greedy non è consigliato ed è stato rimosso dalla libreria.</span><span class="sxs-lookup"><span data-stu-id="013e9-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="013e9-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="013e9-171">Next steps</span></span>
<span data-ttu-id="013e9-172">Per ulteriori informazioni sull'archiviazione di Azure e sulla libreria Client per C++, vedere le risorse seguenti.</span><span class="sxs-lookup"><span data-stu-id="013e9-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="013e9-173">Come usare l’archiviazione BLOB da C++</span><span class="sxs-lookup"><span data-stu-id="013e9-173">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="013e9-174">Come usare l’archiviazione tabelle da C++</span><span class="sxs-lookup"><span data-stu-id="013e9-174">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="013e9-175">Come usare l’archiviazione delle code da C++</span><span class="sxs-lookup"><span data-stu-id="013e9-175">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="013e9-176">Documentazione relativa alla libreria Client di archiviazione Azure per API C++.</span><span class="sxs-lookup"><span data-stu-id="013e9-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="013e9-177">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="013e9-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="013e9-178">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="013e9-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

