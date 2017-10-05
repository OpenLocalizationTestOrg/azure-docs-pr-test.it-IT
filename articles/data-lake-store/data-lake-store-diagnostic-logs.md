---
title: Visualizzazione dei log di diagnostica per Azure Data Lake Store | Documentazione Microsoft
description: 'Informazioni su come configurare e accedere ai log di diagnostica per Archivio Data Lake di Azure  '
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="de993-103">Accesso ai log di diagnostica per Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="de993-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="de993-104">Informazioni su come abilitare la registrazione diagnostica per l'account di Archivio Data Lake e su come visualizzare i log raccolti per l'account.</span><span class="sxs-lookup"><span data-stu-id="de993-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="de993-105">Le organizzazioni possono abilitare la registrazione diagnostica per il loro account di Archivio Data Lake di Azure per raccogliere gli audit trial di accesso ai dati che forniscono varie informazioni, come l’elenco di utenti che hanno avuto accesso ai dati, la frequenza di accesso ai dati, la quantità di dati archiviati nell’account, ecc.</span><span class="sxs-lookup"><span data-stu-id="de993-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de993-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="de993-106">Prerequisites</span></span>
* <span data-ttu-id="de993-107">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="de993-107">**An Azure subscription**.</span></span> <span data-ttu-id="de993-108">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de993-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="de993-109">**Account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="de993-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="de993-110">Seguire le istruzioni fornite in [Introduzione ad Archivio Azure Data Lake tramite il portale di Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="de993-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="de993-111">Abilitare la registrazione diagnostica per l'account di Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="de993-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="de993-112">Accedere al nuovo [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de993-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="de993-113">Aprire l'account di Data Lake Store e nel pannello corrispondente fare clic su **Impostazioni** e quindi su **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="de993-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="de993-114">Nel pannello **Log di diagnostica**, fare clic su **Attivare la diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="de993-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="de993-115">![Abilitare la funzionalità di registrazione diagnostica](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Abilitare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="de993-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="de993-116">Nel pannello **Diagnostica** , apportare le modifiche seguenti per configurare la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="de993-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="de993-117">![Abilitare la funzionalità di registrazione diagnostica](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Abilitare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="de993-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="de993-118">Impostare lo **Stato** su **Attivo** per abilitare la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="de993-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="de993-119">È possibile scegliere di archiviare/elaborare i dati in modi diversi.</span><span class="sxs-lookup"><span data-stu-id="de993-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="de993-120">Selezionare l'opzione per **archiviare in un account di archiviazione** per archiviare i log in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="de993-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="de993-121">Utilizzare questa opzione se si desidera archiviare i dati che saranno elaborati in batch in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="de993-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="de993-122">Se si seleziona questa opzione è necessario fornire un account di archiviazione di Azure in cui salvare i log.</span><span class="sxs-lookup"><span data-stu-id="de993-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="de993-123">Selezionare l'opzione per eseguire lo **streaming in Hub eventi** per trasmettere i dati di log a un Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="de993-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="de993-124">Molto probabilmente questa opzione viene utilizzata se si dispone di una pipeline di elaborazione a valle per analizzare in tempo reale i log in ingresso.</span><span class="sxs-lookup"><span data-stu-id="de993-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="de993-125">Se si seleziona questa opzione, è necessario fornire i dettagli dell'Hub eventi di Azure che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="de993-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="de993-126">Selezionare l'opzione per **inviare a Log Analytics** per usare il servizio Log Analytics di Azure per analizzare i dati di log generati.</span><span class="sxs-lookup"><span data-stu-id="de993-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="de993-127">Se si seleziona questa opzione, è necessario fornire i dettagli per l'area di lavoro di Operations Management Suite che si vuole usare per eseguire l'analisi dei log.</span><span class="sxs-lookup"><span data-stu-id="de993-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="de993-128">Specificare se si desidera ottenere i log di controllo, i log delle richieste o entrambi.</span><span class="sxs-lookup"><span data-stu-id="de993-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="de993-129">Specificare il numero di giorni per cui devono essere conservati i dati.</span><span class="sxs-lookup"><span data-stu-id="de993-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="de993-130">La conservazione dei dati è disponibile solo se si usano account di archiviazione di Azure per archiviare i dati del log.</span><span class="sxs-lookup"><span data-stu-id="de993-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="de993-131">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="de993-131">Click **Save**.</span></span>

<span data-ttu-id="de993-132">Dopo aver attivato le impostazioni di diagnostica, è possibile controllare i log nella scheda **Log di diagnostica** .</span><span class="sxs-lookup"><span data-stu-id="de993-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="de993-133">Visualizzare i log di diagnostica dell'account di Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="de993-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="de993-134">Esistono due modi per visualizzare i dati di log dell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="de993-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="de993-135">Dalla visualizzazione delle impostazioni dell'account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="de993-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="de993-136">Dall'account di Archiviazione di Azure dove sono archiviati i dati</span><span class="sxs-lookup"><span data-stu-id="de993-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="de993-137">Usando la visualizzazione Impostazioni dell'account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="de993-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="de993-138">Nel pannello **Impostazioni** dell'account Data Lake Store fare clic su **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="de993-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="de993-139">![Visualizzare la registrazione diagnostica](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "Visualizzare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="de993-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="de993-140">Nel pannello **Log di diagnostica** vengono visualizzati i log classificati come **log di controllo** e **log delle richieste**.</span><span class="sxs-lookup"><span data-stu-id="de993-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="de993-141">I log delle richieste acquisiscono tutte le richieste API fatte nell’account di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="de993-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="de993-142">I log di controllo sono simili a quelli delle richieste ma forniscono una suddivisione più dettagliata delle operazioni eseguite nell'account di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="de993-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="de993-143">Ad esempio, una singola chiamata API di caricamento nei log delle richieste potrebbe risultare in molteplici operazioni di "Aggiungi" nei log di controllo.</span><span class="sxs-lookup"><span data-stu-id="de993-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="de993-144">Fare clic sul link **Scarica** di ogni voce di log per scaricare i log.</span><span class="sxs-lookup"><span data-stu-id="de993-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="de993-145">Dall'account di Archiviazione di Azure che contiene i dati di log</span><span class="sxs-lookup"><span data-stu-id="de993-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="de993-146">Aprire il pannello Account di Archiviazione di Azure associato a Data Lake Store per la registrazione e quindi fare clic su BLOB.</span><span class="sxs-lookup"><span data-stu-id="de993-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="de993-147">Il pannello **Servizio BLOB** elenca due contenitori.</span><span class="sxs-lookup"><span data-stu-id="de993-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="de993-148">![Visualizzare la registrazione diagnostica](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Visualizzare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="de993-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="de993-149">Il contenitore **insights-logs-audit** contiene i log di controllo.</span><span class="sxs-lookup"><span data-stu-id="de993-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="de993-150">Il contenitore **insights-logs-requests** contiene i log delle richieste.</span><span class="sxs-lookup"><span data-stu-id="de993-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="de993-151">All'interno di questi contenitori i log vengono archiviati con la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="de993-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="de993-152">![Visualizzare la registrazione diagnostica](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "Visualizzare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="de993-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="de993-153">Ad esempio, il percorso completo a un log di controllo potrebbe essere `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="de993-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="de993-154">Analogamente, il percorso completo a un log della richiesta potrebbe essere `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="de993-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="de993-155">Informazioni sulla struttura dei dati del log</span><span class="sxs-lookup"><span data-stu-id="de993-155">Understand the structure of the log data</span></span>
<span data-ttu-id="de993-156">I log di controllo e delle richieste sono in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="de993-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="de993-157">In questa sezione, viene esaminata la struttura di JSON per i log delle richieste e di controllo.</span><span class="sxs-lookup"><span data-stu-id="de993-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="de993-158">Request Logs</span><span class="sxs-lookup"><span data-stu-id="de993-158">Request logs</span></span>
<span data-ttu-id="de993-159">Di seguito viene riportata una voce di esempio nel log delle richieste in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="de993-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="de993-160">Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.</span><span class="sxs-lookup"><span data-stu-id="de993-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="de993-161">Schema del log delle richieste</span><span class="sxs-lookup"><span data-stu-id="de993-161">Request log schema</span></span>
| <span data-ttu-id="de993-162">Nome</span><span class="sxs-lookup"><span data-stu-id="de993-162">Name</span></span> | <span data-ttu-id="de993-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="de993-163">Type</span></span> | <span data-ttu-id="de993-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de993-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de993-165">time</span><span class="sxs-lookup"><span data-stu-id="de993-165">time</span></span> |<span data-ttu-id="de993-166">String</span><span class="sxs-lookup"><span data-stu-id="de993-166">String</span></span> |<span data-ttu-id="de993-167">Il timestamp del log (fusorario UTC)</span><span class="sxs-lookup"><span data-stu-id="de993-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="de993-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="de993-168">resourceId</span></span> |<span data-ttu-id="de993-169">String</span><span class="sxs-lookup"><span data-stu-id="de993-169">String</span></span> |<span data-ttu-id="de993-170">L’ID della risorsa interessata dall’operazione</span><span class="sxs-lookup"><span data-stu-id="de993-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="de993-171">category</span><span class="sxs-lookup"><span data-stu-id="de993-171">category</span></span> |<span data-ttu-id="de993-172">String</span><span class="sxs-lookup"><span data-stu-id="de993-172">String</span></span> |<span data-ttu-id="de993-173">La categoria di log.</span><span class="sxs-lookup"><span data-stu-id="de993-173">The log category.</span></span> <span data-ttu-id="de993-174">Ad esempio, **Richieste**.</span><span class="sxs-lookup"><span data-stu-id="de993-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="de993-175">operationName</span><span class="sxs-lookup"><span data-stu-id="de993-175">operationName</span></span> |<span data-ttu-id="de993-176">String</span><span class="sxs-lookup"><span data-stu-id="de993-176">String</span></span> |<span data-ttu-id="de993-177">Il nome dell'operazione registrata.</span><span class="sxs-lookup"><span data-stu-id="de993-177">Name of the operation that is logged.</span></span> <span data-ttu-id="de993-178">Ad esempio, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="de993-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="de993-179">resultType</span><span class="sxs-lookup"><span data-stu-id="de993-179">resultType</span></span> |<span data-ttu-id="de993-180">String</span><span class="sxs-lookup"><span data-stu-id="de993-180">String</span></span> |<span data-ttu-id="de993-181">Lo stato dell'operazione, ad esempio 200.</span><span class="sxs-lookup"><span data-stu-id="de993-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="de993-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="de993-182">callerIpAddress</span></span> |<span data-ttu-id="de993-183">String</span><span class="sxs-lookup"><span data-stu-id="de993-183">String</span></span> |<span data-ttu-id="de993-184">L’indirizzo IP del client che esegue la richiesta</span><span class="sxs-lookup"><span data-stu-id="de993-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="de993-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="de993-185">correlationId</span></span> |<span data-ttu-id="de993-186">String</span><span class="sxs-lookup"><span data-stu-id="de993-186">String</span></span> |<span data-ttu-id="de993-187">L'ID del log utilizzato per raggruppare un set di voci di log correlate</span><span class="sxs-lookup"><span data-stu-id="de993-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="de993-188">identity</span><span class="sxs-lookup"><span data-stu-id="de993-188">identity</span></span> |<span data-ttu-id="de993-189">Oggetto</span><span class="sxs-lookup"><span data-stu-id="de993-189">Object</span></span> |<span data-ttu-id="de993-190">L'identità che ha generato il log</span><span class="sxs-lookup"><span data-stu-id="de993-190">The identity that generated the log</span></span> |
| <span data-ttu-id="de993-191">properties</span><span class="sxs-lookup"><span data-stu-id="de993-191">properties</span></span> |<span data-ttu-id="de993-192">JSON</span><span class="sxs-lookup"><span data-stu-id="de993-192">JSON</span></span> |<span data-ttu-id="de993-193">Vedere di seguito per ulteriori dettagli</span><span class="sxs-lookup"><span data-stu-id="de993-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="de993-194">Schema delle proprietà del log di richiesta</span><span class="sxs-lookup"><span data-stu-id="de993-194">Request log properties schema</span></span>
| <span data-ttu-id="de993-195">Nome</span><span class="sxs-lookup"><span data-stu-id="de993-195">Name</span></span> | <span data-ttu-id="de993-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="de993-196">Type</span></span> | <span data-ttu-id="de993-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de993-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de993-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="de993-198">HttpMethod</span></span> |<span data-ttu-id="de993-199">String</span><span class="sxs-lookup"><span data-stu-id="de993-199">String</span></span> |<span data-ttu-id="de993-200">Il metodo HTTP utilizzato per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="de993-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="de993-201">Esempio: GET.</span><span class="sxs-lookup"><span data-stu-id="de993-201">For example, GET.</span></span> |
| <span data-ttu-id="de993-202">Path</span><span class="sxs-lookup"><span data-stu-id="de993-202">Path</span></span> |<span data-ttu-id="de993-203">String</span><span class="sxs-lookup"><span data-stu-id="de993-203">String</span></span> |<span data-ttu-id="de993-204">Il percorso coinvolto nell'operazione</span><span class="sxs-lookup"><span data-stu-id="de993-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="de993-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="de993-205">RequestContentLength</span></span> |<span data-ttu-id="de993-206">int</span><span class="sxs-lookup"><span data-stu-id="de993-206">int</span></span> |<span data-ttu-id="de993-207">La lunghezza del contenuto della richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="de993-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="de993-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="de993-208">ClientRequestId</span></span> |<span data-ttu-id="de993-209">String</span><span class="sxs-lookup"><span data-stu-id="de993-209">String</span></span> |<span data-ttu-id="de993-210">L’ID che identifica in modo univoco la richiesta</span><span class="sxs-lookup"><span data-stu-id="de993-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="de993-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="de993-211">StartTime</span></span> |<span data-ttu-id="de993-212">String</span><span class="sxs-lookup"><span data-stu-id="de993-212">String</span></span> |<span data-ttu-id="de993-213">L'ora in cui il server ha ricevuto la richiesta</span><span class="sxs-lookup"><span data-stu-id="de993-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="de993-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="de993-214">EndTime</span></span> |<span data-ttu-id="de993-215">String</span><span class="sxs-lookup"><span data-stu-id="de993-215">String</span></span> |<span data-ttu-id="de993-216">L'ora in cui il server ha inviato una risposta</span><span class="sxs-lookup"><span data-stu-id="de993-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="de993-217">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="de993-217">Audit logs</span></span>
<span data-ttu-id="de993-218">Di seguito viene riportata una voce di esempio nel log di controllo in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="de993-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="de993-219">Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.</span><span class="sxs-lookup"><span data-stu-id="de993-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="de993-220">Schema del log di controllo</span><span class="sxs-lookup"><span data-stu-id="de993-220">Audit log schema</span></span>
| <span data-ttu-id="de993-221">Nome</span><span class="sxs-lookup"><span data-stu-id="de993-221">Name</span></span> | <span data-ttu-id="de993-222">Tipo</span><span class="sxs-lookup"><span data-stu-id="de993-222">Type</span></span> | <span data-ttu-id="de993-223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de993-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de993-224">time</span><span class="sxs-lookup"><span data-stu-id="de993-224">time</span></span> |<span data-ttu-id="de993-225">String</span><span class="sxs-lookup"><span data-stu-id="de993-225">String</span></span> |<span data-ttu-id="de993-226">Il timestamp del log (fusorario UTC)</span><span class="sxs-lookup"><span data-stu-id="de993-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="de993-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="de993-227">resourceId</span></span> |<span data-ttu-id="de993-228">String</span><span class="sxs-lookup"><span data-stu-id="de993-228">String</span></span> |<span data-ttu-id="de993-229">L’ID della risorsa interessata dall’operazione</span><span class="sxs-lookup"><span data-stu-id="de993-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="de993-230">category</span><span class="sxs-lookup"><span data-stu-id="de993-230">category</span></span> |<span data-ttu-id="de993-231">String</span><span class="sxs-lookup"><span data-stu-id="de993-231">String</span></span> |<span data-ttu-id="de993-232">La categoria di log.</span><span class="sxs-lookup"><span data-stu-id="de993-232">The log category.</span></span> <span data-ttu-id="de993-233">Ad esempio, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="de993-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="de993-234">operationName</span><span class="sxs-lookup"><span data-stu-id="de993-234">operationName</span></span> |<span data-ttu-id="de993-235">String</span><span class="sxs-lookup"><span data-stu-id="de993-235">String</span></span> |<span data-ttu-id="de993-236">Il nome dell'operazione registrata.</span><span class="sxs-lookup"><span data-stu-id="de993-236">Name of the operation that is logged.</span></span> <span data-ttu-id="de993-237">Ad esempio, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="de993-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="de993-238">resultType</span><span class="sxs-lookup"><span data-stu-id="de993-238">resultType</span></span> |<span data-ttu-id="de993-239">String</span><span class="sxs-lookup"><span data-stu-id="de993-239">String</span></span> |<span data-ttu-id="de993-240">Lo stato dell'operazione, ad esempio 200.</span><span class="sxs-lookup"><span data-stu-id="de993-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="de993-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="de993-241">correlationId</span></span> |<span data-ttu-id="de993-242">String</span><span class="sxs-lookup"><span data-stu-id="de993-242">String</span></span> |<span data-ttu-id="de993-243">L'ID del log utilizzato per raggruppare un set di voci di log correlate</span><span class="sxs-lookup"><span data-stu-id="de993-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="de993-244">identity</span><span class="sxs-lookup"><span data-stu-id="de993-244">identity</span></span> |<span data-ttu-id="de993-245">Oggetto</span><span class="sxs-lookup"><span data-stu-id="de993-245">Object</span></span> |<span data-ttu-id="de993-246">L'identità che ha generato il log</span><span class="sxs-lookup"><span data-stu-id="de993-246">The identity that generated the log</span></span> |
| <span data-ttu-id="de993-247">properties</span><span class="sxs-lookup"><span data-stu-id="de993-247">properties</span></span> |<span data-ttu-id="de993-248">JSON</span><span class="sxs-lookup"><span data-stu-id="de993-248">JSON</span></span> |<span data-ttu-id="de993-249">Vedere di seguito per ulteriori dettagli</span><span class="sxs-lookup"><span data-stu-id="de993-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="de993-250">Schema delle proprietà del log di controllo</span><span class="sxs-lookup"><span data-stu-id="de993-250">Audit log properties schema</span></span>
| <span data-ttu-id="de993-251">Nome</span><span class="sxs-lookup"><span data-stu-id="de993-251">Name</span></span> | <span data-ttu-id="de993-252">Tipo</span><span class="sxs-lookup"><span data-stu-id="de993-252">Type</span></span> | <span data-ttu-id="de993-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de993-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de993-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="de993-254">StreamName</span></span> |<span data-ttu-id="de993-255">String</span><span class="sxs-lookup"><span data-stu-id="de993-255">String</span></span> |<span data-ttu-id="de993-256">Il percorso coinvolto nell'operazione</span><span class="sxs-lookup"><span data-stu-id="de993-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="de993-257">Esempi per elaborare i dati di log</span><span class="sxs-lookup"><span data-stu-id="de993-257">Samples to process the log data</span></span>
<span data-ttu-id="de993-258">Azure Data Lake Store fornisce un esempio su come elaborare e analizzare i dati di log.</span><span class="sxs-lookup"><span data-stu-id="de993-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="de993-259">È possibile trovare l'esempio all'indirizzo [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="de993-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="de993-260">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="de993-260">See also</span></span>
* [<span data-ttu-id="de993-261">Panoramica di Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="de993-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="de993-262">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="de993-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

