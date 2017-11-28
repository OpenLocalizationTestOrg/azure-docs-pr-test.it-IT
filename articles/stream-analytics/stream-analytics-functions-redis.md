---
title: l'elaborazione in tempo reale aaaStream Analitica per le funzioni di Azure | Documenti Microsoft
description: "Informazioni su modalità di connessione di una coda del Bus di servizio, una Cache Redis di Azure dall'output di hello di un processo di flusso Analitica toopopulate toouse una funzione di Azure."
keywords: flusso di dati, cache redis, coda bus di servizio
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="b9090-104">Come dati toostore Analitica di flusso di Azure in una Cache di Redis di Azure utilizzando le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b9090-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="b9090-105">Analitica di flusso di Azure consente di sviluppare e distribuire informazioni in tempo reale di soluzioni a basso costo toogain da dispositivi, sensori, infrastruttura e le applicazioni o qualsiasi flusso di dati rapidamente.</span><span class="sxs-lookup"><span data-stu-id="b9090-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="b9090-106">Ciò consente vari casi di utilizzo, tra cui: monitoraggio e gestione in tempo reale, comando e controllo, rilevamento di frodi, automobili connesse e molti altri.</span><span class="sxs-lookup"><span data-stu-id="b9090-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="b9090-107">In molti scenari, è consigliabile toostore dati restituiti da Azure Analitica di flusso in un archivio dati distribuiti, ad esempio una cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9090-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="b9090-108">Immaginare di far parte di una società di telecomunicazioni.</span><span class="sxs-lookup"><span data-stu-id="b9090-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="b9090-109">Si sta tentando di frode SIM toodetect in più chiamate provenienti da hello stessa identità, in hello stesso tempo, ma in diverse località geografiche percorsi.</span><span class="sxs-lookup"><span data-stu-id="b9090-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="b9090-110">Si desidera archiviare tutti hello potenzialmente illecite telefonate in una cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9090-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="b9090-111">In questo blog, vengono fornite le indicazioni su come è possibile completare tale operazione.</span><span class="sxs-lookup"><span data-stu-id="b9090-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b9090-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b9090-112">Prerequisites</span></span>
<span data-ttu-id="b9090-113">Hello completo [in tempo reale la rilevazione di frodi] [ fraud-detection] procedura dettagliata per ASA</span><span class="sxs-lookup"><span data-stu-id="b9090-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="b9090-114">Panoramica dell'architettura</span><span class="sxs-lookup"><span data-stu-id="b9090-114">Architecture Overview</span></span>
![Schermata dell'architettura](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="b9090-116">Come illustrato nella figura precedente hello, Analitica di flusso consente il flusso di dati di input toobe eseguire una query e inviati tooan output.</span><span class="sxs-lookup"><span data-stu-id="b9090-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="b9090-117">Basati sull'output di hello, funzioni di Azure può quindi attivare un tipo di evento.</span><span class="sxs-lookup"><span data-stu-id="b9090-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="b9090-118">In questo blog, è lo stato attivo sulla parte di Azure funzioni hello della pipeline o hello in particolare l'attivazione di un evento che archivia i dati fraudolenti nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="b9090-119">Dopo aver completato hello [in tempo reale la rilevazione di frodi] [ fraud-detection] esercitazione, è un input (un hub di eventi), una query e un output (archiviazione blob) già configurato e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b9090-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="b9090-120">In questo blog, abbiamo modificare hello output toouse una coda del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="b9090-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="b9090-121">Successivamente, la connessione è una coda di toothis della funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9090-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="b9090-122">Creare e collegare un output della coda di del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="b9090-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="b9090-123">toocreate una coda del Bus di servizio, seguire i passaggi 1 e 2 della sezione .NET hello [Introduzione a code di Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="b9090-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="b9090-124">Ora si connettono hello coda toohello Analitica flusso processo è stato creato in hello precedente procedura dettagliata di rilevamento di frodi.</span><span class="sxs-lookup"><span data-stu-id="b9090-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="b9090-125">Nel portale di Azure hello, passare toohello **output** pannello del processo e selezionare **Aggiungi** nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![Aggiunta di output](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="b9090-127">Scegliere **coda di Service Bus** come hello **Sink** e seguire le istruzioni di hello nella schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="b9090-128">Che toochoose hello uno spazio dei nomi di hello coda del Bus di servizio è stato creato in [Introduzione a code di Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="b9090-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="b9090-129">Al termine, fare clic su pulsante "right" hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="b9090-130">Specificare i seguenti valori hello:</span><span class="sxs-lookup"><span data-stu-id="b9090-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="b9090-131">**Formato serializzatore eventi**: JSON</span><span class="sxs-lookup"><span data-stu-id="b9090-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="b9090-132">**Codifica**: UTF8</span><span class="sxs-lookup"><span data-stu-id="b9090-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="b9090-133">**FORMATO**: riga separata</span><span class="sxs-lookup"><span data-stu-id="b9090-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="b9090-134">Fare clic su hello **crea** pulsante tooadd l'origine ed tooverify Analitica di flusso che può connettersi toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b9090-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="b9090-135">In hello **Query** scheda, sostituire la query corrente hello con hello seguente.</span><span class="sxs-lookup"><span data-stu-id="b9090-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="b9090-136">Sostituire * YOUR NAME BUS di servizio * con il nome di output di hello creato nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="b9090-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="b9090-137">Creare una cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="b9090-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="b9090-138">Creare una cache Redis di Azure eseguendo la seguente sezione .NET hello [come tooUse Cache Redis di Azure] [ use-rediscache] fino alla sezione hello ***configurare i client della cache di hello***.</span><span class="sxs-lookup"><span data-stu-id="b9090-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="b9090-139">Al termine dell'operazione, è disponibile una nuova cache Redis.</span><span class="sxs-lookup"><span data-stu-id="b9090-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="b9090-140">In **tutte le impostazioni**selezionare **le chiavi di accesso** e annotare hello ***stringa di connessione primaria***.</span><span class="sxs-lookup"><span data-stu-id="b9090-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![Schermata dell'architettura](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="b9090-142">Creare una funzione di Azure</span><span class="sxs-lookup"><span data-stu-id="b9090-142">Create an Azure Function</span></span>
<span data-ttu-id="b9090-143">Seguire [creare la prima funzione Azure] [ functions-getstarted] tooget esercitazione introduttiva funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9090-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="b9090-144">Se si dispone già di una funzione di Azure viene ad esempio toouse, quindi andare troppo[tooRedis Cache di scrittura](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="b9090-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="b9090-145">Nel portale di hello, selezionare servizi App dal riquadro di spostamento a sinistra hello, quindi fare clic su sito Web di app la funzione Azure app nome tooget toohello della funzione.</span><span class="sxs-lookup"><span data-stu-id="b9090-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="b9090-146">![Schermata dell'elenco di funzioni dei servizi app](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="b9090-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="b9090-147">Fare clic su **Nuova funzione > ServiceBusQueueTrigger – C#**.</span><span class="sxs-lookup"><span data-stu-id="b9090-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="b9090-148">Per hello campi seguenti, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="b9090-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="b9090-149">**Nome della coda**: hello stesso nome come nome di hello immesso al momento della creazione della coda di hello in [Introduzione a code di Service Bus] [ servicebus-getstarted] (non nome hello del bus di servizio hello).</span><span class="sxs-lookup"><span data-stu-id="b9090-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="b9090-150">Assicurarsi di utilizzare coda hello toohello connesso Analitica di flusso di output.</span><span class="sxs-lookup"><span data-stu-id="b9090-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="b9090-151">**Connessione del bus di servizio**: selezionare **Aggiungere una stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="b9090-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="b9090-152">stringa di connessione hello toofind, andare toohello portale classico, selezionare **Bus di servizio**, bus di servizio è stato creato, hello e **informazioni di connessione** in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="b9090-153">Verificare che la schermata principale hello, in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="b9090-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="b9090-154">Copiare e incollare la stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="b9090-155">È gratuito tooenter qualsiasi nome di connessione.</span><span class="sxs-lookup"><span data-stu-id="b9090-155">Feel free tooenter any connection name.</span></span>
     
       ![Schermata di connessione al bus di servizio](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="b9090-157">**AccessRights**: scegliere **Gestisci**</span><span class="sxs-lookup"><span data-stu-id="b9090-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="b9090-158">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="b9090-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="b9090-159">TooRedis scrittura Cache</span><span class="sxs-lookup"><span data-stu-id="b9090-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="b9090-160">A questo punto è stata creata una funzione di Azure leggibile dalla coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="b9090-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="b9090-161">Tutto ciò che viene lasciato toodo è utilizzare la funzione toowrite questo toohello dati Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="b9090-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="b9090-162">Selezionare il nuovo **ServiceBusQueueTrigger**, fare clic su **funzione impostazioni app** su hello angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="b9090-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="b9090-163">Selezionare **Vai tooApp servizio impostazioni > Impostazioni > Impostazioni applicazione**</span><span class="sxs-lookup"><span data-stu-id="b9090-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="b9090-164">Nella sezione delle stringhe di connessione hello, creare un nome in hello **nome** sezione.</span><span class="sxs-lookup"><span data-stu-id="b9090-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="b9090-165">Incollare una stringa di connessione primaria hello trovato in hello **creare una Cache Redis** Esegui istruzione hello **valore** sezione.</span><span class="sxs-lookup"><span data-stu-id="b9090-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="b9090-166">Selezionare **Personalizzato** per **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="b9090-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="b9090-167">Fare clic su **salvare** nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-167">Click **Save** at hello top.</span></span>
   
    ![Schermata di connessione al bus di servizio](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="b9090-169">Tornare toohello impostazioni di servizio App e selezionare **strumenti > Editor di servizio App (anteprima) > su > passare**.</span><span class="sxs-lookup"><span data-stu-id="b9090-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Schermata di connessione al bus di servizio](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="b9090-171">In un editor di propria scelta, creare un file JSON denominato **Project** con hello seguente e salvarlo su disco locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="b9090-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="b9090-172">Caricare il file nella directory radice hello della funzione (non WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="b9090-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="b9090-173">Dovrebbe essere un file denominato **lock** vengono visualizzati automaticamente, per confermare che hello Nuget pacchetti "Stackexchange" e "Newtonsoft. JSON" sono stati importati.</span><span class="sxs-lookup"><span data-stu-id="b9090-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="b9090-174">In hello **run.csx** file, sostituire codice generati in precedenza hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="b9090-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="b9090-175">Nella funzione lazyConnection hello, sostituire "CONN NAME" con il nome di hello creato nel passaggio 2 di **archiviare i dati nella cache di hello Redis**.</span><span class="sxs-lookup"><span data-stu-id="b9090-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="b9090-176">Avviare il processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="b9090-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="b9090-177">Avviare un'applicazione hello telcodatagen.exe.</span><span class="sxs-lookup"><span data-stu-id="b9090-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="b9090-178">utilizzo di Hello è come segue:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="b9090-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="b9090-179">Dal Pannello di processo di flusso Analitica hello nel portale di hello, fare clic su **avviare** nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![Schermata del processo di avvio](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="b9090-181">In hello **inizio processo** pannello viene visualizzato, selezionare **ora** e quindi fare clic su hello **avviare** pulsante in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="b9090-182">stato del processo di Hello diventa tooStarting e tardi tooRunning le modifiche.</span><span class="sxs-lookup"><span data-stu-id="b9090-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![Schermata di selezione dell'ora del processo di avvio](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="b9090-184">Eseguire la soluzione e verificarne i risultati</span><span class="sxs-lookup"><span data-stu-id="b9090-184">Run solution and check results</span></span>
<span data-ttu-id="b9090-185">Se si torna indietro tooyour **ServiceBusQueueTrigger** pagina, dovrebbe essere istruzioni di log.</span><span class="sxs-lookup"><span data-stu-id="b9090-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="b9090-186">Questi log indicano che un elemento ottenuto dal hello coda di Service Bus, inserirlo nel database di hello e viene recuperato utilizzando ora hello come chiave hello!</span><span class="sxs-lookup"><span data-stu-id="b9090-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="b9090-187">tooverify che i dati sono in cache Redis, Vai a pagina di cache Redis tooyour nel nuovo portale di hello (come mostrato nella precedente hello [creare una Cache Redis di Azure](#Create-an-Azure-Redis-Cache) passaggio) e selezionare Console.</span><span class="sxs-lookup"><span data-stu-id="b9090-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="b9090-188">È ora possibile scrivere Redis comandi tooconfirm che siano effettivamente nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="b9090-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Schermata della console Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="b9090-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9090-190">Next steps</span></span>
<span data-ttu-id="b9090-191">Siamo entusiasti di nuovi elementi di hello Azure funzioni analitica di flusso è possibile eseguire insieme e ci auguriamo che questa operazione sblocca nuove possibilità per l'utente.</span><span class="sxs-lookup"><span data-stu-id="b9090-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="b9090-192">Se si dispone di commenti al successivo come si desidera, è possibile toouse libero hello [sito UserVoice Azure](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="b9090-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="b9090-193">Nel caso di nuova versione di Microsoft Azure, la invitiamo tootry out per registrarsi per un [senza account di valutazione Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9090-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="b9090-194">Se si è nuovo tooStream Analitica, quindi vi invitiamo troppo[creare il primo processo di flusso Analitica](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="b9090-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="b9090-195">In caso di domande o per ricevere assistenza, pubblicare un messaggio nel forum [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) o [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="b9090-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="b9090-196">È inoltre possibile visualizzare hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="b9090-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="b9090-197">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b9090-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="b9090-198">Guida di riferimento per gli sviluppatori C# di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b9090-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="b9090-199">Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#</span><span class="sxs-lookup"><span data-stu-id="b9090-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="b9090-200">Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b9090-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="b9090-201">Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b9090-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="b9090-202">La modalità di Cache Redis di Azure di toomonitor</span><span class="sxs-lookup"><span data-stu-id="b9090-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="b9090-203">Seguire toostay aggiornate tutte le notizie più recenti hello e funzionalità, [ @AzureStreaming ](https://twitter.com/AzureStreaming) su Twitter.</span><span class="sxs-lookup"><span data-stu-id="b9090-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
