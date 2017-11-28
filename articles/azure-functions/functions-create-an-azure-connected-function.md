---
title: una funzione che si connette a servizi tooAzure aaaCreate | Documenti Microsoft
description: Utilizzare le funzioni di Azure toocreate un'applicazione senza che si connette tooother Azure servizi.
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="69bbe-104">Utilizzare le funzioni di Azure toocreate una funzione che si connette tooother Azure servizi</span><span class="sxs-lookup"><span data-stu-id="69bbe-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="69bbe-105">In questo argomento viene illustrata la modalità toocreate una funzione in funzioni di Azure che toomessages su un hello di coda e copie di archiviazione di Azure è in ascolto dei messaggi toorows in una tabella di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="69bbe-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="69bbe-106">Una funzione di timer di attivazione è tooload utilizzati messaggi nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="69bbe-107">Una seconda funzione legge dalla coda hello e scrive nella tabella toohello messaggi.</span><span class="sxs-lookup"><span data-stu-id="69bbe-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="69bbe-108">Coda hello sia la tabella hello vengono creati automaticamente dalle funzioni di Azure in base alle definizioni di associazione hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="69bbe-109">toomake cose più interessante, una funzione scritta in JavaScript e altri hello è scritto in c# script.</span><span class="sxs-lookup"><span data-stu-id="69bbe-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="69bbe-110">Questo dimostra che un'app per le funzioni può avere funzioni scritte in linguaggi diversi.</span><span class="sxs-lookup"><span data-stu-id="69bbe-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="69bbe-111">È possibile vedere la dimostrazione di questo scenario in un [video di Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="69bbe-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="69bbe-112">Creare una funzione che scrive toohello coda</span><span class="sxs-lookup"><span data-stu-id="69bbe-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="69bbe-113">Prima di potersi connettere tooa coda di archiviazione, è necessario toocreate una funzione che carica la coda di messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="69bbe-114">Questa funzione JavaScript utilizza un trigger timer che scrive una coda di messaggi toohello ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="69bbe-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="69bbe-115">Se si dispone già di un account Azure, consultare hello [provare Azure funzioni](https://functions.azure.com/try) esperienza, o [creare l'account di Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="69bbe-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="69bbe-116">Andare toohello portale di Azure e individuare l'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="69bbe-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="69bbe-117">Fare clic su **Nuova funzione** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="69bbe-118">Nome funzione hello **FunctionsBindingsDemo1**, immettere un valore dell'espressione cron `0/10 * * * * *` per **pianificazione**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Aggiungere una funzione attivata da un timer](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="69bbe-120">A questo punto è stata creata una funzione attivata da un timer che viene eseguita ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="69bbe-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="69bbe-121">In hello **sviluppare** scheda, fare clic su **log** e visualizzare le attività di hello nel log di hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="69bbe-122">Si noti che viene scritta una voce di log ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="69bbe-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Funzionamento di visualizzazione hello log tooverify hello (funzione)](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="69bbe-124">Aggiungere un'associazione di output della coda dei messaggi</span><span class="sxs-lookup"><span data-stu-id="69bbe-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="69bbe-125">In hello **integrazione** scegliere **nuovo Output** > **coda di archiviazione di Azure** > **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Aggiungere una funzione attivata da un timer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="69bbe-127">Immettere `myQueueItem` per **nome del parametro messaggio** e `functions-bindings` per **nome coda**, selezionare un oggetto esistente **connessione ad account di archiviazione** oppure fare clic su **nuova** toocreate uno spazio di archiviazione account di connessione e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Creare una coda di archiviazione toohello associazione hello output](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="69bbe-129">In hello **sviluppare** scheda, aggiungere hello toohello codice che segue:</span><span class="sxs-lookup"><span data-stu-id="69bbe-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="69bbe-130">Individuare hello *se* istruzione circa 9 della funzione hello di riga e di codice seguente hello di inserimento dopo tale istruzione.</span><span class="sxs-lookup"><span data-stu-id="69bbe-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="69bbe-131">Questo codice crea un **myQueueItem** e imposta il relativo **ora** timeStamp corrente di proprietà toohello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="69bbe-132">Aggiunge quindi hello nuova coda elemento toohello del contesto **myQueueItem** associazione.</span><span class="sxs-lookup"><span data-stu-id="69bbe-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="69bbe-133">Fare clic su **Salva ed esegui**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="69bbe-134">Visualizzare gli aggiornamenti di archiviazione usando Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="69bbe-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="69bbe-135">È possibile verificare che la funzione sta visualizzando i messaggi nella coda di hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="69bbe-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="69bbe-136">È possibile connettersi tooyour coda di archiviazione tramite Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69bbe-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="69bbe-137">Tuttavia, portale hello rende facile tooconnect tooyour account di archiviazione tramite Esplora archivi di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="69bbe-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="69bbe-138">In hello **integrazione** , fare clic sulla coda di associazione di output > **documentazione**Scopri hello stringa di connessione per l'account di archiviazione e copiare il valore di hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="69bbe-139">Utilizzare questo account di archiviazione tooyour tooconnect valore.</span><span class="sxs-lookup"><span data-stu-id="69bbe-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Scaricare Azure Storage Explorer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="69bbe-141">Se non è già stato fatto, scaricare e installare [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="69bbe-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="69bbe-142">In Esplora archivi, fare clic su hello tooAzure archiviazione icona della connessione, incollare la stringa di connessione hello nel campo hello e completare la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Storage Explorer aggiunge una connessione](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="69bbe-144">In **locale e associata**, espandere **gli account di archiviazione** > l'account di archiviazione > **code** > **funzioni-bindings**e verificare che i messaggi vengono scritti toohello coda.</span><span class="sxs-lookup"><span data-stu-id="69bbe-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Visualizzazione di messaggi nella coda di hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="69bbe-146">Se la coda hello non esiste o è vuota, è probabilmente un problema con l'associazione di funzione o il codice.</span><span class="sxs-lookup"><span data-stu-id="69bbe-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="69bbe-147">Creare una funzione che legge dalla coda hello</span><span class="sxs-lookup"><span data-stu-id="69bbe-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="69bbe-148">Ora che hai aggiunti toohello coda di messaggi, è possibile creare un'altra funzione che legge dalla coda hello hello scrive i messaggi e in modo permanente tooan tabella di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="69bbe-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="69bbe-149">Fare clic su **Nuova funzione** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="69bbe-150">Nome funzione hello `FunctionsBindingsDemo2`, immettere **funzioni associazioni** in hello **nome coda** campo, selezionare un account di archiviazione esistente o crearne uno e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Aggiungere una funzione timer della coda di output](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="69bbe-152">(Facoltativo) È possibile verificare che hello nuovo funzionamento visualizzando nuova coda hello in soluzioni di archiviazione come prima.</span><span class="sxs-lookup"><span data-stu-id="69bbe-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="69bbe-153">È anche possibile usare Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="69bbe-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="69bbe-154">(Facoltativo) Aggiornare hello **funzioni associazioni** coda e notare che sono stati rimossi elementi dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="69bbe-155">Hello rimozione si verifica perché la funzione hello associato toohello **funzioni associazioni** coda come una funzione di trigger e hello input legge coda hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="69bbe-156">Aggiungere un'associazione di output della tabella</span><span class="sxs-lookup"><span data-stu-id="69bbe-156">Add a table output binding</span></span>

1. <span data-ttu-id="69bbe-157">In FunctionsBindingsDemo2 fare clic su **Integrazione** > **Nuovo output** > **Archiviazione tabelle di Azure** > **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Aggiungere una tabella di archiviazione di Azure tooan associazione](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="69bbe-159">Immettere `functionbindings` per **Nome tabella** e `myTable` per **Nome del parametro della tabella**, scegliere una **Connessione dell'account di archiviazione** o crearne una nuova e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configurare l'associazione di tabella di archiviazione hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="69bbe-161">In hello **sviluppare** scheda, sostituire il codice di funzione esistente hello con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="69bbe-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="69bbe-162">Hello **TableItem** classe rappresenta una riga nella tabella di archiviazione hello e si aggiunta hello elemento toohello `myTable` insieme di **TableItem** oggetti.</span><span class="sxs-lookup"><span data-stu-id="69bbe-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="69bbe-163">È necessario impostare hello **PartitionKey** e **RowKey** tooinsert in grado di proprietà toobe nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="69bbe-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="69bbe-164">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="69bbe-164">Click **Save**.</span></span>  <span data-ttu-id="69bbe-165">Infine, è possibile verificare il funzionamento di funzione hello visualizzando la tabella hello in soluzioni di archiviazione o di Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="69bbe-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="69bbe-166">(Facoltativo) Nell'account di archiviazione in Esplora archivi, espandere **tabelle** > **functionsbindings** e verificare che le righe vengono aggiunte toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="69bbe-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="69bbe-167">È possibile eseguire stesso hello in Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69bbe-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Visualizzazione di righe nella tabella hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="69bbe-169">Se la tabella hello non esiste o è vuota, è probabilmente un problema con l'associazione di funzione o il codice.</span><span class="sxs-lookup"><span data-stu-id="69bbe-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="69bbe-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69bbe-170">Next steps</span></span>
<span data-ttu-id="69bbe-171">Per ulteriori informazioni sulle funzioni di Azure, vedere hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="69bbe-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="69bbe-172">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="69bbe-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="69bbe-173">Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="69bbe-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="69bbe-174">Test di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="69bbe-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="69bbe-175">Descrive diversi strumenti e tecniche per il test delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="69bbe-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="69bbe-176">Come tooscale funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="69bbe-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="69bbe-177">Vengono descritti i piani di servizio disponibili con le funzioni di Azure, piano di hosting consumo hello e come toochoose hello giusta.</span><span class="sxs-lookup"><span data-stu-id="69bbe-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

