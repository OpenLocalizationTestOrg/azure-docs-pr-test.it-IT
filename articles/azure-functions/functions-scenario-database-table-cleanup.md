---
title: "Usare Funzioni di Azure per eseguire un'attività di pulizia del database | Microsoft Docs"
description: "Usare Funzioni di Azure per pianificare un'attività che si connette al database SQL di Azure per eseguire una pulizia periodica delle righe."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="7bc7e-103">Usare Funzioni di Azure per connettersi al database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="7bc7e-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="7bc7e-104">In questo argomento viene illustrato come usare Funzioni di Azure per creare un processo pianificato al fine di eseguire la pulizia delle righe in una tabella del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="7bc7e-105">La nuova funzione C# viene creata in base a un modello predefinito di attivazione del timer nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="7bc7e-106">Per supportare questo scenario, è necessario anche impostare una stringa di connessione di database come impostazione nell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="7bc7e-107">Questo scenario esegue un'operazione in blocco sul database.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="7bc7e-108">Affinché la funzione elabori le singole operazioni CRUD in una tabella di un'app per dispositivi mobili, è necessario usare invece le [associazioni all'app per dispositivi mobili](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="7bc7e-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bc7e-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7bc7e-109">Prerequisites</span></span>

+ <span data-ttu-id="7bc7e-110">Questo argomento usa una funzione attivata da un timer.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="7bc7e-111">Completare i passaggi nell'argomento [Creare una funzione in Azure attivata da un timer](functions-create-scheduled-function.md) per creare una versione C# di questa funzione.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="7bc7e-112">Questo argomento illustra un comando Transact-SQL che esegue un'operazione di pulizia in blocco nella tabella **SalesOrderHeader** nel database di esempio AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="7bc7e-113">Per creare il database di esempio AdventureWorksLT, completare la procedura nell'argomento [Creare un database SQL di Azure nel portale di Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7bc7e-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="7bc7e-114">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="7bc7e-114">Get connection information</span></span>

<span data-ttu-id="7bc7e-115">È necessario ottenere la stringa di connessione per il database creato dopo avere completato [Creare un database SQL di Azure nel portale di Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7bc7e-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="7bc7e-116">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7bc7e-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="7bc7e-117">Scegliere **Database SQL** dal menu a sinistra, quindi scegliere il database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="7bc7e-118">Selezionare **Mostra stringhe di connessione del database** e copiare tutta la stringa di connessione **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![Copiare la stringa di connessione ADO.NET.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="7bc7e-120">Impostare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="7bc7e-120">Set the connection string</span></span> 

<span data-ttu-id="7bc7e-121">Un'app per le funzioni ospita l'esecuzione delle funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="7bc7e-122">È consigliabile archiviare le stringhe di connessione e altre informazioni riservate nelle impostazioni dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="7bc7e-123">L'uso delle impostazioni dell'applicazione impedisce la diffusione accidentale della stringa di connessione con il codice.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="7bc7e-124">Passare all'app per le funzioni creata in [Creare una funzione in Azure attivata da un timer](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="7bc7e-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="7bc7e-125">Selezionare **Funzionalità della piattaforma** > **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Impostazioni applicazioni per l'app per le funzioni.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="7bc7e-127">Scorrere verso il basso fino a **Stringhe di connessione** e aggiungere una stringa di connessione usando le impostazioni come indicato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Aggiungere una stringa di connessione alle impostazioni dell'app per le funzioni.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="7bc7e-129">Impostazione</span><span class="sxs-lookup"><span data-stu-id="7bc7e-129">Setting</span></span>       | <span data-ttu-id="7bc7e-130">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="7bc7e-130">Suggested value</span></span> | <span data-ttu-id="7bc7e-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7bc7e-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="7bc7e-132">**Nome**</span><span class="sxs-lookup"><span data-stu-id="7bc7e-132">**Name**</span></span>  |  <span data-ttu-id="7bc7e-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="7bc7e-133">sqldb_connection</span></span>  | <span data-ttu-id="7bc7e-134">Usato per accedere alla stringa di connessione memorizzata nel codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="7bc7e-135">**Valore**</span><span class="sxs-lookup"><span data-stu-id="7bc7e-135">**Value**</span></span> | <span data-ttu-id="7bc7e-136">Stringa copiata</span><span class="sxs-lookup"><span data-stu-id="7bc7e-136">Copied string</span></span>  | <span data-ttu-id="7bc7e-137">Incollare la stringa di connessione copiata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="7bc7e-138">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="7bc7e-138">**Type**</span></span> | <span data-ttu-id="7bc7e-139">Database SQL</span><span class="sxs-lookup"><span data-stu-id="7bc7e-139">SQL Database</span></span> | <span data-ttu-id="7bc7e-140">Usare la connessione al database SQL predefinita.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="7bc7e-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-141">Click **Save**.</span></span>

<span data-ttu-id="7bc7e-142">A questo punto, è possibile aggiungere il codice della funzione C# che si connette al database SQL.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="7bc7e-143">Aggiornare il codice di funzione</span><span class="sxs-lookup"><span data-stu-id="7bc7e-143">Update your function code</span></span>

1. <span data-ttu-id="7bc7e-144">Nell'app per le funzioni, selezionare la funzione attivata dal timer.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="7bc7e-145">Aggiungere i riferimenti assembly seguenti all'inizio del codice della funzione esistente:</span><span class="sxs-lookup"><span data-stu-id="7bc7e-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="7bc7e-146">Aggiungere le istruzioni `using` seguenti alla funzione:</span><span class="sxs-lookup"><span data-stu-id="7bc7e-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="7bc7e-147">Sostituire la funzione **Run** esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7bc7e-147">Replace the existing **Run** function with the following code:</span></span>
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="7bc7e-148">Questo comando di esempio aggiorna la colonna **Stato** in base alla data di spedizione.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="7bc7e-149">Aggiorna 32 righe di dati.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="7bc7e-150">Fare clic su **Salva**, osservare le finestre **Log** per l'esecuzione della funzione successiva e quindi prendere nota del numero di righe aggiornate nella tabella **SalesOrderHeader**.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![Visualizzare i log di funzione.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="7bc7e-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bc7e-152">Next steps</span></span>

<span data-ttu-id="7bc7e-153">Ora si apprenderà come usare le funzioni con l'app per la logica per l'integrazione con altri servizi.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="7bc7e-154">Creare una funzione che si integra con le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="7bc7e-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="7bc7e-155">Per altre informazioni sulle funzioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bc7e-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="7bc7e-156">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="7bc7e-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="7bc7e-157">Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="7bc7e-158">Test di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="7bc7e-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="7bc7e-159">Descrive diversi strumenti e tecniche per il test delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="7bc7e-159">Describes various tools and techniques for testing your functions.</span></span>  
