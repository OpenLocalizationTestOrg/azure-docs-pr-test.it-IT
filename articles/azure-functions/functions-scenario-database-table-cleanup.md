---
title: "aaaUse funzioni Azure tooperform un pulitura del database attività | Documenti Microsoft"
description: "Utilizzare le funzioni di Azure tooschedule un'attività che si connette tooAzure Database SQL tooperiodically eseguire la pulizia delle righe."
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
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="3e2fb-103">Utilizzare le funzioni di Azure tooconnect tooan Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="3e2fb-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="3e2fb-104">Questo argomento viene illustrato come toouse toocreate di funzioni di Azure un processo che pulisce le righe in una tabella in un Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="3e2fb-105">funzione Hello nuovo c# viene creato in base a un modello di trigger timer predefiniti nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="3e2fb-106">toosupport questo scenario, è necessario impostare anche una stringa di connessione di database come un'impostazione di app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="3e2fb-107">Questo scenario viene utilizzata un'operazione bulk database hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="3e2fb-108">toohave la funzione processo singole operazioni CRUD in una tabella di App per dispositivi mobili, è opportuno utilizzare [associazioni di App per dispositivi mobili](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3e2fb-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e2fb-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3e2fb-109">Prerequisites</span></span>

+ <span data-ttu-id="3e2fb-110">Questo argomento usa una funzione attivata da un timer.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="3e2fb-111">Hello completato i passaggi in argomento hello [creare una funzione in Azure che viene attivata da un timer](functions-create-scheduled-function.md) toocreate c# versione di questa funzione.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="3e2fb-112">In questo argomento viene illustrato un comando di Transact-SQL che esegue un'operazione di pulizia delle operazioni bulk in hello **SalesOrderHeader** tabella nel database di esempio AdventureWorksLT hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="3e2fb-113">database di esempio AdventureWorksLT hello toocreate, hello completato i passaggi in argomento hello [creare un database SQL di Azure nel portale di Azure hello](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3e2fb-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="3e2fb-114">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="3e2fb-114">Get connection information</span></span>

<span data-ttu-id="3e2fb-115">Stringa di connessione hello tooget necessari per il database di hello è stato creato dopo avere completato [creare un database SQL di Azure nel portale di Azure hello](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3e2fb-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="3e2fb-116">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3e2fb-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="3e2fb-117">Selezionare **database SQL** dal menu a sinistra, hello e selezionare il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="3e2fb-118">Selezionare **Mostra le stringhe di connessione di database** hello copia completa e **ADO.NET** stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Copiare una stringa di connessione ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="3e2fb-120">Impostare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="3e2fb-120">Set hello connection string</span></span> 

<span data-ttu-id="3e2fb-121">Un'app di funzione ospita esecuzione hello delle funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="3e2fb-122">È un stringhe di connessione di best practice toostore e altri segreti nelle impostazioni dell'app (funzione).</span><span class="sxs-lookup"><span data-stu-id="3e2fb-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="3e2fb-123">Utilizzando le impostazioni dell'applicazione impedisce la diffusione accidentale della stringa di connessione hello con il codice.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="3e2fb-124">Passare tooyour funzione app creato [creare una funzione in Azure che viene attivata da un timer](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="3e2fb-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="3e2fb-125">Selezionare **Funzionalità della piattaforma** > **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Impostazioni applicazione per app di funzione hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="3e2fb-127">Scorrere verso il basso troppo**le stringhe di connessione** e aggiungere una stringa di connessione utilizzando le impostazioni di hello come specificato nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![Aggiungere impostazioni connessione stringa toohello funzione app.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="3e2fb-129">Impostazione</span><span class="sxs-lookup"><span data-stu-id="3e2fb-129">Setting</span></span>       | <span data-ttu-id="3e2fb-130">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="3e2fb-130">Suggested value</span></span> | <span data-ttu-id="3e2fb-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3e2fb-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="3e2fb-132">**Nome**</span><span class="sxs-lookup"><span data-stu-id="3e2fb-132">**Name**</span></span>  |  <span data-ttu-id="3e2fb-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="3e2fb-133">sqldb_connection</span></span>  | <span data-ttu-id="3e2fb-134">Hello tooaccess utilizzati archiviati stringa di connessione nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="3e2fb-135">**Valore**</span><span class="sxs-lookup"><span data-stu-id="3e2fb-135">**Value**</span></span> | <span data-ttu-id="3e2fb-136">Stringa copiata</span><span class="sxs-lookup"><span data-stu-id="3e2fb-136">Copied string</span></span>  | <span data-ttu-id="3e2fb-137">Dopo la stringa di connessione hello copiata nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="3e2fb-138">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="3e2fb-138">**Type**</span></span> | <span data-ttu-id="3e2fb-139">Database SQL</span><span class="sxs-lookup"><span data-stu-id="3e2fb-139">SQL Database</span></span> | <span data-ttu-id="3e2fb-140">Utilizzare connessione di Database SQL di hello predefinita.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="3e2fb-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-141">Click **Save**.</span></span>

<span data-ttu-id="3e2fb-142">A questo punto, è possibile aggiungere hello funzione codice c# che si connette tooyour Database SQL.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="3e2fb-143">Aggiornare il codice di funzione</span><span class="sxs-lookup"><span data-stu-id="3e2fb-143">Update your function code</span></span>

1. <span data-ttu-id="3e2fb-144">Nell'app (funzione), Seleziona funzione di attivazione del timer hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="3e2fb-145">Aggiungere hello riferimenti ad assembly nella parte superiore di hello hello esistente del codice di funzione seguente:</span><span class="sxs-lookup"><span data-stu-id="3e2fb-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="3e2fb-146">Aggiungere il seguente hello `using` funzione toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="3e2fb-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="3e2fb-147">Sostituire hello **eseguire** funzione con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="3e2fb-147">Replace hello existing **Run** function with hello following code:</span></span>
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
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="3e2fb-148">Questo comando di esempio aggiorna hello **stato** colonna in base alla data di spedizione hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="3e2fb-149">Aggiorna 32 righe di dati.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="3e2fb-150">Fare clic su **salvare**, hello watch **registri** windows per hello successivamente funzione esecuzione, quindi annotare hello numero di righe aggiornate nella hello **SalesOrderHeader** tabella.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Consente di visualizzare i log delle funzioni hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="3e2fb-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e2fb-152">Next steps</span></span>

<span data-ttu-id="3e2fb-153">Per ulteriori informazioni come toouse funziona con la logica App toointegrate con altri servizi.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="3e2fb-154">Creare una funzione che si integra con le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="3e2fb-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="3e2fb-155">Per ulteriori informazioni sulle funzioni, vedere hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="3e2fb-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="3e2fb-156">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="3e2fb-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="3e2fb-157">Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="3e2fb-158">Test di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="3e2fb-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="3e2fb-159">Descrive diversi strumenti e tecniche per il test delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="3e2fb-159">Describes various tools and techniques for testing your functions.</span></span>  
