---
title: Esportare da Azure Application Insights usando l'analisi di flusso | Documentazione Microsoft
description: "L'analisi di flusso può trasformare, filtrare e instradare continuativamente i dati esportati da Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6a84d8ff67c420ce712de905ab1172632502a863
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="165b6-103">Usare l'analisi di flusso per elaborare dati esportati da Application Insights</span><span class="sxs-lookup"><span data-stu-id="165b6-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="165b6-104">L'[analisi di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/) è lo strumento ideale per elaborare dati [esportati da Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="165b6-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="165b6-105">L'analisi di flusso può eseguire il pull di dati da un'ampia gamma di origini.</span><span class="sxs-lookup"><span data-stu-id="165b6-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="165b6-106">Può trasformare e filtrare i dati e quindi instradarli a molti sink diversi.</span><span class="sxs-lookup"><span data-stu-id="165b6-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="165b6-107">In questo esempio verrà creato un adattatore che recupera dati da Application Insights, rinomina ed elabora alcuni dei campi e invia tramite pipe i dati in Power BI.</span><span class="sxs-lookup"><span data-stu-id="165b6-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="165b6-108">Esistono [modi consigliati migliori e più semplici per visualizzare dati di Application Insights in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="165b6-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="165b6-109">Il percorso descritto qui è solo un esempio per mostrare come elaborare dati esportati.</span><span class="sxs-lookup"><span data-stu-id="165b6-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![Diagramma a blocchi per l'esportazione tramite SA in PBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="165b6-111">Creare l'archivio in Azure</span><span class="sxs-lookup"><span data-stu-id="165b6-111">Create storage in Azure</span></span>
<span data-ttu-id="165b6-112">L'esportazione continua invia sempre i dati a un account di Archiviazione di Azure, pertanto è prima necessario creare l'archivio.</span><span class="sxs-lookup"><span data-stu-id="165b6-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="165b6-113">Creare un account di archiviazione "classico" per la sottoscrizione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="165b6-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![Nel portale di Azure scegliere Nuovo, Dati, Archiviazione](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="165b6-115">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="165b6-115">Create a container</span></span>
   
    ![Nel nuovo archivio selezionare Contenitori, fare clic sul riquadro Contenitori e quindi su Aggiungi](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="165b6-117">Copiare la chiave di accesso alle risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="165b6-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="165b6-118">Sarà presto necessaria per configurare l'input per il servizio di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="165b6-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![Nella risorsa di archiviazione aprire Impostazioni, Chiavi ed eseguire una copia della chiave di accesso primaria](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="165b6-120">Avviare l'esportazione continua nell'archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="165b6-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="165b6-121">[Esportazione continua](app-insights-export-telemetry.md) sposta i dati da Application Insights nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="165b6-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="165b6-122">Nel portale di Azure passare alla risorsa di Application Insights creata per la propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="165b6-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Scegliere Sfoglia, Application Insights e quindi l'applicazione](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="165b6-124">Creare un'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="165b6-124">Create a continuous export.</span></span>
   
    ![Scegliere Impostazioni, Esportazione continua, Aggiungi](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="165b6-126">Selezionare l'account di archiviazione creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="165b6-126">Select the storage account you created earlier:</span></span>

    ![Impostare la destinazione di esportazione](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="165b6-128">Impostare i tipi di eventi da visualizzare:</span><span class="sxs-lookup"><span data-stu-id="165b6-128">Set the event types you want to see:</span></span>

    ![Scegliere i tipi di eventi](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="165b6-130">Lasciare che alcuni dati si accumulino.</span><span class="sxs-lookup"><span data-stu-id="165b6-130">Let some data accumulate.</span></span> <span data-ttu-id="165b6-131">Attendere che gli utenti usino l'applicazione per qualche tempo.</span><span class="sxs-lookup"><span data-stu-id="165b6-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="165b6-132">Verranno restituiti i dati di telemetria e sarà possibile esaminare i grafici statistici in [Esplora metriche](app-insights-metrics-explorer.md) e i singoli eventi in [Ricerca diagnostica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="165b6-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="165b6-133">I dati verranno inoltre esportati nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="165b6-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="165b6-134">Esaminare i dati esportati.</span><span class="sxs-lookup"><span data-stu-id="165b6-134">Inspect the exported data.</span></span> <span data-ttu-id="165b6-135">In Visual Studio, scegliere **Visualizza/Cloud Explorer**e aprire Azure/Archiviazione.</span><span class="sxs-lookup"><span data-stu-id="165b6-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="165b6-136">(Se non si dispone di tale opzione del menu, è necessario installare l’SDK di Azure: aprire la finestra di dialogo Nuovo progetto, aprire Visual C#/Cloud/Ottieni Microsoft Azure SDK per .NET).</span><span class="sxs-lookup"><span data-stu-id="165b6-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="165b6-137">Prendere nota della parte comune del nome del percorso, derivata dal nome dell’applicazione e dalla chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="165b6-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="165b6-138">Gli eventi vengono scritti nei file BLOB in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="165b6-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="165b6-139">Ogni file può contenere uno o più eventi.</span><span class="sxs-lookup"><span data-stu-id="165b6-139">Each file may contain one or more events.</span></span> <span data-ttu-id="165b6-140">A questo punto sarà possibile leggere i dati degli eventi e filtrare i campi preferiti.</span><span class="sxs-lookup"><span data-stu-id="165b6-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="165b6-141">È possibile eseguire una serie di operazioni sui dati, ma lo scopo di questo articolo è usare l'analisi di flusso per spostare i dati in un Power BI.</span><span class="sxs-lookup"><span data-stu-id="165b6-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="165b6-142">Creare un'istanza di analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="165b6-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="165b6-143">Nel [portale di Azure classico](https://manage.windowsazure.com/)selezionare il servizio di analisi di flusso di Azure e creare un nuovo processo di analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="165b6-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="165b6-144">Quando viene creato il nuovo processo, espanderne i dettagli:</span><span class="sxs-lookup"><span data-stu-id="165b6-144">When the new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="165b6-145">Impostare il percorso BLOB</span><span class="sxs-lookup"><span data-stu-id="165b6-145">Set blob location</span></span>
<span data-ttu-id="165b6-146">Impostarlo in modo da accettare l'input dal BLOB di esportazione continua:</span><span class="sxs-lookup"><span data-stu-id="165b6-146">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="165b6-147">A questo punto è necessaria la chiave di accesso primaria dell'account di archiviazione, di cui si è preso nota in precedenza.</span><span class="sxs-lookup"><span data-stu-id="165b6-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="165b6-148">Impostarla come chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="165b6-148">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="165b6-149">Impostare lo schema prefisso percorso</span><span class="sxs-lookup"><span data-stu-id="165b6-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="165b6-150">**Assicurarsi di impostare il formato della data su AAAA-MM-GG (con i trattini).**</span><span class="sxs-lookup"><span data-stu-id="165b6-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="165b6-151">Lo schema prefisso percorso specifica dove l'analisi di flusso trova i file di input nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="165b6-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="165b6-152">È necessario configurarlo in modo che corrisponda alla modalità di archiviazione dei dati dell'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="165b6-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="165b6-153">Impostarlo come segue:</span><span class="sxs-lookup"><span data-stu-id="165b6-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="165b6-154">Esempio:</span><span class="sxs-lookup"><span data-stu-id="165b6-154">In this example:</span></span>

* <span data-ttu-id="165b6-155">`webapplication27` è il nome della risorsa di Application Insights, **tutto minuscolo**.</span><span class="sxs-lookup"><span data-stu-id="165b6-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="165b6-156">`1234...` è la chiave di strumentazione della risorsa di Application Insights, **senza trattini**.</span><span class="sxs-lookup"><span data-stu-id="165b6-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="165b6-157">`PageViews` è il tipo di dati da analizzare.</span><span class="sxs-lookup"><span data-stu-id="165b6-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="165b6-158">I tipi disponibili dipendono dal filtro impostato nell'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="165b6-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="165b6-159">Esaminare i dati esportati per vedere gli altri tipi disponibili e vedere il [modello di dati di esportazione](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="165b6-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="165b6-160">`/{date}/{time}` è uno schema scritto letteralmente.</span><span class="sxs-lookup"><span data-stu-id="165b6-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="165b6-161">Controllare lo spazio di archiviazione per assicurarsi di ottenere il percorso corretto.</span><span class="sxs-lookup"><span data-stu-id="165b6-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="165b6-162">Completare l'installazione iniziale</span><span class="sxs-lookup"><span data-stu-id="165b6-162">Finish initial setup</span></span>
<span data-ttu-id="165b6-163">Verificare il formato di serializzazione:</span><span class="sxs-lookup"><span data-stu-id="165b6-163">Confirm the serialization format:</span></span>

![Confermare e chiudere la procedura guidata](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="165b6-165">Chiudere la procedura guidata e attendere il completamento dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="165b6-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="165b6-166">Utilizzare il comando di esempio per scaricare alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="165b6-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="165b6-167">Utilizzare come esempio di test per eseguire il debug della query.</span><span class="sxs-lookup"><span data-stu-id="165b6-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="165b6-168">Visualizzare l'output</span><span class="sxs-lookup"><span data-stu-id="165b6-168">Set the output</span></span>
<span data-ttu-id="165b6-169">Selezionare il processo e impostare l'output.</span><span class="sxs-lookup"><span data-stu-id="165b6-169">Now select your job and set the output.</span></span>

![Selezionare il nuovo canale, fare clic su Output, su Aggiungi e quindi su Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="165b6-171">Fornire l’ **account aziendale o dell’istituto di istruzione** per autorizzare l'analisi di flusso per l’accesso alla risorsa di Power BI.</span><span class="sxs-lookup"><span data-stu-id="165b6-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="165b6-172">Creare quindi un nome per l'output e per il set di dati Power BI e la tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="165b6-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![Inventare tre nomi](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="165b6-174">Impostare la query</span><span class="sxs-lookup"><span data-stu-id="165b6-174">Set the query</span></span>
<span data-ttu-id="165b6-175">La query gestisce la conversione dall'input all'output.</span><span class="sxs-lookup"><span data-stu-id="165b6-175">The query governs the translation from input to output.</span></span>

![Selezionare il processo e fare clic su Query.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="165b6-178">Utilizzare la funzione Test per verificare di ottenere l'output corretto.</span><span class="sxs-lookup"><span data-stu-id="165b6-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="165b6-179">Assegnare i dati di esempio presenti nella pagina di input.</span><span class="sxs-lookup"><span data-stu-id="165b6-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="165b6-180">Query per visualizzare i conteggi degli eventi</span><span class="sxs-lookup"><span data-stu-id="165b6-180">Query to display counts of events</span></span>
<span data-ttu-id="165b6-181">Incollare questa query:</span><span class="sxs-lookup"><span data-stu-id="165b6-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="165b6-182">export-input è l'alias assegnato all'input del flusso</span><span class="sxs-lookup"><span data-stu-id="165b6-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="165b6-183">pbi-output è l'alias dell'output definito</span><span class="sxs-lookup"><span data-stu-id="165b6-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="165b6-184">Utilizziamo [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) perché il nome dell'evento si trova in una matrice JSON annidata.</span><span class="sxs-lookup"><span data-stu-id="165b6-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="165b6-185">L'istruzione SELECT seleziona quindi il nome dell'evento insieme al conteggio del numero di istanze che presentano tale nome nel periodo di tempo indicato.</span><span class="sxs-lookup"><span data-stu-id="165b6-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="165b6-186">La clausola [GROUP BY](https://msdn.microsoft.com/library/azure/dn835023.aspx) raggruppa gli elementi in periodi di tempo di 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="165b6-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="165b6-187">Query per visualizzare i valori delle metriche</span><span class="sxs-lookup"><span data-stu-id="165b6-187">Query to display metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="165b6-188">Questa query entra nella telemetria delle metriche per ottenere l'ora dell'evento e il valore della metrica.</span><span class="sxs-lookup"><span data-stu-id="165b6-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="165b6-189">I valori delle metriche sono all'interno di una matrice, pertanto si utilizza il modello OUTER APPLY GetElements per estrarre le righe.</span><span class="sxs-lookup"><span data-stu-id="165b6-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="165b6-190">"myMetric" è il nome della metrica in questo caso.</span><span class="sxs-lookup"><span data-stu-id="165b6-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="165b6-191">Query per includere i valori delle proprietà delle dimensioni</span><span class="sxs-lookup"><span data-stu-id="165b6-191">Query to include values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="165b6-192">Questa query include i valori delle proprietà delle dimensioni senza dipendere da una dimensione specifica in un indice fissato nella matrice di dimensioni.</span><span class="sxs-lookup"><span data-stu-id="165b6-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="165b6-193">Eseguire il processo</span><span class="sxs-lookup"><span data-stu-id="165b6-193">Run the job</span></span>
<span data-ttu-id="165b6-194">Per la data di inizio del processo, è possibile selezionare una data nel passato.</span><span class="sxs-lookup"><span data-stu-id="165b6-194">You can select a date in the past to start the job from.</span></span> 

![Selezionare il processo e fare clic su Query.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="165b6-197">Attendere fino al termine dell'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="165b6-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="165b6-198">Visualizzare i risultati in Power BI</span><span class="sxs-lookup"><span data-stu-id="165b6-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="165b6-199">Esistono [modi consigliati migliori e più semplici per visualizzare dati di Application Insights in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="165b6-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="165b6-200">Il percorso descritto qui è solo un esempio per mostrare come elaborare dati esportati.</span><span class="sxs-lookup"><span data-stu-id="165b6-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="165b6-201">Aprire Power BI con l’account aziendale o dell’istituto di istruzione e selezionare il set di dati e la tabella definiti come output del processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="165b6-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![In Power BI selezionare il set di dati e i campi.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="165b6-203">È ora possibile usare questo set di dati nei report e nei dashboard in [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="165b6-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![In Power BI selezionare il set di dati e i campi.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="165b6-205">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="165b6-205">No data?</span></span>
* <span data-ttu-id="165b6-206">Verificare di aver [impostato il formato di data](#set-path-prefix-pattern) correttamente su AAAA-MM-GG (con i trattini).</span><span class="sxs-lookup"><span data-stu-id="165b6-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="165b6-207">Video</span><span class="sxs-lookup"><span data-stu-id="165b6-207">Video</span></span>
<span data-ttu-id="165b6-208">Noam Ben Zeev mostra come elaborare dati esportati usando l'analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="165b6-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="165b6-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="165b6-209">Next steps</span></span>
* [<span data-ttu-id="165b6-210">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="165b6-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="165b6-211">Riferimento dettagliato al modello di dati per i valori e i tipi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="165b6-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="165b6-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="165b6-212">Application Insights</span></span>](app-insights-overview.md)

