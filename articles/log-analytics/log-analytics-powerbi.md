---
title: Esportare i dati di Log Analytics in Power BI | Microsoft Docs
description: "Power BI è un servizio di analisi business basato sul cloud di Microsoft che fornisce report e visualizzazioni dettagliate per l'analisi di diversi set di dati.  Log Analytics può esportare continuamente dati dal repository OMS in Power BI per poterne sfruttare gli strumenti di analisi e le visualizzazioni.  Questo articolo descrive come configurare query in Log Analytics che eseguono automaticamente l'esportazione in Power BI a intervalli regolari."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 98befb16d27387e8f65a27771a2a32c264119d74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="export-log-analytics-data-to-power-bi"></a><span data-ttu-id="1748d-105">Esportare i dati di Log Analytics in Power BI</span><span class="sxs-lookup"><span data-stu-id="1748d-105">Export Log Analytics data to Power BI</span></span>

>[!NOTE]
> <span data-ttu-id="1748d-106">Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), questo processo per esportare i dati di Log Analytics in Power BI non funzionerà più.</span><span class="sxs-lookup"><span data-stu-id="1748d-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data to Power BI will no longer work.</span></span>  <span data-ttu-id="1748d-107">Le pianificazioni esistenti create prima dell'aggiornamento verranno disabilitate.</span><span class="sxs-lookup"><span data-stu-id="1748d-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="1748d-108">Dopo l'aggiornamento, Azure Log Analytics usa la stessa piattaforma di Application Insights e il processo per esportare le query di Log Analytics in Power BI è uguale al [processo usato per esportare le query di Application Insights in Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span><span class="sxs-lookup"><span data-stu-id="1748d-108">After upgrade, Azure Log Analytics uses the same platform as Application Insights, and you use the same process to export Log Analytics queries to Power BI as [the process to export Application Insights queries to Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="1748d-109">È possibile esportare la query usando la console di Analytics descritta in tale articolo oppure è possibile selezionare il pulsante **Power BI** nella parte superiore della schermata nel portale di ricerca log.</span><span class="sxs-lookup"><span data-stu-id="1748d-109">You can either export the query using the Analytics console as described in that article, or you can select the **Power BI** button at the top of the screen in the Log Search portal.</span></span>



<span data-ttu-id="1748d-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) è un servizio di analisi business basato sul cloud di Microsoft che fornisce visualizzazioni dettagliate e report per l'analisi di differenti set di dati.</span><span class="sxs-lookup"><span data-stu-id="1748d-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="1748d-111">Log Analytics può esportare automaticamente dati dal repository OMS in Power BI per poterne sfruttare gli strumenti di analisi e le visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="1748d-111">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="1748d-112">Quando si configura Power BI con Log Analytics, si creano query di log che esportano i risultati nei set di dati corrispondenti in Power BI.</span><span class="sxs-lookup"><span data-stu-id="1748d-112">When you configure Power BI with Log Analytics, you create log queries that export their results to corresponding datasets in Power BI.</span></span>  <span data-ttu-id="1748d-113">La query e l'esportazione continuano a essere eseguite automaticamente in base a una pianificazione definita dall'utente per mantenere aggiornato il set di dati con gli ultimi dati raccolti da Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1748d-113">The query and export continues to automatically run on a schedule that you define to keep the dataset up to date with the latest data collected by Log Analytics.</span></span>

![Log Analytics in Power BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="1748d-115">Pianificazioni di Power BI</span><span class="sxs-lookup"><span data-stu-id="1748d-115">Power BI Schedules</span></span>
<span data-ttu-id="1748d-116">Una *pianificazione di Power BI* include una ricerca dei log che esporta un set di dati dal repository OMS per un set di dati corrispondente in Power BI e una pianificazione che definisce la frequenza con cui viene eseguita la ricerca per mantenere aggiornato il set di dati.</span><span class="sxs-lookup"><span data-stu-id="1748d-116">A *Power BI Schedule* includes a log search that exports a set of data from the OMS repository to a corresponding dataset in Power BI and a schedule that defines how often this search is run to keep the dataset current.</span></span>

<span data-ttu-id="1748d-117">I campi nel set di dati corrisponderanno alle proprietà dei record restituiti dalla ricerca dei log.</span><span class="sxs-lookup"><span data-stu-id="1748d-117">The fields in the dataset will match the properties of the records returned by the log search.</span></span>  <span data-ttu-id="1748d-118">Se la ricerca restituisce i record di tipi diversi, il set di dati includerà tutte le proprietà di ognuno dei tipi di record inclusi.</span><span class="sxs-lookup"><span data-stu-id="1748d-118">If the search returns records of different types then the dataset will include all of the properties from each of the included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="1748d-119">La procedura consigliata consiste nell'usare una query di ricerca dei log che restituisce dati non elaborati invece di eseguire una qualsiasi operazione di consolidamento usando comandi come [Measure](log-analytics-search-reference.md#measure).</span><span class="sxs-lookup"><span data-stu-id="1748d-119">It is a best practice to use a log search query that returns raw data as opposed to performing any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="1748d-120">È possibile eseguire qualsiasi aggregazione e calcoli in Power BI da dati non elaborati.</span><span class="sxs-lookup"><span data-stu-id="1748d-120">You can perform any aggregation and calculations in Power BI from the raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-to-power-bi"></a><span data-ttu-id="1748d-121">Connessione dell'area di lavoro di OMS a Power BI</span><span class="sxs-lookup"><span data-stu-id="1748d-121">Connecting OMS workspace to Power BI</span></span>
<span data-ttu-id="1748d-122">Prima di poter esportare da Log Analytics in Power BI, è necessario connettersi l'area di lavoro di OMS all'account Power BI usando la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="1748d-122">Before you can export from Log Analytics to Power BI, you must connect your OMS workspace to your Power BI account using the following procedure.</span></span>  

1. <span data-ttu-id="1748d-123">Nella console di OMS selezionare il riquadro **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="1748d-123">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="1748d-124">Selezionare **Account**.</span><span class="sxs-lookup"><span data-stu-id="1748d-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="1748d-125">Nella sezione **Informazioni area di lavoro** fare clic su **Connetti all'account Power BI**.</span><span class="sxs-lookup"><span data-stu-id="1748d-125">In the **Workspace Information** section click **Connect to Power BI Account**.</span></span>
4. <span data-ttu-id="1748d-126">Immettere le credenziali per l'account Power BI.</span><span class="sxs-lookup"><span data-stu-id="1748d-126">Enter the credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="1748d-127">Creare una pianificazione di Power BI</span><span class="sxs-lookup"><span data-stu-id="1748d-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="1748d-128">Creare una pianificazione di Power BI per ogni set di dati usando la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="1748d-128">Create a Power BI Schedule for each dataset using the following procedure.</span></span>

1. <span data-ttu-id="1748d-129">Nella console di OMS selezionare il riquadro **Ricerca log** .</span><span class="sxs-lookup"><span data-stu-id="1748d-129">In the OMS console click the **Log Search** tile.</span></span>
2. <span data-ttu-id="1748d-130">Digitare una nuova query o selezionare una ricerca salvata che restituisca i dati da esportare in **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="1748d-130">Type in a new query or select a saved search that returns the data that you want to export to **Power BI**.</span></span>  
3. <span data-ttu-id="1748d-131">Fare clic sul pulsante **Power BI** nella parte superiore della pagina per aprire la finestra di dialogo **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="1748d-131">Click the **Power BI** button at the top of the page to open the **Power BI** dialog.</span></span>
4. <span data-ttu-id="1748d-132">Fornire le informazioni nella tabella seguente e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1748d-132">Provide the information in the following table and click **Save**.</span></span>

| <span data-ttu-id="1748d-133">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1748d-133">Property</span></span> | <span data-ttu-id="1748d-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1748d-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1748d-135">Nome</span><span class="sxs-lookup"><span data-stu-id="1748d-135">Name</span></span> |<span data-ttu-id="1748d-136">Nome per identificare la pianificazione quando si visualizza l'elenco di pianificazioni di Power BI.</span><span class="sxs-lookup"><span data-stu-id="1748d-136">Name to identify the schedule when you view the list of Power BI schedules.</span></span> |
| <span data-ttu-id="1748d-137">Ricerca salvata</span><span class="sxs-lookup"><span data-stu-id="1748d-137">Saved Search</span></span> |<span data-ttu-id="1748d-138">Ricerca dei log da eseguire.</span><span class="sxs-lookup"><span data-stu-id="1748d-138">The log search to run.</span></span>  <span data-ttu-id="1748d-139">È possibile selezionare la query corrente o selezionare una ricerca salvata dalla casella a discesa.</span><span class="sxs-lookup"><span data-stu-id="1748d-139">You can either select the current query or select an existing saved search from the dropdown box.</span></span> |
| <span data-ttu-id="1748d-140">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="1748d-140">Schedule</span></span> |<span data-ttu-id="1748d-141">Frequenza con cui eseguire la ricerca salvata ed esportare nel set di dati di Power BI.</span><span class="sxs-lookup"><span data-stu-id="1748d-141">How often to run the saved search and export to the Power BI dataset.</span></span>  <span data-ttu-id="1748d-142">Il valore deve essere compreso tra 15 minuti e 24 ore.</span><span class="sxs-lookup"><span data-stu-id="1748d-142">The value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="1748d-143">Nome del set di dati</span><span class="sxs-lookup"><span data-stu-id="1748d-143">Dataset Name</span></span> |<span data-ttu-id="1748d-144">Nome del set di dati in Power BI.</span><span class="sxs-lookup"><span data-stu-id="1748d-144">The name of the dataset in Power BI.</span></span>  <span data-ttu-id="1748d-145">Verrà creato se non esiste e aggiornato se esiste.</span><span class="sxs-lookup"><span data-stu-id="1748d-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="1748d-146">Visualizzazione e rimozione di pianificazioni di Power BI</span><span class="sxs-lookup"><span data-stu-id="1748d-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="1748d-147">Visualizzare l'elenco di pianificazioni di Power BI esistenti con la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="1748d-147">View the list of existing Power BI Schedules with the following procedure.</span></span>

1. <span data-ttu-id="1748d-148">Nella console di OMS selezionare il riquadro **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="1748d-148">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="1748d-149">Selezionare **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="1748d-149">Select **Power BI**.</span></span>

<span data-ttu-id="1748d-150">Oltre ai dettagli della pianificazione, vengono visualizzati il numero di volte in cui è stata eseguita la pianificazione nella settimana precedente e lo stato dell'ultima sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="1748d-150">In addition to the details of the schedule, the number of times that the schedule has run in the past week and the status of the last sync are displayed.</span></span>  <span data-ttu-id="1748d-151">Se la sincronizzazione ha rilevato errori, è possibile fare clic sul collegamento per eseguire una ricerca dei log e trovare i record con i dettagli dell'errore.</span><span class="sxs-lookup"><span data-stu-id="1748d-151">If the sync encountered errors, you can click the link to run a log search for records with details of the error.</span></span>

<span data-ttu-id="1748d-152">È possibile rimuovere una pianificazione facendo clic su **X** nella colonna **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="1748d-152">You can remove a schedule by clicking on the **X** in the **Remove column**.</span></span>  <span data-ttu-id="1748d-153">È possibile disabilitare una pianificazione selezionando **No**.</span><span class="sxs-lookup"><span data-stu-id="1748d-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="1748d-154">Per modificare una pianificazione è necessario rimuoverla e ricrearla con le nuove impostazioni.</span><span class="sxs-lookup"><span data-stu-id="1748d-154">To modify a schedule you must remove it and recreate it with the new settings.</span></span>

![Pianificazioni di Power BI](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="1748d-156">Procedura dettagliata di esempio</span><span class="sxs-lookup"><span data-stu-id="1748d-156">Sample walkthrough</span></span>
<span data-ttu-id="1748d-157">La sezione seguente illustra un esempio di creazione di una pianificazione di Power BI e dell'uso del relativo set di dati per creare un report semplice.</span><span class="sxs-lookup"><span data-stu-id="1748d-157">The following section walks through an example of creating a Power BI Schedule and using its dataset to create a simple report.</span></span>  <span data-ttu-id="1748d-158">In questo esempio tutti i dati sulle prestazioni per un gruppo di computer vengono esportati in Power BI e viene creato un grafico a linee per visualizzare l'utilizzo del processore.</span><span class="sxs-lookup"><span data-stu-id="1748d-158">In this example, all performance data for a set of computers is exported to Power BI and then a line graph is created to display processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="1748d-159">Creare una ricerca dei log</span><span class="sxs-lookup"><span data-stu-id="1748d-159">Create log search</span></span>
<span data-ttu-id="1748d-160">Si inizierà dalla creazione di una ricerca dei log per trovare i dati da inviare al set di dati.</span><span class="sxs-lookup"><span data-stu-id="1748d-160">We start by creating a log search for the data that we want to send to the dataset.</span></span>  <span data-ttu-id="1748d-161">In questo esempio si userà una query che restituisce tutti i dati sulle prestazioni per i computer con un nome che inizia con *srv*.</span><span class="sxs-lookup"><span data-stu-id="1748d-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Pianificazioni di Power BI](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="1748d-163">Creare una ricerca di Power BI</span><span class="sxs-lookup"><span data-stu-id="1748d-163">Create Power BI Search</span></span>
<span data-ttu-id="1748d-164">Fare clic sul pulsante **Power BI** per aprire la finestra di dialogo di Power BI e fornire le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="1748d-164">We click the **Power BI** button to open the Power BI dialog and provide the required information.</span></span>  <span data-ttu-id="1748d-165">Questa ricerca dovrà essere eseguita una volta ogni ora e sarà necessario creare un set di dati denominato *Contoso Perf*.</span><span class="sxs-lookup"><span data-stu-id="1748d-165">We want this search to run once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="1748d-166">Poiché è già aperta una ricerca che crea i dati desiderati, si manterrà il valore predefinito di *Usa query di ricerca corrente* per **Ricerca salvata**.</span><span class="sxs-lookup"><span data-stu-id="1748d-166">Since we already have the search open that creates the data we want, we keep the default of *Use current search query* for **Saved Search**.</span></span>

![Ricerca di Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="1748d-168">Verificare la ricerca di Power BI</span><span class="sxs-lookup"><span data-stu-id="1748d-168">Verify Power BI Search</span></span>
<span data-ttu-id="1748d-169">Per verificare che la pianificazione sia stata creata correttamente, visualizzare l'elenco delle ricerche di Power BI nel riquadro **Impostazioni** nel dashboard di OMS.</span><span class="sxs-lookup"><span data-stu-id="1748d-169">To verify that we created the schedule correctly, we view the list of Power BI Searches under the **Settings** tile in the OMS dashboard.</span></span>  <span data-ttu-id="1748d-170">Attendere alcuni minuti e aggiornare la visualizzazione fino a quando non segnalerà che la sincronizzazione è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="1748d-170">We wait several minutes and refresh this view until it reports that the sync has been run.</span></span>

![Ricerca di Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-the-dataset-in-power-bi"></a><span data-ttu-id="1748d-172">Verificare il set di dati in Power BI</span><span class="sxs-lookup"><span data-stu-id="1748d-172">Verify the dataset in Power BI</span></span>
<span data-ttu-id="1748d-173">Accedere con il proprio account a [powerbi.microsoft.com](http://powerbi.microsoft.com/) e scorrere fino alla **et di dati** nella parte inferiore del riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1748d-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll to **Datasets** at the bottom of the left pane.</span></span>  <span data-ttu-id="1748d-174">È possibile notare che il set di dati *Contoso Perf* è elencato e indica che l'esportazione è stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="1748d-174">We can see that the *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Set di dati di Power BI](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="1748d-176">Creare report basato sul set di dati</span><span class="sxs-lookup"><span data-stu-id="1748d-176">Create report based on dataset</span></span>
<span data-ttu-id="1748d-177">Selezionare il set di dati **Contoso Perf** e quindi fare clic su **Risultati** nel riquadro **Campi** a destra per visualizzare i campi che fanno parte di questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="1748d-177">We select the **Contoso Perf** dataset and then click on **Results** in the **Fields** pane on the right to view the fields that are part of this dataset.</span></span>  <span data-ttu-id="1748d-178">Per creare un grafico a linee che mostra l'utilizzo del processore per ogni computer, eseguire queste azioni.</span><span class="sxs-lookup"><span data-stu-id="1748d-178">To create a line graph showing processor utilization for each computer, we perform the following actions.</span></span>

1. <span data-ttu-id="1748d-179">Selezionare la visualizzazione Grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="1748d-179">Select the Line chart visualization.</span></span>
2. <span data-ttu-id="1748d-180">Trascinare **ObjectName** in **Filtri a livello di report** e selezionare **Processore**.</span><span class="sxs-lookup"><span data-stu-id="1748d-180">Drag **ObjectName** to **Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="1748d-181">Trascinare **CounterName** in **Filtri a livello di report** e selezionare **% tempo processore**.</span><span class="sxs-lookup"><span data-stu-id="1748d-181">Drag **CounterName** to **Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="1748d-182">Trascinare **CounterValue** in **Valori**.</span><span class="sxs-lookup"><span data-stu-id="1748d-182">Drag **CounterValue** to **Values**.</span></span>
5. <span data-ttu-id="1748d-183">Trascinare **Computer** in **Legenda**.</span><span class="sxs-lookup"><span data-stu-id="1748d-183">Drag **Computer** to **Legend**.</span></span>
6. <span data-ttu-id="1748d-184">Trascinare **TimeGenerated** in **Asse**.</span><span class="sxs-lookup"><span data-stu-id="1748d-184">Drag **TimeGenerated** to **Axis**.</span></span>

<span data-ttu-id="1748d-185">Si noterà che il grafico risultante viene visualizzato con i dati dal set di dati.</span><span class="sxs-lookup"><span data-stu-id="1748d-185">We can see that the resulting line graph is displayed with the data from our dataset.</span></span>

![Grafico a linee di Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-the-report"></a><span data-ttu-id="1748d-187">Salvare il report</span><span class="sxs-lookup"><span data-stu-id="1748d-187">Save the report</span></span>
<span data-ttu-id="1748d-188">Per salvare il report fare clic sul pulsante Salva nella parte superiore della schermata e verificare che sia elencato nella sezione Report nel riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1748d-188">We save the report by clicking on the Save button at the top of the screen and validate that it is now listed in the Reports section in the left pane.</span></span>

![Report di Power BI](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="1748d-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1748d-190">Next steps</span></span>
* <span data-ttu-id="1748d-191">Informazioni su [ricerche dei log](log-analytics-log-searches.md) per compilare query che possono essere esportate in Power BI.</span><span class="sxs-lookup"><span data-stu-id="1748d-191">Learn about [log searches](log-analytics-log-searches.md) to build queries that can be exported to Power BI.</span></span>
* <span data-ttu-id="1748d-192">Altre informazioni su [Power BI](http://powerbi.microsoft.com) per generare visualizzazioni basate sulle esportazioni di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1748d-192">Learn more about [Power BI](http://powerbi.microsoft.com) to build visualizations based on Log Analytics exports.</span></span>
