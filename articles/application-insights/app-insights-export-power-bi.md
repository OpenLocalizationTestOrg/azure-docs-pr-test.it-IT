---
title: aaaExport tooPower BI da Application Insights | Documenti Microsoft
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
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="423cb-103">Feed di Power BI da Application Insights</span><span class="sxs-lookup"><span data-stu-id="423cb-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="423cb-104">[Power BI](http://www.powerbi.com/) è una suite di strumenti di analisi business che consente di analizzare i dati e condividere informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="423cb-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="423cb-105">Dashboard completi sono disponibili in tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="423cb-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="423cb-106">È possibile combinare dati provenienti da diverse origini, incluse le query di Analytics di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="423cb-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="423cb-107">Esistono tre metodi consigliati per l'esportazione di dati di Application Insights tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="423cb-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="423cb-108">Possono essere usati insieme o separatamente.</span><span class="sxs-lookup"><span data-stu-id="423cb-108">You can use them separately or together.</span></span>

* <span data-ttu-id="423cb-109">[**Adattatore Power BI**](#power-pi-adapter): consente di impostare un dashboard di dati di telemetria completo dall'app.</span><span class="sxs-lookup"><span data-stu-id="423cb-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="423cb-110">set di grafici di Hello è predefinita, ma è possibile aggiungere query personalizzate da tutte le altre origini.</span><span class="sxs-lookup"><span data-stu-id="423cb-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="423cb-111">[**Esportazione delle query Analitica** ](#export-analytics-queries) -scrivere una query tramite Analitica ed esportarlo tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="423cb-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="423cb-112">È possibile inserire questa query in un dashboard insieme a tutti gli altri dati.</span><span class="sxs-lookup"><span data-stu-id="423cb-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="423cb-113">[**L'esportazione continua e Analitica flusso** ](app-insights-export-stream-analytics.md) -questa operazione richiede più lavoro tooset backup.</span><span class="sxs-lookup"><span data-stu-id="423cb-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="423cb-114">È utile se si desidera tookeep i dati per lunghi periodi di tempo.</span><span class="sxs-lookup"><span data-stu-id="423cb-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="423cb-115">In caso contrario, hello altri metodi sono consigliati.</span><span class="sxs-lookup"><span data-stu-id="423cb-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="423cb-116">Adattatore Power BI</span><span class="sxs-lookup"><span data-stu-id="423cb-116">Power BI adapter</span></span>
<span data-ttu-id="423cb-117">Con questo metodo si crea un dashboard di dati di telemetria completo per l'utente.</span><span class="sxs-lookup"><span data-stu-id="423cb-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="423cb-118">set di dati iniziale Hello è predefinita, ma è possibile aggiungere ulteriori dati tooit.</span><span class="sxs-lookup"><span data-stu-id="423cb-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="423cb-119">Ottenere hello scheda</span><span class="sxs-lookup"><span data-stu-id="423cb-119">Get hello adapter</span></span>
1. <span data-ttu-id="423cb-120">Accedi troppo[Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="423cb-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="423cb-121">Aprire **Get Data** (Ottieni dati), **Servizi**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="423cb-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Scaricare da un'origine dati di Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="423cb-123">Fornire dettagli hello della risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="423cb-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Scaricare da un'origine dati di Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="423cb-125">Attendere un minuto o due per hello toobe di dati importati.</span><span class="sxs-lookup"><span data-stu-id="423cb-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Adattatore Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="423cb-127">È possibile modificare il dashboard di hello, la combinazione di grafici di Application Insights hello con quelli di altre origini e con query Analitica.</span><span class="sxs-lookup"><span data-stu-id="423cb-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="423cb-128">È disponibile una raccolta di visualizzazioni nella quale è possibile ottenere più grafici e ogni grafico include parametri che possono essere impostati.</span><span class="sxs-lookup"><span data-stu-id="423cb-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="423cb-129">Dopo l'importazione iniziale hello, dashboard hello e report hello continuare tooupdate ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="423cb-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="423cb-130">È possibile controllare pianificazione dell'aggiornamento hello hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="423cb-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="423cb-131">Esportare query di Analisi</span><span class="sxs-lookup"><span data-stu-id="423cb-131">Export Analytics queries</span></span>
<span data-ttu-id="423cb-132">La route consente toowrite qualsiasi Analitica si desidera eseguire una query e quindi esportare i dashboard di Power BI tooa.</span><span class="sxs-lookup"><span data-stu-id="423cb-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="423cb-133">(È possibile aggiungere dashboard toohello creato dall'adapter hello).</span><span class="sxs-lookup"><span data-stu-id="423cb-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="423cb-134">Operazione da eseguire una sola volta: installazione di Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="423cb-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="423cb-135">tooimport della query di Application Insights, si utilizza hello versione desktop di Power BI.</span><span class="sxs-lookup"><span data-stu-id="423cb-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="423cb-136">Ma è possibile pubblicarla, web toohello o tooyour dell'area di lavoro di Power BI cloud.</span><span class="sxs-lookup"><span data-stu-id="423cb-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="423cb-137">Installare [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="423cb-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="423cb-138">Esportare una query di Analisi</span><span class="sxs-lookup"><span data-stu-id="423cb-138">Export an Analytics query</span></span>
1. <span data-ttu-id="423cb-139">[Aprire Analisi e scrivere la query](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="423cb-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="423cb-140">Testare e perfezionare query hello finché non si è soddisfatti dei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="423cb-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="423cb-141">**Verificare che tale query hello viene eseguito correttamente in Analitica prima di esportarlo.**</span><span class="sxs-lookup"><span data-stu-id="423cb-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="423cb-142">In hello **esportare** menu, scegliere **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="423cb-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="423cb-143">Salvare il file di testo hello.</span><span class="sxs-lookup"><span data-stu-id="423cb-143">Save hello text file.</span></span>
   
    ![Esportare la query di Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="423cb-145">In Power BI Desktop selezionare **recupera dati, Query vuota** e quindi in hello editor di query, in **vista** selezionare **Editor avanzato Query di**.</span><span class="sxs-lookup"><span data-stu-id="423cb-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="423cb-146">Incollare lo script di linguaggio M hello esportata nella hello avanzate dell'Editor di Query.</span><span class="sxs-lookup"><span data-stu-id="423cb-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Editor query avanzata](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="423cb-148">Potrebbe essere tooprovide credenziali tooallow Power BI tooaccess Azure.</span><span class="sxs-lookup"><span data-stu-id="423cb-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="423cb-149">Utilizzare toosign 'account aziendale' con l'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="423cb-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Fornire le credenziali di Azure tooenable Power BI toorun query Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="423cb-151">(Se sono necessarie le credenziali di hello tooverify, utilizzare hello impostazioni dell'origine dati menu comando hello Editor di Query.</span><span class="sxs-lookup"><span data-stu-id="423cb-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="423cb-152">Prestare attenzione credenziali di hello toospecify utilizzate per Azure, potrebbe essere diverso dalle credenziali per Power BI.)</span><span class="sxs-lookup"><span data-stu-id="423cb-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="423cb-153">Scegliere una visualizzazione per la query e selezionare i campi di hello per l'asse x, y e segmentazione dimensione.</span><span class="sxs-lookup"><span data-stu-id="423cb-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Selezionare la visualizzazione](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="423cb-155">Pubblicare report tooyour Power BI cloud area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="423cb-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="423cb-156">Da qui è possibile incorporare una versione sincronizzata in altre pagine Web.</span><span class="sxs-lookup"><span data-stu-id="423cb-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Selezionare la visualizzazione](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="423cb-158">Aggiornare manualmente i report hello a intervalli o di impostare un aggiornamento pianificato nella pagina di opzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="423cb-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="423cb-159">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="423cb-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="423cb-160">401 o 403 - Non autorizzato</span><span class="sxs-lookup"><span data-stu-id="423cb-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="423cb-161">Questo errore può verificarsi se il token di aggiornamento non è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="423cb-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="423cb-162">Provare a tooensure questi passaggi sarà comunque possibile accedere.</span><span class="sxs-lookup"><span data-stu-id="423cb-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="423cb-163">Se si dispone dell'accesso e le credenziali di aggiornamento hello non funziona, aprire un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="423cb-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="423cb-164">Accedere al portale di Azure hello e assicurarsi che sia possibile accedere a risorse hello</span><span class="sxs-lookup"><span data-stu-id="423cb-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="423cb-165">Provare a specificare credenziali hello toorefresh per hello Dashboard</span><span class="sxs-lookup"><span data-stu-id="423cb-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="423cb-166">502 - Gateway non valido</span><span class="sxs-lookup"><span data-stu-id="423cb-166">502 Bad Gateway</span></span>
<span data-ttu-id="423cb-167">Questo errore è in genere causato da una query di Analisi che restituisce troppi dati.</span><span class="sxs-lookup"><span data-stu-id="423cb-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="423cb-168">È consigliabile provare con un intervallo di tempo inferiore o utilizzando hello [fa](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) o [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) solo funzioni [progetto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello campi necessari.</span><span class="sxs-lookup"><span data-stu-id="423cb-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="423cb-169">Se la riduzione di hello set di dati provenienti da query Analitica hello non soddisfa i requisiti, è consigliabile utilizzare hello [API](https://dev.applicationinsights.io/documentation/overview) toopull un set di dati più grande.</span><span class="sxs-lookup"><span data-stu-id="423cb-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="423cb-170">Di seguito sono istruzioni sulla procedura di esportazione toouse hello API tooconvert hello M-Query.</span><span class="sxs-lookup"><span data-stu-id="423cb-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="423cb-171">Creare una [chiave API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="423cb-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="423cb-172">Hello aggiornamento dello script di Power BI M esportato da Analitica sostituendo hello URL ARM con API AI (vedere l'esempio riportato di seguito)</span><span class="sxs-lookup"><span data-stu-id="423cb-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="423cb-173">Sostituire **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="423cb-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="423cb-174">con **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="423cb-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="423cb-175">Infine, aggiornare le credenziali toobasic e utilizzare la chiave API</span><span class="sxs-lookup"><span data-stu-id="423cb-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="423cb-176">**Script esistente**</span><span class="sxs-lookup"><span data-stu-id="423cb-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="423cb-177">**Script aggiornato**</span><span class="sxs-lookup"><span data-stu-id="423cb-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="423cb-178">Informazioni sul campionamento</span><span class="sxs-lookup"><span data-stu-id="423cb-178">About sampling</span></span>
<span data-ttu-id="423cb-179">Se l'applicazione invia una grande quantità di dati, funzionalità di campionamento adattivo hello possono operare e inviare solo una percentuale dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="423cb-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="423cb-180">Hello che stesso vale se manualmente impostate campionamento in hello SDK o in un inserimento.</span><span class="sxs-lookup"><span data-stu-id="423cb-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="423cb-181">Altre informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="423cb-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="423cb-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="423cb-182">Next steps</span></span>
* [<span data-ttu-id="423cb-183">Power BI - Informazioni</span><span class="sxs-lookup"><span data-stu-id="423cb-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="423cb-184">Esercitazione su Analisi</span><span class="sxs-lookup"><span data-stu-id="423cb-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

