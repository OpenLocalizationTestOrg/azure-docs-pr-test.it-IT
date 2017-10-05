---
title: Visualizzazione dei log di diagnostica per Azure Data Lake Analytics | Documentazione Microsoft
description: 'Informazioni su come configurare e accedere ai log di diagnostica per Azure Data Lake Analytics  '
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 6c74db1659742aa41306388273bec46800ba7609
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="3810a-103">Accesso ai log di diagnostica per Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3810a-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="3810a-104">La registrazione diagnostica consente di raccogliere audit trail di accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="3810a-104">Diagnostic logging allows you to collect data access audit trails.</span></span> <span data-ttu-id="3810a-105">Questi registri includono informazioni quali:</span><span class="sxs-lookup"><span data-stu-id="3810a-105">These logs provide information such as:</span></span>

* <span data-ttu-id="3810a-106">Un elenco di utenti che hanno avuto accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="3810a-106">A list of users that accessed the data.</span></span>
* <span data-ttu-id="3810a-107">La frequenza con cui si accede ai dati.</span><span class="sxs-lookup"><span data-stu-id="3810a-107">How frequently the data is accessed.</span></span>
* <span data-ttu-id="3810a-108">La quantità di dati archiviati nell'account.</span><span class="sxs-lookup"><span data-stu-id="3810a-108">How much data is stored in the account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="3810a-109">Abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="3810a-109">Enable logging</span></span>

1. <span data-ttu-id="3810a-110">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3810a-110">Sign on to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3810a-111">Aprire l'account Data Lake Analytics e selezionare **Log di diagnostica** dalla sezione __Monitoraggio__.</span><span class="sxs-lookup"><span data-stu-id="3810a-111">Open your Data Lake Analytics account and select **Diagnostic logs** from the __Monitor__ section.</span></span> <span data-ttu-id="3810a-112">Selezionare quindi __Turn on diagnostics__ (Attiva diagnostica).</span><span class="sxs-lookup"><span data-stu-id="3810a-112">Next, select __Turn on diagnostics__.</span></span>

    ![Attivare la diagnostica per acquisire i log di controllo e i log delle richieste.](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="3810a-114">Dalle __Impostazioni di diagnostica__, impostare lo stato su __Attivo__ e selezionare le opzioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="3810a-114">From __Diagnostics settings__, set the status to __On__ and select logging options.</span></span>

    <span data-ttu-id="3810a-115">![Attivare la diagnostica per acquisire i log di controllo e i log delle richieste](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Abilitare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="3810a-115">![Turn on diagnostics to collect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="3810a-116">Impostare lo **Stato** su **Attivo** per abilitare la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="3810a-116">Set **Status** to **On** to enable diagnostic logging.</span></span>

   * <span data-ttu-id="3810a-117">È possibile scegliere di archiviare/elaborare i dati in tre modi diversi.</span><span class="sxs-lookup"><span data-stu-id="3810a-117">You can choose to store/process the data in three different ways.</span></span>

     * <span data-ttu-id="3810a-118">Selezionare __Archive to a storage account__ (Archivia in un account di archiviazione) per archiviare i log in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3810a-118">Select __Archive to a storage account__ to store logs in an Azure storage account.</span></span> <span data-ttu-id="3810a-119">Usare questa opzione se si vogliono archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="3810a-119">Use this option if you want to archive the data.</span></span> <span data-ttu-id="3810a-120">Se si seleziona questa opzione è necessario fornire un account di archiviazione di Azure in cui salvare i log.</span><span class="sxs-lookup"><span data-stu-id="3810a-120">If you select this option, you must provide an Azure storage account to save the logs to.</span></span>

     * <span data-ttu-id="3810a-121">Selezionare **Stream to an Event Hub** (Esegui streaming in un Hub eventi) per trasmettere i dati di log a un Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="3810a-121">Select **Stream to an Event Hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="3810a-122">Usare questa opzione se si ha una pipeline di elaborazione downstream che analizza in tempo reale i log in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3810a-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="3810a-123">Se si seleziona questa opzione, è necessario fornire i dettagli dell'Hub eventi di Azure che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="3810a-123">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

     * <span data-ttu-id="3810a-124">Selezionare __Send to Log Analytics__ (Invia a Log Analytics) per inviare i dati al servizio Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3810a-124">Select __Send to Log Analytics__ to send the data to the Log Analytics service.</span></span> <span data-ttu-id="3810a-125">Usare questa opzione per raccogliere e analizzare i log con Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3810a-125">Use this option if you want to use Log Analytics to gather and analyze logs.</span></span>
   * <span data-ttu-id="3810a-126">Specificare se si desidera ottenere i log di controllo, i log delle richieste o entrambi.</span><span class="sxs-lookup"><span data-stu-id="3810a-126">Specify whether you want to get audit logs or request logs or both.</span></span>  <span data-ttu-id="3810a-127">Un log delle richieste acquisisce tutte le richieste API.</span><span class="sxs-lookup"><span data-stu-id="3810a-127">A request log captures every API request.</span></span> <span data-ttu-id="3810a-128">Un log di controllo registra tutte le operazioni attivate dalla richiesta dell'API.</span><span class="sxs-lookup"><span data-stu-id="3810a-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="3810a-129">Per __Archivia in un account di archiviazione__ specificare il numero di giorni per cui i dati verranno conservati.</span><span class="sxs-lookup"><span data-stu-id="3810a-129">For __Archive to a storage account__, specify the number of days to retain the data.</span></span>

   * <span data-ttu-id="3810a-130">Fare clic su __Salva__.</span><span class="sxs-lookup"><span data-stu-id="3810a-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="3810a-131">È necessario selezionare una tra le opzioni __Archivia in un account di archiviazione__, __Streaming in un hub eventi__ o __Invia a Log Analytics__ prima di fare clic sul pulsante __Salva__.</span><span class="sxs-lookup"><span data-stu-id="3810a-131">You must select either __Archive to a storage account__, __Stream to an Event Hub__ or __Send to Log Analytics__ before clicking the __Save__ button.</span></span>

<span data-ttu-id="3810a-132">Dopo avere abilitato le impostazioni di diagnostica, è possibile tornare al pannello __Log di diagnostica__ per visualizzare i log.</span><span class="sxs-lookup"><span data-stu-id="3810a-132">Once you have enabled diagnostic settings, you can return to the __Diagnostics logs__ blade to view the logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="3810a-133">Visualizzare i log</span><span class="sxs-lookup"><span data-stu-id="3810a-133">View logs</span></span>

### <a name="use-the-data-lake-analytics-view"></a><span data-ttu-id="3810a-134">Usare la visualizzazione di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3810a-134">Use the Data Lake Analytics view</span></span>

1. <span data-ttu-id="3810a-135">Dal pannello dell'account Data Lake Analytics selezionare **Log di diagnostica** in **Monitoraggio** e quindi selezionare una voce per la quale visualizzare i log.</span><span class="sxs-lookup"><span data-stu-id="3810a-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry to display logs for.</span></span>

    <span data-ttu-id="3810a-136">![Visualizzare la registrazione diagnostica](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Visualizzare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="3810a-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="3810a-137">I log sono suddivisi in **Log di controllo** e **Log delle richieste**.</span><span class="sxs-lookup"><span data-stu-id="3810a-137">The logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![Voci del log](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="3810a-139">I log delle richieste acquisiscono tutte le richieste API fatte nell'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3810a-139">Request logs capture every API request made on the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="3810a-140">I log di controllo sono simili a quelli delle richieste ma forniscono una suddivisione più dettagliata delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="3810a-140">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations.</span></span> <span data-ttu-id="3810a-141">Ad esempio, una singola chiamata API di caricamento in un log delle richieste può restituire più operazioni di aggiunta nel log di controllo.</span><span class="sxs-lookup"><span data-stu-id="3810a-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="3810a-142">Fare clic sul collegamento **Scarica** di una voce di log per scaricare il log.</span><span class="sxs-lookup"><span data-stu-id="3810a-142">Click the **Download** link for a log entry to download that log.</span></span>

### <a name="use-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="3810a-143">Usare l'account di archiviazione di Azure contenente i dati di log</span><span class="sxs-lookup"><span data-stu-id="3810a-143">Use the Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="3810a-144">Aprire il pannello dell'account di archiviazione di Azure associato a Data Lake Analytics per la registrazione e quindi fare clic su __BLOB__.</span><span class="sxs-lookup"><span data-stu-id="3810a-144">Open the Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="3810a-145">Il pannello **Servizio BLOB** elenca due contenitori.</span><span class="sxs-lookup"><span data-stu-id="3810a-145">The **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="3810a-146">![Visualizzare la registrazione diagnostica](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Visualizzare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="3810a-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="3810a-147">Il contenitore **insights-logs-audit** contiene i log di controllo.</span><span class="sxs-lookup"><span data-stu-id="3810a-147">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="3810a-148">Il contenitore **insights-logs-requests** contiene i log delle richieste.</span><span class="sxs-lookup"><span data-stu-id="3810a-148">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="3810a-149">All'interno di questi contenitori i log vengono archiviati con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="3810a-149">Within these containers, the logs are stored under the following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="3810a-150">Il pannello `##` nel percorso contengono l'anno, il mese, il giorno e l'ora in cui è stato creato il log.</span><span class="sxs-lookup"><span data-stu-id="3810a-150">The `##` entries in the path contain the year, month, day, and hour in which the log was created.</span></span> <span data-ttu-id="3810a-151">Data Lake Analytics crea un file ogni ora, in modo `m=` contenga sempre un valore di `00`.</span><span class="sxs-lookup"><span data-stu-id="3810a-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="3810a-152">Ad esempio, il percorso completo a un log di controllo potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="3810a-152">As an example, the complete path to an audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="3810a-153">Analogamente, il percorso completo a un log della richiesta potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="3810a-153">Similarly, the complete path to a request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="3810a-154">Struttura di log</span><span class="sxs-lookup"><span data-stu-id="3810a-154">Log structure</span></span>

<span data-ttu-id="3810a-155">I log di controllo e delle richieste sono in formato JSON strutturato.</span><span class="sxs-lookup"><span data-stu-id="3810a-155">The audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="3810a-156">Request Logs</span><span class="sxs-lookup"><span data-stu-id="3810a-156">Request logs</span></span>

<span data-ttu-id="3810a-157">Di seguito viene riportata una voce di esempio nel log delle richieste in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3810a-157">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="3810a-158">Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.</span><span class="sxs-lookup"><span data-stu-id="3810a-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="3810a-159">Schema del log delle richieste</span><span class="sxs-lookup"><span data-stu-id="3810a-159">Request log schema</span></span>

| <span data-ttu-id="3810a-160">Nome</span><span class="sxs-lookup"><span data-stu-id="3810a-160">Name</span></span> | <span data-ttu-id="3810a-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="3810a-161">Type</span></span> | <span data-ttu-id="3810a-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3810a-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3810a-163">time</span><span class="sxs-lookup"><span data-stu-id="3810a-163">time</span></span> |<span data-ttu-id="3810a-164">String</span><span class="sxs-lookup"><span data-stu-id="3810a-164">String</span></span> |<span data-ttu-id="3810a-165">Il timestamp del log (fusorario UTC)</span><span class="sxs-lookup"><span data-stu-id="3810a-165">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="3810a-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="3810a-166">resourceId</span></span> |<span data-ttu-id="3810a-167">String</span><span class="sxs-lookup"><span data-stu-id="3810a-167">String</span></span> |<span data-ttu-id="3810a-168">Identificatore della risorsa interessata dall'operazione</span><span class="sxs-lookup"><span data-stu-id="3810a-168">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="3810a-169">category</span><span class="sxs-lookup"><span data-stu-id="3810a-169">category</span></span> |<span data-ttu-id="3810a-170">String</span><span class="sxs-lookup"><span data-stu-id="3810a-170">String</span></span> |<span data-ttu-id="3810a-171">La categoria di log.</span><span class="sxs-lookup"><span data-stu-id="3810a-171">The log category.</span></span> <span data-ttu-id="3810a-172">Ad esempio, **Richieste**.</span><span class="sxs-lookup"><span data-stu-id="3810a-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="3810a-173">operationName</span><span class="sxs-lookup"><span data-stu-id="3810a-173">operationName</span></span> |<span data-ttu-id="3810a-174">String</span><span class="sxs-lookup"><span data-stu-id="3810a-174">String</span></span> |<span data-ttu-id="3810a-175">Il nome dell'operazione registrata.</span><span class="sxs-lookup"><span data-stu-id="3810a-175">Name of the operation that is logged.</span></span> <span data-ttu-id="3810a-176">Ad esempio, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="3810a-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="3810a-177">resultType</span><span class="sxs-lookup"><span data-stu-id="3810a-177">resultType</span></span> |<span data-ttu-id="3810a-178">String</span><span class="sxs-lookup"><span data-stu-id="3810a-178">String</span></span> |<span data-ttu-id="3810a-179">Lo stato dell'operazione, ad esempio 200.</span><span class="sxs-lookup"><span data-stu-id="3810a-179">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="3810a-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="3810a-180">callerIpAddress</span></span> |<span data-ttu-id="3810a-181">String</span><span class="sxs-lookup"><span data-stu-id="3810a-181">String</span></span> |<span data-ttu-id="3810a-182">L’indirizzo IP del client che esegue la richiesta</span><span class="sxs-lookup"><span data-stu-id="3810a-182">The IP address of the client making the request</span></span> |
| <span data-ttu-id="3810a-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="3810a-183">correlationId</span></span> |<span data-ttu-id="3810a-184">String</span><span class="sxs-lookup"><span data-stu-id="3810a-184">String</span></span> |<span data-ttu-id="3810a-185">Identificatore del log.</span><span class="sxs-lookup"><span data-stu-id="3810a-185">The identifier of the log.</span></span> <span data-ttu-id="3810a-186">Questo valore può essere usato per raggruppare un set di voci di log correlate.</span><span class="sxs-lookup"><span data-stu-id="3810a-186">This value can be used to group a set of related log entries.</span></span> |
| <span data-ttu-id="3810a-187">identity</span><span class="sxs-lookup"><span data-stu-id="3810a-187">identity</span></span> |<span data-ttu-id="3810a-188">Oggetto</span><span class="sxs-lookup"><span data-stu-id="3810a-188">Object</span></span> |<span data-ttu-id="3810a-189">L'identità che ha generato il log</span><span class="sxs-lookup"><span data-stu-id="3810a-189">The identity that generated the log</span></span> |
| <span data-ttu-id="3810a-190">properties</span><span class="sxs-lookup"><span data-stu-id="3810a-190">properties</span></span> |<span data-ttu-id="3810a-191">JSON</span><span class="sxs-lookup"><span data-stu-id="3810a-191">JSON</span></span> |<span data-ttu-id="3810a-192">Per informazioni dettagliate, vedere la sezione successiva (Schema delle proprietà del log di richiesta)</span><span class="sxs-lookup"><span data-stu-id="3810a-192">See the next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="3810a-193">Schema delle proprietà del log di richiesta</span><span class="sxs-lookup"><span data-stu-id="3810a-193">Request log properties schema</span></span>

| <span data-ttu-id="3810a-194">Nome</span><span class="sxs-lookup"><span data-stu-id="3810a-194">Name</span></span> | <span data-ttu-id="3810a-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="3810a-195">Type</span></span> | <span data-ttu-id="3810a-196">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3810a-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3810a-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="3810a-197">HttpMethod</span></span> |<span data-ttu-id="3810a-198">String</span><span class="sxs-lookup"><span data-stu-id="3810a-198">String</span></span> |<span data-ttu-id="3810a-199">Il metodo HTTP utilizzato per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="3810a-199">The HTTP Method used for the operation.</span></span> <span data-ttu-id="3810a-200">Esempio: GET.</span><span class="sxs-lookup"><span data-stu-id="3810a-200">For example, GET.</span></span> |
| <span data-ttu-id="3810a-201">Path</span><span class="sxs-lookup"><span data-stu-id="3810a-201">Path</span></span> |<span data-ttu-id="3810a-202">String</span><span class="sxs-lookup"><span data-stu-id="3810a-202">String</span></span> |<span data-ttu-id="3810a-203">Il percorso coinvolto nell'operazione</span><span class="sxs-lookup"><span data-stu-id="3810a-203">The path the operation was performed on</span></span> |
| <span data-ttu-id="3810a-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="3810a-204">RequestContentLength</span></span> |<span data-ttu-id="3810a-205">int</span><span class="sxs-lookup"><span data-stu-id="3810a-205">int</span></span> |<span data-ttu-id="3810a-206">La lunghezza del contenuto della richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="3810a-206">The content length of the HTTP request</span></span> |
| <span data-ttu-id="3810a-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="3810a-207">ClientRequestId</span></span> |<span data-ttu-id="3810a-208">String</span><span class="sxs-lookup"><span data-stu-id="3810a-208">String</span></span> |<span data-ttu-id="3810a-209">Identificatore che identifica in modo univoco la richiesta</span><span class="sxs-lookup"><span data-stu-id="3810a-209">The identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="3810a-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="3810a-210">StartTime</span></span> |<span data-ttu-id="3810a-211">String</span><span class="sxs-lookup"><span data-stu-id="3810a-211">String</span></span> |<span data-ttu-id="3810a-212">L'ora in cui il server ha ricevuto la richiesta</span><span class="sxs-lookup"><span data-stu-id="3810a-212">The time at which the server received the request</span></span> |
| <span data-ttu-id="3810a-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="3810a-213">EndTime</span></span> |<span data-ttu-id="3810a-214">String</span><span class="sxs-lookup"><span data-stu-id="3810a-214">String</span></span> |<span data-ttu-id="3810a-215">L'ora in cui il server ha inviato una risposta</span><span class="sxs-lookup"><span data-stu-id="3810a-215">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="3810a-216">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="3810a-216">Audit logs</span></span>

<span data-ttu-id="3810a-217">Di seguito viene riportata una voce di esempio nel log di controllo in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3810a-217">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="3810a-218">Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.</span><span class="sxs-lookup"><span data-stu-id="3810a-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="3810a-219">Schema del log di controllo</span><span class="sxs-lookup"><span data-stu-id="3810a-219">Audit log schema</span></span>

| <span data-ttu-id="3810a-220">Nome</span><span class="sxs-lookup"><span data-stu-id="3810a-220">Name</span></span> | <span data-ttu-id="3810a-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="3810a-221">Type</span></span> | <span data-ttu-id="3810a-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3810a-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3810a-223">time</span><span class="sxs-lookup"><span data-stu-id="3810a-223">time</span></span> |<span data-ttu-id="3810a-224">String</span><span class="sxs-lookup"><span data-stu-id="3810a-224">String</span></span> |<span data-ttu-id="3810a-225">Il timestamp del log (fusorario UTC)</span><span class="sxs-lookup"><span data-stu-id="3810a-225">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="3810a-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="3810a-226">resourceId</span></span> |<span data-ttu-id="3810a-227">String</span><span class="sxs-lookup"><span data-stu-id="3810a-227">String</span></span> |<span data-ttu-id="3810a-228">Identificatore della risorsa interessata dall'operazione</span><span class="sxs-lookup"><span data-stu-id="3810a-228">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="3810a-229">category</span><span class="sxs-lookup"><span data-stu-id="3810a-229">category</span></span> |<span data-ttu-id="3810a-230">String</span><span class="sxs-lookup"><span data-stu-id="3810a-230">String</span></span> |<span data-ttu-id="3810a-231">La categoria di log.</span><span class="sxs-lookup"><span data-stu-id="3810a-231">The log category.</span></span> <span data-ttu-id="3810a-232">Ad esempio, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="3810a-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="3810a-233">operationName</span><span class="sxs-lookup"><span data-stu-id="3810a-233">operationName</span></span> |<span data-ttu-id="3810a-234">String</span><span class="sxs-lookup"><span data-stu-id="3810a-234">String</span></span> |<span data-ttu-id="3810a-235">Il nome dell'operazione registrata.</span><span class="sxs-lookup"><span data-stu-id="3810a-235">Name of the operation that is logged.</span></span> <span data-ttu-id="3810a-236">Ad esempio, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="3810a-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="3810a-237">resultType</span><span class="sxs-lookup"><span data-stu-id="3810a-237">resultType</span></span> |<span data-ttu-id="3810a-238">String</span><span class="sxs-lookup"><span data-stu-id="3810a-238">String</span></span> |<span data-ttu-id="3810a-239">Stato secondario per lo stato del processo (operationName).</span><span class="sxs-lookup"><span data-stu-id="3810a-239">A substatus for the job status (operationName).</span></span> |
| <span data-ttu-id="3810a-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="3810a-240">resultSignature</span></span> |<span data-ttu-id="3810a-241">String</span><span class="sxs-lookup"><span data-stu-id="3810a-241">String</span></span> |<span data-ttu-id="3810a-242">Informazioni aggiuntive sullo stato di processo (operationName).</span><span class="sxs-lookup"><span data-stu-id="3810a-242">Additional details on the job status (operationName).</span></span> |
| <span data-ttu-id="3810a-243">identity</span><span class="sxs-lookup"><span data-stu-id="3810a-243">identity</span></span> |<span data-ttu-id="3810a-244">String</span><span class="sxs-lookup"><span data-stu-id="3810a-244">String</span></span> |<span data-ttu-id="3810a-245">L'utente che ha richiesto l'operazione.</span><span class="sxs-lookup"><span data-stu-id="3810a-245">The user that requested the operation.</span></span> <span data-ttu-id="3810a-246">Ad esempio, susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3810a-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="3810a-247">properties</span><span class="sxs-lookup"><span data-stu-id="3810a-247">properties</span></span> |<span data-ttu-id="3810a-248">JSON</span><span class="sxs-lookup"><span data-stu-id="3810a-248">JSON</span></span> |<span data-ttu-id="3810a-249">Per informazioni dettagliate, vedere la sezione successiva (Schema delle proprietà del log di controllo)</span><span class="sxs-lookup"><span data-stu-id="3810a-249">See the next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="3810a-250">**resultType** e **resultSignature** offrono informazioni sul risultato di un'operazione e contengono un valore solo se un'operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="3810a-250">**resultType** and **resultSignature** provide information on the result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="3810a-251">Ad esempio, contengono un valore solo quando **operationName** contiene un valore **JobStarted** o **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="3810a-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="3810a-252">Schema delle proprietà del log di controllo</span><span class="sxs-lookup"><span data-stu-id="3810a-252">Audit log properties schema</span></span>

| <span data-ttu-id="3810a-253">Nome</span><span class="sxs-lookup"><span data-stu-id="3810a-253">Name</span></span> | <span data-ttu-id="3810a-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="3810a-254">Type</span></span> | <span data-ttu-id="3810a-255">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3810a-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3810a-256">JobId</span><span class="sxs-lookup"><span data-stu-id="3810a-256">JobId</span></span> |<span data-ttu-id="3810a-257">String</span><span class="sxs-lookup"><span data-stu-id="3810a-257">String</span></span> |<span data-ttu-id="3810a-258">L'ID assegnato al processo</span><span class="sxs-lookup"><span data-stu-id="3810a-258">The ID assigned to the job</span></span> |
| <span data-ttu-id="3810a-259">JobName</span><span class="sxs-lookup"><span data-stu-id="3810a-259">JobName</span></span> |<span data-ttu-id="3810a-260">String</span><span class="sxs-lookup"><span data-stu-id="3810a-260">String</span></span> |<span data-ttu-id="3810a-261">Il nome fornito per il processo</span><span class="sxs-lookup"><span data-stu-id="3810a-261">The name that was provided for the job</span></span> |
| <span data-ttu-id="3810a-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="3810a-262">JobRunTime</span></span> |<span data-ttu-id="3810a-263">String</span><span class="sxs-lookup"><span data-stu-id="3810a-263">String</span></span> |<span data-ttu-id="3810a-264">Il runtime usato per l'elaborazione del processo</span><span class="sxs-lookup"><span data-stu-id="3810a-264">The runtime used to process the job</span></span> |
| <span data-ttu-id="3810a-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="3810a-265">SubmitTime</span></span> |<span data-ttu-id="3810a-266">String</span><span class="sxs-lookup"><span data-stu-id="3810a-266">String</span></span> |<span data-ttu-id="3810a-267">Ora (UTC) in cui è stato inviato il processo</span><span class="sxs-lookup"><span data-stu-id="3810a-267">The time (in UTC) that the job was submitted</span></span> |
| <span data-ttu-id="3810a-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="3810a-268">StartTime</span></span> |<span data-ttu-id="3810a-269">String</span><span class="sxs-lookup"><span data-stu-id="3810a-269">String</span></span> |<span data-ttu-id="3810a-270">Ora di avvio dell'esecuzione del processo dopo l'invio (in UTC)</span><span class="sxs-lookup"><span data-stu-id="3810a-270">The time the job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="3810a-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="3810a-271">EndTime</span></span> |<span data-ttu-id="3810a-272">String</span><span class="sxs-lookup"><span data-stu-id="3810a-272">String</span></span> |<span data-ttu-id="3810a-273">Ora di fine del processo</span><span class="sxs-lookup"><span data-stu-id="3810a-273">The time the job ended</span></span> |
| <span data-ttu-id="3810a-274">Parallelismo</span><span class="sxs-lookup"><span data-stu-id="3810a-274">Parallelism</span></span> |<span data-ttu-id="3810a-275">String</span><span class="sxs-lookup"><span data-stu-id="3810a-275">String</span></span> |<span data-ttu-id="3810a-276">Numero di unità di Data Lake Analytics richieste per questo processo durante l'invio</span><span class="sxs-lookup"><span data-stu-id="3810a-276">The number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="3810a-277">**SubmitTime**, **StartTime**, **EndTime** e **Parallelism** forniscono informazioni su un'operazione.</span><span class="sxs-lookup"><span data-stu-id="3810a-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="3810a-278">Queste voci contengono un valore solo se l'operazione è stata avviata o completata.</span><span class="sxs-lookup"><span data-stu-id="3810a-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="3810a-279">Ad esempio, **SubmitTime** contiene un valore solo dopo che **operationName** ha il valore **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="3810a-279">For example, **SubmitTime** only contains a value after **operationName** has the value **JobSubmitted**.</span></span>

## <a name="process-the-log-data"></a><span data-ttu-id="3810a-280">Elaborare i dati di log</span><span class="sxs-lookup"><span data-stu-id="3810a-280">Process the log data</span></span>

<span data-ttu-id="3810a-281">Azure Data Lake Analytics fornisce un esempio su come elaborare e analizzare i dati di log.</span><span class="sxs-lookup"><span data-stu-id="3810a-281">Azure Data Lake Analytics provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="3810a-282">È possibile trovare l'esempio all'indirizzo [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="3810a-282">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3810a-283">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3810a-283">Next steps</span></span>
* [<span data-ttu-id="3810a-284">Panoramica di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3810a-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
