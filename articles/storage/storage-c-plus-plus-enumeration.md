---
title: risorse di archiviazione di Azure aaaList con hello libreria Client di archiviazione per C++ | Documenti Microsoft
description: "Informazioni su come hello toouse elenco API nella libreria Client di archiviazione di Microsoft Azure per i contenitori tooenumerate C++, BLOB, code, tabelle ed entità."
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
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="474fa-103">Elenco delle risorse di archiviazione di Azure in C++</span><span class="sxs-lookup"><span data-stu-id="474fa-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="474fa-104">Elenco operazioni sono gli scenari di sviluppo toomany chiave con l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="474fa-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="474fa-105">In questo articolo viene descritto come toomost enumerare in modo efficiente gli oggetti nell'archiviazione di Azure utilizzando hello elencare le API disponibili in Microsoft Azure Storage Client Library hello per C++.</span><span class="sxs-lookup"><span data-stu-id="474fa-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="474fa-106">Questa guida è destinata hello Azure Storage Client Library per C++ versione 2. x, che è disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="474fa-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="474fa-107">Hello libreria Client di archiviazione offre un'ampia gamma di toolist metodi o gli oggetti query in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="474fa-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="474fa-108">Questo articolo illustra hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="474fa-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="474fa-109">Contenitori di elenco in un account</span><span class="sxs-lookup"><span data-stu-id="474fa-109">List containers in an account</span></span>
* <span data-ttu-id="474fa-110">Elencare i BLOB in un contenitore o una directory blob virtuale</span><span class="sxs-lookup"><span data-stu-id="474fa-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="474fa-111">Elenco delle code in un account</span><span class="sxs-lookup"><span data-stu-id="474fa-111">List queues in an account</span></span>
* <span data-ttu-id="474fa-112">Elenco di tabelle in un account</span><span class="sxs-lookup"><span data-stu-id="474fa-112">List tables in an account</span></span>
* <span data-ttu-id="474fa-113">Entità di query in una tabella</span><span class="sxs-lookup"><span data-stu-id="474fa-113">Query entities in a table</span></span>

<span data-ttu-id="474fa-114">Ognuno di questi metodi viene visualizzato utilizzando diversi overload per scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="474fa-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="474fa-115">Asincrono o sincrono</span><span class="sxs-lookup"><span data-stu-id="474fa-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="474fa-116">Poiché hello libreria Client di archiviazione per C++ si basa su hello [libreria di C++ REST](https://github.com/Microsoft/cpprestsdk), è progettato per supportare operazioni asincrone utilizzando [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="474fa-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="474fa-117">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="474fa-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="474fa-118">Operazioni sincrone incapsulare operazioni asincrone di hello corrispondente:</span><span class="sxs-lookup"><span data-stu-id="474fa-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="474fa-119">Se si lavora con più applicazioni o servizi di threading, è consigliabile utilizzare async hello API direttamente anziché la creazione di una sincronizzazione di hello toocall API, che influiscono significativamente sulle prestazioni del thread.</span><span class="sxs-lookup"><span data-stu-id="474fa-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="474fa-120">Elenco segmentato</span><span class="sxs-lookup"><span data-stu-id="474fa-120">Segmented listing</span></span>
<span data-ttu-id="474fa-121">scala Hello di archiviazione cloud richiede segmentata elenco.</span><span class="sxs-lookup"><span data-stu-id="474fa-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="474fa-122">Ad esempio, è possibile avere più di un milione di BLOB in un contenitore di blob di Azure o più di un miliardo di entità in una tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="474fa-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="474fa-123">Non sono numeri teorici, ma casi di utilizzo di clienti reali.</span><span class="sxs-lookup"><span data-stu-id="474fa-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="474fa-124">È pertanto poco toolist tutti gli oggetti in una singola risposta.</span><span class="sxs-lookup"><span data-stu-id="474fa-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="474fa-125">Al contrario, è possibile elencare gli oggetti utilizzando la paginazione.</span><span class="sxs-lookup"><span data-stu-id="474fa-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="474fa-126">Ciascuna delle hello elenco API dispone di un *segmentata* rapporto di overload.</span><span class="sxs-lookup"><span data-stu-id="474fa-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="474fa-127">risposta Hello per un'operazione elenco segmentata include:</span><span class="sxs-lookup"><span data-stu-id="474fa-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="474fa-128"><i>_segment</i>, che contiene hello set di risultati restituiti per toohello una singola chiamata API di elenco.</span><span class="sxs-lookup"><span data-stu-id="474fa-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="474fa-129">*continuation_token*, che viene passato toohello successiva chiamata nell'ordine tooget hello pagina di risultati successiva.</span><span class="sxs-lookup"><span data-stu-id="474fa-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="474fa-130">Quando sono non presenti più tooreturn risultati, il token di continuazione hello è null.</span><span class="sxs-lookup"><span data-stu-id="474fa-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="474fa-131">Ad esempio, un toolist tipica chiamata tutti i BLOB in un contenitore potrebbero simile hello seguente frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="474fa-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="474fa-132">codice Hello è disponibile nel nostro [esempi](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="474fa-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
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

<span data-ttu-id="474fa-133">Si noti che il numero di hello di risultati restituiti in una pagina può essere controllato dal parametro hello *max_results* in overload hello di ogni API, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="474fa-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="474fa-134">Se non si specifica hello *max_results* parametro predefinito hello viene restituito il valore massimo di backup too5000 risultati in una singola pagina.</span><span class="sxs-lookup"><span data-stu-id="474fa-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="474fa-135">Si noti inoltre che una query sull'archiviazione tabelle di Azure può restituire alcun record o un numero di record di valore hello di hello *max_results* parametro specificato, anche se il token di continuazione hello non è vuoto.</span><span class="sxs-lookup"><span data-stu-id="474fa-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="474fa-136">Un motivo per cui potrebbe essere che Impossibile completare la query hello in cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="474fa-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="474fa-137">Fino a quando il token di continuazione hello non è vuoto, deve continuare query hello e il codice non deve presupporre dimensioni hello dei risultati di segmento.</span><span class="sxs-lookup"><span data-stu-id="474fa-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="474fa-138">Hello consiglia di modello per la maggior parte degli scenari di codifica è segmentata elenco, che fornisce lo stato di avanzamento esplicita di elenco o l'esecuzione di query e modalità di risposta del servizio hello tooeach richiesta.</span><span class="sxs-lookup"><span data-stu-id="474fa-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="474fa-139">In particolare per i servizi o applicazioni di C++, il controllo di livello inferiore di hello elenca lo stato di avanzamento consentono di memoria di controllo e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="474fa-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="474fa-140">Elenco greedy</span><span class="sxs-lookup"><span data-stu-id="474fa-140">Greedy listing</span></span>
<span data-ttu-id="474fa-141">Le versioni precedenti di hello libreria Client di archiviazione per C++ (versioni 0.5.0 visualizzare in anteprima e versioni precedenti) incluso non segmentato listato API per le tabelle e code, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="474fa-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="474fa-142">Questi metodi sono stati implementati come wrapper di API segmentate.</span><span class="sxs-lookup"><span data-stu-id="474fa-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="474fa-143">Per ogni risposta di inserzione segmentati, codice hello aggiunto vettore di tooa risultati hello e restituiti tutti i risultati dopo che sono stati analizzati i contenitori completo hello.</span><span class="sxs-lookup"><span data-stu-id="474fa-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="474fa-144">Questo approccio potrebbe funzionare quando l'account di archiviazione hello o una tabella contiene un numero ridotto di oggetti.</span><span class="sxs-lookup"><span data-stu-id="474fa-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="474fa-145">Tuttavia, con un aumento nel numero hello di oggetti, memoria hello richiesta potrebbe aumentare senza limitazioni, perché tutti i risultati sono rimasti in memoria.</span><span class="sxs-lookup"><span data-stu-id="474fa-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="474fa-146">Un'operazione di elenco può richiedere molto tempo, durante i quali hello chiamante non disponeva di informazioni sul relativo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="474fa-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="474fa-147">Questi greedy elenco API hello SDK non esiste in c#, Java, o hello ambiente JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="474fa-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="474fa-148">tooavoid hello potenziali problemi di utilizzo di queste API greedy, sono state rimosse le versione 0.6.0 anteprima.</span><span class="sxs-lookup"><span data-stu-id="474fa-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="474fa-149">Se il codice chiama tali API greedy:</span><span class="sxs-lookup"><span data-stu-id="474fa-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="474fa-150">Quindi è necessario modificare il codice hello toouse segmentata elenco API:</span><span class="sxs-lookup"><span data-stu-id="474fa-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

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

<span data-ttu-id="474fa-151">Specificando hello *max_results* parametro del segmento di hello, è possibile bilanciare tra un numero di richieste hello e considerazioni sulle prestazioni di memoria utilizzo toomeet per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="474fa-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="474fa-152">Inoltre, se si sta utilizzando l'elenco segmentata API ma archiviano dati hello in una raccolta locale in uno stile "greedy", è inoltre consigliabile effettuare il refactoring del toohandle codice l'archiviazione dei dati in una raccolta locale con attenzione su larga scala.</span><span class="sxs-lookup"><span data-stu-id="474fa-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="474fa-153">Elenco Lazy</span><span class="sxs-lookup"><span data-stu-id="474fa-153">Lazy listing</span></span>
<span data-ttu-id="474fa-154">Sebbene listato greedy generato potenziali problemi, è utile se sono presenti troppi oggetti nel contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="474fa-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="474fa-155">Se si utilizza anche in c# o Oracle Java SDK, è necessario conoscere hello enumerabile modello di programmazione, che offre un differita di tipo elenco, in cui hello dati a un determinato offset solo se viene recuperati è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="474fa-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="474fa-156">In C++, il modello basato su iteratore hello fornisce inoltre un approccio simile.</span><span class="sxs-lookup"><span data-stu-id="474fa-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="474fa-157">Un'API tipica ad elenco lazy, che usa **list_blobs** come esempio, è simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="474fa-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="474fa-158">Un frammento di codice tipico che utilizza il modello di elenco lazy hello potrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="474fa-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
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

<span data-ttu-id="474fa-159">Si noti che l’elenco lazy è disponibile solo in modalità sincrona.</span><span class="sxs-lookup"><span data-stu-id="474fa-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="474fa-160">Un elenco lazy rispetto a un elenco greedy, recupera i dati solo quando necessario.</span><span class="sxs-lookup"><span data-stu-id="474fa-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="474fa-161">In realtà hello, il recupero dei dati da archiviazione di Azure solo quando si sposta iteratore successivo hello nel segmento successivo.</span><span class="sxs-lookup"><span data-stu-id="474fa-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="474fa-162">Pertanto, utilizzo della memoria è controllato con dimensioni limitate e operazione hello è veloce.</span><span class="sxs-lookup"><span data-stu-id="474fa-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="474fa-163">Elenco lazy API sono inclusi in hello libreria Client di archiviazione per C++ nella versione 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="474fa-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="474fa-164">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="474fa-164">Conclusion</span></span>
<span data-ttu-id="474fa-165">In questo articolo sono descritti diversi overload per elencare le API per vari oggetti in hello libreria Client di archiviazione per C++.</span><span class="sxs-lookup"><span data-stu-id="474fa-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="474fa-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="474fa-166">toosummarize:</span></span>

* <span data-ttu-id="474fa-167">Le API asincrone sono fortemente consigliate in più scenari di threading.</span><span class="sxs-lookup"><span data-stu-id="474fa-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="474fa-168">L’elenco segmentato è consigliabile per la maggior parte degli scenari.</span><span class="sxs-lookup"><span data-stu-id="474fa-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="474fa-169">Elenco lazy viene fornita nella libreria hello un wrapper utile negli scenari sincroni.</span><span class="sxs-lookup"><span data-stu-id="474fa-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="474fa-170">Elenco greedy non è consigliata ed è stata rimossa dalla libreria hello.</span><span class="sxs-lookup"><span data-stu-id="474fa-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="474fa-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="474fa-171">Next steps</span></span>
<span data-ttu-id="474fa-172">Per ulteriori informazioni sull'archiviazione di Azure e la libreria Client per C++, vedere hello seguenti risorse.</span><span class="sxs-lookup"><span data-stu-id="474fa-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="474fa-173">Come toouse archiviazione Blob da C++</span><span class="sxs-lookup"><span data-stu-id="474fa-173">How toouse Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="474fa-174">Come toouse archiviazione tabelle da C++</span><span class="sxs-lookup"><span data-stu-id="474fa-174">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="474fa-175">Come toouse l'archiviazione delle code da C++</span><span class="sxs-lookup"><span data-stu-id="474fa-175">How toouse Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="474fa-176">Documentazione relativa alla libreria Client di archiviazione Azure per API C++.</span><span class="sxs-lookup"><span data-stu-id="474fa-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="474fa-177">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="474fa-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="474fa-178">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="474fa-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

