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
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>Elenco delle risorse di archiviazione di Azure in C++
Elenco operazioni sono gli scenari di sviluppo toomany chiave con l'archiviazione di Azure. In questo articolo viene descritto come toomost enumerare in modo efficiente gli oggetti nell'archiviazione di Azure utilizzando hello elencare le API disponibili in Microsoft Azure Storage Client Library hello per C++.

> [!NOTE]
> Questa guida è destinata hello Azure Storage Client Library per C++ versione 2. x, che è disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Hello libreria Client di archiviazione offre un'ampia gamma di toolist metodi o gli oggetti query in archiviazione di Azure. Questo articolo illustra hello seguenti scenari:

* Contenitori di elenco in un account
* Elencare i BLOB in un contenitore o una directory blob virtuale
* Elenco delle code in un account
* Elenco di tabelle in un account
* Entità di query in una tabella

Ognuno di questi metodi viene visualizzato utilizzando diversi overload per scenari diversi.

## <a name="asynchronous-versus-synchronous"></a>Asincrono o sincrono
Poiché hello libreria Client di archiviazione per C++ si basa su hello [libreria di C++ REST](https://github.com/Microsoft/cpprestsdk), è progettato per supportare operazioni asincrone utilizzando [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). ad esempio:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Operazioni sincrone incapsulare operazioni asincrone di hello corrispondente:

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

Se si lavora con più applicazioni o servizi di threading, è consigliabile utilizzare async hello API direttamente anziché la creazione di una sincronizzazione di hello toocall API, che influiscono significativamente sulle prestazioni del thread.

## <a name="segmented-listing"></a>Elenco segmentato
scala Hello di archiviazione cloud richiede segmentata elenco. Ad esempio, è possibile avere più di un milione di BLOB in un contenitore di blob di Azure o più di un miliardo di entità in una tabella di Azure. Non sono numeri teorici, ma casi di utilizzo di clienti reali.

È pertanto poco toolist tutti gli oggetti in una singola risposta. Al contrario, è possibile elencare gli oggetti utilizzando la paginazione. Ciascuna delle hello elenco API dispone di un *segmentata* rapporto di overload.

risposta Hello per un'operazione elenco segmentata include:

* <i>_segment</i>, che contiene hello set di risultati restituiti per toohello una singola chiamata API di elenco.
* *continuation_token*, che viene passato toohello successiva chiamata nell'ordine tooget hello pagina di risultati successiva. Quando sono non presenti più tooreturn risultati, il token di continuazione hello è null.

Ad esempio, un toolist tipica chiamata tutti i BLOB in un contenitore potrebbero simile hello seguente frammento di codice. codice Hello è disponibile nel nostro [esempi](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

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

Si noti che il numero di hello di risultati restituiti in una pagina può essere controllato dal parametro hello *max_results* in overload hello di ogni API, ad esempio:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Se non si specifica hello *max_results* parametro predefinito hello viene restituito il valore massimo di backup too5000 risultati in una singola pagina.

Si noti inoltre che una query sull'archiviazione tabelle di Azure può restituire alcun record o un numero di record di valore hello di hello *max_results* parametro specificato, anche se il token di continuazione hello non è vuoto. Un motivo per cui potrebbe essere che Impossibile completare la query hello in cinque secondi. Fino a quando il token di continuazione hello non è vuoto, deve continuare query hello e il codice non deve presupporre dimensioni hello dei risultati di segmento.

Hello consiglia di modello per la maggior parte degli scenari di codifica è segmentata elenco, che fornisce lo stato di avanzamento esplicita di elenco o l'esecuzione di query e modalità di risposta del servizio hello tooeach richiesta. In particolare per i servizi o applicazioni di C++, il controllo di livello inferiore di hello elenca lo stato di avanzamento consentono di memoria di controllo e le prestazioni.

## <a name="greedy-listing"></a>Elenco greedy
Le versioni precedenti di hello libreria Client di archiviazione per C++ (versioni 0.5.0 visualizzare in anteprima e versioni precedenti) incluso non segmentato listato API per le tabelle e code, come in hello di esempio seguente:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Questi metodi sono stati implementati come wrapper di API segmentate. Per ogni risposta di inserzione segmentati, codice hello aggiunto vettore di tooa risultati hello e restituiti tutti i risultati dopo che sono stati analizzati i contenitori completo hello.

Questo approccio potrebbe funzionare quando l'account di archiviazione hello o una tabella contiene un numero ridotto di oggetti. Tuttavia, con un aumento nel numero hello di oggetti, memoria hello richiesta potrebbe aumentare senza limitazioni, perché tutti i risultati sono rimasti in memoria. Un'operazione di elenco può richiedere molto tempo, durante i quali hello chiamante non disponeva di informazioni sul relativo stato di avanzamento.

Questi greedy elenco API hello SDK non esiste in c#, Java, o hello ambiente JavaScript Node.js. tooavoid hello potenziali problemi di utilizzo di queste API greedy, sono state rimosse le versione 0.6.0 anteprima.

Se il codice chiama tali API greedy:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Quindi è necessario modificare il codice hello toouse segmentata elenco API:

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

Specificando hello *max_results* parametro del segmento di hello, è possibile bilanciare tra un numero di richieste hello e considerazioni sulle prestazioni di memoria utilizzo toomeet per l'applicazione.

Inoltre, se si sta utilizzando l'elenco segmentata API ma archiviano dati hello in una raccolta locale in uno stile "greedy", è inoltre consigliabile effettuare il refactoring del toohandle codice l'archiviazione dei dati in una raccolta locale con attenzione su larga scala.

## <a name="lazy-listing"></a>Elenco Lazy
Sebbene listato greedy generato potenziali problemi, è utile se sono presenti troppi oggetti nel contenitore di hello.

Se si utilizza anche in c# o Oracle Java SDK, è necessario conoscere hello enumerabile modello di programmazione, che offre un differita di tipo elenco, in cui hello dati a un determinato offset solo se viene recuperati è obbligatorio. In C++, il modello basato su iteratore hello fornisce inoltre un approccio simile.

Un'API tipica ad elenco lazy, che usa **list_blobs** come esempio, è simile a quanto segue:

```cpp
list_blob_item_iterator list_blobs() const;
```

Un frammento di codice tipico che utilizza il modello di elenco lazy hello potrebbe essere simile al seguente:

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

Si noti che l’elenco lazy è disponibile solo in modalità sincrona.

Un elenco lazy rispetto a un elenco greedy, recupera i dati solo quando necessario. In realtà hello, il recupero dei dati da archiviazione di Azure solo quando si sposta iteratore successivo hello nel segmento successivo. Pertanto, utilizzo della memoria è controllato con dimensioni limitate e operazione hello è veloce.

Elenco lazy API sono inclusi in hello libreria Client di archiviazione per C++ nella versione 2.2.0.

## <a name="conclusion"></a>Conclusioni
In questo articolo sono descritti diversi overload per elencare le API per vari oggetti in hello libreria Client di archiviazione per C++. toosummarize:

* Le API asincrone sono fortemente consigliate in più scenari di threading.
* L’elenco segmentato è consigliabile per la maggior parte degli scenari.
* Elenco lazy viene fornita nella libreria hello un wrapper utile negli scenari sincroni.
* Elenco greedy non è consigliata ed è stata rimossa dalla libreria hello.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'archiviazione di Azure e la libreria Client per C++, vedere hello seguenti risorse.

* [Come toouse archiviazione Blob da C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Come toouse archiviazione tabelle da C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Come toouse l'archiviazione delle code da C++](../storage-c-plus-plus-how-to-use-queues.md)
* [Documentazione relativa alla libreria Client di archiviazione Azure per API C++.](http://azure.github.io/azure-storage-cpp/)
* [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Documentazione di Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)

