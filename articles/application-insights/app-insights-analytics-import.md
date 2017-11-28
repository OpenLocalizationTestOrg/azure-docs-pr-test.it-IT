---
title: aaaImport tooAnalytics i dati in Azure Application Insights | Documenti Microsoft
description: Importare i dati statici toojoin con dati di telemetria app oppure importare una tooquery di flusso di dati separato con Analitica.
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
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="23dc8-104">Importazione di dati in Analytics</span><span class="sxs-lookup"><span data-stu-id="23dc8-104">Import data into Analytics</span></span>

<span data-ttu-id="23dc8-105">Importare i dati tabulari in [Analitica](app-insights-analytics.md), entrambi toojoin con [Application Insights](app-insights-overview.md) telemetria dall'app, o in modo che sia possibile analizzarli come flusso separato.</span><span class="sxs-lookup"><span data-stu-id="23dc8-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="23dc8-106">Analitica è un timestamp con volumi elevati flussi di query avanzate language tooanalyzing ideale di telemetria.</span><span class="sxs-lookup"><span data-stu-id="23dc8-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="23dc8-107">È possibile importare dati in Analytics usando uno schema personalizzato.</span><span class="sxs-lookup"><span data-stu-id="23dc8-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="23dc8-108">Non dispone di schemi standard Application Insights toouse hello, ad esempio traccia o di richiesta.</span><span class="sxs-lookup"><span data-stu-id="23dc8-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="23dc8-109">È possibile importare i file JSON o DSV (Delimiter-Separated Values: virgola, punto e virgola o tabulazione).</span><span class="sxs-lookup"><span data-stu-id="23dc8-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="23dc8-110">Ci sono tre i casi in cui l'importazione tooAnalytics è utile:</span><span class="sxs-lookup"><span data-stu-id="23dc8-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="23dc8-111">**Creare un join con la telemetria dell'app.**</span><span class="sxs-lookup"><span data-stu-id="23dc8-111">**Join with app telemetry.**</span></span> <span data-ttu-id="23dc8-112">Ad esempio, è possibile importare una tabella che esegue il mapping degli URL tra i titoli di pagina leggibile toomore sito Web.</span><span class="sxs-lookup"><span data-stu-id="23dc8-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="23dc8-113">In Analitica, è possibile creare un report di grafico del dashboard che mostra le pagine di più diffusi dieci hello nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="23dc8-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="23dc8-114">Ora consente di visualizzare hello titoli delle pagine anziché hello URL.</span><span class="sxs-lookup"><span data-stu-id="23dc8-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="23dc8-115">**Correlare la telemetria dell'applicazione** con altre origini, ad esempio il traffico di rete, i dati del server o i file di log della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="23dc8-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="23dc8-116">**Applicare flusso dei dati distinto tooa Analitica.**</span><span class="sxs-lookup"><span data-stu-id="23dc8-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="23dc8-117">Application Insights Analytics è uno strumento potente, che funziona bene con flussi di timestamp frammentati, spesso in modo più efficace di SQL.</span><span class="sxs-lookup"><span data-stu-id="23dc8-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="23dc8-118">Se si dispone di tale flusso da un'altra origine, è possibile analizzarlo con Analytics.</span><span class="sxs-lookup"><span data-stu-id="23dc8-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="23dc8-119">L'invio di dati tooyour origine dati è semplice.</span><span class="sxs-lookup"><span data-stu-id="23dc8-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="23dc8-120">(Una volta) Definizione di schema hello dei dati in un'origine di dati' '.</span><span class="sxs-lookup"><span data-stu-id="23dc8-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="23dc8-121">(Periodicamente) Caricamento dell'archiviazione dei dati tooAzure e contattarci toonotify API REST hello in attesa per l'inserimento di nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="23dc8-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="23dc8-122">Entro pochi minuti, dati hello sono disponibili per query in Analitica.</span><span class="sxs-lookup"><span data-stu-id="23dc8-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="23dc8-123">Hello frequenza di caricamento hello è definita dall'utente e la velocità con cui si desidera toobe i dati disponibili per le query.</span><span class="sxs-lookup"><span data-stu-id="23dc8-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="23dc8-124">È più efficiente tooupload i dati in blocchi più grandi, ma non maggiore di 1GB.</span><span class="sxs-lookup"><span data-stu-id="23dc8-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="23dc8-125">*Hai un numero elevato di tooanalyze di origini dati?*</span><span class="sxs-lookup"><span data-stu-id="23dc8-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="23dc8-126">*È consigliabile utilizzare* logstash *tooship i dati in Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="23dc8-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="23dc8-127">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="23dc8-127">Before you start</span></span>

<span data-ttu-id="23dc8-128">Sono necessari:</span><span class="sxs-lookup"><span data-stu-id="23dc8-128">You need:</span></span>

1. <span data-ttu-id="23dc8-129">Una risorsa di Application Insights in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="23dc8-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="23dc8-130">Se si desidera tooanalyze dati separatamente da eventuali altri dati di telemetria [creare una nuova risorsa di Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="23dc8-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="23dc8-131">Se si è aggiunta o il confronto dei dati con dati di telemetria da un'app è già configurata con Application Insights, è possibile utilizzare risorse hello per l'app.</span><span class="sxs-lookup"><span data-stu-id="23dc8-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="23dc8-132">Risorsa toothat di accesso proprietario o collaboratore.</span><span class="sxs-lookup"><span data-stu-id="23dc8-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="23dc8-133">nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="23dc8-133">Azure storage.</span></span> <span data-ttu-id="23dc8-134">Caricare archiviazione tooAzure e Analitica Ottiene i dati da tale posizione.</span><span class="sxs-lookup"><span data-stu-id="23dc8-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="23dc8-135">È consigliabile creare un account di archiviazione dedicato per i BLOB.</span><span class="sxs-lookup"><span data-stu-id="23dc8-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="23dc8-136">Se i BLOB sono condivise con altri processi, richiede più tempo per i processi tooread i BLOB.</span><span class="sxs-lookup"><span data-stu-id="23dc8-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="23dc8-137">Definire lo schema</span><span class="sxs-lookup"><span data-stu-id="23dc8-137">Define your schema</span></span>

<span data-ttu-id="23dc8-138">È possibile importare dati, è necessario definire un *origine dati,* che consente di specificare schema hello dei dati.</span><span class="sxs-lookup"><span data-stu-id="23dc8-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="23dc8-139">È possibile avere fino a too50 origini di dati in una singola risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="23dc8-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="23dc8-140">Avviare Creazione guidata origine dati di hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-140">Start hello data source wizard.</span></span> <span data-ttu-id="23dc8-141">Usare il pulsante "Aggiungi nuova origine dati".</span><span class="sxs-lookup"><span data-stu-id="23dc8-141">Use "Add new data source" button.</span></span> <span data-ttu-id="23dc8-142">In alternativa, fare clic sul pulsante Impostazioni nell'angolo in alto a destra e scegliere "Origini dati" nel menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="23dc8-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Aggiungere la nuova origine dati](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="23dc8-144">Immettere un nome per la nuova origine dati.</span><span class="sxs-lookup"><span data-stu-id="23dc8-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="23dc8-145">Definire formato di file hello che verrà caricato.</span><span class="sxs-lookup"><span data-stu-id="23dc8-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="23dc8-146">È possibile definire il formato di hello manualmente o caricare un file di esempio.</span><span class="sxs-lookup"><span data-stu-id="23dc8-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="23dc8-147">Dati hello sono in formato CSV, hello prima riga dell'esempio hello possibile caso le intestazioni di colonna.</span><span class="sxs-lookup"><span data-stu-id="23dc8-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="23dc8-148">È possibile modificare i nomi dei campi hello nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="23dc8-149">esempio Hello deve includere almeno 10 righe o record di dati.</span><span class="sxs-lookup"><span data-stu-id="23dc8-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="23dc8-150">I nomi di colonna o di campo devono essere alfanumerici (senza spazi o punteggiatura).</span><span class="sxs-lookup"><span data-stu-id="23dc8-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Caricare un file di esempio](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="23dc8-152">Ha ottenuto schema hello revisione hello procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="23dc8-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="23dc8-153">Se dedotto tipi hello da un esempio, potrebbe essere tipi di hello dedotto tooadjust delle colonne di hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Schema inferito hello revisione](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="23dc8-155">Facoltativo. Caricare una definizione dello schema.</span><span class="sxs-lookup"><span data-stu-id="23dc8-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="23dc8-156">Vedere hello formato riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="23dc8-156">See hello format below.</span></span>

 * <span data-ttu-id="23dc8-157">Selezionare un timestamp.</span><span class="sxs-lookup"><span data-stu-id="23dc8-157">Select a Timestamp.</span></span> <span data-ttu-id="23dc8-158">Tutti i dati in Analytics devono avere un campo di timestamp.</span><span class="sxs-lookup"><span data-stu-id="23dc8-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="23dc8-159">Il tipo deve essere `datetime`, ma non è toobe denominato 'timestamp'.</span><span class="sxs-lookup"><span data-stu-id="23dc8-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="23dc8-160">Se i dati includono una colonna contenente una data e ora in formato ISO, scegliere questa opzione come colonna di tipo timestamp hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="23dc8-161">In caso contrario, scegliere "come dati ricevuti" e il processo di importazione hello viene aggiunto un campo di timestamp.</span><span class="sxs-lookup"><span data-stu-id="23dc8-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="23dc8-162">Creare l'origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="23dc8-163">Formato del file di definizione dello schema</span><span class="sxs-lookup"><span data-stu-id="23dc8-163">Schema definition file format</span></span>

<span data-ttu-id="23dc8-164">Anziché la modifica dello schema hello nell'interfaccia utente, è possibile caricare la definizione dello schema hello da un file.</span><span class="sxs-lookup"><span data-stu-id="23dc8-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="23dc8-165">formato di definizione dello schema Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="23dc8-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="23dc8-166">Formato delimitato</span><span class="sxs-lookup"><span data-stu-id="23dc8-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="23dc8-167">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="23dc8-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="23dc8-168">Ogni colonna viene identificato dal tipo, nome e percorso hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="23dc8-169">Ubicazione: per formattare file delimitato è posizione hello del valore di hello mappato.</span><span class="sxs-lookup"><span data-stu-id="23dc8-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="23dc8-170">Per il formato JSON, è jpath hello della chiave hello mappato.</span><span class="sxs-lookup"><span data-stu-id="23dc8-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="23dc8-171">Nome: hello visualizzati nome della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="23dc8-172">Tipo: tipo di dati hello di tale colonna.</span><span class="sxs-lookup"><span data-stu-id="23dc8-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="23dc8-173">Nel caso in cui è stata utilizzata una data di esempio e ha un formato di file delimitato, la definizione dello schema hello deve eseguire il mapping di tutte le colonne e aggiungere nuove colonne alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="23dc8-174">JSON consente il mapping parziale dei dati di hello, pertanto hello definizione dello schema di formato JSON non ha toomap ogni chiave è presente in dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="23dc8-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="23dc8-175">Anche possibile eseguire il mapping di colonne che non fanno parte di dati di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="23dc8-176">Importa dati</span><span class="sxs-lookup"><span data-stu-id="23dc8-176">Import data</span></span>

<span data-ttu-id="23dc8-177">dati tooimport, caricarlo tooAzure archiviazione, creare una chiave di accesso per tale e quindi effettuare una chiamata API REST.</span><span class="sxs-lookup"><span data-stu-id="23dc8-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Aggiungere la nuova origine dati](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="23dc8-179">È possibile eseguire hello seguente processo manualmente o configurare un toodo automatico di sistema, a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="23dc8-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="23dc8-180">È necessario toofollow questi passaggi per ogni blocco di dati si desidera tooimport.</span><span class="sxs-lookup"><span data-stu-id="23dc8-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="23dc8-181">Caricare dati hello troppo[archiviazione blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="23dc8-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="23dc8-182">BLOB possono essere di qualsiasi dimensione di too1GB non compressi.</span><span class="sxs-lookup"><span data-stu-id="23dc8-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="23dc8-183">I BLOB di centinaia di MB sono ideali dal punto di vista delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="23dc8-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="23dc8-184">È possibile comprimere, con tempo di caricamento tooimprove Gzip e la latenza di hello toobe di dati disponibili per le query.</span><span class="sxs-lookup"><span data-stu-id="23dc8-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="23dc8-185">Hello utilizzare `.gz` estensione del nome file.</span><span class="sxs-lookup"><span data-stu-id="23dc8-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="23dc8-186">A tale scopo, chiamate tooavoid dai vari servizi rallentare le prestazioni è migliore toouse un account di archiviazione separata.</span><span class="sxs-lookup"><span data-stu-id="23dc8-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="23dc8-187">Quando si inviano dati ad alta frequenza, ogni pochi secondi, è consigliabile toouse più di un account di archiviazione, per motivi di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="23dc8-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="23dc8-188">[Creare una chiave di firma di accesso condiviso per il blob hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="23dc8-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="23dc8-189">chiave di Hello deve avere un periodo di scadenza di un giorno e forniscono l'accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="23dc8-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="23dc8-190">Verificare un toonotify chiamata REST Application Insights in attesa di dati.</span><span class="sxs-lookup"><span data-stu-id="23dc8-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="23dc8-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="23dc8-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="23dc8-192">Metodo HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="23dc8-192">HTTP method: POST</span></span>
 * <span data-ttu-id="23dc8-193">Payload:</span><span class="sxs-lookup"><span data-stu-id="23dc8-193">Payload:</span></span>

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

<span data-ttu-id="23dc8-194">segnaposto Hello sono:</span><span class="sxs-lookup"><span data-stu-id="23dc8-194">hello placeholders are:</span></span>

* <span data-ttu-id="23dc8-195">`Blob URI with Shared Access Key`: Questa procedura hello per la creazione di una chiave.</span><span class="sxs-lookup"><span data-stu-id="23dc8-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="23dc8-196">È il blob toohello specifico.</span><span class="sxs-lookup"><span data-stu-id="23dc8-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="23dc8-197">`Schema ID`: hello ID dello schema generato per lo schema definito.</span><span class="sxs-lookup"><span data-stu-id="23dc8-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="23dc8-198">dati Hello in questo blob devono essere conformi toohello schema.</span><span class="sxs-lookup"><span data-stu-id="23dc8-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="23dc8-199">`DateTime`: ora hello in cui hello viene inoltrata una richiesta, UTC.</span><span class="sxs-lookup"><span data-stu-id="23dc8-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="23dc8-200">Vengono accettati i seguenti formati: ISO8601 (ad esempio "2016-01-01 13:45:01"); RFC822 ("mer, 14 dic 16 14:57:01 +0000"); RFC850 ("mercoledì, 14-dic-16 14:57:00 UTC"); RFC1123 ("mer, 14 dic 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="23dc8-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="23dc8-201">`Instrumentation key` della risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="23dc8-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="23dc8-202">dati Hello sono disponibili in Analitica dopo alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="23dc8-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="23dc8-203">Risposte agli errori</span><span class="sxs-lookup"><span data-stu-id="23dc8-203">Error responses</span></span>

* <span data-ttu-id="23dc8-204">**400 richiesta non valida**: indica che il payload della richiesta hello è valido.</span><span class="sxs-lookup"><span data-stu-id="23dc8-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="23dc8-205">Controllare:</span><span class="sxs-lookup"><span data-stu-id="23dc8-205">Check:</span></span>
 * <span data-ttu-id="23dc8-206">Chiave di strumentazione corretta.</span><span class="sxs-lookup"><span data-stu-id="23dc8-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="23dc8-207">Valore dell'ora valido.</span><span class="sxs-lookup"><span data-stu-id="23dc8-207">Valid time value.</span></span> <span data-ttu-id="23dc8-208">Dovrebbe essere ora hello ora UTC.</span><span class="sxs-lookup"><span data-stu-id="23dc8-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="23dc8-209">JSON dell'evento hello conforme toohello schema.</span><span class="sxs-lookup"><span data-stu-id="23dc8-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="23dc8-210">**403-accesso negato**: blob hello è stato inviato non è accessibile.</span><span class="sxs-lookup"><span data-stu-id="23dc8-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="23dc8-211">Verificare che tale chiave di accesso condiviso hello sia valido e non sia scaduto.</span><span class="sxs-lookup"><span data-stu-id="23dc8-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="23dc8-212">**404 - Pagina non trovata**:</span><span class="sxs-lookup"><span data-stu-id="23dc8-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="23dc8-213">blob Hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="23dc8-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="23dc8-214">sourceId Hello è errato.</span><span class="sxs-lookup"><span data-stu-id="23dc8-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="23dc8-215">Informazioni più dettagliate sono disponibili nel messaggio di errore di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="23dc8-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="23dc8-216">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="23dc8-216">Sample code</span></span>

<span data-ttu-id="23dc8-217">Questo codice Usa hello [newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="23dc8-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="23dc8-218">Classi</span><span class="sxs-lookup"><span data-stu-id="23dc8-218">Classes</span></span>

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

### <a name="ingest-data"></a><span data-ttu-id="23dc8-219">Inserire dati</span><span class="sxs-lookup"><span data-stu-id="23dc8-219">Ingest data</span></span>

<span data-ttu-id="23dc8-220">Usare questo codice per ogni BLOB.</span><span class="sxs-lookup"><span data-stu-id="23dc8-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="23dc8-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23dc8-221">Next steps</span></span>

* [<span data-ttu-id="23dc8-222">Panoramica del linguaggio di query Log Analitica hello</span><span class="sxs-lookup"><span data-stu-id="23dc8-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="23dc8-223">Utilizzare *Logstash* toosend dati tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="23dc8-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
