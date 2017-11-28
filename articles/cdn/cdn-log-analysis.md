---
title: analisi aaaLog per la rete CDN di Azure | Documenti Microsoft
description: "Il cliente può abilitare l'analisi dei log per la rete CDN di Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="34a18-103">Log di diagnostica per la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="34a18-104">Dopo l'abilitazione della rete CDN per l'applicazione, verrà probabilmente desidera utilizzo della rete CDN di hello toomonitor, controllare l'integrità di hello del recapito e risolvere eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="34a18-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="34a18-105">La rete CDN di Azure offre queste funzionalità tramite l'[analisi principale della rete CDN](cdn-analyze-usage-patterns.md) e i [log di diagnostica](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="34a18-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="34a18-106">Analisi principale della rete CDN</span><span class="sxs-lookup"><span data-stu-id="34a18-106">CDN Core Analytics</span></span>
<span data-ttu-id="34a18-107">Come un utente di rete CDN di Azure corrente con Verizon standard o un profilo premium, si è già analitica core tooview in grado di nel portale supplementare hello accessibile tramite l'opzione "Gestisci" hello da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="34a18-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="34a18-108">Log di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="34a18-109">Con questa nuova funzionalità di Azure è ora possibile visualizzare analisi principali e salvarle in una o più destinazioni, tra cui:</span><span class="sxs-lookup"><span data-stu-id="34a18-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="34a18-110">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-110">Azure Storage account</span></span>
 - <span data-ttu-id="34a18-111">Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="34a18-112">Repository di OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34a18-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="34a18-113">Questa funzionalità è disponibile per tutti gli endpoint rete CDN appartenenti tooVerizon (Standard e Premium) e i profili di rete CDN Akamai (Standard).</span><span class="sxs-lookup"><span data-stu-id="34a18-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="34a18-114">I log di diagnostica consentono di metriche di utilizzo di base tooexport dalla gamma di tooa endpoint rete CDN di origini in modo che sia possibile utilizzarli in modo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="34a18-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="34a18-115">Ad esempio, è possibile eseguire hello i tipi di esportazione dei dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="34a18-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="34a18-116">Esportare l'archiviazione dei dati tooblob, esportare tooCSV e generare grafici in excel.</span><span class="sxs-lookup"><span data-stu-id="34a18-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="34a18-117">Esportare gli hub tooevent dati e correlare i dati da altri servizi di azure.</span><span class="sxs-lookup"><span data-stu-id="34a18-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="34a18-118">Esportare dati toolog analitica e visualizzare i dati nello spazio di lavoro OMS</span><span class="sxs-lookup"><span data-stu-id="34a18-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="34a18-119">Hello figura seguente mostra una vista Analitica Core della rete CDN tipico nei dati.</span><span class="sxs-lookup"><span data-stu-id="34a18-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![portale - Log di diagnostica](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="34a18-121">*Figura 1 - Visualizzazione di analisi principale della rete CDN*</span><span class="sxs-lookup"><span data-stu-id="34a18-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="34a18-122">seguendo questa procedura dettagliata Hello passa attraverso schema hello dati hello core analitica, i passaggi necessari per abilitare la funzionalità di hello e inviarli toovarious destinazioni e utilizzo di queste destinazioni.</span><span class="sxs-lookup"><span data-stu-id="34a18-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="34a18-123">Abilitare la registrazione con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="34a18-124">Hello log di diagnostica sono attivati **off** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="34a18-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="34a18-125">Seguire i passaggi di hello sotto registrazione tooenable con Analitica Core della rete CDN:</span><span class="sxs-lookup"><span data-stu-id="34a18-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="34a18-126">Accedi toohello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34a18-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="34a18-127">Se non si è già abilitata per il proprio flusso di lavoro, [abilitare la rete CDN di Azure](cdn-create-new-endpoint.md) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="34a18-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="34a18-128">Nel portale di hello passare troppo**profilo CDN**.</span><span class="sxs-lookup"><span data-stu-id="34a18-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="34a18-129">Selezionare un profilo di rete CDN, quindi selezionare l'endpoint rete CDN hello che si desidera tooenable **log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="34a18-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="34a18-131">Andare troppo**log di diagnostica** pannello **monitoraggio** sezione, quindi modificare lo stato di hello troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="34a18-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="34a18-133">Abilitare la registrazione con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="34a18-134">toouse archiviazione di Azure toostore hello registri, selezionare **archiviare l'account di archiviazione tooa**, selezionare i giorni di conservazione e fare clic su **CoreAnalytics** in **Log**.</span><span class="sxs-lookup"><span data-stu-id="34a18-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![portale - Log di diagnostica](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="34a18-136">*Figura 2 - Registrazione con Archiviazione di Azure*</span><span class="sxs-lookup"><span data-stu-id="34a18-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="34a18-137">Registrazione con OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34a18-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="34a18-138">log hello toostore di toouse Analitica di Log di OMS, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="34a18-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="34a18-139">Da hello **log di diagnostica** pannello **monitoraggio**selezionare **inviare tooLog Analitica** da</span><span class="sxs-lookup"><span data-stu-id="34a18-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="34a18-141">Configurare la registrazione Analitica Log hello facendo clic su Configura.</span><span class="sxs-lookup"><span data-stu-id="34a18-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="34a18-142">Verrà visualizzata la finestra di dialogo tooa in cui è possibile selezionare un'area di lavoro precedente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="34a18-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="34a18-144">Fare clic su **Crea una nuova area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="34a18-144">Click **Create New Workspace**.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="34a18-146">È quindi necessario selezionare il nome della nuova area di lavoro, la sottoscrizione esistente, un gruppo di risorse (nuovo o esistente), la posizione e il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="34a18-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="34a18-147">È possibile hello di aggiunta di questo dashboard tooyour di configurazione.</span><span class="sxs-lookup"><span data-stu-id="34a18-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="34a18-148">Fare clic su configurazione hello toocomplete OK.</span><span class="sxs-lookup"><span data-stu-id="34a18-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="34a18-149">È quindi necessario visualizzare l'area di lavoro con i nomi dell'area di lavoro e del gruppo di risorse di OMS.</span><span class="sxs-lookup"><span data-stu-id="34a18-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="34a18-150">I nomi devono essere univoci e possono contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="34a18-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="34a18-151">Gli spazi e i caratteri di sottolineatura non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="34a18-151">Spaces and underscores are not allowed.</span></span> 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="34a18-153">È quindi ottenere un breve messaggio che informa che è stato creato l'area di lavoro e si ritorna tooyour schermata di configurazione di registrazione.</span><span class="sxs-lookup"><span data-stu-id="34a18-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="34a18-154">È possibile verificare il nome di hello dell'area di lavoro Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="34a18-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="34a18-156">Dopo aver impostato la configurazione di Log Analitica hello, assicurarsi che anche casella hello CoreAnalytics per la registrazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="34a18-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="34a18-157">Se tutto è tooyour desiderato, fare clic su hello **salvare** pulsante nella parte superiore di hello della finestra di dialogo Configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="34a18-159">Hello **salvare** pulsante non è più attivo e tale hello in/DISATTIVAZIONE pulsante è ON, ma blu anziché viola.</span><span class="sxs-lookup"><span data-stu-id="34a18-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="34a18-160">Se si desidera toosee nuova area di lavoro OMS, tooyour visitare il portale di Azure Dashboard, fare clic su nome hello dell'area di lavoro Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="34a18-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="34a18-161">Successivamente verrà visualizzato nell'area di lavoro (verificare che l'area di lavoro OMS è evidenziato a sinistra di hello).</span><span class="sxs-lookup"><span data-stu-id="34a18-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="34a18-162">Fare clic su hello portale OMS riquadro toosee l'area di lavoro nel repository OMS hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="34a18-164">Il repository OMS è ora pronto toolog dati.</span><span class="sxs-lookup"><span data-stu-id="34a18-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="34a18-165">Ordinare tooconsume che i dati, è necessario utilizzare un [soluzioni OMS](#consuming-oms-log-analytics-data), coperto più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="34a18-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="34a18-166">Per altre informazioni sui ritardi dei dati di log, vedere [qui](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="34a18-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="34a18-167">Abilitare la registrazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="34a18-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="34a18-168">Di seguito è riportato un esempio di come tooenable e ottenere log di diagnostica tramite hello cmdlet PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="34a18-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="34a18-169">Abilitare log di diagnostica in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="34a18-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="34a18-170">Prima di tutto, accedere e selezionare una sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="34a18-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="34a18-171">tooEnable i log di diagnostica in un Account di archiviazione, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="34a18-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="34a18-172">tooEnable i log di diagnostica in un'area di lavoro OMS, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="34a18-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="34a18-173">Utilizzo di log di diagnostica da Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="34a18-174">In questa sezione descrive schema hello di analitica di core della rete CDN hello, come questi sono organizzati all'interno di un Account di archiviazione di Azure e fornisce hello toodownload codice di esempio i log nel file CSV tooa.</span><span class="sxs-lookup"><span data-stu-id="34a18-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="34a18-175">Uso di Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="34a18-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="34a18-176">Prima di accedere a dati analitica di hello principali da hello Account di archiviazione di Azure, è necessario innanzitutto un contenuto hello tooaccess di strumento in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="34a18-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="34a18-177">Anche se sono disponibili diversi strumenti disponibili in commercio hello, hello che è consigliabile è hello Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="34a18-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="34a18-178">È possibile scaricare lo strumento hello da [qui](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="34a18-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="34a18-179">Dopo il download e installazione del software di hello, configurare toouse hello stesso Account di archiviazione di Azure che è stato configurato come un toohello di destinazione, i log di diagnostica di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="34a18-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="34a18-180">Aprire **Microsoft Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="34a18-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="34a18-181">Individuare l'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="34a18-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="34a18-182">Passare toohello **"Contenitori Blob"** nodo in questo archivio account ed espandere il nodo di hello</span><span class="sxs-lookup"><span data-stu-id="34a18-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="34a18-183">Contenitore hello selezionare denominato **"insights-log-coreanalytics"** e fare doppio clic</span><span class="sxs-lookup"><span data-stu-id="34a18-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="34a18-184">Mostra i risultati di in hello riquadro di destra a partire da hello primo livello, che è simile **"resourceId ="**.</span><span class="sxs-lookup"><span data-stu-id="34a18-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="34a18-185">Continuare a fare clic tutti modo hello fino a visualizzare il file hello **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="34a18-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="34a18-186">Vedere la nota per una descrizione del percorso hello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="34a18-187">Ogni blob **PT1H.json** rappresenta hello registri analitica per un'ora per un endpoint rete CDN specifico o il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="34a18-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="34a18-188">schema di Hello contenuto hello di questo file JSON viene descritta nella sezione di hello dello Schema di hello registri Analitica Core</span><span class="sxs-lookup"><span data-stu-id="34a18-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="34a18-189">**Formato del percorso BLOB**</span><span class="sxs-lookup"><span data-stu-id="34a18-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="34a18-190">I log dell'analisi principale vengono generati ogni ora.</span><span class="sxs-lookup"><span data-stu-id="34a18-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="34a18-191">Tutti i dati per un'ora sono raccolti e archiviati all'interno di un unico BLOB di Azure come payload JSON.</span><span class="sxs-lookup"><span data-stu-id="34a18-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="34a18-192">percorso di Hello toothis Blob di Azure viene visualizzato come se vi è una struttura gerarchica.</span><span class="sxs-lookup"><span data-stu-id="34a18-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="34a18-193">Questo è perché lo strumento Esplora di archiviazione hello interpreta '/' come separatore di directory e viene illustrata la gerarchia hello per praticità.</span><span class="sxs-lookup"><span data-stu-id="34a18-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="34a18-194">In realtà, percorso completo di hello rappresenta solo il nome di blob hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="34a18-195">Questo nome di blob hello segue hello convenzione di denominazione seguente</span><span class="sxs-lookup"><span data-stu-id="34a18-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="34a18-196">**Descrizione dei campi:**</span><span class="sxs-lookup"><span data-stu-id="34a18-196">**Description of fields:**</span></span>

|<span data-ttu-id="34a18-197">value</span><span class="sxs-lookup"><span data-stu-id="34a18-197">value</span></span>|<span data-ttu-id="34a18-198">description</span><span class="sxs-lookup"><span data-stu-id="34a18-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="34a18-199">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="34a18-199">Subscription ID</span></span>    |<span data-ttu-id="34a18-200">ID della sottoscrizione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="34a18-201">Questo è in formato Guid hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="34a18-202">Risorsa</span><span class="sxs-lookup"><span data-stu-id="34a18-202">Resource</span></span> |<span data-ttu-id="34a18-203">Nome gruppo di risorse della rete CDN di hello risorsa gruppo toowhich hello appartiene.</span><span class="sxs-lookup"><span data-stu-id="34a18-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="34a18-204">Nome profilo</span><span class="sxs-lookup"><span data-stu-id="34a18-204">Profile Name</span></span> |<span data-ttu-id="34a18-205">Nome del profilo CDN hello</span><span class="sxs-lookup"><span data-stu-id="34a18-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="34a18-206">Nome endpoint</span><span class="sxs-lookup"><span data-stu-id="34a18-206">Endpoint Name</span></span> |<span data-ttu-id="34a18-207">Nome dell'Endpoint rete CDN hello</span><span class="sxs-lookup"><span data-stu-id="34a18-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="34a18-208">Year</span><span class="sxs-lookup"><span data-stu-id="34a18-208">Year</span></span>|  <span data-ttu-id="34a18-209">rappresentazione di 4 cifre dell'anno hello 2017, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="34a18-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="34a18-210">Mese</span><span class="sxs-lookup"><span data-stu-id="34a18-210">Month</span></span>| <span data-ttu-id="34a18-211">rappresentazione di 2 cifre del numero del mese hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="34a18-212">01=Gennaio... 12=Dicembre</span><span class="sxs-lookup"><span data-stu-id="34a18-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="34a18-213">Giorno</span><span class="sxs-lookup"><span data-stu-id="34a18-213">Day</span></span>|   <span data-ttu-id="34a18-214">rappresentazione a 2 cifre del giorno hello hello mese</span><span class="sxs-lookup"><span data-stu-id="34a18-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="34a18-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="34a18-215">PT1H.json</span></span>| <span data-ttu-id="34a18-216">File JSON effettivo dove vengono archiviati dati analitica hello</span><span class="sxs-lookup"><span data-stu-id="34a18-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="34a18-217">Esportazione di hello Core Analitica dati tooa File CSV</span><span class="sxs-lookup"><span data-stu-id="34a18-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="34a18-218">toomake it tooaccess facile hello Core Analitica, Microsoft fornisce un esempio di codice per uno strumento che consente il download di file JSON di hello in un formato di file flat delimitato da virgole, che può essere utilizzato tooeasily, creare grafici o altre aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="34a18-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="34a18-219">Ecco come è possibile utilizzare lo strumento hello:</span><span class="sxs-lookup"><span data-stu-id="34a18-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="34a18-220">Visitare il collegamento di github hello: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="34a18-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="34a18-221">Scaricare codice hello</span><span class="sxs-lookup"><span data-stu-id="34a18-221">Download hello code</span></span>
3.  <span data-ttu-id="34a18-222">Seguire le istruzioni toocompile e configurare</span><span class="sxs-lookup"><span data-stu-id="34a18-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="34a18-223">Eseguire lo strumento hello</span><span class="sxs-lookup"><span data-stu-id="34a18-223">Run hello tool</span></span>
5.  <span data-ttu-id="34a18-224">File CSV risultante Mostra dati analitica hello in una semplice gerarchia flat.</span><span class="sxs-lookup"><span data-stu-id="34a18-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="34a18-225">Utilizzo di log di diagnostica da un repository di OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34a18-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="34a18-226">Log Analitica è un servizio Operations Management Suite (OMS) che consente di monitorare il toomaintain ambienti cloud e locali loro disponibilità e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="34a18-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="34a18-227">Vengono raccolti i dati generati dalle risorse negli ambienti di cloud e locali e da altre analisi di tooprovide strumenti monitoraggio in più origini.</span><span class="sxs-lookup"><span data-stu-id="34a18-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="34a18-228">toouse Log Analitica, è necessario [abilitare la registrazione](#enable-logging-with-azure-storage) repository di Azure OMS Log Analitica toohello, come illustrato in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="34a18-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="34a18-229">Utilizzo di hello Repository OMS</span><span class="sxs-lookup"><span data-stu-id="34a18-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="34a18-230">Hello seguente diagramma illustra l'architettura hello di input hello e di output del repository hello:</span><span class="sxs-lookup"><span data-stu-id="34a18-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![Repository di OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="34a18-232">*Figura 3 - Repository di Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="34a18-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="34a18-233">È possibile visualizzare dati hello in diversi modi con le soluzioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="34a18-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="34a18-234">Per ottenere soluzioni di gestione di hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="34a18-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="34a18-235">È possibile installare le soluzioni di gestione da Azure marketplace facendo hello **Scarica adesso** collegamento nella parte inferiore di hello di ciascuna soluzione.</span><span class="sxs-lookup"><span data-stu-id="34a18-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="34a18-236">Aggiunta di una soluzione di gestione della rete CDN di OMS</span><span class="sxs-lookup"><span data-stu-id="34a18-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="34a18-237">Seguire questi tooadd passaggi una soluzione di gestione:</span><span class="sxs-lookup"><span data-stu-id="34a18-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="34a18-238">Se non già stato fatto, accedere toohello portale di Azure tramite la sottoscrizione di Azure e passare tooyour Dashboard.</span><span class="sxs-lookup"><span data-stu-id="34a18-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="34a18-239">![Dashboard di Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="34a18-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="34a18-240">In hello **New** pannello **Marketplace**selezionare **monitoraggio + gestione**.</span><span class="sxs-lookup"><span data-stu-id="34a18-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="34a18-242">In hello **monitoraggio + gestione** pannello, fare clic su **tutti**.</span><span class="sxs-lookup"><span data-stu-id="34a18-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="34a18-244">Ricerca per la rete CDN nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-244">Search for CDN in hello search box.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="34a18-246">Selezionare **Azure CDN Core Analytics** (Analisi principale rete CDN di Azure).</span><span class="sxs-lookup"><span data-stu-id="34a18-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="34a18-248">Dopo aver fatto clic **crea**, sarà richiesto toocreate una nuova area di lavoro OMS o utilizzarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="34a18-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="34a18-250">Selezionare l'area di lavoro hello creata prima.</span><span class="sxs-lookup"><span data-stu-id="34a18-250">Select hello workspace you created before.</span></span> <span data-ttu-id="34a18-251">È quindi necessario tooadd un account di automazione.</span><span class="sxs-lookup"><span data-stu-id="34a18-251">You then need tooadd an automation account.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="34a18-253">Hello seguente schermata Mostra form dell'account di automazione hello che è necessario compilare.</span><span class="sxs-lookup"><span data-stu-id="34a18-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="34a18-255">Dopo aver creato l'account di automazione hello, si è pronti tooadd la soluzione.</span><span class="sxs-lookup"><span data-stu-id="34a18-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="34a18-256">Fare clic su hello **crea** pulsante.</span><span class="sxs-lookup"><span data-stu-id="34a18-256">Click hello **Create** button.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="34a18-258">La soluzione è stato aggiunto a questo punto tooyour dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="34a18-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="34a18-259">Tornare tooyour Dashboard portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="34a18-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="34a18-261">Fare clic su area di lavoro di Log Analitica hello creata toogo tooyour area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="34a18-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="34a18-262">Fare clic su hello **portale OMS** riquadro toosee la nuova soluzione nel portale OMS hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="34a18-264">Il portale OMS a questo punto dovrebbe essere simile hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="34a18-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="34a18-266">Fare clic su uno di hello riquadri toosee diverse visualizzazioni sui dati.</span><span class="sxs-lookup"><span data-stu-id="34a18-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="34a18-268">È possibile scorrere a sinistra o destra toosee ulteriormente riquadri rappresentano visualizzazioni singole in dati hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="34a18-269">Fare clic su uno dei riquadri hello vengono forniti maggiori dettagli sui dati.</span><span class="sxs-lookup"><span data-stu-id="34a18-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Visualizzare tutto](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="34a18-271">Offerte e piani tariffari</span><span class="sxs-lookup"><span data-stu-id="34a18-271">Offers and pricing tiers</span></span>

<span data-ttu-id="34a18-272">Le offerte e i piani tariffari per le soluzioni di gestione di OMS sono disponibili [qui](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="34a18-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="34a18-273">Personalizzazione delle visualizzazioni</span><span class="sxs-lookup"><span data-stu-id="34a18-273">Customizing views</span></span>

<span data-ttu-id="34a18-274">È possibile personalizzare hello Visualizza i dati utilizzando hello **Visualizza finestra di progettazione**.</span><span class="sxs-lookup"><span data-stu-id="34a18-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="34a18-275">Visitare l'area di lavoro OMS tooyour e inizia a progettare facendo hello **Visualizza finestra di progettazione** riquadro.</span><span class="sxs-lookup"><span data-stu-id="34a18-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![Progettazione viste](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="34a18-277">È possibile trascinare ed eliminare i tipi di grafici da sinistra hello e specificare i dettagli di dati hello desiderato tooanalyze su hello a sinistra.</span><span class="sxs-lookup"><span data-stu-id="34a18-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![Progettazione viste](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="34a18-279">Ritardi dei dati di log</span><span class="sxs-lookup"><span data-stu-id="34a18-279">Log data delays</span></span>

<span data-ttu-id="34a18-280">Ritardi dei dati di log di Verizon</span><span class="sxs-lookup"><span data-stu-id="34a18-280">Verizon log data delays</span></span> | <span data-ttu-id="34a18-281">Ritardi dei dati di log di Akamai</span><span class="sxs-lookup"><span data-stu-id="34a18-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="34a18-282">Dati del log Verizon viene posticipati 1 ora e richiedere too2 ore toostart visualizzati dopo il completamento di propagazione di endpoint.</span><span class="sxs-lookup"><span data-stu-id="34a18-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="34a18-283">Dati del log Akamai sono 24 ore ritardate e occupano too2 ore toostart visualizzato se è stato creato più di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="34a18-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="34a18-284">Se è stato creato di recente, può richiedere ore too25 per hello registri toostart visualizzati.</span><span class="sxs-lookup"><span data-stu-id="34a18-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="34a18-285">Tipi di log di diagnostica per l'analisi principale della rete CDN</span><span class="sxs-lookup"><span data-stu-id="34a18-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="34a18-286">Offriamo attualmente solo Core Analitica nei registri, che contengono le metriche che mostra le statistiche in uscita come illustrato da hello POP CDN/bordi e risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="34a18-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="34a18-287">Dettagli delle metriche dell'analisi principale</span><span class="sxs-lookup"><span data-stu-id="34a18-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="34a18-288">Hello nella tabella seguente mostra un elenco delle metriche disponibili in hello che Analitica di componenti di base del log.</span><span class="sxs-lookup"><span data-stu-id="34a18-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="34a18-289">Non tutte le metriche sono disponibili da tutti i provider, sebbene le differenze siano minime.</span><span class="sxs-lookup"><span data-stu-id="34a18-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="34a18-290">Nella tabella seguente, anche Hello Mostra se una determinata metrica è disponibile presso un provider.</span><span class="sxs-lookup"><span data-stu-id="34a18-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="34a18-291">Si noti che le metriche hello sono disponibili per solo gli endpoint CDN con il traffico su di essi.</span><span class="sxs-lookup"><span data-stu-id="34a18-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="34a18-292">Metrica</span><span class="sxs-lookup"><span data-stu-id="34a18-292">Metric</span></span>                     | <span data-ttu-id="34a18-293">Descrizione</span><span class="sxs-lookup"><span data-stu-id="34a18-293">Description</span></span>   | <span data-ttu-id="34a18-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="34a18-294">Verizon</span></span>  | <span data-ttu-id="34a18-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="34a18-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="34a18-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="34a18-296">RequestCountTotal</span></span>         |<span data-ttu-id="34a18-297">Numero totale di riscontri della richiesta durante questo periodo</span><span class="sxs-lookup"><span data-stu-id="34a18-297">Total number of request hits during this period</span></span>| <span data-ttu-id="34a18-298">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-298">Yes</span></span>  |<span data-ttu-id="34a18-299">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-299">Yes</span></span>   |
| <span data-ttu-id="34a18-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="34a18-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="34a18-301">Conteggio di tutte le richieste che hanno generato un codice HTTP 2xx (ad esempio 200, 202)</span><span class="sxs-lookup"><span data-stu-id="34a18-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="34a18-302">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-302">Yes</span></span>  |<span data-ttu-id="34a18-303">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-303">Yes</span></span>   |
| <span data-ttu-id="34a18-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="34a18-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="34a18-305">Conteggio di tutte le richieste che hanno generato un codice HTTP 3xx (ad esempio 300, 302)</span><span class="sxs-lookup"><span data-stu-id="34a18-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="34a18-306">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-306">Yes</span></span>  |<span data-ttu-id="34a18-307">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-307">Yes</span></span>   |
| <span data-ttu-id="34a18-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="34a18-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="34a18-309">Conteggio di tutte le richieste che hanno generato un codice HTTP 4xx (ad esempio 400, 404)</span><span class="sxs-lookup"><span data-stu-id="34a18-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="34a18-310">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-310">Yes</span></span>   |<span data-ttu-id="34a18-311">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-311">Yes</span></span>   |
| <span data-ttu-id="34a18-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="34a18-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="34a18-313">Conteggio di tutte le richieste che hanno generato un codice HTTP 5xx (ad esempio 500, 504)</span><span class="sxs-lookup"><span data-stu-id="34a18-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="34a18-314">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-314">Yes</span></span>  |<span data-ttu-id="34a18-315">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-315">Yes</span></span>   |
| <span data-ttu-id="34a18-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="34a18-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="34a18-317">Conteggio di tutti gli altri codici HTTP (non inclusi nell'intervallo 2xx-5xx)</span><span class="sxs-lookup"><span data-stu-id="34a18-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="34a18-318">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-318">Yes</span></span>  |<span data-ttu-id="34a18-319">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-319">Yes</span></span>   |
| <span data-ttu-id="34a18-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="34a18-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="34a18-321">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 200</span><span class="sxs-lookup"><span data-stu-id="34a18-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="34a18-322">No</span><span class="sxs-lookup"><span data-stu-id="34a18-322">No</span></span>   |<span data-ttu-id="34a18-323">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-323">Yes</span></span>   |
| <span data-ttu-id="34a18-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="34a18-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="34a18-325">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 206</span><span class="sxs-lookup"><span data-stu-id="34a18-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="34a18-326">No</span><span class="sxs-lookup"><span data-stu-id="34a18-326">No</span></span>   |<span data-ttu-id="34a18-327">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-327">Yes</span></span>   |
| <span data-ttu-id="34a18-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="34a18-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="34a18-329">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 302</span><span class="sxs-lookup"><span data-stu-id="34a18-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="34a18-330">No</span><span class="sxs-lookup"><span data-stu-id="34a18-330">No</span></span>   |<span data-ttu-id="34a18-331">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-331">Yes</span></span>   |
| <span data-ttu-id="34a18-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="34a18-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="34a18-333">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 304</span><span class="sxs-lookup"><span data-stu-id="34a18-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="34a18-334">No</span><span class="sxs-lookup"><span data-stu-id="34a18-334">No</span></span>   |<span data-ttu-id="34a18-335">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-335">Yes</span></span>   |
| <span data-ttu-id="34a18-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="34a18-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="34a18-337">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 404</span><span class="sxs-lookup"><span data-stu-id="34a18-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="34a18-338">No</span><span class="sxs-lookup"><span data-stu-id="34a18-338">No</span></span>   |<span data-ttu-id="34a18-339">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-339">Yes</span></span>   |
| <span data-ttu-id="34a18-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="34a18-340">RequestCountCacheHit</span></span> |<span data-ttu-id="34a18-341">Conteggio di tutte le richieste che hanno generato un riscontro nella cache.</span><span class="sxs-lookup"><span data-stu-id="34a18-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="34a18-342">Ciò significa che è stata gestita asset hello direttamente da toohello POP hello Client.</span><span class="sxs-lookup"><span data-stu-id="34a18-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="34a18-343">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-343">Yes</span></span>  |<span data-ttu-id="34a18-344">No</span><span class="sxs-lookup"><span data-stu-id="34a18-344">No</span></span>   |
| <span data-ttu-id="34a18-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="34a18-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="34a18-346">Conteggio di tutte le richieste che hanno generato un mancato riscontro nella cache.</span><span class="sxs-lookup"><span data-stu-id="34a18-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="34a18-347">Ciò significa hello asset non trovato nel client toohello più vicino di hello POP e pertanto è stato recuperato dall'origine hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="34a18-348">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-348">Yes</span></span>   | <span data-ttu-id="34a18-349">No</span><span class="sxs-lookup"><span data-stu-id="34a18-349">No</span></span>  |
| <span data-ttu-id="34a18-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="34a18-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="34a18-351">Conteggio di tutte le richieste asset tooan esclusi dalla memorizzazione nella cache a causa di configurazione utente tooa sul bordo hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="34a18-352">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-352">Yes</span></span>   | <span data-ttu-id="34a18-353">No</span><span class="sxs-lookup"><span data-stu-id="34a18-353">No</span></span>  |
| <span data-ttu-id="34a18-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="34a18-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="34a18-355">Conteggio di tutti i richiede tooassets esclusi dalla memorizzazione nella cache dalla Cache-Control dell'asset hello e scade intestazioni, che indicano che è necessario non memorizzare nella cache in un POP o da client hello HTTP</span><span class="sxs-lookup"><span data-stu-id="34a18-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="34a18-356">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-356">Yes</span></span>   |<span data-ttu-id="34a18-357">No</span><span class="sxs-lookup"><span data-stu-id="34a18-357">No</span></span>   |
| <span data-ttu-id="34a18-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="34a18-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="34a18-359">Conteggio di tutte le richieste con stato della cache non coperto dalle metriche precedenti.</span><span class="sxs-lookup"><span data-stu-id="34a18-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="34a18-360">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-360">Yes</span></span>   | <span data-ttu-id="34a18-361">No</span><span class="sxs-lookup"><span data-stu-id="34a18-361">No</span></span>  |
| <span data-ttu-id="34a18-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="34a18-362">EgressTotal</span></span> | <span data-ttu-id="34a18-363">Trasferimento di dati in uscita in GB</span><span class="sxs-lookup"><span data-stu-id="34a18-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="34a18-364">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-364">Yes</span></span>   |<span data-ttu-id="34a18-365">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-365">Yes</span></span>   |
| <span data-ttu-id="34a18-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="34a18-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="34a18-367">Trasferimento di dati in uscita* per risposte con codici di stato HTTP 2xx in GB</span><span class="sxs-lookup"><span data-stu-id="34a18-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="34a18-368">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-368">Yes</span></span>   |<span data-ttu-id="34a18-369">No</span><span class="sxs-lookup"><span data-stu-id="34a18-369">No</span></span>   |
| <span data-ttu-id="34a18-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="34a18-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="34a18-371">Trasferimento di dati in uscita per risposte con codici di stato HTTP 3xx in GB</span><span class="sxs-lookup"><span data-stu-id="34a18-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="34a18-372">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-372">Yes</span></span>   |<span data-ttu-id="34a18-373">No</span><span class="sxs-lookup"><span data-stu-id="34a18-373">No</span></span>   |
| <span data-ttu-id="34a18-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="34a18-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="34a18-375">Trasferimento di dati in uscita per risposte con codici di stato HTTP 4xx in GB</span><span class="sxs-lookup"><span data-stu-id="34a18-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="34a18-376">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-376">Yes</span></span>   | <span data-ttu-id="34a18-377">No</span><span class="sxs-lookup"><span data-stu-id="34a18-377">No</span></span>  |
| <span data-ttu-id="34a18-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="34a18-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="34a18-379">Trasferimento di dati in uscita per risposte con codici di stato HTTP 5xx in GB</span><span class="sxs-lookup"><span data-stu-id="34a18-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="34a18-380">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-380">Yes</span></span>   |  <span data-ttu-id="34a18-381">No</span><span class="sxs-lookup"><span data-stu-id="34a18-381">No</span></span> |
| <span data-ttu-id="34a18-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="34a18-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="34a18-383">Trasferimento di dati in uscita per risposte con altri codici di stato HTTP in GB</span><span class="sxs-lookup"><span data-stu-id="34a18-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="34a18-384">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-384">Yes</span></span>   |<span data-ttu-id="34a18-385">No</span><span class="sxs-lookup"><span data-stu-id="34a18-385">No</span></span>   |
| <span data-ttu-id="34a18-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="34a18-386">EgressCacheHit</span></span> |  <span data-ttu-id="34a18-387">In uscita di trasferimento dei dati per le risposte che sono state recapitate direttamente dalla cache di hello CDN in hello POP CDN/bordi</span><span class="sxs-lookup"><span data-stu-id="34a18-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="34a18-388">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-388">Yes</span></span>   |  <span data-ttu-id="34a18-389">No</span><span class="sxs-lookup"><span data-stu-id="34a18-389">No</span></span> |
| <span data-ttu-id="34a18-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="34a18-390">EgressCacheMiss</span></span> | <span data-ttu-id="34a18-391">Trasferimento dati in uscita per le risposte che non trovate in hello più vicino al server POP e recuperate dal server di origine hello</span><span class="sxs-lookup"><span data-stu-id="34a18-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="34a18-392">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-392">Yes</span></span>   |  <span data-ttu-id="34a18-393">No</span><span class="sxs-lookup"><span data-stu-id="34a18-393">No</span></span> |
| <span data-ttu-id="34a18-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="34a18-394">EgressCacheNoCache</span></span> | <span data-ttu-id="34a18-395">Trasferimento dei dati in uscita per le risorse che hanno impediti viene memorizzato nella cache a causa di configurazione utente tooa sul bordo hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="34a18-396">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-396">Yes</span></span>   |<span data-ttu-id="34a18-397">No</span><span class="sxs-lookup"><span data-stu-id="34a18-397">No</span></span>   |
| <span data-ttu-id="34a18-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="34a18-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="34a18-399">Trasferimento dati in uscita per le risorse che hanno impediti viene memorizzato nella cache dal controllo della Cache e/o intestazioni Expires, che indicano che è necessario non memorizzare nella cache in un POP o da client hello HTTP dell'asset hello</span><span class="sxs-lookup"><span data-stu-id="34a18-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="34a18-400">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-400">Yes</span></span>   | <span data-ttu-id="34a18-401">No</span><span class="sxs-lookup"><span data-stu-id="34a18-401">No</span></span>  |
| <span data-ttu-id="34a18-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="34a18-402">EgressCacheOthers</span></span> |  <span data-ttu-id="34a18-403">Trasferimento di dati in uscita per altri scenari di cache.</span><span class="sxs-lookup"><span data-stu-id="34a18-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="34a18-404">Sì</span><span class="sxs-lookup"><span data-stu-id="34a18-404">Yes</span></span>   | <span data-ttu-id="34a18-405">No</span><span class="sxs-lookup"><span data-stu-id="34a18-405">No</span></span>  |

<span data-ttu-id="34a18-406">* Trasferimento dati in uscita fa riferimento tootraffic inviato dal client di toohello server POP della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="34a18-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="34a18-407">Schema di hello registri Analitica Core</span><span class="sxs-lookup"><span data-stu-id="34a18-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="34a18-408">Tutti i log vengono archiviati in formato JSON e ogni voce include campi stringa in seguito hello schema seguente:</span><span class="sxs-lookup"><span data-stu-id="34a18-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="34a18-409">Dove 'tempo di hello' rappresenta hello ora di inizio del limite di hello ora per il quale viene segnalata statistiche hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="34a18-410">Quando una metrica non è supportata da un provider di rete CDN, anziché un valore double o integer, è specificato un valore null.</span><span class="sxs-lookup"><span data-stu-id="34a18-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="34a18-411">Questo valore null indica l'assenza di hello di una metrica e questo comportamento è diverso da un valore 0.</span><span class="sxs-lookup"><span data-stu-id="34a18-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="34a18-412">Si noti inoltre che non vi saranno una set di queste metriche per ogni dominio configurato nell'endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="34a18-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="34a18-413">Di seguito sono riportate proprietà di esempio:</span><span class="sxs-lookup"><span data-stu-id="34a18-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="34a18-414">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="34a18-414">Additional resources</span></span>

* [<span data-ttu-id="34a18-415">Log di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="34a18-416">Analisi principale tramite il portale supplementare della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="34a18-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="34a18-417">Azure OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34a18-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="34a18-418">API REST di Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34a18-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







