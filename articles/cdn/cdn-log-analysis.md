---
title: Analisi dei log per la rete CDN di Azure | Microsoft Docs
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
ms.openlocfilehash: 03ff74ae4e40d3f2279caaf4f73e9b4aac6a2ebb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="09b5f-103">Log di diagnostica per la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="09b5f-104">Dopo aver abilitato la rete CDN per l'applicazione, è probabile che si voglia monitorare l'uso della rete CDN, controllare l'integrità della distribuzione e risolvere i potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="09b5f-104">After enabling CDN for your application, you will likely want to monitor the CDN usage, check the health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="09b5f-105">La rete CDN di Azure offre queste funzionalità tramite l'[analisi principale della rete CDN](cdn-analyze-usage-patterns.md) e i [log di diagnostica](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="09b5f-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="09b5f-106">Analisi principale della rete CDN</span><span class="sxs-lookup"><span data-stu-id="09b5f-106">CDN Core Analytics</span></span>
<span data-ttu-id="09b5f-107">Gli utenti correnti della rete CDN di Azure con profilo Verizon standard o premium sono già in grado di visualizzare l'analisi principale nel portale supplementare accessibile tramite l'opzione "Gestisci" del portale Azure.</span><span class="sxs-lookup"><span data-stu-id="09b5f-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able to view core analytics in the supplemental portal accessible via the "Manage" option from the Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="09b5f-108">Log di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="09b5f-109">Con questa nuova funzionalità di Azure è ora possibile visualizzare analisi principali e salvarle in una o più destinazioni, tra cui:</span><span class="sxs-lookup"><span data-stu-id="09b5f-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="09b5f-110">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-110">Azure Storage account</span></span>
 - <span data-ttu-id="09b5f-111">Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="09b5f-112">Repository di OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="09b5f-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="09b5f-113">Questa funzionalità è disponibile per tutti gli endpoint della rete CDN che appartengono a profili CDN Verizon (Standard e Premium) e Akamai (Standard).</span><span class="sxs-lookup"><span data-stu-id="09b5f-113">This feature is available for all CDN endpoints belonging to Verizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="09b5f-114">I log di diagnostica consentono di esportare le metriche di utilizzo di base dall'endpoint di rete CDN in diverse origini, per poterle usare in modo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="09b5f-114">Diagnostics logs allow you to export basic usage metrics from your CDN endpoint to a variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="09b5f-115">Ad esempio, è possibile eseguire i tipi di esportazione di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="09b5f-115">For example, you can do the following types of data export:</span></span>

- <span data-ttu-id="09b5f-116">Esportare i dati nell'archiviazione BLOB, esportare in CSV e generare grafici in excel.</span><span class="sxs-lookup"><span data-stu-id="09b5f-116">Export data to blob storage, export to CSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="09b5f-117">Esportare i dati in hub eventi e correlarli con dati provenienti da altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="09b5f-117">Export data to event hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="09b5f-118">Esportare i dati nell'analisi dei log e visualizzarli nella propria area di lavoro OMS</span><span class="sxs-lookup"><span data-stu-id="09b5f-118">Export data to log analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="09b5f-119">La figura seguente mostra una tipica visualizzazione di analisi principale della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="09b5f-119">The following figure shows a typical CDN Core Analytics view into data.</span></span>

![portale - Log di diagnostica](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="09b5f-121">*Figura 1 - Visualizzazione di analisi principale della rete CDN*</span><span class="sxs-lookup"><span data-stu-id="09b5f-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="09b5f-122">La procedura dettagliata seguente descrive in modo dettagliato lo schema dei dati dell'analisi principale, i passaggi necessari per abilitare la funzionalità e distribuire i dati in diverse destinazioni e l'uso da tali destinazioni.</span><span class="sxs-lookup"><span data-stu-id="09b5f-122">The following walkthrough goes through the schema of the core analytics data, steps involved in enabling the feature and delivering them to various destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="09b5f-123">Abilitare la registrazione con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="09b5f-124">I log di diagnostica sono **disattivati** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="09b5f-124">The diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="09b5f-125">Per abilitare la registrazione con l'analisi principale della rete CDN, eseguire i passaggi indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="09b5f-125">Follow the steps below to enable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="09b5f-126">Accedere al [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09b5f-126">Sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="09b5f-127">Se non si è già abilitata per il proprio flusso di lavoro, [abilitare la rete CDN di Azure](cdn-create-new-endpoint.md) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="09b5f-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="09b5f-128">Nel portale spostarsi sul **profilo CDN**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-128">In the portal, navigate to **CDN profile**.</span></span>
2. <span data-ttu-id="09b5f-129">Selezionare un profilo CDN, quindi selezionare l'endpoint della rete CDN per cui si desidera abilitare **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-129">Select a CDN profile, then select the CDN endpoint that you want to enable **Diagnostics Logs**.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="09b5f-131">Andare al pannello **Log di diagnostica** nella sezione **Monitoraggio**, quindi modificare lo stato su **Attivato**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-131">Go to **Diagnostics Logs** blade Under **Monitoring** section, then change the status to **On**.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="09b5f-133">Abilitare la registrazione con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="09b5f-134">Per usare Archiviazione di Azure per archiviare i log, selezionare **Archivia in un account di archiviazione**, selezionare i giorni di conservazione e fare clic su **CoreAnalytics** in **Log**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-134">To use Azure Storage to store the logs, select **Archive to a storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![portale - Log di diagnostica](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="09b5f-136">*Figura 2 - Registrazione con Archiviazione di Azure*</span><span class="sxs-lookup"><span data-stu-id="09b5f-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="09b5f-137">Registrazione con OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="09b5f-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="09b5f-138">Per usare OMS Log Analytics per archiviare i log, eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="09b5f-138">To use OMS Log Analytics to store the logs, follow these steps:</span></span>

1. <span data-ttu-id="09b5f-139">Nel pannello **Log di diagnostica** in **Monitoraggio** selezionare **Invia a Log Analytics** nel</span><span class="sxs-lookup"><span data-stu-id="09b5f-139">From the **Diagnostics Logs** blade Under **Monitoring**, select **Send to Log Analytics** from</span></span> 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="09b5f-141">Configurare la registrazione di Log Analytics facendo clic su Configura.</span><span class="sxs-lookup"><span data-stu-id="09b5f-141">Configure the Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="09b5f-142">Si verrà reindirizzati a una finestra di dialogo in cui è possibile selezionare un'area di lavoro precedente o crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="09b5f-142">This takes you to a dialog where you can select a previous workspace or create a new one.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="09b5f-144">Fare clic su **Crea una nuova area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-144">Click **Create New Workspace**.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="09b5f-146">È quindi necessario selezionare il nome della nuova area di lavoro, la sottoscrizione esistente, un gruppo di risorse (nuovo o esistente), la posizione e il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="09b5f-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="09b5f-147">È possibile aggiungere questa configurazione al dashboard.</span><span class="sxs-lookup"><span data-stu-id="09b5f-147">You have the option of pinning this configuration to your dashboard.</span></span> <span data-ttu-id="09b5f-148">Fare clic su OK per completare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="09b5f-148">Click OK to complete the configuration.</span></span>

    <span data-ttu-id="09b5f-149">È quindi necessario visualizzare l'area di lavoro con i nomi dell'area di lavoro e del gruppo di risorse di OMS.</span><span class="sxs-lookup"><span data-stu-id="09b5f-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="09b5f-150">I nomi devono essere univoci e possono contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="09b5f-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="09b5f-151">Gli spazi e i caratteri di sottolineatura non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="09b5f-151">Spaces and underscores are not allowed.</span></span> 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="09b5f-153">Viene visualizzato un breve messaggio che indica che l'area di lavoro è stata creata e quindi viene visualizzata di nuovo la schermata di configurazione della registrazione.</span><span class="sxs-lookup"><span data-stu-id="09b5f-153">You next get a short message saying that your workspace has been created and you are returned to your logging configuration screen.</span></span> <span data-ttu-id="09b5f-154">È possibile confermare il nome dell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="09b5f-154">You can confirm the name of your Log Analytics workspace.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="09b5f-156">Dopo aver completato la configurazione di Log Analytics, assicurarsi di selezionare anche la casella CoreAnalytics per la registrazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="09b5f-156">Once you have set up the Log Analytics configuration, make sure you also check the CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="09b5f-157">Se è tutto corretto, fare clic sul pulsante **Salva** nella parte superiore della finestra di dialogo di configurazione.</span><span class="sxs-lookup"><span data-stu-id="09b5f-157">If everything is to your liking, click the **Save** button at the top of the configuration dialog.</span></span>

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="09b5f-159">Il pulsante **Salva** non è più attivo e il pulsante Sì/No è ora impostato su Sì, ma è blu anziché viola.</span><span class="sxs-lookup"><span data-stu-id="09b5f-159">The **Save** button is no longer active and that the ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="09b5f-160">Se si vuole visualizzare la nuova area di lavoro OMS, passare al dashboard del portale di Azure e fare clic sul nome dell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="09b5f-160">If you want to see your new OMS workspace, go to your Azure portal Dashboard, click the name of your Log Analytics workspace.</span></span> <span data-ttu-id="09b5f-161">Verrà visualizzata l'area di lavoro. Assicurarsi che l'area di lavoro OMS sia evidenziata a sinistra.</span><span class="sxs-lookup"><span data-stu-id="09b5f-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on the left).</span></span> <span data-ttu-id="09b5f-162">Fare clic sul riquadro Portale di OMS per visualizzare l'area di lavoro nel repository di OMS.</span><span class="sxs-lookup"><span data-stu-id="09b5f-162">Click on the OMS Portal tile to see your workspace in the OMS repository.</span></span> 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="09b5f-164">Il repository di OMS è ora pronto per registrare dati.</span><span class="sxs-lookup"><span data-stu-id="09b5f-164">Your OMS repository is now ready to log data.</span></span> <span data-ttu-id="09b5f-165">Per utilizzare i dati, è necessario usare una [soluzione OMS](#consuming-oms-log-analytics-data), descritta più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="09b5f-165">In order to consume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="09b5f-166">Per altre informazioni sui ritardi dei dati di log, vedere [qui](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="09b5f-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="09b5f-167">Abilitare la registrazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="09b5f-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="09b5f-168">Di seguito viene riportato un esempio di come abilitare e ottenere log di diagnostica tramite i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09b5f-168">Below is an example on how to enable and get Diagnostic Logs via the Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="09b5f-169">Abilitare log di diagnostica in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="09b5f-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="09b5f-170">Prima di tutto, accedere e selezionare una sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="09b5f-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="09b5f-171">Per abilitare i log di diagnostica in un account di archiviazione, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="09b5f-171">To Enable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="09b5f-172">Per abilitare i log di diagnostica in un'area di lavoro OMS, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="09b5f-172">To Enable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="09b5f-173">Utilizzo di log di diagnostica da Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="09b5f-174">Questa sezione descrive lo schema dell'analisi principale della rete CDN e il modo in cui questa è organizzata all'interno di un account di archiviazione di Azure e contiene il codice di esempio per scaricare i log in un file CSV.</span><span class="sxs-lookup"><span data-stu-id="09b5f-174">This section describes the schema of the CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code to download the logs in to a CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="09b5f-175">Uso di Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="09b5f-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="09b5f-176">Per poter accedere ai dati di analisi principali dell'account di archiviazione di Azure, è necessario uno strumento per accedere al contenuto di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="09b5f-176">Before you can access the core analytics data from the Azure Storage Account, you first need a tool to access the contents in a storage account.</span></span> <span data-ttu-id="09b5f-177">Sebbene siano disponibili sul mercato diversi strumenti, si consiglia l'uso di Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="09b5f-177">While there are several tools available in the market, the one that we recommend is the Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="09b5f-178">È possibile scaricare lo strumento [qui](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="09b5f-178">You can download the tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="09b5f-179">Dopo aver scaricato e installato il software, configurarlo per usare lo stesso account di archiviazione di Azure impostato come destinazione dei log di diagnostica della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="09b5f-179">After downloading and installing the software, configure it to use the same Azure Storage Account that was configured as a destination to the CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="09b5f-180">Aprire **Microsoft Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="09b5f-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="09b5f-181">Individuare l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="09b5f-181">Locate the storage account</span></span>
3.  <span data-ttu-id="09b5f-182">Passare al nodo **"Blob Containers"** in questo account di archiviazione ed espanderlo</span><span class="sxs-lookup"><span data-stu-id="09b5f-182">Go to the **“Blob Containers”** node under this storage account and expand the node</span></span>
4.  <span data-ttu-id="09b5f-183">Selezionare il contenitore denominato **"insights-logs-coreanalytics"** e fare doppio clic su di esso</span><span class="sxs-lookup"><span data-stu-id="09b5f-183">Select the container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="09b5f-184">Risultati visualizzati nel riquadro di destra a partire dal primo livello, simili a **"resourceId="**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-184">Results show up on the right-hand pane starting with the first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="09b5f-185">Continuare a fare clic finché non si visualizza il file **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-185">Continue clicking all the way until you see the file **PT1H.json**.</span></span> <span data-ttu-id="09b5f-186">Per una spiegazione del percorso, vedere la nota di seguito.</span><span class="sxs-lookup"><span data-stu-id="09b5f-186">See the following note for explanation of the path.</span></span>
6.  <span data-ttu-id="09b5f-187">Ogni BLOB **PT1H.json** rappresenta i log di analisi per un'ora per un endpoint della rete CDN specifico o per il relativo dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="09b5f-187">Each blob **PT1H.json** represents the analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="09b5f-188">Lo schema del contenuto di questo file JSON è descritto nella sezione Schema dei log dell'analisi principale</span><span class="sxs-lookup"><span data-stu-id="09b5f-188">The schema of the contents of this JSON file is described in the section Schema of the Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="09b5f-189">**Formato del percorso BLOB**</span><span class="sxs-lookup"><span data-stu-id="09b5f-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="09b5f-190">I log dell'analisi principale vengono generati ogni ora.</span><span class="sxs-lookup"><span data-stu-id="09b5f-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="09b5f-191">Tutti i dati per un'ora sono raccolti e archiviati all'interno di un unico BLOB di Azure come payload JSON.</span><span class="sxs-lookup"><span data-stu-id="09b5f-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="09b5f-192">Il percorso di questo BLOB di Azure appare come se fosse presente una struttura gerarchica.</span><span class="sxs-lookup"><span data-stu-id="09b5f-192">The path to this Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="09b5f-193">Questo è dovuto al fatto che lo strumento Storage Explorer interpreta "/" come un separatore di directory e mostra la gerarchia per comodità.</span><span class="sxs-lookup"><span data-stu-id="09b5f-193">This is because the Storage explorer tool interprets '/' as a directory separator and shows the hierarchy for convenience.</span></span> <span data-ttu-id="09b5f-194">In realtà, l'intero percorso è rappresentato solo dal nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="09b5f-194">Actually, the whole path just represents the blob name.</span></span> <span data-ttu-id="09b5f-195">Questo nome del BLOB segue la convenzione di denominazione seguente</span><span class="sxs-lookup"><span data-stu-id="09b5f-195">This name of the blob follows the following naming convention</span></span>   
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="09b5f-196">**Descrizione dei campi:**</span><span class="sxs-lookup"><span data-stu-id="09b5f-196">**Description of fields:**</span></span>

|<span data-ttu-id="09b5f-197">value</span><span class="sxs-lookup"><span data-stu-id="09b5f-197">value</span></span>|<span data-ttu-id="09b5f-198">description</span><span class="sxs-lookup"><span data-stu-id="09b5f-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="09b5f-199">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="09b5f-199">Subscription ID</span></span>    |<span data-ttu-id="09b5f-200">ID della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="09b5f-200">ID of the Azure Subscription.</span></span> <span data-ttu-id="09b5f-201">Questo è in formato Guid.</span><span class="sxs-lookup"><span data-stu-id="09b5f-201">This is in the Guid format.</span></span>|
|<span data-ttu-id="09b5f-202">Risorsa</span><span class="sxs-lookup"><span data-stu-id="09b5f-202">Resource</span></span> |<span data-ttu-id="09b5f-203">Nome gruppo    Nome del gruppo di risorse cui appartengono le risorse della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="09b5f-203">Group Name   Name of the resource group to which the CDN resources belong.</span></span>|
|<span data-ttu-id="09b5f-204">Nome profilo</span><span class="sxs-lookup"><span data-stu-id="09b5f-204">Profile Name</span></span> |<span data-ttu-id="09b5f-205">Nome del profilo CDN</span><span class="sxs-lookup"><span data-stu-id="09b5f-205">Name of the CDN Profile</span></span>|
|<span data-ttu-id="09b5f-206">Nome endpoint</span><span class="sxs-lookup"><span data-stu-id="09b5f-206">Endpoint Name</span></span> |<span data-ttu-id="09b5f-207">Nome dell'endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="09b5f-207">Name of the CDN Endpoint</span></span>|
|<span data-ttu-id="09b5f-208">Year</span><span class="sxs-lookup"><span data-stu-id="09b5f-208">Year</span></span>|  <span data-ttu-id="09b5f-209">Rappresentazione a 4 cifre dell'anno, ad esempio 2017</span><span class="sxs-lookup"><span data-stu-id="09b5f-209">4-digit representation of the year for example, 2017</span></span>|
|<span data-ttu-id="09b5f-210">Mese</span><span class="sxs-lookup"><span data-stu-id="09b5f-210">Month</span></span>| <span data-ttu-id="09b5f-211">Rappresentazione a 2 cifre del numero del mese.</span><span class="sxs-lookup"><span data-stu-id="09b5f-211">2-digit representation of the month number.</span></span> <span data-ttu-id="09b5f-212">01=Gennaio... 12=Dicembre</span><span class="sxs-lookup"><span data-stu-id="09b5f-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="09b5f-213">Giorno</span><span class="sxs-lookup"><span data-stu-id="09b5f-213">Day</span></span>|   <span data-ttu-id="09b5f-214">Rappresentazione a 2 cifre del giorno del mese</span><span class="sxs-lookup"><span data-stu-id="09b5f-214">2 digit representation of the day of the month</span></span>|
|<span data-ttu-id="09b5f-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="09b5f-215">PT1H.json</span></span>| <span data-ttu-id="09b5f-216">File JSON effettivo in cui vengono archiviati i dati di analisi</span><span class="sxs-lookup"><span data-stu-id="09b5f-216">Actual JSON file where the analytics data is stored</span></span>|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a><span data-ttu-id="09b5f-217">Esportazione dei dati dell'analisi principale in un file CSV</span><span class="sxs-lookup"><span data-stu-id="09b5f-217">Exporting the Core Analytics Data to a CSV File</span></span>

<span data-ttu-id="09b5f-218">Per semplificare l'accesso all'analisi principale, è disponibile il codice di esempio per uno strumento che consente di scaricare i file JSON in un formato di file normale con valori delimitati da virgole, che può essere usato per creare grafici o altre aggregazioni in tutta semplicità.</span><span class="sxs-lookup"><span data-stu-id="09b5f-218">To make it easy to access the Core Analytics, we provide a sample code for a tool, which allows downloading the JSON files into a flat comma-separated file format, which can be used to easily create charts or other aggregations.</span></span>

<span data-ttu-id="09b5f-219">Di seguito è illustrato come è possibile usare lo strumento:</span><span class="sxs-lookup"><span data-stu-id="09b5f-219">Here is how you can use the tool:</span></span>

1.  <span data-ttu-id="09b5f-220">Visitare il collegamento github: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="09b5f-220">Visit the github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="09b5f-221">Scaricare il codice</span><span class="sxs-lookup"><span data-stu-id="09b5f-221">Download the code</span></span>
3.  <span data-ttu-id="09b5f-222">Seguire le istruzioni per la compilazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="09b5f-222">Follow instructions to compile and configure</span></span>
4.  <span data-ttu-id="09b5f-223">Eseguire lo strumento</span><span class="sxs-lookup"><span data-stu-id="09b5f-223">Run the tool</span></span>
5.  <span data-ttu-id="09b5f-224">Il file CSV risultate mostra i dati di analisi in una semplice gerarchia.</span><span class="sxs-lookup"><span data-stu-id="09b5f-224">Resulting CSV file shows the analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="09b5f-225">Utilizzo di log di diagnostica da un repository di OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="09b5f-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="09b5f-226">Log Analytics è un servizio in Operations Management Suite (OMS) che monitora gli ambienti cloud e locali per mantenerne la disponibilità e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="09b5f-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments to maintain their availability and performance.</span></span> <span data-ttu-id="09b5f-227">Raccoglie i dati generati dalle risorse negli ambienti cloud e locali e da altri strumenti di monitoraggio per analizzare più origini.</span><span class="sxs-lookup"><span data-stu-id="09b5f-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools to provide analysis across multiple sources.</span></span> 

<span data-ttu-id="09b5f-228">Per usare Log Analytics, è necessario [abilitare la registrazione](#enable-logging-with-azure-storage) nel repository di Azure OMS Log Analytics, descritto in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="09b5f-228">To use Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) to the Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-the-oms-repository"></a><span data-ttu-id="09b5f-229">Uso del repository di OMS</span><span class="sxs-lookup"><span data-stu-id="09b5f-229">Using the OMS Repository</span></span>

 <span data-ttu-id="09b5f-230">Il diagramma seguente mostra l'architettura degli input e output del repository:</span><span class="sxs-lookup"><span data-stu-id="09b5f-230">The following diagram shows the architecture of the inputs and outputs of the repository:</span></span>

![Repository di OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="09b5f-232">*Figura 3 - Repository di Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="09b5f-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="09b5f-233">È possibile visualizzare i dati in svariati modi tramite soluzioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="09b5f-233">You can display the data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="09b5f-234">È possibile ottenere soluzioni di gestione da [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="09b5f-234">You can obtain Management Solutions from the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="09b5f-235">È possibile installare le soluzioni di gestione da Azure Marketplace facendo clic sul collegamento **Get it now** (Scarica adesso) nella parte inferiore di ogni soluzione.</span><span class="sxs-lookup"><span data-stu-id="09b5f-235">You can install management solutions from Azure marketplace by clicking the **Get it now** link at the bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="09b5f-236">Aggiunta di una soluzione di gestione della rete CDN di OMS</span><span class="sxs-lookup"><span data-stu-id="09b5f-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="09b5f-237">Seguire questi passaggi per aggiungere una soluzione di gestione:</span><span class="sxs-lookup"><span data-stu-id="09b5f-237">Follow these steps to add a Management Solution:</span></span>

1.   <span data-ttu-id="09b5f-238">Se non è già stato fatto, accedere al portale di Azure tramite la sottoscrizione di Azure e passare al dashboard.</span><span class="sxs-lookup"><span data-stu-id="09b5f-238">If you haven't already done so, sign in to the Azure portal using your Azure subscription and go to your Dashboard.</span></span>
    <span data-ttu-id="09b5f-239">![Dashboard di Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="09b5f-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="09b5f-240">Nel pannello **Nuovo** in **Marketplace** selezionare **Monitoraggio e gestione**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-240">In the **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="09b5f-242">Nel pannello **Monitoraggio e gestione** fare clic su **Visualizza tutto**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-242">In the **Monitoring + management** blade, click **See all**.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="09b5f-244">Cercare la rete CDN nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="09b5f-244">Search for CDN in the search box.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="09b5f-246">Selezionare **Azure CDN Core Analytics** (Analisi principale rete CDN di Azure).</span><span class="sxs-lookup"><span data-stu-id="09b5f-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="09b5f-248">Dopo aver fatto clic su **Crea**, verrà chiesto se creare una nuova area di lavoro OMS o se usarne una esistente.</span><span class="sxs-lookup"><span data-stu-id="09b5f-248">After clicking **Create**, you will be asked to create a new OMS workspace or use an existing one.</span></span> 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="09b5f-250">Selezionare l'area di lavoro creata prima.</span><span class="sxs-lookup"><span data-stu-id="09b5f-250">Select the workspace you created before.</span></span> <span data-ttu-id="09b5f-251">Sarà quindi necessario aggiungere un account di automazione.</span><span class="sxs-lookup"><span data-stu-id="09b5f-251">You then need to add an automation account.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="09b5f-253">La schermata seguente mostra il modulo dell'account di automazione che è necessario compilare.</span><span class="sxs-lookup"><span data-stu-id="09b5f-253">The following screen shows the automation account form you must fill out.</span></span> 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="09b5f-255">Dopo aver creato l'account di automazione, è possibile aggiungere la soluzione.</span><span class="sxs-lookup"><span data-stu-id="09b5f-255">Once you have created the automation account, you are ready to add your solution.</span></span> <span data-ttu-id="09b5f-256">Selezionare il pulsante **Create** .</span><span class="sxs-lookup"><span data-stu-id="09b5f-256">Click the **Create** button.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="09b5f-258">La soluzione è stata ora aggiunta all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="09b5f-258">Your solution has now been added to your workspace.</span></span> <span data-ttu-id="09b5f-259">Tornare al dashboard del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="09b5f-259">Go back to your Azure portal Dashboard.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="09b5f-261">Fare clic sull'area di lavoro di Log Analytics creata per passare all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="09b5f-261">Click the Log Analytics workspace you created to go to your workspace.</span></span> 

11. <span data-ttu-id="09b5f-262">Fare clic sul riquadro **Portale di OMS** per visualizzare la nuova soluzione nel portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="09b5f-262">Click the **OMS Portal** tile to see your new solution in the OMS portal.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="09b5f-264">Il portale di OMS dovrebbe avere un aspetto simile a quello mostrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="09b5f-264">Your OMS portal should now look like the following screen:</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="09b5f-266">Fare clic su uno dei riquadri per esaminare diverse visualizzazioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="09b5f-266">Click one of the tiles to see several views into your data.</span></span>

    ![Visualizzare tutto](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="09b5f-268">È possibile scorrere verso destra o sinistra per visualizzare altri riquadri che rappresentano singole visualizzazioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="09b5f-268">You can scroll left or right to see further tiles representing individual views into the data.</span></span> 

    <span data-ttu-id="09b5f-269">Facendo clic su uno dei riquadri, è possibile visualizzare altri dettagli sui dati.</span><span class="sxs-lookup"><span data-stu-id="09b5f-269">Clicking one of the tiles gives you more details about your data.</span></span>

     ![Visualizzare tutto](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="09b5f-271">Offerte e piani tariffari</span><span class="sxs-lookup"><span data-stu-id="09b5f-271">Offers and pricing tiers</span></span>

<span data-ttu-id="09b5f-272">Le offerte e i piani tariffari per le soluzioni di gestione di OMS sono disponibili [qui](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="09b5f-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="09b5f-273">Personalizzazione delle visualizzazioni</span><span class="sxs-lookup"><span data-stu-id="09b5f-273">Customizing views</span></span>

<span data-ttu-id="09b5f-274">È possibile personalizzare la visualizzazione dei dati usando **Progettazione viste**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-274">You can customize the view into your data by using the **View Designer**.</span></span> <span data-ttu-id="09b5f-275">Passare all'area di lavoro di OMS e avviare la progettazione facendo clic sul riquadro **Progettazione viste**.</span><span class="sxs-lookup"><span data-stu-id="09b5f-275">Go to your OMS workspace and begin designing by clicking the **View Designer** tile.</span></span>

![Progettazione viste](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="09b5f-277">È possibile trascinare e rilasciare i tipi di grafico dal lato sinistro e immettere i dettagli dei dati da analizzare a destra.</span><span class="sxs-lookup"><span data-stu-id="09b5f-277">You can drag and drop types of charts from the left and fill in the data details you want to analyze on the left.</span></span>

![Progettazione viste](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="09b5f-279">Ritardi dei dati di log</span><span class="sxs-lookup"><span data-stu-id="09b5f-279">Log data delays</span></span>

<span data-ttu-id="09b5f-280">Ritardi dei dati di log di Verizon</span><span class="sxs-lookup"><span data-stu-id="09b5f-280">Verizon log data delays</span></span> | <span data-ttu-id="09b5f-281">Ritardi dei dati di log di Akamai</span><span class="sxs-lookup"><span data-stu-id="09b5f-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="09b5f-282">I dati dei log di Verizon hanno un ritardo di un'ora e richiedono fino a due ore prima di venire visualizzati dopo il completamento della propagazione degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="09b5f-282">Verizon log data is 1 hour delayed, and take up to 2 hours to start appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="09b5f-283">I dati dei log di Akamai hanno un ritardo di 24 ore e richiedono fino a 2 ore prima di venire visualizzati se sono stati creati più di 24 ore prima.</span><span class="sxs-lookup"><span data-stu-id="09b5f-283">Akamai log data is 24 hours delayed, and takes up to 2 hours to start appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="09b5f-284">Se i log sono stati creati di recente, possono essere necessarie fino a 25 ore prima di poterli visualizzare.</span><span class="sxs-lookup"><span data-stu-id="09b5f-284">If it was recently created, it can take up to 25 hours for the logs to start appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="09b5f-285">Tipi di log di diagnostica per l'analisi principale della rete CDN</span><span class="sxs-lookup"><span data-stu-id="09b5f-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="09b5f-286">Attualmente sono disponibili solo i log di analisi principale, contenenti metriche che mostrano le statistiche sulle risposte HTTP e le statistiche relative all'uscita rilevate dai server POP/perimetrali della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="09b5f-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from the CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="09b5f-287">Dettagli delle metriche dell'analisi principale</span><span class="sxs-lookup"><span data-stu-id="09b5f-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="09b5f-288">La tabella seguente mostra un elenco di metriche disponibili nei log di analisi principale.</span><span class="sxs-lookup"><span data-stu-id="09b5f-288">The following table shows a list of metrics available in the Core Analytics logs.</span></span> <span data-ttu-id="09b5f-289">Non tutte le metriche sono disponibili da tutti i provider, sebbene le differenze siano minime.</span><span class="sxs-lookup"><span data-stu-id="09b5f-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="09b5f-290">La tabella seguente indica anche se una metrica specifica è disponibile presso un provider.</span><span class="sxs-lookup"><span data-stu-id="09b5f-290">The following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="09b5f-291">Si noti che le metriche sono disponibili solo per gli endpoint della rete CDN in cui vi è traffico.</span><span class="sxs-lookup"><span data-stu-id="09b5f-291">Please note that the metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="09b5f-292">Metrica</span><span class="sxs-lookup"><span data-stu-id="09b5f-292">Metric</span></span>                     | <span data-ttu-id="09b5f-293">Descrizione</span><span class="sxs-lookup"><span data-stu-id="09b5f-293">Description</span></span>   | <span data-ttu-id="09b5f-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="09b5f-294">Verizon</span></span>  | <span data-ttu-id="09b5f-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="09b5f-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="09b5f-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="09b5f-296">RequestCountTotal</span></span>         |<span data-ttu-id="09b5f-297">Numero totale di riscontri della richiesta durante questo periodo</span><span class="sxs-lookup"><span data-stu-id="09b5f-297">Total number of request hits during this period</span></span>| <span data-ttu-id="09b5f-298">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-298">Yes</span></span>  |<span data-ttu-id="09b5f-299">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-299">Yes</span></span>   |
| <span data-ttu-id="09b5f-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="09b5f-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="09b5f-301">Conteggio di tutte le richieste che hanno generato un codice HTTP 2xx (ad esempio 200, 202)</span><span class="sxs-lookup"><span data-stu-id="09b5f-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="09b5f-302">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-302">Yes</span></span>  |<span data-ttu-id="09b5f-303">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-303">Yes</span></span>   |
| <span data-ttu-id="09b5f-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="09b5f-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="09b5f-305">Conteggio di tutte le richieste che hanno generato un codice HTTP 3xx (ad esempio 300, 302)</span><span class="sxs-lookup"><span data-stu-id="09b5f-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="09b5f-306">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-306">Yes</span></span>  |<span data-ttu-id="09b5f-307">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-307">Yes</span></span>   |
| <span data-ttu-id="09b5f-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="09b5f-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="09b5f-309">Conteggio di tutte le richieste che hanno generato un codice HTTP 4xx (ad esempio 400, 404)</span><span class="sxs-lookup"><span data-stu-id="09b5f-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="09b5f-310">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-310">Yes</span></span>   |<span data-ttu-id="09b5f-311">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-311">Yes</span></span>   |
| <span data-ttu-id="09b5f-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="09b5f-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="09b5f-313">Conteggio di tutte le richieste che hanno generato un codice HTTP 5xx (ad esempio 500, 504)</span><span class="sxs-lookup"><span data-stu-id="09b5f-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="09b5f-314">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-314">Yes</span></span>  |<span data-ttu-id="09b5f-315">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-315">Yes</span></span>   |
| <span data-ttu-id="09b5f-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="09b5f-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="09b5f-317">Conteggio di tutti gli altri codici HTTP (non inclusi nell'intervallo 2xx-5xx)</span><span class="sxs-lookup"><span data-stu-id="09b5f-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="09b5f-318">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-318">Yes</span></span>  |<span data-ttu-id="09b5f-319">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-319">Yes</span></span>   |
| <span data-ttu-id="09b5f-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="09b5f-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="09b5f-321">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 200</span><span class="sxs-lookup"><span data-stu-id="09b5f-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="09b5f-322">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-322">No</span></span>   |<span data-ttu-id="09b5f-323">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-323">Yes</span></span>   |
| <span data-ttu-id="09b5f-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="09b5f-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="09b5f-325">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 206</span><span class="sxs-lookup"><span data-stu-id="09b5f-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="09b5f-326">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-326">No</span></span>   |<span data-ttu-id="09b5f-327">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-327">Yes</span></span>   |
| <span data-ttu-id="09b5f-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="09b5f-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="09b5f-329">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 302</span><span class="sxs-lookup"><span data-stu-id="09b5f-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="09b5f-330">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-330">No</span></span>   |<span data-ttu-id="09b5f-331">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-331">Yes</span></span>   |
| <span data-ttu-id="09b5f-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="09b5f-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="09b5f-333">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 304</span><span class="sxs-lookup"><span data-stu-id="09b5f-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="09b5f-334">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-334">No</span></span>   |<span data-ttu-id="09b5f-335">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-335">Yes</span></span>   |
| <span data-ttu-id="09b5f-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="09b5f-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="09b5f-337">Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 404</span><span class="sxs-lookup"><span data-stu-id="09b5f-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="09b5f-338">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-338">No</span></span>   |<span data-ttu-id="09b5f-339">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-339">Yes</span></span>   |
| <span data-ttu-id="09b5f-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="09b5f-340">RequestCountCacheHit</span></span> |<span data-ttu-id="09b5f-341">Conteggio di tutte le richieste che hanno generato un riscontro nella cache.</span><span class="sxs-lookup"><span data-stu-id="09b5f-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="09b5f-342">Questo significa che l'asset è stato servito direttamente dal POP al client.</span><span class="sxs-lookup"><span data-stu-id="09b5f-342">This means the asset was served directly from the POP to the Client.</span></span>               | <span data-ttu-id="09b5f-343">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-343">Yes</span></span>  |<span data-ttu-id="09b5f-344">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-344">No</span></span>   |
| <span data-ttu-id="09b5f-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="09b5f-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="09b5f-346">Conteggio di tutte le richieste che hanno generato un mancato riscontro nella cache.</span><span class="sxs-lookup"><span data-stu-id="09b5f-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="09b5f-347">Questo significa che l'asset non è stato trovato nel POP più vicino al client e pertanto è stato recuperato dall'origine.</span><span class="sxs-lookup"><span data-stu-id="09b5f-347">This means the asset was not found on the POP closest to the client, and therefore was retrieved from the Origin.</span></span>              |<span data-ttu-id="09b5f-348">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-348">Yes</span></span>   | <span data-ttu-id="09b5f-349">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-349">No</span></span>  |
| <span data-ttu-id="09b5f-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="09b5f-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="09b5f-351">Conteggio di tutte le richieste a un asset a cui è stata impedita la memorizzazione nella cache a causa di una configurazione dell'utente sull'edge.</span><span class="sxs-lookup"><span data-stu-id="09b5f-351">Count of all requests to an asset that are prevented from being cached due to a user configuration on the edge.</span></span>              |<span data-ttu-id="09b5f-352">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-352">Yes</span></span>   | <span data-ttu-id="09b5f-353">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-353">No</span></span>  |
| <span data-ttu-id="09b5f-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="09b5f-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="09b5f-355">Conteggio di tute le richieste su asset a cui è stata impedita la memorizzazione nella cache dalle intestazioni Cache-Control ed Expires dell'asset che indicano che non deve essere memorizzato nella cache in un POP o da un client HTTP</span><span class="sxs-lookup"><span data-stu-id="09b5f-355">Count of all requests to assets that are prevented from being cached by the asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                |<span data-ttu-id="09b5f-356">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-356">Yes</span></span>   |<span data-ttu-id="09b5f-357">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-357">No</span></span>   |
| <span data-ttu-id="09b5f-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="09b5f-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="09b5f-359">Conteggio di tutte le richieste con stato della cache non coperto dalle metriche precedenti.</span><span class="sxs-lookup"><span data-stu-id="09b5f-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="09b5f-360">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-360">Yes</span></span>   | <span data-ttu-id="09b5f-361">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-361">No</span></span>  |
| <span data-ttu-id="09b5f-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="09b5f-362">EgressTotal</span></span> | <span data-ttu-id="09b5f-363">Trasferimento di dati in uscita in GB</span><span class="sxs-lookup"><span data-stu-id="09b5f-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="09b5f-364">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-364">Yes</span></span>   |<span data-ttu-id="09b5f-365">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-365">Yes</span></span>   |
| <span data-ttu-id="09b5f-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="09b5f-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="09b5f-367">Trasferimento di dati in uscita* per risposte con codici di stato HTTP 2xx in GB</span><span class="sxs-lookup"><span data-stu-id="09b5f-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="09b5f-368">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-368">Yes</span></span>   |<span data-ttu-id="09b5f-369">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-369">No</span></span>   |
| <span data-ttu-id="09b5f-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="09b5f-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="09b5f-371">Trasferimento di dati in uscita per risposte con codici di stato HTTP 3xx in GB</span><span class="sxs-lookup"><span data-stu-id="09b5f-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="09b5f-372">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-372">Yes</span></span>   |<span data-ttu-id="09b5f-373">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-373">No</span></span>   |
| <span data-ttu-id="09b5f-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="09b5f-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="09b5f-375">Trasferimento di dati in uscita per risposte con codici di stato HTTP 4xx in GB</span><span class="sxs-lookup"><span data-stu-id="09b5f-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="09b5f-376">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-376">Yes</span></span>   | <span data-ttu-id="09b5f-377">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-377">No</span></span>  |
| <span data-ttu-id="09b5f-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="09b5f-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="09b5f-379">Trasferimento di dati in uscita per risposte con codici di stato HTTP 5xx in GB</span><span class="sxs-lookup"><span data-stu-id="09b5f-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="09b5f-380">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-380">Yes</span></span>   |  <span data-ttu-id="09b5f-381">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-381">No</span></span> |
| <span data-ttu-id="09b5f-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="09b5f-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="09b5f-383">Trasferimento di dati in uscita per risposte con altri codici di stato HTTP in GB</span><span class="sxs-lookup"><span data-stu-id="09b5f-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="09b5f-384">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-384">Yes</span></span>   |<span data-ttu-id="09b5f-385">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-385">No</span></span>   |
| <span data-ttu-id="09b5f-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="09b5f-386">EgressCacheHit</span></span> |  <span data-ttu-id="09b5f-387">Trasferimento di dati in uscita per risposte recapitate direttamente dalla cache CDN su POP/Edge della rete CDN</span><span class="sxs-lookup"><span data-stu-id="09b5f-387">Outbound data transfer for responses that were delivered directly from the CDN cache on the CDN POPs/Edges</span></span>  |<span data-ttu-id="09b5f-388">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-388">Yes</span></span>   |  <span data-ttu-id="09b5f-389">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-389">No</span></span> |
| <span data-ttu-id="09b5f-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="09b5f-390">EgressCacheMiss</span></span> | <span data-ttu-id="09b5f-391">Trasferimento di dati in uscita per risposte non trovate nel server POP più vicino e recuperate dal server di origine</span><span class="sxs-lookup"><span data-stu-id="09b5f-391">Outbound data transfer for responses that were not found on the nearest POP server, and retrieved from the origin server</span></span>              |<span data-ttu-id="09b5f-392">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-392">Yes</span></span>   |  <span data-ttu-id="09b5f-393">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-393">No</span></span> |
| <span data-ttu-id="09b5f-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="09b5f-394">EgressCacheNoCache</span></span> | <span data-ttu-id="09b5f-395">Trasferimento di dati in uscita per asset a cui è stata impedita la memorizzazione nella cache a causa di una configurazione dell'utente sull'edge.</span><span class="sxs-lookup"><span data-stu-id="09b5f-395">Outbound data transfer for assets that are prevented from being cached due to a user configuration on the edge.</span></span>                |<span data-ttu-id="09b5f-396">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-396">Yes</span></span>   |<span data-ttu-id="09b5f-397">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-397">No</span></span>   |
| <span data-ttu-id="09b5f-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="09b5f-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="09b5f-399">Trasferimento di dati in uscita per asset a cui è stata impedita la memorizzazione nella cache dalle intestazioni Cache-Control ed Expires dell'asset che indicano che non deve essere memorizzato nella cache in un POP o da un client HTTP</span><span class="sxs-lookup"><span data-stu-id="09b5f-399">Outbound data transfer for assets that are prevented from being cached by the asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                    |<span data-ttu-id="09b5f-400">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-400">Yes</span></span>   | <span data-ttu-id="09b5f-401">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-401">No</span></span>  |
| <span data-ttu-id="09b5f-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="09b5f-402">EgressCacheOthers</span></span> |  <span data-ttu-id="09b5f-403">Trasferimento di dati in uscita per altri scenari di cache.</span><span class="sxs-lookup"><span data-stu-id="09b5f-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="09b5f-404">Sì</span><span class="sxs-lookup"><span data-stu-id="09b5f-404">Yes</span></span>   | <span data-ttu-id="09b5f-405">No</span><span class="sxs-lookup"><span data-stu-id="09b5f-405">No</span></span>  |

<span data-ttu-id="09b5f-406">*Il trasferimento di dati in uscita si riferisce al traffico recapitato da server POP della rete CDN al client.</span><span class="sxs-lookup"><span data-stu-id="09b5f-406">*Outbound data transfer refers to traffic delivered from CDN POP servers to the client.</span></span>


### <a name="schema-of-the-core-analytics-logs"></a><span data-ttu-id="09b5f-407">Schema dei log dell'analisi principale</span><span class="sxs-lookup"><span data-stu-id="09b5f-407">Schema of the Core Analytics Logs</span></span> 

<span data-ttu-id="09b5f-408">Tutti i log vengono archiviati in formato JSON e per ogni voce sono presenti campi stringa che seguono lo schema seguente:</span><span class="sxs-lookup"><span data-stu-id="09b5f-408">All logs are stored in JSON format and each entry has string fields following the below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
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

<span data-ttu-id="09b5f-409">Dove 'time' rappresenta l'ora di inizio del limite di ore per cui vengono restituite le statistiche.</span><span class="sxs-lookup"><span data-stu-id="09b5f-409">Where the ‘time’ represents the start time of the hour boundary for which the statistics is reported.</span></span> <span data-ttu-id="09b5f-410">Quando una metrica non è supportata da un provider di rete CDN, anziché un valore double o integer, è specificato un valore null.</span><span class="sxs-lookup"><span data-stu-id="09b5f-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="09b5f-411">Questo valore null indica l'assenza di una metrica e questo comportamento è diverso da un valore 0.</span><span class="sxs-lookup"><span data-stu-id="09b5f-411">This null value indicates the absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="09b5f-412">Notare inoltre che è presente un insieme di metriche per ogni dominio configurato sull'endpoint.</span><span class="sxs-lookup"><span data-stu-id="09b5f-412">Also note that there will be one set of these metrics per domain configured on the endpoint.</span></span>

<span data-ttu-id="09b5f-413">Di seguito sono riportate proprietà di esempio:</span><span class="sxs-lookup"><span data-stu-id="09b5f-413">Example properties below:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="09b5f-414">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="09b5f-414">Additional resources</span></span>

* [<span data-ttu-id="09b5f-415">Log di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="09b5f-416">Analisi principale tramite il portale supplementare della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="09b5f-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="09b5f-417">Azure OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="09b5f-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="09b5f-418">API REST di Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="09b5f-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







