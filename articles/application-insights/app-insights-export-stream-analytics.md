---
title: aaaExport tramite flusso Analitica da Azure Application Insights | Documenti Microsoft
description: "Flusso Analitica è possibile trasformare in modo continuo, filtro e dati della route hello esportare da Application Insights."
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
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="86f0f-103">Utilizzare Analitica flusso tooprocess esportati dati da Application Insights</span><span class="sxs-lookup"><span data-stu-id="86f0f-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="86f0f-104">[Azure Analitica flusso](https://azure.microsoft.com/services/stream-analytics/) hello strumento ideale per l'elaborazione dati [esportato da Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="86f0f-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="86f0f-105">L'analisi di flusso può eseguire il pull di dati da un'ampia gamma di origini.</span><span class="sxs-lookup"><span data-stu-id="86f0f-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="86f0f-106">Può trasformare e filtrare i dati di hello e quindi distribuirla tooa svariati sink.</span><span class="sxs-lookup"><span data-stu-id="86f0f-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="86f0f-107">In questo esempio, si creerà un adattatore che accetta dati da Application Insights, ridenominazioni ed elabora alcuni campi, hello e invia tramite pipe a Power BI.</span><span class="sxs-lookup"><span data-stu-id="86f0f-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="86f0f-108">Esistono molto migliore e più facile [consigliati per i dati di Application Insights toodisplay in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="86f0f-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="86f0f-109">percorso illustrato di seguito Hello è semplicemente un tooillustrate esempio tooprocess come i dati esportati.</span><span class="sxs-lookup"><span data-stu-id="86f0f-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![Diagramma a blocchi per l'esportazione tramite tooPBI SA](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="86f0f-111">Creare l'archivio in Azure</span><span class="sxs-lookup"><span data-stu-id="86f0f-111">Create storage in Azure</span></span>
<span data-ttu-id="86f0f-112">L'esportazione continua restituisce sempre l'account di archiviazione Azure tooan di dati, pertanto è necessario innanzitutto archiviazione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="86f0f-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="86f0f-113">Creare un account di archiviazione "classiche" nella sottoscrizione in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86f0f-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![Nel portale di Azure scegliere Nuovo, Dati, Archiviazione](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="86f0f-115">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="86f0f-115">Create a container</span></span>
   
    ![In hello nuova risorsa di archiviazione, selezionare i contenitori, fare clic su riquadro contenitori hello, quindi su Aggiungi](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="86f0f-117">Chiave di accesso di archiviazione hello copia</span><span class="sxs-lookup"><span data-stu-id="86f0f-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="86f0f-118">È necessario prima tooset hello toohello input flusso analitica servizio.</span><span class="sxs-lookup"><span data-stu-id="86f0f-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Nel servizio di archiviazione hello, aprire le impostazioni, chiavi e richiedere una copia della chiave di accesso primaria hello](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="86f0f-120">Avviare l'esportazione continua tooAzure archiviazione</span><span class="sxs-lookup"><span data-stu-id="86f0f-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="86f0f-121">[Esportazione continua](app-insights-export-telemetry.md) sposta i dati da Application Insights nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="86f0f-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="86f0f-122">Nel portale di Azure hello, Sfoglia risorsa di Application Insights toohello creata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="86f0f-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Scegliere Sfoglia, Application Insights e quindi l'applicazione](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="86f0f-124">Creare un'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="86f0f-124">Create a continuous export.</span></span>
   
    ![Scegliere Impostazioni, Esportazione continua, Aggiungi](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="86f0f-126">Selezionare l'account di archiviazione hello creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="86f0f-126">Select hello storage account you created earlier:</span></span>

    ![Set di destinazione dell'esportazione hello](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="86f0f-128">Impostare i tipi di evento hello da toosee:</span><span class="sxs-lookup"><span data-stu-id="86f0f-128">Set hello event types you want toosee:</span></span>

    ![Scegliere i tipi di eventi](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="86f0f-130">Lasciare che alcuni dati si accumulino.</span><span class="sxs-lookup"><span data-stu-id="86f0f-130">Let some data accumulate.</span></span> <span data-ttu-id="86f0f-131">Attendere che gli utenti usino l'applicazione per qualche tempo.</span><span class="sxs-lookup"><span data-stu-id="86f0f-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="86f0f-132">Verranno restituiti i dati di telemetria e sarà possibile esaminare i grafici statistici in [Esplora metriche](app-insights-metrics-explorer.md) e i singoli eventi in [Ricerca diagnostica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="86f0f-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="86f0f-133">E inoltre dati hello esporterà tooyour archiviazione.</span><span class="sxs-lookup"><span data-stu-id="86f0f-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="86f0f-134">Esaminare i dati di hello esportata.</span><span class="sxs-lookup"><span data-stu-id="86f0f-134">Inspect hello exported data.</span></span> <span data-ttu-id="86f0f-135">In Visual Studio, scegliere **Visualizza/Cloud Explorer**e aprire Azure/Archiviazione.</span><span class="sxs-lookup"><span data-stu-id="86f0f-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="86f0f-136">(Se non si dispone di questa opzione, è necessario tooinstall hello Azure SDK: aprire finestra di dialogo Nuovo progetto hello e Visual c# / Cloud / ottenere Microsoft Azure SDK per .NET.)</span><span class="sxs-lookup"><span data-stu-id="86f0f-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="86f0f-137">Prendere nota di parte in comune hello del nome di percorso hello, che viene derivato dalla chiave di nome e la strumentazione dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="86f0f-138">gli eventi di Hello vengono scritti i file tooblob in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="86f0f-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="86f0f-139">Ogni file può contenere uno o più eventi.</span><span class="sxs-lookup"><span data-stu-id="86f0f-139">Each file may contain one or more events.</span></span> <span data-ttu-id="86f0f-140">In modo desideriamo tooread hello dati dell'evento e filtro campi hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="86f0f-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="86f0f-141">Sono disponibili tutti i tipi di operazioni che è possibile farlo con dati hello, ma il piano è oggi toouse flusso Analitica toopipe hello dati tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="86f0f-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="86f0f-142">Creare un'istanza di analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="86f0f-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="86f0f-143">Da hello [portale di Azure classico](https://manage.windowsazure.com/), selezionare il servizio di Azure flusso Analitica hello e creare un nuovo processo di flusso Analitica:</span><span class="sxs-lookup"><span data-stu-id="86f0f-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="86f0f-144">Quando viene creato il nuovo processo di hello, espandere i dettagli:</span><span class="sxs-lookup"><span data-stu-id="86f0f-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="86f0f-145">Impostare il percorso BLOB</span><span class="sxs-lookup"><span data-stu-id="86f0f-145">Set blob location</span></span>
<span data-ttu-id="86f0f-146">Impostarlo input tootake dal blob di esportazione continua:</span><span class="sxs-lookup"><span data-stu-id="86f0f-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="86f0f-147">A questo punto è necessario hello chiave di accesso primaria dall'Account di archiviazione, annotati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="86f0f-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="86f0f-148">Impostare come hello chiave Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="86f0f-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="86f0f-149">Impostare lo schema prefisso percorso</span><span class="sxs-lookup"><span data-stu-id="86f0f-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="86f0f-150">**Impossibile verificare tooset hello formato data tooYYYY-MM-GG (con i trattini).**</span><span class="sxs-lookup"><span data-stu-id="86f0f-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="86f0f-151">Hello modello prefisso del percorso specifica in cui flusso Analitica Individua file di input hello nel servizio di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="86f0f-152">È necessario tooset è toohow toocorrespond esportazione continua archivia dati hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="86f0f-153">Impostarlo come segue:</span><span class="sxs-lookup"><span data-stu-id="86f0f-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="86f0f-154">Esempio:</span><span class="sxs-lookup"><span data-stu-id="86f0f-154">In this example:</span></span>

* <span data-ttu-id="86f0f-155">`webapplication27`è il nome di hello della risorsa di Application Insights hello **lettere minuscole**.</span><span class="sxs-lookup"><span data-stu-id="86f0f-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="86f0f-156">`1234...`è la chiave di strumentazione hello della risorsa di Application Insights, hello **l'omissione di trattini**.</span><span class="sxs-lookup"><span data-stu-id="86f0f-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="86f0f-157">`PageViews`hello tipo di dati si desidera tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="86f0f-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="86f0f-158">tipi di Hello disponibili dipendono dal filtro hello impostato nell'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="86f0f-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="86f0f-159">Esaminare altri tipi disponibili di hello toosee di dati esportati hello e vedere hello [Esporta modello di dati](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="86f0f-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="86f0f-160">`/{date}/{time}` è uno schema scritto letteralmente.</span><span class="sxs-lookup"><span data-stu-id="86f0f-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="86f0f-161">Controllare toomake archiviazione hello si ottiene il percorso di hello destra.</span><span class="sxs-lookup"><span data-stu-id="86f0f-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="86f0f-162">Completare l'installazione iniziale</span><span class="sxs-lookup"><span data-stu-id="86f0f-162">Finish initial setup</span></span>
<span data-ttu-id="86f0f-163">Verificare il formato di serializzazione hello:</span><span class="sxs-lookup"><span data-stu-id="86f0f-163">Confirm hello serialization format:</span></span>

![Confermare e chiudere la procedura guidata](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="86f0f-165">Chiudere la procedura guidata hello e attendere hello toocomplete di programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="86f0f-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="86f0f-166">Utilizzare toodownload comando di esempio hello alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="86f0f-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="86f0f-167">Mantenerlo come un toodebug di esempio di test della query.</span><span class="sxs-lookup"><span data-stu-id="86f0f-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="86f0f-168">Output di hello set</span><span class="sxs-lookup"><span data-stu-id="86f0f-168">Set hello output</span></span>
<span data-ttu-id="86f0f-169">Selezionare il processo e impostare l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-169">Now select your job and set hello output.</span></span>

![Selezionare il nuovo canale di hello, fare clic su output, Add, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="86f0f-171">Fornire il **di lavoro o scuola account** tooauthorize tooaccess Analitica di flusso della risorsa di Power BI.</span><span class="sxs-lookup"><span data-stu-id="86f0f-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="86f0f-172">Creare quindi un nome per l'output di hello e per la tabella e il set di dati di hello destinazione Power BI.</span><span class="sxs-lookup"><span data-stu-id="86f0f-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![Inventare tre nomi](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="86f0f-174">Set hello query</span><span class="sxs-lookup"><span data-stu-id="86f0f-174">Set hello query</span></span>
<span data-ttu-id="86f0f-175">query Hello regola traduzione hello da toooutput input.</span><span class="sxs-lookup"><span data-stu-id="86f0f-175">hello query governs hello translation from input toooutput.</span></span>

![Selezionare il processo di hello e fare clic su Query.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="86f0f-178">Utilizzare hello toocheck di funzione di Test che si otterrà un output di destra hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="86f0f-179">Assegnare i dati di esempio hello impiegato dalla pagina input hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="86f0f-180">Query toodisplay conteggi di eventi</span><span class="sxs-lookup"><span data-stu-id="86f0f-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="86f0f-181">Incollare questa query:</span><span class="sxs-lookup"><span data-stu-id="86f0f-181">Paste this query:</span></span>

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

* <span data-ttu-id="86f0f-182">input di esportazione è alias hello è stato assegnato l'input del flusso toohello</span><span class="sxs-lookup"><span data-stu-id="86f0f-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="86f0f-183">output di PBI è l'alias di output di hello è definiti</span><span class="sxs-lookup"><span data-stu-id="86f0f-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="86f0f-184">Utilizziamo [OUTER GetElements applicare](https://msdn.microsoft.com/library/azure/dn706229.aspx) nome di evento hello è in un arrray JSON annidati.</span><span class="sxs-lookup"><span data-stu-id="86f0f-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="86f0f-185">Quindi seleziona selezionare hello hello nome dell'evento, con un conteggio del numero di hello di istanze con lo stesso nome in hello periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="86f0f-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="86f0f-186">Hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clausola Raggruppa elementi hello in periodi di tempo di 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="86f0f-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="86f0f-187">Valori della metrica toodisplay query</span><span class="sxs-lookup"><span data-stu-id="86f0f-187">Query toodisplay metric values</span></span>
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

* <span data-ttu-id="86f0f-188">Questa query drill-ora dell'evento hello tooget telemetria metriche hello e valore della metrica hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="86f0f-189">valori della metrica Hello sono all'interno di una matrice, righe di hello OUTER GetElements Applica modello tooextract hello permette di usare.</span><span class="sxs-lookup"><span data-stu-id="86f0f-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="86f0f-190">in questo caso, "myMetric" è il nome di hello della metrica di hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="86f0f-191">Valori delle proprietà di dimensione tooinclude di query</span><span class="sxs-lookup"><span data-stu-id="86f0f-191">Query tooinclude values of dimension properties</span></span>
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

* <span data-ttu-id="86f0f-192">La query include i valori delle proprietà di dimensione hello senza in base a una dimensione specifica in un indice nella matrice di dimensione hello fisso.</span><span class="sxs-lookup"><span data-stu-id="86f0f-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="86f0f-193">Eseguire il processo di hello</span><span class="sxs-lookup"><span data-stu-id="86f0f-193">Run hello job</span></span>
<span data-ttu-id="86f0f-194">È possibile selezionare una data in hello oltre toostart hello processo da.</span><span class="sxs-lookup"><span data-stu-id="86f0f-194">You can select a date in hello past toostart hello job from.</span></span> 

![Selezionare il processo di hello e fare clic su Query.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="86f0f-197">Attendere fino a quando non è in esecuzione il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="86f0f-198">Visualizzare i risultati in Power BI</span><span class="sxs-lookup"><span data-stu-id="86f0f-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="86f0f-199">Esistono molto migliore e più facile [consigliati per i dati di Application Insights toodisplay in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="86f0f-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="86f0f-200">percorso illustrato di seguito Hello è semplicemente un tooillustrate esempio tooprocess come i dati esportati.</span><span class="sxs-lookup"><span data-stu-id="86f0f-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="86f0f-201">Aprire Power BI con l'account dell'istituto di istruzione e set di dati selezionare hello e o tabella in cui è definito come output di hello del processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="86f0f-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![In Power BI selezionare il set di dati e i campi.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="86f0f-203">È ora possibile usare questo set di dati nei report e nei dashboard in [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="86f0f-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![In Power BI selezionare il set di dati e i campi.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="86f0f-205">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="86f0f-205">No data?</span></span>
* <span data-ttu-id="86f0f-206">Verificare che si [formato di data set hello](#set-path-prefix-pattern) correttamente tooYYYY-MM-GG (con i trattini).</span><span class="sxs-lookup"><span data-stu-id="86f0f-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="86f0f-207">Video</span><span class="sxs-lookup"><span data-stu-id="86f0f-207">Video</span></span>
<span data-ttu-id="86f0f-208">Noam Ben Zeev viene illustrata la modalità di esportazione di dati tramite flusso Analitica tooprocess.</span><span class="sxs-lookup"><span data-stu-id="86f0f-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="86f0f-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86f0f-209">Next steps</span></span>
* [<span data-ttu-id="86f0f-210">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="86f0f-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="86f0f-211">Riferimento per i tipi di proprietà hello e i valori del modello di dati dettagliati.</span><span class="sxs-lookup"><span data-stu-id="86f0f-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="86f0f-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="86f0f-212">Application Insights</span></span>](app-insights-overview.md)

