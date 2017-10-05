---
title: Creare una funzione che connette ai servizi di Azure | Documentazione Microsoft
description: Usare Funzioni di Azure per creare un'applicazione senza server che connette ad altri servizi di Azure.
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
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="9dcbb-104">Usare Funzioni di Azure per creare una funzione che connette ad altri servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="9dcbb-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="9dcbb-105">Questo argomento illustra come creare una funzione in Funzioni di Azure che ascolta i messaggi in una coda di Azure e li copia nelle righe di una tabella di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="9dcbb-106">Per caricare i messaggi nella coda viene usata una funzione attivata da un timer.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="9dcbb-107">Una seconda funzione legge i messaggi dalla coda e li scrive nella tabella.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="9dcbb-108">Sia la coda che la tabella vengono create da funzioni di Azure sulla base delle definizioni di associazione.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="9dcbb-109">Per rendere le cose più interessanti, una funzione è scritta in JavaScript e l'altra in C#.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="9dcbb-110">Questo dimostra che un'app per le funzioni può avere funzioni scritte in linguaggi diversi.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="9dcbb-111">È possibile vedere la dimostrazione di questo scenario in un [video di Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="9dcbb-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="9dcbb-112">Creare una funzione che scrive nella coda</span><span class="sxs-lookup"><span data-stu-id="9dcbb-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="9dcbb-113">Prima di connettersi a una coda di archiviazione, è necessario creare una funzione che carica la coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="9dcbb-114">La funzione JavaScript usa un trigger basato su timer che scrive un messaggio nella coda ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="9dcbb-115">Se non si dispone già di un account Azure, vedere [Prova Funzioni di Azure](https://functions.azure.com/try) oppure [creare un account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9dcbb-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="9dcbb-116">Passare al portale di Azure e trovare l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="9dcbb-117">Fare clic su **Nuova funzione** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="9dcbb-118">Assegnare alla funzione il nome **FunctionsBindingsDemo1**, immettere un valore di espressione cron `0/10 * * * * *` per **Pianificazione** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Aggiungere una funzione attivata da un timer](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="9dcbb-120">A questo punto è stata creata una funzione attivata da un timer che viene eseguita ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="9dcbb-121">Nella scheda **Sviluppo** fare clic su **Log** e visualizzare l'attività nel log.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="9dcbb-122">Si noti che viene scritta una voce di log ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Visualizzare il log per verificare il funzionamento della funzione](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="9dcbb-124">Aggiungere un'associazione di output della coda dei messaggi</span><span class="sxs-lookup"><span data-stu-id="9dcbb-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="9dcbb-125">Nella scheda **Integrazione** scegliere **Nuovo output** > **Archiviazione code di Azure** > **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Aggiungere una funzione attivata da un timer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="9dcbb-127">Immettere `myQueueItem` per **Nome del parametro del messaggio** e `functions-bindings` per **Nome coda**, selezionare una **Connessione dell'account di archiviazione** esistente o fare clic su **nuova** per creare una connessione dell'account di archiviazione, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![Creare l'associazione di output alla coda dei messaggi](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="9dcbb-129">Tornare alla scheda **Sviluppo** e aggiungere alla funzione il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9dcbb-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="9dcbb-130">Individuare l'istruzione *if* più o meno in corrispondenza della riga 9 della funzione e inserire dopo di essa il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="9dcbb-131">Questo codice crea un oggetto **myQueueItem** e ne imposta la proprietà **time** sul valore corrente di timeStamp.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="9dcbb-132">Aggiunge quindi il nuovo elemento della coda all'associazione **myQueueItem** del contesto.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="9dcbb-133">Fare clic su **Salva ed esegui**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="9dcbb-134">Visualizzare gli aggiornamenti di archiviazione usando Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="9dcbb-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="9dcbb-135">È possibile verificare il funzionamento della funzione visualizzando i messaggi nella coda creata.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="9dcbb-136">È possibile connettersi alla coda di archiviazione usando Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="9dcbb-137">Usando il portale e Microsoft Azure Storage Explorer, tuttavia, la connessione all'account di archiviazione risulta più semplice.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="9dcbb-138">Nella scheda **Integrazione** selezionare l'associazione di output della coda > **Documentazione**, visualizzare la stringa di connessione per l'account di archiviazione e quindi copiare il valore.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="9dcbb-139">Usare questo valore per la connessione all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-139">You use this value to connect to your storage account.</span></span>

    ![Scaricare Azure Storage Explorer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="9dcbb-141">Se non è già stato fatto, scaricare e installare [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="9dcbb-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="9dcbb-142">In Storage Explorer fare clic sull'icona Connetti ad Archiviazione di Azure, incollare la stringa di connessione nel campo e completare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Storage Explorer aggiunge una connessione](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="9dcbb-144">In **Local and attached** (Locale e collegato) espandere **Account di archiviazione** > account di archiviazione > **Code** > **functions-bindings** e verificare che i messaggi vengano scritti nella coda.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![Visualizzazione dei messaggi nella coda](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="9dcbb-146">Se la coda non esiste o è vuota, è probabile che si tratti di un problema relativo al codice o all'associazione della funzione.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="9dcbb-147">Creare una funzione che legge dalla coda</span><span class="sxs-lookup"><span data-stu-id="9dcbb-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="9dcbb-148">Dopo aver aggiunto i messaggi alla coda, è possibile creare un'altra funzione che legge dalla coda e scrive i messaggi in modo permanente in una tabella di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="9dcbb-149">Fare clic su **Nuova funzione** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="9dcbb-150">Assegnare alla funzione il nome `FunctionsBindingsDemo2`, immettere **functions-bindings** nel campo **Nome coda**, selezionare un account di archiviazione esistente o crearne uno e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Aggiungere una funzione timer della coda di output](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="9dcbb-152">(Facoltativo) È possibile verificare il funzionamento della nuova funzione visualizzando la nuova coda in Storage Explorer, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="9dcbb-153">È anche possibile usare Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="9dcbb-154">(Facoltativo) Aggiornare la coda **functions-bindings**: notare che sono state rimossi alcuni elementi.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="9dcbb-155">La rimozione si verifica perché la funzione è associata alla coda **functions-bindings** come trigger di input e legge tale coda.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="9dcbb-156">Aggiungere un'associazione di output della tabella</span><span class="sxs-lookup"><span data-stu-id="9dcbb-156">Add a table output binding</span></span>

1. <span data-ttu-id="9dcbb-157">In FunctionsBindingsDemo2 fare clic su **Integrazione** > **Nuovo output** > **Archiviazione tabelle di Azure** > **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Aggiungere un'associazione a una tabella di Archiviazione di Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="9dcbb-159">Immettere `functionbindings` per **Nome tabella** e `myTable` per **Nome del parametro della tabella**, scegliere una **Connessione dell'account di archiviazione** o crearne una nuova e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configurare l'associazione della tabella di archiviazione](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="9dcbb-161">Nella scheda **Sviluppo** sostituire il codice della funzione esistente con il seguente:</span><span class="sxs-lookup"><span data-stu-id="9dcbb-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
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
        
        // Add the item to the table binding collection.
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
    <span data-ttu-id="9dcbb-162">La classe **TableItem** rappresenta una riga della tabella di archiviazione. Aggiungere l'elemento alla raccolta `myTable` di oggetti **TableItem**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="9dcbb-163">Per inserire voci nella tabella, è necessario impostare le proprietà **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="9dcbb-164">Fare clic su **Salva**</span><span class="sxs-lookup"><span data-stu-id="9dcbb-164">Click **Save**.</span></span>  <span data-ttu-id="9dcbb-165">Al termine, è possibile verificare il funzionamento della funzione visualizzando la tabella in Storage Explorer o Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="9dcbb-166">(Facoltativo) Nell'account di archiviazione di Storage Explorer espandere **Tabelle** > **functionsbindings** e verificare che alla tabella vengano aggiunte delle righe.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="9dcbb-167">È possibile eseguire la stessa operazione in Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![Visualizzazione delle righe della tabella](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="9dcbb-169">Se la tabella non esiste o è vuota, è probabile che si tratti di un problema relativo al codice o all'associazione della funzione.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="9dcbb-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9dcbb-170">Next steps</span></span>
<span data-ttu-id="9dcbb-171">Per altre informazioni su Funzioni di Azure, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dcbb-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="9dcbb-172">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9dcbb-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="9dcbb-173">Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="9dcbb-174">Test di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9dcbb-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="9dcbb-175">Descrive diversi strumenti e tecniche per il test delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="9dcbb-176">Come aumentare le prestazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9dcbb-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="9dcbb-177">Presenta i piani di servizio disponibili con Funzioni di Azure, tra cui il piano di hosting A consumo, e spiega come scegliere quello più appropriato.</span><span class="sxs-lookup"><span data-stu-id="9dcbb-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

