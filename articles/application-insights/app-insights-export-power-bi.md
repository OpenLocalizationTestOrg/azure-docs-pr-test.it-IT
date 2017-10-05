---
title: Esportare in Power BI da Application Insights | Documentazione Microsoft
description: Le query di Analisi possono essere visualizzate in Power BI.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 350a65b1c6432baf258e014c9e63133d2b29e34f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="e2905-103">Feed di Power BI da Application Insights</span><span class="sxs-lookup"><span data-stu-id="e2905-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="e2905-104">[Power BI](http://www.powerbi.com/) è una suite di strumenti di analisi business che consente di analizzare i dati e condividere informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e2905-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="e2905-105">Dashboard completi sono disponibili in tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="e2905-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="e2905-106">È possibile combinare dati provenienti da diverse origini, incluse le query di Analytics di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2905-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="e2905-107">Esistono tre metodi consigliati per esportare i dati di Application Insights in Power BI.</span><span class="sxs-lookup"><span data-stu-id="e2905-107">There are three recommended methods of exporting Application Insights data to Power BI.</span></span> <span data-ttu-id="e2905-108">Possono essere usati insieme o separatamente.</span><span class="sxs-lookup"><span data-stu-id="e2905-108">You can use them separately or together.</span></span>

* <span data-ttu-id="e2905-109">[**Adattatore Power BI**](#power-pi-adapter): consente di impostare un dashboard di dati di telemetria completo dall'app.</span><span class="sxs-lookup"><span data-stu-id="e2905-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="e2905-110">Il set di tabelle è predefinito, ma è possibile aggiungere query da qualsiasi altra origine.</span><span class="sxs-lookup"><span data-stu-id="e2905-110">The set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="e2905-111">[**Esportazione di query di Analisi**](#export-analytics-queries): consiste di scrivere qualsiasi query con Analisi e poi di esportarla in Power BI.</span><span class="sxs-lookup"><span data-stu-id="e2905-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it to Power BI.</span></span> <span data-ttu-id="e2905-112">È possibile inserire questa query in un dashboard insieme a tutti gli altri dati.</span><span class="sxs-lookup"><span data-stu-id="e2905-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="e2905-113">[**Esportazione continua e analisi di flusso**](app-insights-export-stream-analytics.md): l'impostazione è più impegnativa.</span><span class="sxs-lookup"><span data-stu-id="e2905-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work to set up.</span></span> <span data-ttu-id="e2905-114">È utile se si desidera conservare i dati per lunghi periodi.</span><span class="sxs-lookup"><span data-stu-id="e2905-114">It is useful if you want to keep your data for long periods.</span></span> <span data-ttu-id="e2905-115">Altrimenti, si consiglia di usare gli altri metodi.</span><span class="sxs-lookup"><span data-stu-id="e2905-115">Otherwise, the other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="e2905-116">Adattatore Power BI</span><span class="sxs-lookup"><span data-stu-id="e2905-116">Power BI adapter</span></span>
<span data-ttu-id="e2905-117">Con questo metodo si crea un dashboard di dati di telemetria completo per l'utente.</span><span class="sxs-lookup"><span data-stu-id="e2905-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="e2905-118">Il set di dati iniziale è predefinito, ma è possibile aggiungere altri dati.</span><span class="sxs-lookup"><span data-stu-id="e2905-118">The initial data set is predefined, but you can add more data to it.</span></span>

### <a name="get-the-adapter"></a><span data-ttu-id="e2905-119">Scaricare l'adattatore</span><span class="sxs-lookup"><span data-stu-id="e2905-119">Get the adapter</span></span>
1. <span data-ttu-id="e2905-120">Accedere a [Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="e2905-120">Sign in to [Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="e2905-121">Aprire **Get Data** (Ottieni dati), **Servizi**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="e2905-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Scaricare da un'origine dati di Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="e2905-123">Specificare i dettagli della risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e2905-123">Provide the details of your Application Insights resource.</span></span>
   
    ![Scaricare da un'origine dati di Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="e2905-125">Attendere uno o due minuti per il completamento dell'importazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="e2905-125">Wait a minute or two for the data to be imported.</span></span>
   
    ![Adattatore Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="e2905-127">È possibile modificare il dashboard unendo i grafici di Application Insights con i grafici di altre origini e con le query di Analisi.</span><span class="sxs-lookup"><span data-stu-id="e2905-127">You can edit the dashboard, combining the Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="e2905-128">È disponibile una raccolta di visualizzazioni nella quale è possibile ottenere più grafici e ogni grafico include parametri che possono essere impostati.</span><span class="sxs-lookup"><span data-stu-id="e2905-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="e2905-129">Dopo l'importazione iniziale, il dashboard e i report continuano a essere aggiornati ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="e2905-129">After the initial import, the dashboard and the reports continue to update daily.</span></span> <span data-ttu-id="e2905-130">È possibile controllare la pianificazione dell'aggiornamento nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="e2905-130">You can control the refresh schedule on the dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="e2905-131">Esportare query di Analisi</span><span class="sxs-lookup"><span data-stu-id="e2905-131">Export Analytics queries</span></span>
<span data-ttu-id="e2905-132">Questo percorso consente di scrivere tutte le query di Analisi desiderate e di esportarle in un dashboard di Power BI.</span><span class="sxs-lookup"><span data-stu-id="e2905-132">This route allows you to write any Analytics query you like, and then export that to a Power BI dashboard.</span></span> <span data-ttu-id="e2905-133">È possibile aggiungerle al dashboard creato dall'adattatore.</span><span class="sxs-lookup"><span data-stu-id="e2905-133">(You can add to the dashboard created by the adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="e2905-134">Operazione da eseguire una sola volta: installazione di Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="e2905-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="e2905-135">Per importare la query di Application Insights, usare la versione desktop di Power BI.</span><span class="sxs-lookup"><span data-stu-id="e2905-135">To import your Application Insights query, you use the desktop version of Power BI.</span></span> <span data-ttu-id="e2905-136">Tuttavia, successivamente è possibile pubblicarla sul Web o nell'area di lavoro cloud di Power BI.</span><span class="sxs-lookup"><span data-stu-id="e2905-136">But then you can publish it to the web or to your Power BI cloud workspace.</span></span> 

<span data-ttu-id="e2905-137">Installare [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="e2905-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="e2905-138">Esportare una query di Analisi</span><span class="sxs-lookup"><span data-stu-id="e2905-138">Export an Analytics query</span></span>
1. <span data-ttu-id="e2905-139">[Aprire Analisi e scrivere la query](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="e2905-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="e2905-140">Testare e affinare la query fino a quando non si è soddisfatti dei risultati.</span><span class="sxs-lookup"><span data-stu-id="e2905-140">Test and refine the query until you're happy with the results.</span></span>

   <span data-ttu-id="e2905-141">**Verificare che la query venga eseguita correttamente in Analytics prima di esportarla.**</span><span class="sxs-lookup"><span data-stu-id="e2905-141">**Make sure that the query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="e2905-142">Nel menu **Esporta** scegliere **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="e2905-142">On the **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="e2905-143">Salvare il file di testo.</span><span class="sxs-lookup"><span data-stu-id="e2905-143">Save the text file.</span></span>
   
    ![Esportare la query di Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="e2905-145">In Power BI Desktop selezionare **Get Data (Ottieni dati), Query vuota** e quindi nell'editor di query andare su **Visualizza** e selezionare **Editor query avanzata**.</span><span class="sxs-lookup"><span data-stu-id="e2905-145">In Power BI Desktop select **Get Data, Blank Query** and then in the query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="e2905-146">Incollare lo script del linguaggio M esportato nell'Editor query avanzata.</span><span class="sxs-lookup"><span data-stu-id="e2905-146">Paste the exported M Language script into the Advanced Query Editor.</span></span>

    ![Editor query avanzata](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="e2905-148">Potrebbe essere necessario fornire le credenziali per consentire a Power BI di accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="e2905-148">You might have to provide credentials to allow Power BI to access Azure.</span></span> <span data-ttu-id="e2905-149">Andare su Account aziendale per accedere con l'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e2905-149">Use 'organizational account' to sign in with your Microsoft account.</span></span>
   
    ![Specificare le credenziali di Azure per consentire a Power BI di eseguire la query di Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="e2905-151">Se è necessario verificare le credenziali, usare il comando di menu Impostazioni origine dati nell'editor di query.</span><span class="sxs-lookup"><span data-stu-id="e2905-151">(If you need to verify the credentials, use the Data Source Settings menu command in the Query Editor.</span></span> <span data-ttu-id="e2905-152">Assicurarsi di specificare le credenziali usate per Azure, che potrebbero essere diverse da quelle di Power BI.</span><span class="sxs-lookup"><span data-stu-id="e2905-152">Take care to specify the credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="e2905-153">Scegliere una visualizzazione per la query e selezionare i campi per l'asse x, l'asse y e le dimensioni di segmentazione.</span><span class="sxs-lookup"><span data-stu-id="e2905-153">Choose a visualization for your query and select the fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Selezionare la visualizzazione](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="e2905-155">Pubblicare il report nell'area di lavoro cloud di Power BI.</span><span class="sxs-lookup"><span data-stu-id="e2905-155">Publish your report to your Power BI cloud workspace.</span></span> <span data-ttu-id="e2905-156">Da qui è possibile incorporare una versione sincronizzata in altre pagine Web.</span><span class="sxs-lookup"><span data-stu-id="e2905-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Selezionare la visualizzazione](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="e2905-158">Aggiornare manualmente il report a intervalli oppure impostare un aggiornamento pianificato nella pagina Opzioni.</span><span class="sxs-lookup"><span data-stu-id="e2905-158">Refresh the report manually at intervals, or set up a scheduled refresh on the options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e2905-159">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e2905-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="e2905-160">401 o 403 - Non autorizzato</span><span class="sxs-lookup"><span data-stu-id="e2905-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="e2905-161">Questo errore può verificarsi se il token di aggiornamento non è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="e2905-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="e2905-162">Provare a eseguire la procedura seguente per verificare di avere ancora accesso.</span><span class="sxs-lookup"><span data-stu-id="e2905-162">Try these steps to ensure you still have access.</span></span> <span data-ttu-id="e2905-163">Se si ha accesso e non è possibile aggiornare le credenziali, aprire un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="e2905-163">If you do have access and refershing the credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="e2905-164">Accedere al portale di Azure e verificare di poter accedere alla risorsa</span><span class="sxs-lookup"><span data-stu-id="e2905-164">Log into the Azure Portal and make sure you can access the resource</span></span>
2. <span data-ttu-id="e2905-165">Provare ad aggiornare le credenziali per il dashboard</span><span class="sxs-lookup"><span data-stu-id="e2905-165">Try to refresh the credentials for the Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="e2905-166">502 - Gateway non valido</span><span class="sxs-lookup"><span data-stu-id="e2905-166">502 Bad Gateway</span></span>
<span data-ttu-id="e2905-167">Questo errore è in genere causato da una query di Analisi che restituisce troppi dati.</span><span class="sxs-lookup"><span data-stu-id="e2905-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="e2905-168">Provare a usare un intervallo di tempo minore oppure usare le funzioni [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) o [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) per [includere tramite l'operatore project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) solo i campi necessari.</span><span class="sxs-lookup"><span data-stu-id="e2905-168">You should try using a smaller time range or by using the [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) the fields you need.</span></span>

<span data-ttu-id="e2905-169">Se la riduzione del set di dati proveniente dalla query di Analisi non soddisfa i propri requisiti, può essere utile usare l'[API](https://dev.applicationinsights.io/documentation/overview) per estrarre un set di dati di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="e2905-169">If reducing the dataset coming from the Analytics query doesn't meet your requirements you should consider using the [API](https://dev.applicationinsights.io/documentation/overview) to pull a larger dataset.</span></span> <span data-ttu-id="e2905-170">Di seguito sono riportate le istruzioni per convertire l'esportazione della query M per l'uso dell'API.</span><span class="sxs-lookup"><span data-stu-id="e2905-170">Here are instructions on how to convert the M-Query export to use the API.</span></span>

1. <span data-ttu-id="e2905-171">Creare una [chiave API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="e2905-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="e2905-172">Aggiornare lo script M di Power BI esportato da Analisi sostituendo l'URL ARM con l'API AI (vedere l'esempio seguente)</span><span class="sxs-lookup"><span data-stu-id="e2905-172">Update the Power BI M script that you exported from Analytics by replacing the ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="e2905-173">Sostituire **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="e2905-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="e2905-174">con **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="e2905-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="e2905-175">Infine, aggiornare le credenziali in credenziali base e usare la chiave API</span><span class="sxs-lookup"><span data-stu-id="e2905-175">Finally, update credentials to basic, and use your API Key</span></span>
  

<span data-ttu-id="e2905-176">**Script esistente**</span><span class="sxs-lookup"><span data-stu-id="e2905-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="e2905-177">**Script aggiornato**</span><span class="sxs-lookup"><span data-stu-id="e2905-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="e2905-178">Informazioni sul campionamento</span><span class="sxs-lookup"><span data-stu-id="e2905-178">About sampling</span></span>
<span data-ttu-id="e2905-179">Se l'applicazione invia una grande quantità di dati, la funzionalità di campionamento adattivo può essere usata e inviare solo una percentuale dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="e2905-179">If your application sends a lot of data, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="e2905-180">La stessa considerazione vale se il campionamento è stato impostato manualmente nell'SDK o durante l'inserimento.</span><span class="sxs-lookup"><span data-stu-id="e2905-180">The same is true if you have manually set sampling either in the SDK or on ingestion.</span></span> [<span data-ttu-id="e2905-181">Altre informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="e2905-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="e2905-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2905-182">Next steps</span></span>
* [<span data-ttu-id="e2905-183">Power BI - Informazioni</span><span class="sxs-lookup"><span data-stu-id="e2905-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="e2905-184">Esercitazione su Analisi</span><span class="sxs-lookup"><span data-stu-id="e2905-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

