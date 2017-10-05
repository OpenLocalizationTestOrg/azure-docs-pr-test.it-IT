---
title: Importare i dati in Analytics in Azure Application Insights | Microsoft Docs
description: Importare i dati statici per creare un join con la telemetria dell'app o importare un flusso di dati separato per eseguire query con Analytics.
services: application-insights
keywords: schema aperto, importazione dei dati
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: aa855a9050ec4e5e7c5db88b7209b8bb48bdba51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="9bf0c-104">Importazione di dati in Analytics</span><span class="sxs-lookup"><span data-stu-id="9bf0c-104">Import data into Analytics</span></span>

<span data-ttu-id="9bf0c-105">Importare i dati tabulari in [Analytics](app-insights-analytics.md), ad esempio per creare un join con [Application Insights](app-insights-overview.md) Telemetry dall'app o altro in modo che sia possibile eseguire l'analisi come flusso separato.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-105">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="9bf0c-106">Analytics è un linguaggio di query avanzato ideale per l'analisi dei flussi di timestamp a volume elevato di telemetria.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-106">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="9bf0c-107">È possibile importare dati in Analytics usando uno schema personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="9bf0c-108">Non è necessario usare gli schemi di Application Insights standard, come la richiesta o la traccia.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-108">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="9bf0c-109">È possibile importare i file JSON o DSV (Delimiter-Separated Values: virgola, punto e virgola o tabulazione).</span><span class="sxs-lookup"><span data-stu-id="9bf0c-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="9bf0c-110">L'importazione in Analytics è utile in tre situazioni:</span><span class="sxs-lookup"><span data-stu-id="9bf0c-110">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="9bf0c-111">**Creare un join con la telemetria dell'app.**</span><span class="sxs-lookup"><span data-stu-id="9bf0c-111">**Join with app telemetry.**</span></span> <span data-ttu-id="9bf0c-112">Ad esempio, è possibile importare una tabella che associa gli URL dal sito Web a titoli di pagine più leggibili.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-112">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="9bf0c-113">In Analytics è possibile creare un report grafico del dashboard che mostra le dieci pagine più visitate nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-113">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="9bf0c-114">Consente ora di visualizzare i titoli delle pagine anziché gli URL.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-114">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="9bf0c-115">**Correlare la telemetria dell'applicazione** con altre origini, ad esempio il traffico di rete, i dati del server o i file di log della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="9bf0c-116">**Applicare Analytics a un flusso di dati separato.**</span><span class="sxs-lookup"><span data-stu-id="9bf0c-116">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="9bf0c-117">Application Insights Analytics è uno strumento potente, che funziona bene con flussi di timestamp frammentati, spesso in modo più efficace di SQL.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="9bf0c-118">Se si dispone di tale flusso da un'altra origine, è possibile analizzarlo con Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="9bf0c-119">L'invio di dati all'origine dati è semplice.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-119">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="9bf0c-120">(Una volta) Definire lo schema dei dati in un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-120">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="9bf0c-121">(Periodicamente) Caricare i dati nell'Archiviazione di Azure e chiamare l'API REST per segnalare che nuovi dati sono in attesa per l'inserimento.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-121">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="9bf0c-122">Entro pochi minuti i dati sono disponibili per le query di Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-122">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="9bf0c-123">La frequenza del processo di caricamento viene definita dall'utente e dalla velocità con cui si vuole rendere disponibili i dati per le query.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-123">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="9bf0c-124">È più efficiente caricare i dati in blocchi più grandi, ma non maggiori di 1 GB.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-124">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="9bf0c-125">*Il numero di origini dati da analizzare è elevato?*</span><span class="sxs-lookup"><span data-stu-id="9bf0c-125">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="9bf0c-126">*Si consiglia di usare* logstash *per fornire i dati in Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="9bf0c-126">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="9bf0c-127">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="9bf0c-127">Before you start</span></span>

<span data-ttu-id="9bf0c-128">Sono necessari:</span><span class="sxs-lookup"><span data-stu-id="9bf0c-128">You need:</span></span>

1. <span data-ttu-id="9bf0c-129">Una risorsa di Application Insights in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="9bf0c-130">Se si vuole analizzare i dati separatamente da altra telemetria, [creare una nuova risorsa di Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="9bf0c-130">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="9bf0c-131">Se si sta eseguendo il join o il confronto dei dati con la telemetria di un'app già configurata con Application Insights, è possibile usare la risorsa per questa app.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="9bf0c-132">Accesso del collaboratore o del proprietario a questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-132">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="9bf0c-133">nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-133">Azure storage.</span></span> <span data-ttu-id="9bf0c-134">Si caricano i dati in Archiviazione di Azure e Analytics recupera i dati da questa posizione.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-134">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="9bf0c-135">È consigliabile creare un account di archiviazione dedicato per i BLOB.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="9bf0c-136">Se i BLOB sono condivisi con altri processi, la lettura dei BLOB da parte dei processi richiede più tempo.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-136">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="9bf0c-137">Definire lo schema</span><span class="sxs-lookup"><span data-stu-id="9bf0c-137">Define your schema</span></span>

<span data-ttu-id="9bf0c-138">Prima di poter importare dati, è necessario definire un'*origine dati* che specifica lo schema dei dati.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-138">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="9bf0c-139">È possibile avere fino a 50 origini dati in una singola risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="9bf0c-139">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="9bf0c-140">Avviare la Creazione guidata origine dati.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-140">Start the data source wizard.</span></span> <span data-ttu-id="9bf0c-141">Usare il pulsante "Aggiungi nuova origine dati".</span><span class="sxs-lookup"><span data-stu-id="9bf0c-141">Use "Add new data source" button.</span></span> <span data-ttu-id="9bf0c-142">In alternativa, fare clic sul pulsante Impostazioni nell'angolo in alto a destra e scegliere "Origini dati" nel menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Aggiungere la nuova origine dati](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="9bf0c-144">Immettere un nome per la nuova origine dati.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="9bf0c-145">Definire il formato dei file da caricare.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-145">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="9bf0c-146">È possibile definire il formato manualmente o caricare un file di esempio.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-146">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="9bf0c-147">Se i dati sono in formato CSV, la prima riga dell'esempio può essere costituita da intestazioni di colonna.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-147">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="9bf0c-148">Nel passaggio successivo è possibile modificare i nomi dei campi.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-148">You can change the field names in the next step.</span></span>

    <span data-ttu-id="9bf0c-149">L'esempio deve includere almeno 10 righe o record di dati.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-149">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="9bf0c-150">I nomi di colonna o di campo devono essere alfanumerici (senza spazi o punteggiatura).</span><span class="sxs-lookup"><span data-stu-id="9bf0c-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Caricare un file di esempio](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="9bf0c-152">Esaminare lo schema della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-152">Review the schema that the wizard has got.</span></span> <span data-ttu-id="9bf0c-153">Se i tipi sono stati dedotti da un campione, è possibile che si debbano modificare i tipi dedotti delle colonne.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-153">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![Esaminare lo schema dedotto](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="9bf0c-155">Facoltativo. Caricare una definizione dello schema.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="9bf0c-156">Vedere il formato riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-156">See the format below.</span></span>

 * <span data-ttu-id="9bf0c-157">Selezionare un timestamp.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-157">Select a Timestamp.</span></span> <span data-ttu-id="9bf0c-158">Tutti i dati in Analytics devono avere un campo di timestamp.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="9bf0c-159">Il tipo deve essere `datetime`, ma non deve essere denominato "timestamp".</span><span class="sxs-lookup"><span data-stu-id="9bf0c-159">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="9bf0c-160">Se i dati includono una colonna contenente una data e ora in formato ISO, scegliere questa opzione come colonna di timestamp.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-160">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="9bf0c-161">In caso contrario, scegliere "as data arrived" e il processo di importazione aggiungerà un campo di timestamp.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-161">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="9bf0c-162">Creare l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-162">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="9bf0c-163">Formato del file di definizione dello schema</span><span class="sxs-lookup"><span data-stu-id="9bf0c-163">Schema definition file format</span></span>

<span data-ttu-id="9bf0c-164">Invece di modificare lo schema nell'interfaccia utente, è possibile caricare la definizione dello schema da un file.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-164">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="9bf0c-165">Il formato della definizione dello schema è il seguente:</span><span class="sxs-lookup"><span data-stu-id="9bf0c-165">The schema definition format is as follows:</span></span> 

<span data-ttu-id="9bf0c-166">Formato delimitato</span><span class="sxs-lookup"><span data-stu-id="9bf0c-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="9bf0c-167">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="9bf0c-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="9bf0c-168">Ogni colonna viene identificata da posizione, nome e tipo.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-168">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="9bf0c-169">Location: per un formato file delimitato, indica la posizione del valore di cui è stato eseguito il mapping.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-169">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="9bf0c-170">Per il formato JSON, è il jpath della chiave di cui è stato eseguito il mapping.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-170">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="9bf0c-171">Name: nome visualizzato della colonna.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-171">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="9bf0c-172">Type: tipo di dati della colonna.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-172">Type – the data type of that column.</span></span>
 
<span data-ttu-id="9bf0c-173">Se sono stati usati dati di esempio e se il formato file è delimitato, la definizione dello schema deve eseguire il mapping di tutte le colonne e aggiungere nuove colonne alla fine.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-173">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="9bf0c-174">JSON consente il mapping parziale dei dati, pertanto la definizione dello schema del formato JSON non deve necessariamente eseguire il mapping di ogni chiave individuata nei dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-174">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="9bf0c-175">Può inoltre eseguire il mapping di colonne non appartenenti ai dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-175">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="9bf0c-176">Importa dati</span><span class="sxs-lookup"><span data-stu-id="9bf0c-176">Import data</span></span>

<span data-ttu-id="9bf0c-177">Per importare i dati, caricarli in Archiviazione di Azure, creare una chiave di accesso corrispondente ed eseguire una chiamata API REST.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-177">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![Aggiungere la nuova origine dati](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="9bf0c-179">È possibile eseguire manualmente il processo seguente o configurare un sistema automatizzato per eseguire questa operazione a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-179">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="9bf0c-180">È necessario seguire questi passaggi per ogni blocco di dati da importare.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-180">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="9bf0c-181">Caricare dati nell'[Archiviazione BLOB di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="9bf0c-181">Upload the data to [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="9bf0c-182">I BLOB possono essere di qualsiasi dimensione, fino a 1 GB non compressi.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-182">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="9bf0c-183">I BLOB di centinaia di MB sono ideali dal punto di vista delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="9bf0c-184">È possibile comprimerli con Gzip per migliorare i tempi di caricamento e la latenza per i dati che devono essere disponibili per la query.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-184">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="9bf0c-185">Usare l'estensione del nome file `.gz`.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-185">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="9bf0c-186">È consigliabile usare un account di archiviazione separato per questo scopo, per evitare che le chiamate da altri servizi riducano le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-186">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="9bf0c-187">Quando si inviano dati a frequenza elevata, a intervalli di pochi secondi, è consigliabile usare più account di archiviazione per non incidere sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-187">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="9bf0c-188">[Creare una chiave di firma di accesso condiviso per il BLOB](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="9bf0c-188">[Create a Shared Access Signature key for the blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="9bf0c-189">La chiave deve avere un periodo di scadenza di un giorno e fornire l'accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-189">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="9bf0c-190">Eseguire una chiamata REST per notificare ad Application Insights che i dati sono in attesa.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-190">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="9bf0c-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="9bf0c-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="9bf0c-192">Metodo HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="9bf0c-192">HTTP method: POST</span></span>
 * <span data-ttu-id="9bf0c-193">Payload:</span><span class="sxs-lookup"><span data-stu-id="9bf0c-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="9bf0c-194">I segnaposto sono:</span><span class="sxs-lookup"><span data-stu-id="9bf0c-194">The placeholders are:</span></span>

* <span data-ttu-id="9bf0c-195">`Blob URI with Shared Access Key`: valore ottenuto dalla procedura per la creazione di una chiave.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-195">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="9bf0c-196">È specifico per il BLOB.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-196">It is specific to the blob.</span></span>
* <span data-ttu-id="9bf0c-197">`Schema ID`: l'ID di schema generato per lo schema definito.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-197">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="9bf0c-198">I dati in questo BLOB devono essere conformi allo schema.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-198">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="9bf0c-199">`DateTime`: ora in cui viene inviata la richiesta, UTC.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-199">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="9bf0c-200">Vengono accettati i seguenti formati: ISO8601 (ad esempio "2016-01-01 13:45:01"); RFC822 ("mer, 14 dic 16 14:57:01 +0000"); RFC850 ("mercoledì, 14-dic-16 14:57:00 UTC"); RFC1123 ("mer, 14 dic 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="9bf0c-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="9bf0c-201">`Instrumentation key` della risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="9bf0c-202">I dati sono disponibili in Analytics dopo alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-202">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="9bf0c-203">Risposte agli errori</span><span class="sxs-lookup"><span data-stu-id="9bf0c-203">Error responses</span></span>

* <span data-ttu-id="9bf0c-204">**400 richiesta non valida**: indica che il payload della richiesta non è valido.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-204">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="9bf0c-205">Controllare:</span><span class="sxs-lookup"><span data-stu-id="9bf0c-205">Check:</span></span>
 * <span data-ttu-id="9bf0c-206">Chiave di strumentazione corretta.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="9bf0c-207">Valore dell'ora valido.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-207">Valid time value.</span></span> <span data-ttu-id="9bf0c-208">L'ora dovrebbe essere in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-208">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="9bf0c-209">Il codice JSON dell'evento è conforme allo schema.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-209">JSON of the event conforms to the schema.</span></span>
* <span data-ttu-id="9bf0c-210">**403 - Accesso negato**: non è possibile accedere al BLOB inviato.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-210">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="9bf0c-211">Assicurarsi che la chiave di accesso condiviso sia valida e non scaduta.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-211">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="9bf0c-212">**404 - Pagina non trovata**:</span><span class="sxs-lookup"><span data-stu-id="9bf0c-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="9bf0c-213">Il BLOB non esiste.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-213">The blob doesn't exist.</span></span>
 * <span data-ttu-id="9bf0c-214">Il valore sourceId non è valido.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-214">The sourceId is wrong.</span></span>

<span data-ttu-id="9bf0c-215">Informazioni più dettagliate sono disponibili nel messaggio di errore della risposta.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-215">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="9bf0c-216">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="9bf0c-216">Sample code</span></span>

<span data-ttu-id="9bf0c-217">Questo codice usa il pacchetto NuGet [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1).</span><span class="sxs-lookup"><span data-stu-id="9bf0c-217">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="9bf0c-218">Classi</span><span class="sxs-lookup"><span data-stu-id="9bf0c-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="9bf0c-219">Inserire dati</span><span class="sxs-lookup"><span data-stu-id="9bf0c-219">Ingest data</span></span>

<span data-ttu-id="9bf0c-220">Usare questo codice per ogni BLOB.</span><span class="sxs-lookup"><span data-stu-id="9bf0c-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="9bf0c-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bf0c-221">Next steps</span></span>

* [<span data-ttu-id="9bf0c-222">Presentazione del linguaggio di query di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9bf0c-222">Tour of the Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="9bf0c-223">Usare *Logstash* per inviare i dati ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="9bf0c-223">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
