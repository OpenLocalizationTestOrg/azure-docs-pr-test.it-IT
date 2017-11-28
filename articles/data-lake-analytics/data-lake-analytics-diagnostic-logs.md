---
title: log di diagnostica per Azure Data Lake Analitica aaaViewing | Documenti Microsoft
description: 'Comprendere come toosetup e accesso diagnostica nei registri dati di Azure analitica Lake '
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
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="7df19-103">Accesso ai log di diagnostica per Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7df19-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="7df19-104">La registrazione diagnostica consente di itinerari di controllo di accesso ai dati toocollect.</span><span class="sxs-lookup"><span data-stu-id="7df19-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="7df19-105">Questi registri includono informazioni quali:</span><span class="sxs-lookup"><span data-stu-id="7df19-105">These logs provide information such as:</span></span>

* <span data-ttu-id="7df19-106">Un elenco di utenti che accede a dati hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="7df19-107">Frequenza hello di accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="7df19-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="7df19-108">La quantità di dati viene archiviato nell'account hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="7df19-109">Abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="7df19-109">Enable logging</span></span>

1. <span data-ttu-id="7df19-110">Accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7df19-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7df19-111">Aprire l'account Data Lake Analitica e selezionare **log di diagnostica** da hello __monitoraggio__ sezione.</span><span class="sxs-lookup"><span data-stu-id="7df19-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="7df19-112">Selezionare quindi __Turn on diagnostics__ (Attiva diagnostica).</span><span class="sxs-lookup"><span data-stu-id="7df19-112">Next, select __Turn on diagnostics__.</span></span>

    ![Attivare la diagnostica toocollect audit e registri di richieste](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="7df19-114">Da __le impostazioni di diagnostica__, impostare too__On__ stato hello e selezionare le opzioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="7df19-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="7df19-115">![Attivare la diagnostica toocollect audit e registri di richieste](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "abilitare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="7df19-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="7df19-116">Impostare **stato** troppo**su** tooenable la registrazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="7df19-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="7df19-117">È possibile scegliere i dati hello toostore o il processo in tre modi diversi.</span><span class="sxs-lookup"><span data-stu-id="7df19-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="7df19-118">Selezionare __archiviare l'account di archiviazione tooa__ toostore registra in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7df19-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="7df19-119">Utilizzare questa opzione se si desidera tooarchive hello dati.</span><span class="sxs-lookup"><span data-stu-id="7df19-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="7df19-120">Se si seleziona questa opzione, è necessario fornire un log hello toosave dell'account di archiviazione di Azure per.</span><span class="sxs-lookup"><span data-stu-id="7df19-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="7df19-121">Selezionare **tooan Hub eventi del flusso** toostream log dati tooan Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="7df19-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="7df19-122">Usare questa opzione se si ha una pipeline di elaborazione downstream che analizza in tempo reale i log in ingresso.</span><span class="sxs-lookup"><span data-stu-id="7df19-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="7df19-123">Se si seleziona questa opzione, è necessario specificare i dettagli di hello per hello desiderato toouse Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="7df19-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="7df19-124">Selezionare __inviare tooLog Analitica__ toosend hello dati toohello servizio Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="7df19-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="7df19-125">Utilizzare questa opzione se si desidera toouse Analitica Log toogather e analizzare i log.</span><span class="sxs-lookup"><span data-stu-id="7df19-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="7df19-126">Specificare se si desidera tooget i log di controllo e/o i log delle richieste.</span><span class="sxs-lookup"><span data-stu-id="7df19-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="7df19-127">Un log delle richieste acquisisce tutte le richieste API.</span><span class="sxs-lookup"><span data-stu-id="7df19-127">A request log captures every API request.</span></span> <span data-ttu-id="7df19-128">Un log di controllo registra tutte le operazioni attivate dalla richiesta dell'API.</span><span class="sxs-lookup"><span data-stu-id="7df19-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="7df19-129">Per __archiviare l'account di archiviazione tooa__, specificare il numero di hello di dati di hello tooretain giorni.</span><span class="sxs-lookup"><span data-stu-id="7df19-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="7df19-130">Fare clic su __Salva__.</span><span class="sxs-lookup"><span data-stu-id="7df19-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="7df19-131">È necessario selezionare una __archiviare l'account di archiviazione tooa__, __tooan Hub eventi del flusso__ o __inviare tooLog Analitica__ prima di scegliere hello __salvare__pulsante.</span><span class="sxs-lookup"><span data-stu-id="7df19-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="7df19-132">Dopo aver attivato le impostazioni di diagnostica, è possibile restituire toohello __log di diagnostica__ pannello tooview hello registri.</span><span class="sxs-lookup"><span data-stu-id="7df19-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="7df19-133">Visualizzare i log</span><span class="sxs-lookup"><span data-stu-id="7df19-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="7df19-134">Utilizzare la visualizzazione di dati Lake Analitica hello</span><span class="sxs-lookup"><span data-stu-id="7df19-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="7df19-135">Da Analitica di Lake i dati dell'account pannello in **monitoraggio**selezionare **i log di diagnostica** e quindi selezionare i registri toodisplay una voce per.</span><span class="sxs-lookup"><span data-stu-id="7df19-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="7df19-136">![Visualizzare la registrazione diagnostica](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Visualizzare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="7df19-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="7df19-137">Hello registri sono organizzati per **i log di controllo** e **log delle richieste**.</span><span class="sxs-lookup"><span data-stu-id="7df19-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![Voci del log](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="7df19-139">I log delle richieste di acquisire tutte le richieste API inviate su hello account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="7df19-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="7df19-140">I log di controllo sono registri toorequest simile, ma forniscono una suddivisione di operazioni di hello molto più dettagliata.</span><span class="sxs-lookup"><span data-stu-id="7df19-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="7df19-141">Ad esempio, una singola chiamata API di caricamento in un log delle richieste può restituire più operazioni di aggiunta nel log di controllo.</span><span class="sxs-lookup"><span data-stu-id="7df19-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="7df19-142">Fare clic su hello **scaricare** collegamento per un toodownload voce di log che di log.</span><span class="sxs-lookup"><span data-stu-id="7df19-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="7df19-143">Utilizzare account di archiviazione Azure hello che contiene i dati di log</span><span class="sxs-lookup"><span data-stu-id="7df19-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="7df19-144">Aprire Pannello di account di archiviazione di Azure hello associata a dati Lake Analitica per la registrazione e quindi fare clic su __BLOB__.</span><span class="sxs-lookup"><span data-stu-id="7df19-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="7df19-145">Hello **servizio Blob** blade sono elencati due contenitori.</span><span class="sxs-lookup"><span data-stu-id="7df19-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="7df19-146">![Visualizzare la registrazione diagnostica](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Visualizzare i log di diagnostica")</span><span class="sxs-lookup"><span data-stu-id="7df19-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="7df19-147">contenitore Hello **insights-log-controllo** contiene i log di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="7df19-148">contenitore Hello **insights-log-richieste** contiene i log delle richieste hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="7df19-149">All'interno di questi contenitori, hello sono memorizzate in hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="7df19-149">Within these containers, hello logs are stored under hello following structure:</span></span>

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
   > <span data-ttu-id="7df19-150">Hello `##` voci presenti nel percorso hello contengono hello anno, mese, giorno e ora in cui hello log è stato creato.</span><span class="sxs-lookup"><span data-stu-id="7df19-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="7df19-151">Data Lake Analytics crea un file ogni ora, in modo `m=` contenga sempre un valore di `00`.</span><span class="sxs-lookup"><span data-stu-id="7df19-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="7df19-152">Ad esempio, potrebbe essere log di controllo tooan hello percorso completo:</span><span class="sxs-lookup"><span data-stu-id="7df19-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="7df19-153">Analogamente, log delle richieste tooa hello percorso completo può essere:</span><span class="sxs-lookup"><span data-stu-id="7df19-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="7df19-154">Struttura di log</span><span class="sxs-lookup"><span data-stu-id="7df19-154">Log structure</span></span>

<span data-ttu-id="7df19-155">Hello registri di controllo e di richiesta sono in formato JSON strutturato.</span><span class="sxs-lookup"><span data-stu-id="7df19-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="7df19-156">Request Logs</span><span class="sxs-lookup"><span data-stu-id="7df19-156">Request logs</span></span>

<span data-ttu-id="7df19-157">Di seguito è una voce di esempio nel registro eventi di richiesta in formato JSON hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="7df19-158">Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.</span><span class="sxs-lookup"><span data-stu-id="7df19-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="request-log-schema"></a><span data-ttu-id="7df19-159">Schema del log delle richieste</span><span class="sxs-lookup"><span data-stu-id="7df19-159">Request log schema</span></span>

| <span data-ttu-id="7df19-160">Nome</span><span class="sxs-lookup"><span data-stu-id="7df19-160">Name</span></span> | <span data-ttu-id="7df19-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="7df19-161">Type</span></span> | <span data-ttu-id="7df19-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7df19-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7df19-163">time</span><span class="sxs-lookup"><span data-stu-id="7df19-163">time</span></span> |<span data-ttu-id="7df19-164">String</span><span class="sxs-lookup"><span data-stu-id="7df19-164">String</span></span> |<span data-ttu-id="7df19-165">timestamp (in UTC) del log hello Hello</span><span class="sxs-lookup"><span data-stu-id="7df19-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="7df19-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="7df19-166">resourceId</span></span> |<span data-ttu-id="7df19-167">String</span><span class="sxs-lookup"><span data-stu-id="7df19-167">String</span></span> |<span data-ttu-id="7df19-168">Identificatore Hello della risorsa hello che ha richiesto l'operazione Inserisci in</span><span class="sxs-lookup"><span data-stu-id="7df19-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="7df19-169">category</span><span class="sxs-lookup"><span data-stu-id="7df19-169">category</span></span> |<span data-ttu-id="7df19-170">String</span><span class="sxs-lookup"><span data-stu-id="7df19-170">String</span></span> |<span data-ttu-id="7df19-171">categoria di log Hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-171">hello log category.</span></span> <span data-ttu-id="7df19-172">Ad esempio, **Richieste**.</span><span class="sxs-lookup"><span data-stu-id="7df19-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="7df19-173">operationName</span><span class="sxs-lookup"><span data-stu-id="7df19-173">operationName</span></span> |<span data-ttu-id="7df19-174">String</span><span class="sxs-lookup"><span data-stu-id="7df19-174">String</span></span> |<span data-ttu-id="7df19-175">Nome dell'operazione di hello che viene registrato.</span><span class="sxs-lookup"><span data-stu-id="7df19-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="7df19-176">Ad esempio, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="7df19-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="7df19-177">resultType</span><span class="sxs-lookup"><span data-stu-id="7df19-177">resultType</span></span> |<span data-ttu-id="7df19-178">String</span><span class="sxs-lookup"><span data-stu-id="7df19-178">String</span></span> |<span data-ttu-id="7df19-179">stato di Hello dell'operazione di hello, ad esempio 200.</span><span class="sxs-lookup"><span data-stu-id="7df19-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="7df19-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="7df19-180">callerIpAddress</span></span> |<span data-ttu-id="7df19-181">String</span><span class="sxs-lookup"><span data-stu-id="7df19-181">String</span></span> |<span data-ttu-id="7df19-182">indirizzo IP Hello del client hello hello richiesta</span><span class="sxs-lookup"><span data-stu-id="7df19-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="7df19-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="7df19-183">correlationId</span></span> |<span data-ttu-id="7df19-184">String</span><span class="sxs-lookup"><span data-stu-id="7df19-184">String</span></span> |<span data-ttu-id="7df19-185">Identificatore Hello del log hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-185">hello identifier of hello log.</span></span> <span data-ttu-id="7df19-186">Questo valore può essere utilizzato toogroup un set di voci di log correlate.</span><span class="sxs-lookup"><span data-stu-id="7df19-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="7df19-187">identity</span><span class="sxs-lookup"><span data-stu-id="7df19-187">identity</span></span> |<span data-ttu-id="7df19-188">Oggetto</span><span class="sxs-lookup"><span data-stu-id="7df19-188">Object</span></span> |<span data-ttu-id="7df19-189">identità Hello che ha generato il log di hello</span><span class="sxs-lookup"><span data-stu-id="7df19-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="7df19-190">properties</span><span class="sxs-lookup"><span data-stu-id="7df19-190">properties</span></span> |<span data-ttu-id="7df19-191">JSON</span><span class="sxs-lookup"><span data-stu-id="7df19-191">JSON</span></span> |<span data-ttu-id="7df19-192">Nella sezione hello successivo (schema di proprietà del Registro di richiesta) per informazioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="7df19-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="7df19-193">Schema delle proprietà del log di richiesta</span><span class="sxs-lookup"><span data-stu-id="7df19-193">Request log properties schema</span></span>

| <span data-ttu-id="7df19-194">Nome</span><span class="sxs-lookup"><span data-stu-id="7df19-194">Name</span></span> | <span data-ttu-id="7df19-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="7df19-195">Type</span></span> | <span data-ttu-id="7df19-196">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7df19-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7df19-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="7df19-197">HttpMethod</span></span> |<span data-ttu-id="7df19-198">String</span><span class="sxs-lookup"><span data-stu-id="7df19-198">String</span></span> |<span data-ttu-id="7df19-199">Hello metodo HTTP utilizzato per l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="7df19-200">Esempio: GET.</span><span class="sxs-lookup"><span data-stu-id="7df19-200">For example, GET.</span></span> |
| <span data-ttu-id="7df19-201">Path</span><span class="sxs-lookup"><span data-stu-id="7df19-201">Path</span></span> |<span data-ttu-id="7df19-202">String</span><span class="sxs-lookup"><span data-stu-id="7df19-202">String</span></span> |<span data-ttu-id="7df19-203">è stata eseguita un'operazione di hello percorso Hello in</span><span class="sxs-lookup"><span data-stu-id="7df19-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="7df19-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="7df19-204">RequestContentLength</span></span> |<span data-ttu-id="7df19-205">int</span><span class="sxs-lookup"><span data-stu-id="7df19-205">int</span></span> |<span data-ttu-id="7df19-206">lunghezza del contenuto della richiesta HTTP hello Hello</span><span class="sxs-lookup"><span data-stu-id="7df19-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="7df19-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="7df19-207">ClientRequestId</span></span> |<span data-ttu-id="7df19-208">String</span><span class="sxs-lookup"><span data-stu-id="7df19-208">String</span></span> |<span data-ttu-id="7df19-209">Identificatore Hello che identifica in modo univoco questa richiesta</span><span class="sxs-lookup"><span data-stu-id="7df19-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="7df19-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="7df19-210">StartTime</span></span> |<span data-ttu-id="7df19-211">String</span><span class="sxs-lookup"><span data-stu-id="7df19-211">String</span></span> |<span data-ttu-id="7df19-212">ora di Hello in quale richiesta di hello hello server ricevuto</span><span class="sxs-lookup"><span data-stu-id="7df19-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="7df19-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="7df19-213">EndTime</span></span> |<span data-ttu-id="7df19-214">String</span><span class="sxs-lookup"><span data-stu-id="7df19-214">String</span></span> |<span data-ttu-id="7df19-215">ora di Hello in cui hello server inviato una risposta</span><span class="sxs-lookup"><span data-stu-id="7df19-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="7df19-216">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="7df19-216">Audit logs</span></span>

<span data-ttu-id="7df19-217">Di seguito è una voce di esempio nel log di controllo in formato JSON di hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="7df19-218">Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.</span><span class="sxs-lookup"><span data-stu-id="7df19-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="audit-log-schema"></a><span data-ttu-id="7df19-219">Schema del log di controllo</span><span class="sxs-lookup"><span data-stu-id="7df19-219">Audit log schema</span></span>

| <span data-ttu-id="7df19-220">Nome</span><span class="sxs-lookup"><span data-stu-id="7df19-220">Name</span></span> | <span data-ttu-id="7df19-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="7df19-221">Type</span></span> | <span data-ttu-id="7df19-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7df19-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7df19-223">time</span><span class="sxs-lookup"><span data-stu-id="7df19-223">time</span></span> |<span data-ttu-id="7df19-224">String</span><span class="sxs-lookup"><span data-stu-id="7df19-224">String</span></span> |<span data-ttu-id="7df19-225">timestamp (in UTC) del log hello Hello</span><span class="sxs-lookup"><span data-stu-id="7df19-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="7df19-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="7df19-226">resourceId</span></span> |<span data-ttu-id="7df19-227">String</span><span class="sxs-lookup"><span data-stu-id="7df19-227">String</span></span> |<span data-ttu-id="7df19-228">Identificatore Hello della risorsa hello che ha richiesto l'operazione Inserisci in</span><span class="sxs-lookup"><span data-stu-id="7df19-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="7df19-229">category</span><span class="sxs-lookup"><span data-stu-id="7df19-229">category</span></span> |<span data-ttu-id="7df19-230">String</span><span class="sxs-lookup"><span data-stu-id="7df19-230">String</span></span> |<span data-ttu-id="7df19-231">categoria di log Hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-231">hello log category.</span></span> <span data-ttu-id="7df19-232">Ad esempio, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="7df19-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="7df19-233">operationName</span><span class="sxs-lookup"><span data-stu-id="7df19-233">operationName</span></span> |<span data-ttu-id="7df19-234">String</span><span class="sxs-lookup"><span data-stu-id="7df19-234">String</span></span> |<span data-ttu-id="7df19-235">Nome dell'operazione di hello che viene registrato.</span><span class="sxs-lookup"><span data-stu-id="7df19-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="7df19-236">Ad esempio, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="7df19-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="7df19-237">resultType</span><span class="sxs-lookup"><span data-stu-id="7df19-237">resultType</span></span> |<span data-ttu-id="7df19-238">String</span><span class="sxs-lookup"><span data-stu-id="7df19-238">String</span></span> |<span data-ttu-id="7df19-239">Uno stato secondario per lo stato del processo hello (operationName).</span><span class="sxs-lookup"><span data-stu-id="7df19-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="7df19-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="7df19-240">resultSignature</span></span> |<span data-ttu-id="7df19-241">String</span><span class="sxs-lookup"><span data-stu-id="7df19-241">String</span></span> |<span data-ttu-id="7df19-242">Dettagli aggiuntivi sullo stato del processo hello (operationName).</span><span class="sxs-lookup"><span data-stu-id="7df19-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="7df19-243">identity</span><span class="sxs-lookup"><span data-stu-id="7df19-243">identity</span></span> |<span data-ttu-id="7df19-244">String</span><span class="sxs-lookup"><span data-stu-id="7df19-244">String</span></span> |<span data-ttu-id="7df19-245">utente Hello che ha richiesto l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-245">hello user that requested hello operation.</span></span> <span data-ttu-id="7df19-246">ad esempio susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7df19-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="7df19-247">properties</span><span class="sxs-lookup"><span data-stu-id="7df19-247">properties</span></span> |<span data-ttu-id="7df19-248">JSON</span><span class="sxs-lookup"><span data-stu-id="7df19-248">JSON</span></span> |<span data-ttu-id="7df19-249">Nella sezione hello successivo (schema di proprietà del Registro di controllo) per informazioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="7df19-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="7df19-250">**elemento resultType** e **resultSignature** forniscono informazioni sul risultato di hello di un'operazione e contenere solo un valore se un'operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="7df19-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="7df19-251">Ad esempio, contengono un valore solo quando **operationName** contiene un valore **JobStarted** o **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="7df19-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="7df19-252">Schema delle proprietà del log di controllo</span><span class="sxs-lookup"><span data-stu-id="7df19-252">Audit log properties schema</span></span>

| <span data-ttu-id="7df19-253">Nome</span><span class="sxs-lookup"><span data-stu-id="7df19-253">Name</span></span> | <span data-ttu-id="7df19-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="7df19-254">Type</span></span> | <span data-ttu-id="7df19-255">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7df19-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7df19-256">JobId</span><span class="sxs-lookup"><span data-stu-id="7df19-256">JobId</span></span> |<span data-ttu-id="7df19-257">String</span><span class="sxs-lookup"><span data-stu-id="7df19-257">String</span></span> |<span data-ttu-id="7df19-258">processo di Hello ID assegnato toohello</span><span class="sxs-lookup"><span data-stu-id="7df19-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="7df19-259">JobName</span><span class="sxs-lookup"><span data-stu-id="7df19-259">JobName</span></span> |<span data-ttu-id="7df19-260">String</span><span class="sxs-lookup"><span data-stu-id="7df19-260">String</span></span> |<span data-ttu-id="7df19-261">nome fornito per il processo di hello Hello</span><span class="sxs-lookup"><span data-stu-id="7df19-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="7df19-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="7df19-262">JobRunTime</span></span> |<span data-ttu-id="7df19-263">String</span><span class="sxs-lookup"><span data-stu-id="7df19-263">String</span></span> |<span data-ttu-id="7df19-264">runtime di Hello utilizzato processo hello tooprocess</span><span class="sxs-lookup"><span data-stu-id="7df19-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="7df19-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="7df19-265">SubmitTime</span></span> |<span data-ttu-id="7df19-266">String</span><span class="sxs-lookup"><span data-stu-id="7df19-266">String</span></span> |<span data-ttu-id="7df19-267">tempo di Hello (in UTC) che il processo di hello è stato inviato</span><span class="sxs-lookup"><span data-stu-id="7df19-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="7df19-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="7df19-268">StartTime</span></span> |<span data-ttu-id="7df19-269">String</span><span class="sxs-lookup"><span data-stu-id="7df19-269">String</span></span> |<span data-ttu-id="7df19-270">processo di hello ora Hello avviato dopo l'invio (in UTC)</span><span class="sxs-lookup"><span data-stu-id="7df19-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="7df19-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="7df19-271">EndTime</span></span> |<span data-ttu-id="7df19-272">String</span><span class="sxs-lookup"><span data-stu-id="7df19-272">String</span></span> |<span data-ttu-id="7df19-273">Hello ora hello processo terminato</span><span class="sxs-lookup"><span data-stu-id="7df19-273">hello time hello job ended</span></span> |
| <span data-ttu-id="7df19-274">Parallelismo</span><span class="sxs-lookup"><span data-stu-id="7df19-274">Parallelism</span></span> |<span data-ttu-id="7df19-275">String</span><span class="sxs-lookup"><span data-stu-id="7df19-275">String</span></span> |<span data-ttu-id="7df19-276">numero di Hello di unità Data Lake Analitica richieste per il processo durante l'invio</span><span class="sxs-lookup"><span data-stu-id="7df19-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="7df19-277">**SubmitTime**, **StartTime**, **EndTime** e **Parallelism** forniscono informazioni su un'operazione.</span><span class="sxs-lookup"><span data-stu-id="7df19-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="7df19-278">Queste voci contengono un valore solo se l'operazione è stata avviata o completata.</span><span class="sxs-lookup"><span data-stu-id="7df19-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="7df19-279">Ad esempio, **SubmitTime** contiene solo un valore dopo **operationName** ha valore hello **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="7df19-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="7df19-280">Dati del log hello processo</span><span class="sxs-lookup"><span data-stu-id="7df19-280">Process hello log data</span></span>

<span data-ttu-id="7df19-281">Azure Data Lake Analitica viene fornito un esempio su come tooprocess e analizzare i dati di log hello.</span><span class="sxs-lookup"><span data-stu-id="7df19-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="7df19-282">È possibile trovare l'esempio hello in [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="7df19-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7df19-283">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7df19-283">Next steps</span></span>
* [<span data-ttu-id="7df19-284">Panoramica di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7df19-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
