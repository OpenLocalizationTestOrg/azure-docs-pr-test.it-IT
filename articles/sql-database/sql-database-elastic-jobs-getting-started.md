---
title: Introduzione a processi di database elastici | Documentazione Microsoft
description: come utilizzare i processi di database elastici
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 05c20e880d4eb1eacdecc0c4c7e7491dfe1e6a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="e8954-103">Introduzione ai processi di Database Elastici</span><span class="sxs-lookup"><span data-stu-id="e8954-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="e8954-104">I processi di database elastici (anteprima) per il database SQL di Azure consentono di eseguire in maniera affidabile script T-SQL che si estendono su più database e effettuano tentativi automatici per garantire il completamento delle operazioni .</span><span class="sxs-lookup"><span data-stu-id="e8954-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="e8954-105">Per ulteriori informazioni sulla funzionalità dei processi di database elastici, vedere la [panoramica della funzionalità](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8954-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="e8954-106">Questo argomento supporta l'esempio presentato in [Introduzione agli strumenti del Database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8954-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="e8954-107">Al termine, si apprenderà come creare e gestire processi di gestione di un gruppo di database correlati.</span><span class="sxs-lookup"><span data-stu-id="e8954-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="e8954-108">Non è necessario usare gli strumenti di scalabilità elastica per sfruttare i vantaggi dei processi elastici.</span><span class="sxs-lookup"><span data-stu-id="e8954-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8954-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e8954-109">Prerequisites</span></span>
<span data-ttu-id="e8954-110">Scaricare ed eseguire [Introduzione allo strumento di esempio del Database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8954-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="e8954-111">Creare un gestore mappe partizione utilizzando l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="e8954-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="e8954-112">Di seguito si creerà un gestore mappe partizione con diverse partizioni, seguita dall'inserimento di dati nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="e8954-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="e8954-113">Se si dispone già di programma di installazione di partizioni con dati partizionati in essi, è possibile ignorare i passaggi seguenti e passare alla sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="e8954-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="e8954-114">Compilare ed eseguire l’applicazione di esempio **Introduzione agli strumenti del Database elastico** .</span><span class="sxs-lookup"><span data-stu-id="e8954-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="e8954-115">Seguire la procedura fino al passaggio 7 nella sezione [Scaricare ed eseguire l'app di esempio](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="e8954-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="e8954-116">Alla fine del passaggio 7, verrà visualizzato il seguente prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="e8954-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![Aprire il prompt dei comandi.](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="e8954-118">Nella finestra di comando, digitare "1" e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="e8954-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="e8954-119">Viene creato il gestore delle mappe partizioni e aggiunge due partizioni al server.</span><span class="sxs-lookup"><span data-stu-id="e8954-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="e8954-120">Digitare "3" e premere **Invia**. Ripetere l'operazione quattro volte.</span><span class="sxs-lookup"><span data-stu-id="e8954-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="e8954-121">Consente di inserire righe di dati di esempio nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="e8954-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="e8954-122">Il [portale di Azure](https://portal.azure.com) dovrebbe mostrare tre nuovi database:</span><span class="sxs-lookup"><span data-stu-id="e8954-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Conferma di Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="e8954-124">A questo punto, si creerà un insieme di database personalizzati che riflette tutti i database del mapping della partizione.</span><span class="sxs-lookup"><span data-stu-id="e8954-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="e8954-125">Questo consentirà di creare ed eseguire un processo che aggiunge una nuova tabella tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="e8954-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="e8954-126">Si creerà una destinazione di partizionamento della mappa, utilizzando il cmdlet **New-AzureSqlJobTarget** .</span><span class="sxs-lookup"><span data-stu-id="e8954-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="e8954-127">Il database di gestione della mappa di partizione deve essere impostato come destinazione di database e quindi il mapping di partizione specifico viene specificato come destinazione.</span><span class="sxs-lookup"><span data-stu-id="e8954-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="e8954-128">In questo caso, invece, tutti i database nel server dovranno essere enumerati e aggiunti alla nuova raccolta personalizzata, ad eccezione del database master.</span><span class="sxs-lookup"><span data-stu-id="e8954-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="e8954-129">Crea una raccolta personalizzata e aggiunge tutti i database nel server alla destinazione della raccolta personalizzata ad eccezione del database master.</span><span class="sxs-lookup"><span data-stu-id="e8954-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="e8954-130">Creare uno Script T-SQL per l'esecuzione tra database</span><span class="sxs-lookup"><span data-stu-id="e8954-130">Create a T-SQL Script for execution across databases</span></span>
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="e8954-131">Creare il processo per eseguire uno script in un gruppo personalizzato di database</span><span class="sxs-lookup"><span data-stu-id="e8954-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="e8954-132">Eseguire il processo</span><span class="sxs-lookup"><span data-stu-id="e8954-132">Execute the job</span></span>
<span data-ttu-id="e8954-133">Il seguente script PowerShell può essere utilizzato per eseguire un processo esistente:</span><span class="sxs-lookup"><span data-stu-id="e8954-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="e8954-134">Aggiornare la variabile seguente per riflettere il nome del processo desiderato da eseguire:</span><span class="sxs-lookup"><span data-stu-id="e8954-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="e8954-135">Recuperare lo stato di un singolo processo di esecuzione</span><span class="sxs-lookup"><span data-stu-id="e8954-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="e8954-136">Usare lo stesso cmdlet **Get-AzureSqlJobExecution** con il parametro **IncludeChildren** per visualizzare lo stato delle esecuzioni del processo figlio, ovvero lo stato specifico per ogni esecuzione del processo in ogni database di destinazione del processo.</span><span class="sxs-lookup"><span data-stu-id="e8954-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="e8954-137">Visualizzare lo stato su più esecuzioni del processo</span><span class="sxs-lookup"><span data-stu-id="e8954-137">View the state across multiple job executions</span></span>
<span data-ttu-id="e8954-138">Il cmdlet **Get-AzureSqlJobExecution** ha più parametri facoltativi che possono essere utilizzati per visualizzare più esecuzioni di processo, filtrate tramite i parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="e8954-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="e8954-139">Di seguito vengono illustrati alcuni dei possibili modi per utilizzare Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="e8954-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="e8954-140">Recuperare tutte le esecuzioni attive di processo di primo livello:</span><span class="sxs-lookup"><span data-stu-id="e8954-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="e8954-141">Recuperare tutte le esecuzioni di processo di primo livello, incluse le esecuzioni di processo inattive:</span><span class="sxs-lookup"><span data-stu-id="e8954-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="e8954-142">Recuperare tutte le esecuzioni di processo figlio di un ID di esecuzione processo fornito, incluse le esecuzioni di processo inattive:</span><span class="sxs-lookup"><span data-stu-id="e8954-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="e8954-143">Recuperare tutte le esecuzioni di processo create utilizzando una pianificazione / processo di combinazione, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="e8954-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="e8954-144">Recuperare tutti i processi destinati a una mappa di partizione specificata, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="e8954-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="e8954-145">Recuperare tutti i processi destinati a una raccolta personalizzata specificata, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="e8954-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="e8954-146">Recuperare l'elenco delle esecuzioni delle attività di processo in una esecuzione di processo specifica:</span><span class="sxs-lookup"><span data-stu-id="e8954-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="e8954-147">Recuperare i dettagli di esecuzione delle attività di processo:</span><span class="sxs-lookup"><span data-stu-id="e8954-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="e8954-148">Il seguente script PowerShell può essere utilizzato per visualizzare i dettagli di un'esecuzione delle attività di processo, che è particolarmente utile durante il debug degli errori di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e8954-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="e8954-149">Recuperare gli errori all'interno delle esecuzioni delle attività di processo</span><span class="sxs-lookup"><span data-stu-id="e8954-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="e8954-150">L'oggetto JobTaskExecution include una proprietà per il ciclo di vita dell'attività insieme ad una proprietà del messaggio.</span><span class="sxs-lookup"><span data-stu-id="e8954-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="e8954-151">Se un'esecuzione delle attività di processo ha esito negativo,la proprietà del ciclo di vita verrà impostata su *Non riuscita* e la proprietà del messaggio verrà impostata sul messaggio di eccezione risultante e il  relativo stack.</span><span class="sxs-lookup"><span data-stu-id="e8954-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="e8954-152">Se un processo ha esito negativo, è importante visualizzare i dettagli delle attività di processo che non sono riuscite per un determinato processo.</span><span class="sxs-lookup"><span data-stu-id="e8954-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="e8954-153">In attesa del completamento dell’esecuzione del processo</span><span class="sxs-lookup"><span data-stu-id="e8954-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="e8954-154">Il seguente script PowerShell può essere utilizzato per attendere che un’attività di processo venga completata: </span><span class="sxs-lookup"><span data-stu-id="e8954-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="e8954-155">Creare un criterio di esecuzione personalizzata</span><span class="sxs-lookup"><span data-stu-id="e8954-155">Create a custom execution policy</span></span>
<span data-ttu-id="e8954-156">I processi di database elastici supportano la creazione di criteri di esecuzione personalizzati che possono essere applicati all'avvio dei processi.</span><span class="sxs-lookup"><span data-stu-id="e8954-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="e8954-157">Criteri di esecuzione che attualmente consentono la definizione di:</span><span class="sxs-lookup"><span data-stu-id="e8954-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="e8954-158">Nome: Identificatore del criterio di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e8954-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="e8954-159">Timeout del processo: tempo totale prima che un processo venga annullato dai processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="e8954-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="e8954-160">Intervallo tra tentativi iniziale: intervallo di attesa prima del primo tentativo.</span><span class="sxs-lookup"><span data-stu-id="e8954-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="e8954-161">Intervallo massimo di tentativi: estremità degli intervalli tra i tentativi da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="e8954-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="e8954-162">Coefficiente di backoff dell’intervallo tra tentativi: coefficiente utilizzato per calcolare l’intervallo successivo tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="e8954-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="e8954-163">Viene utilizzata la seguente formula: (Intervallo tentativi iniziale) * Math.pow((Coefficiente di backoff dell’intervallo), (Numero di tentativi) - 2).</span><span class="sxs-lookup"><span data-stu-id="e8954-163">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="e8954-164">Numero massimo di tentativi: Il numero massimo di tentativi all'interno di un processo.</span><span class="sxs-lookup"><span data-stu-id="e8954-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="e8954-165">Il criterio di esecuzione predefinito utilizza i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8954-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="e8954-166">Nome: Criterio di esecuzione predefinito</span><span class="sxs-lookup"><span data-stu-id="e8954-166">Name: Default execution policy</span></span>
* <span data-ttu-id="e8954-167">Timeout del processo: 1 settimana</span><span class="sxs-lookup"><span data-stu-id="e8954-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="e8954-168">Intervallo tra tentativi iniziale: 100 millisecondi</span><span class="sxs-lookup"><span data-stu-id="e8954-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="e8954-169">Intervallo massimo tra tentativi: 30 minuti</span><span class="sxs-lookup"><span data-stu-id="e8954-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="e8954-170">Coefficiente di intervallo tra tentativi: 2</span><span class="sxs-lookup"><span data-stu-id="e8954-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="e8954-171">Numero massimo di tentativi: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="e8954-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="e8954-172">Creare il criterio di esecuzione desiderato:</span><span class="sxs-lookup"><span data-stu-id="e8954-172">Create the desired execution policy:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="e8954-173">Aggiornare il criterio di esecuzione personalizzato</span><span class="sxs-lookup"><span data-stu-id="e8954-173">Update a custom execution policy</span></span>
<span data-ttu-id="e8954-174">Aggiornare l'aggiornamento del criterio di esecuzione desiderato:</span><span class="sxs-lookup"><span data-stu-id="e8954-174">Update the desired execution policy to update:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a><span data-ttu-id="e8954-175">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="e8954-175">Cancel a job</span></span>
<span data-ttu-id="e8954-176">I processi di database elastico supportano le richieste di annullamento dei processi.</span><span class="sxs-lookup"><span data-stu-id="e8954-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="e8954-177">Se i processi di database elastici rilevano una richiesta di annullamento per un processo in fase di esecuzione, verrà effettuato un tentativo di arresto del processo.</span><span class="sxs-lookup"><span data-stu-id="e8954-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="e8954-178">E’ possibile cancellare un processo in due modi diversi tramite i processi di database elastici:</span><span class="sxs-lookup"><span data-stu-id="e8954-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="e8954-179">Annullamento delle attività attualmente in esecuzione: se viene rilevato un annullamento mentre un'attività è attualmente in esecuzione, si tenterà di cancellare l’aspetto di esecuzione corrente dell’attività.</span><span class="sxs-lookup"><span data-stu-id="e8954-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="e8954-180">Ad esempio: se viene eseguita una query con esecuzione prolungata quando si tenta di eseguire un annullamento, si verificherà un tentativo di annullare la query.</span><span class="sxs-lookup"><span data-stu-id="e8954-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="e8954-181">Annullamento attività tentativi: Se un annullamento viene rilevato dal thread di controllo prima dell’avvio dell’esecuzione di un'attività, il thread di controllo eviterà l’avvio dell'attività e annullerà la richiesta.</span><span class="sxs-lookup"><span data-stu-id="e8954-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="e8954-182">Se viene richiesto un annullamento del processo per un processo padre, tale richiesta verrà rispettata per il processo padre e per tutti i relativi processi figlio.</span><span class="sxs-lookup"><span data-stu-id="e8954-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="e8954-183">Per inviare una richiesta di annullamento, usare il cmdlet **Stop-AzureSqlJobExecution** e impostare il parametro **JobExecutionId**.</span><span class="sxs-lookup"><span data-stu-id="e8954-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="e8954-184">Eliminare un processo in base al nome e la cronologia del processo</span><span class="sxs-lookup"><span data-stu-id="e8954-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="e8954-185">I processi di database elastici supportano l'eliminazione asincrona dei processi.</span><span class="sxs-lookup"><span data-stu-id="e8954-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="e8954-186">Un processo può essere contrassegnato per l'eliminazione e il sistema lo eliminerà con tutta la relativa cronologia dopo il completamento di tutte le esecuzioni di processo per tale processo.</span><span class="sxs-lookup"><span data-stu-id="e8954-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="e8954-187">Il sistema non annullerà automaticamente le esecuzioni di processo attive.</span><span class="sxs-lookup"><span data-stu-id="e8954-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="e8954-188">Al contrario, è necessario richiamare Stop-AzureSqlJobExecution per annullare le esecuzioni di processo attive.</span><span class="sxs-lookup"><span data-stu-id="e8954-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="e8954-189">Per attivare l'eliminazione di processi, usare il cmdlet **Remove-AzureSqlJob** e impostare il parametro **JobName**.</span><span class="sxs-lookup"><span data-stu-id="e8954-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="e8954-190">Creare una destinazione database personalizzata</span><span class="sxs-lookup"><span data-stu-id="e8954-190">Create a custom database target</span></span>
<span data-ttu-id="e8954-191">Le destinazioni personalizzate per i database possono essere definite nei processi di database elastici che possono essere utilizzati per l'esecuzione diretta o per l'inclusione in un gruppo di database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e8954-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="e8954-192">Poiché i **pool elastici** non sono ancora direttamente supportati tramite le API PowerShell, è sufficiente creare una destinazione database e una destinazione per la raccolta dei database personalizzate che comprenda tutti i database nel pool.</span><span class="sxs-lookup"><span data-stu-id="e8954-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="e8954-193">Impostare le seguenti variabili in modo da riflettere le informazioni desiderate sul database:</span><span class="sxs-lookup"><span data-stu-id="e8954-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="e8954-194">Creare una destinazione per la raccolta dei database personalizzata</span><span class="sxs-lookup"><span data-stu-id="e8954-194">Create a custom database collection target</span></span>
<span data-ttu-id="e8954-195">È possibile definire una destinazione per la raccolta dei database personalizzata per consentire l'esecuzione in più destinazioni dei database definiti.</span><span class="sxs-lookup"><span data-stu-id="e8954-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="e8954-196">Dopo aver creato un gruppo di database, i database possono essere associati alla destinazione della raccolta personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e8954-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="e8954-197">Impostare le seguenti variabili in modo da riflettere la configurazione della destinazione della raccolta personalizzata desiderata:</span><span class="sxs-lookup"><span data-stu-id="e8954-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="e8954-198">Aggiungere database a una destinazione per la raccolta dei database personalizzata</span><span class="sxs-lookup"><span data-stu-id="e8954-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="e8954-199">Le destinazioni di database possono essere associate alle destinazioni delle raccolte di database personalizzate per creare un gruppo di database.</span><span class="sxs-lookup"><span data-stu-id="e8954-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="e8954-200">Ogni volta che viene creato un processo destinato a una destinazione della raccolta di database personalizzata, esso verrà esteso ai database associati al gruppo al momento dell’esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e8954-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="e8954-201">Aggiungere il database desiderato a una raccolta personalizzata specifica:</span><span class="sxs-lookup"><span data-stu-id="e8954-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="e8954-202">Verificare i database in una destinazione per la raccolta dei database personalizzata</span><span class="sxs-lookup"><span data-stu-id="e8954-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="e8954-203">Utilizzare il cmdlet **Get-AzureSqlJobTarget** per recuperare i database figlio all'interno di una destinazione di una raccolta database personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e8954-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="e8954-204">Creare un processo per eseguire uno script in una destinazione di una raccolta database personalizzata</span><span class="sxs-lookup"><span data-stu-id="e8954-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="e8954-205">Utilizzare il cmdlet **New-AzureSqlJob** per creare un processo su un gruppo di database definito da una destinazione di raccolta database personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e8954-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="e8954-206">I processi di database elastici espanderanno il processo in più processi figlio, ognuno corrispondente a un database associato alla destinazione di raccolta database personalizzata e eseguiranno lo script in tutti i database.</span><span class="sxs-lookup"><span data-stu-id="e8954-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="e8954-207">Anche in questo caso, è importante che gli script siano idempotenti per essere flessibili ai tentativi.</span><span class="sxs-lookup"><span data-stu-id="e8954-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="e8954-208">Raccolta dei dati tra database</span><span class="sxs-lookup"><span data-stu-id="e8954-208">Data collection across databases</span></span>
<span data-ttu-id="e8954-209">**Processi di database elastici** supportano l'esecuzione di una query su un gruppo di database e inviano i risultati alla tabella del database specificata.</span><span class="sxs-lookup"><span data-stu-id="e8954-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="e8954-210">E’ possibile eseguire una query sulla tabella dopo aver visualizzato i risultati della query da ciascun database.</span><span class="sxs-lookup"><span data-stu-id="e8954-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="e8954-211">Questo fornisce un meccanismo asincrono per eseguire una query in molti database.</span><span class="sxs-lookup"><span data-stu-id="e8954-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="e8954-212">I casi di errore, come quando ad esempio uno dei database viene reso temporaneamente non disponibile, vengono gestiti automaticamente tramite tentativi.</span><span class="sxs-lookup"><span data-stu-id="e8954-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="e8954-213">La tabella di destinazione specificata verrà creata automaticamente se non esiste ancora una corrispondenza con lo schema del set di risultati restituito.</span><span class="sxs-lookup"><span data-stu-id="e8954-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="e8954-214">Se un'esecuzione di script restituisce più set di risultati, i processi di database elastici invieranno solo il primo risultato alla tabella di destinazione specificata.</span><span class="sxs-lookup"><span data-stu-id="e8954-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="e8954-215">Il seguente script PowerShell consente di eseguire uno script che raccolga i propri risultati in una tabella specificata.</span><span class="sxs-lookup"><span data-stu-id="e8954-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="e8954-216">Questo script presuppone che uno script T-SQL sia stato creato e che restituisca un singolo set di risultati e che una destinazione di raccolta database personalizzata sia stata creata.</span><span class="sxs-lookup"><span data-stu-id="e8954-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="e8954-217">Impostare quanto segue in modo da riflettere lo script, le credenziali e la destinazione di esecuzione desiderati:</span><span class="sxs-lookup"><span data-stu-id="e8954-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="e8954-218">Creare e avviare un processo per scenari di raccolta dati</span><span class="sxs-lookup"><span data-stu-id="e8954-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="e8954-219">Creare una pianificazione per l'esecuzione del processo utilizzando un trigger di processo</span><span class="sxs-lookup"><span data-stu-id="e8954-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="e8954-220">Il seguente script di PowerShell può essere utilizzato per creare una pianificazione ricorrente.</span><span class="sxs-lookup"><span data-stu-id="e8954-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="e8954-221">Questo script usa l'intervallo di minuti, ma New-AzureSqlJobSchedule supporta anche i parametri -DayInterval, -HourInterval, -MonthInterval e -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="e8954-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="e8954-222">Le pianificazioni che vengono eseguite una sola volta possono essere create specificando -OneTime.</span><span class="sxs-lookup"><span data-stu-id="e8954-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="e8954-223">Creare una nuova pianificazione:</span><span class="sxs-lookup"><span data-stu-id="e8954-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="e8954-224">Creare un trigger di processo per eseguire un processo in una pianificazione temporale</span><span class="sxs-lookup"><span data-stu-id="e8954-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="e8954-225">È possibile definire un trigger di processo per eseguire un processo in base a una pianificazione temporale.</span><span class="sxs-lookup"><span data-stu-id="e8954-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="e8954-226">Il seguente script di PowerShell può essere utilizzato per creare un trigger di processo.</span><span class="sxs-lookup"><span data-stu-id="e8954-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="e8954-227">Impostare le seguenti variabili in modo che corrispondano al processo e alla pianificazione desiderati:</span><span class="sxs-lookup"><span data-stu-id="e8954-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="e8954-228">Rimuovere un'associazione pianificata per arrestare l'esecuzione di processo pianificata</span><span class="sxs-lookup"><span data-stu-id="e8954-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="e8954-229">Per sospendere l'esecuzione del processo ricorrente tramite un trigger di processo, è possibile rimuovere il trigger di processo.</span><span class="sxs-lookup"><span data-stu-id="e8954-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="e8954-230">Rimuovere un trigger di processo per arrestare l’esecuzione di un processo in base a una pianificazione mediante il cmdlet **Remove-AzureSqlJobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="e8954-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="e8954-231">Importare i risultati della query database elastica in Excel</span><span class="sxs-lookup"><span data-stu-id="e8954-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="e8954-232">È possibile importare i risultati da di una query a un file di Excel.</span><span class="sxs-lookup"><span data-stu-id="e8954-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="e8954-233">Avviare Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="e8954-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="e8954-234">Individuare il **dati** della barra multifunzione.</span><span class="sxs-lookup"><span data-stu-id="e8954-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="e8954-235">Fare clic su **Da altre origini** e quindi su **Da SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e8954-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importazione di Excel da altre origini](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="e8954-237">In **Connessione guidata dati** digitare le credenziali di accesso e il nome del server.</span><span class="sxs-lookup"><span data-stu-id="e8954-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="e8954-238">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="e8954-238">Then click **Next**.</span></span>
5. <span data-ttu-id="e8954-239">Nella finestra di dialogo **Selezionare il database contenente i dati desiderati** selezionare il database **ElasticDBQuery**.</span><span class="sxs-lookup"><span data-stu-id="e8954-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="e8954-240">Selezionare la tabella **Customers** nella visualizzazione elenco e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e8954-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="e8954-241">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="e8954-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="e8954-242">Nel modulo **Importa dati** in **Specificare come visualizzare i dati nella cartella di lavoro** selezionare **Tabella** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8954-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="e8954-243">Tutte le righe dalla tabella **Clienti** , archiviate in diverse partizioni sono riportate nel foglio Excel.</span><span class="sxs-lookup"><span data-stu-id="e8954-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8954-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8954-244">Next steps</span></span>
<span data-ttu-id="e8954-245">È ora possibile usare le funzioni dei dati di Excel.</span><span class="sxs-lookup"><span data-stu-id="e8954-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="e8954-246">Usare la stringa di connessione con il nome del server, il nome del database e le credenziali per connettere gli strumenti di integrazione e di Business Intelligence al database di query elastico.</span><span class="sxs-lookup"><span data-stu-id="e8954-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="e8954-247">Assicurarsi che SQL Server sia supportato come origine dati per lo strumento.</span><span class="sxs-lookup"><span data-stu-id="e8954-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="e8954-248">Fare riferimento al database di query elastico e alle tabelle esterne come a qualsiasi database di SQL Server e tabella di SQL Server a cui ci si connette con lo strumento.</span><span class="sxs-lookup"><span data-stu-id="e8954-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="e8954-249">Costi</span><span class="sxs-lookup"><span data-stu-id="e8954-249">Cost</span></span>
<span data-ttu-id="e8954-250">L'uso della funzione di query di database elastico non comporta alcun costo aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="e8954-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="e8954-251">In questo momento questa funzionalità è disponibile solo sui database premium come punto finale, tuttavia, le partizioni possono essere di qualsiasi livello di servizio.</span><span class="sxs-lookup"><span data-stu-id="e8954-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="e8954-252">Per informazioni sui prezzi, vedere [Dettagli prezzi del database SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="e8954-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
