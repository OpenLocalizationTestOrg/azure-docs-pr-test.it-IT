---
title: aaaGetting avviato con i processi di database elastico | Documenti Microsoft
description: come i processi di database elastico toouse
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
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="45f7d-103">Introduzione ai processi di Database Elastici</span><span class="sxs-lookup"><span data-stu-id="45f7d-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="45f7d-104">I processi di Database elastici (anteprima) per Database SQL di Azure consente tooreliability eseguire gli script T-SQL che si estendono su più database durante ritentare automaticamente e fornendo l'eventuale completamento garantisce.</span><span class="sxs-lookup"><span data-stu-id="45f7d-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="45f7d-105">Per ulteriori informazioni sulla funzionalità di processo di Database elastico hello, vedere hello [pagina Panoramica della funzionalità](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45f7d-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="45f7d-106">In questo argomento si estende nell'esempio di hello [Introduzione agli strumenti di Database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="45f7d-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="45f7d-107">Al termine, sarà possibile: informazioni su come toocreate e gestire i processi che gestiscono un gruppo di database correlati.</span><span class="sxs-lookup"><span data-stu-id="45f7d-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="45f7d-108">Non è necessario toouse hello scalabilità elastica strumenti vantaggi hello dei processi elastici sfruttare tootake ordine.</span><span class="sxs-lookup"><span data-stu-id="45f7d-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45f7d-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="45f7d-109">Prerequisites</span></span>
<span data-ttu-id="45f7d-110">Scaricare ed eseguire hello [Guida introduttiva a esempio di strumenti di Database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="45f7d-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="45f7d-111">Creare una mappa partizioni gestione tramite app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="45f7d-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="45f7d-112">Di seguito si creerà una mappa partizioni manager insieme a diverse partizioni, seguita dall'inserimento di dati in partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="45f7d-113">Se si dispone già di partizioni di dati partizionati in essi contenuti, è possibile ignorare hello alla procedura seguente e spostare toohello nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="45f7d-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="45f7d-114">Compilare ed eseguire hello **Introduzione agli strumenti di Database elastico** applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="45f7d-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="45f7d-115">Seguire i passaggi di hello fino al passaggio 7 nella sezione hello [scaricare ed eseguire app di esempio hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="45f7d-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="45f7d-116">Al fine di hello del passaggio 7, verrà visualizzato un hello prompt dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="45f7d-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![Aprire il prompt dei comandi.](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="45f7d-118">Nella finestra di comando hello, digitare "1" e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="45f7d-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="45f7d-119">Questo gestore mappe partizioni di hello crea e aggiunge due partizioni toohello server.</span><span class="sxs-lookup"><span data-stu-id="45f7d-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="45f7d-120">Digitare "3" e premere **Invia**. Ripetere l'operazione quattro volte.</span><span class="sxs-lookup"><span data-stu-id="45f7d-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="45f7d-121">Consente di inserire righe di dati di esempio nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="45f7d-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="45f7d-122">Hello [portale Azure](https://portal.azure.com) deve visualizzare tre nuovi database:</span><span class="sxs-lookup"><span data-stu-id="45f7d-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Conferma di Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="45f7d-124">A questo punto, si creerà una raccolta di database personalizzata che riflette tutti i database hello mappa partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="45f7d-125">Questo consente toocreate e di eseguire un processo che aggiunge una nuova tabella tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="45f7d-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="45f7d-126">Di seguito viene in genere creato una destinazione di mappa partizioni, utilizzando hello **New AzureSqlJobTarget** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45f7d-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="45f7d-127">database di gestione della mappa partizioni Hello deve essere impostato come database di destinazione e mappa partizioni specifici hello viene quindi specificata come destinazione.</span><span class="sxs-lookup"><span data-stu-id="45f7d-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="45f7d-128">In alternativa, siamo tooenumerate passare tutti i database hello server hello e aggiungere hello database toohello nuova raccolta personalizzato con l'eccezione di hello del database master.</span><span class="sxs-lookup"><span data-stu-id="45f7d-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="45f7d-129">Crea una raccolta personalizzata e aggiungere tutti i database nella destinazione di una raccolta personalizzata hello server toohello con eccezione hello del database master.</span><span class="sxs-lookup"><span data-stu-id="45f7d-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
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
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="45f7d-130">Creare uno Script T-SQL per l'esecuzione tra database</span><span class="sxs-lookup"><span data-stu-id="45f7d-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="45f7d-131">Creare uno script di hello processo tooexecute in un gruppo personalizzato di hello di database</span><span class="sxs-lookup"><span data-stu-id="45f7d-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="45f7d-132">Eseguire il processo di hello</span><span class="sxs-lookup"><span data-stu-id="45f7d-132">Execute hello job</span></span>
<span data-ttu-id="45f7d-133">Hello lo script di PowerShell seguente può essere utilizzato tooexecute un processo esistente:</span><span class="sxs-lookup"><span data-stu-id="45f7d-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="45f7d-134">Aggiornare hello toohave nome di variabile tooreflect hello desiderato processo eseguito seguenti:</span><span class="sxs-lookup"><span data-stu-id="45f7d-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="45f7d-135">Recuperare lo stato di hello una singola esecuzione dei processi</span><span class="sxs-lookup"><span data-stu-id="45f7d-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="45f7d-136">Utilizzare hello stesso **Get AzureSqlJobExecution** cmdlet con hello **IncludeChildren** parametro tooview hello stato esecuzioni del processo figlio, vale a dire hello stato specifico per ogni esecuzione del processo su ogni database di destinazione dal processo hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="45f7d-137">Stato di visualizzazione hello tra più esecuzioni di processo</span><span class="sxs-lookup"><span data-stu-id="45f7d-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="45f7d-138">Hello **Get AzureSqlJobExecution** cmdlet ha più parametri facoltativi che possono essere utilizzati toodisplay più esecuzioni di processo, filtrate tramite parametri hello fornito.</span><span class="sxs-lookup"><span data-stu-id="45f7d-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="45f7d-139">esempio Hello vengono illustrate alcune delle possibili modi di hello toouse Get AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="45f7d-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="45f7d-140">Recuperare tutte le esecuzioni attive di processo di primo livello:</span><span class="sxs-lookup"><span data-stu-id="45f7d-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="45f7d-141">Recuperare tutte le esecuzioni di processo di primo livello, incluse le esecuzioni di processo inattive:</span><span class="sxs-lookup"><span data-stu-id="45f7d-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="45f7d-142">Recuperare tutte le esecuzioni di processo figlio di un ID di esecuzione processo fornito, incluse le esecuzioni di processo inattive:</span><span class="sxs-lookup"><span data-stu-id="45f7d-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="45f7d-143">Recuperare tutte le esecuzioni di processo create utilizzando una pianificazione / processo di combinazione, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="45f7d-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="45f7d-144">Recuperare tutti i processi destinati a una mappa di partizione specificata, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="45f7d-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="45f7d-145">Recuperare tutti i processi destinati a una raccolta personalizzata specificata, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="45f7d-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="45f7d-146">Recuperare l'elenco di hello di esecuzioni di attività del processo in esecuzione un processo specifico:</span><span class="sxs-lookup"><span data-stu-id="45f7d-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="45f7d-147">Recuperare i dettagli di esecuzione delle attività di processo:</span><span class="sxs-lookup"><span data-stu-id="45f7d-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="45f7d-148">Hello lo script di PowerShell seguente può essere utilizzato tooview hello dettagli di un'esecuzione di attività di processo, è particolarmente utile quando il debug degli errori di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45f7d-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="45f7d-149">Recuperare gli errori all'interno delle esecuzioni delle attività di processo</span><span class="sxs-lookup"><span data-stu-id="45f7d-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="45f7d-150">oggetto JobTaskExecution Hello include una proprietà per hello del ciclo di vita dell'attività hello insieme a una proprietà del messaggio.</span><span class="sxs-lookup"><span data-stu-id="45f7d-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="45f7d-151">Se un'esecuzione di attività del processo non riuscito, hello del ciclo di vita proprietà verrà impostato troppo*Failed* e proprietà del messaggio hello verrà impostato il messaggio di eccezione risultante toohello e il relativo stack.</span><span class="sxs-lookup"><span data-stu-id="45f7d-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="45f7d-152">Se un processo non riuscito, è importante tooview i dettagli di hello delle attività di processo che non è riuscita per un determinato processo.</span><span class="sxs-lookup"><span data-stu-id="45f7d-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="45f7d-153">In attesa di un toocomplete di esecuzione del processo</span><span class="sxs-lookup"><span data-stu-id="45f7d-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="45f7d-154">Hello lo script di PowerShell seguente può essere utilizzato toowait per un toocomplete attività processo:</span><span class="sxs-lookup"><span data-stu-id="45f7d-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="45f7d-155">Creare un criterio di esecuzione personalizzata</span><span class="sxs-lookup"><span data-stu-id="45f7d-155">Create a custom execution policy</span></span>
<span data-ttu-id="45f7d-156">I processi di database elastici supportano la creazione di criteri di esecuzione personalizzati che possono essere applicati all'avvio dei processi.</span><span class="sxs-lookup"><span data-stu-id="45f7d-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="45f7d-157">Criteri di esecuzione che attualmente consentono la definizione di:</span><span class="sxs-lookup"><span data-stu-id="45f7d-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="45f7d-158">Nome: Identificatore per i criteri di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="45f7d-159">Timeout del processo: tempo totale prima che un processo venga annullato dai processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="45f7d-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="45f7d-160">Intervallo tra tentativi iniziale: Intervallo toowait prima del primo nuovo tentativo.</span><span class="sxs-lookup"><span data-stu-id="45f7d-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="45f7d-161">Intervallo tra tentativi massimo: Limite massimo di tentativi intervalli toouse.</span><span class="sxs-lookup"><span data-stu-id="45f7d-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="45f7d-162">Coefficiente di Backoff intervallo tentativi: Coefficiente utilizzato successivo intervallo hello toocalculate tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="45f7d-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="45f7d-163">Hello formula seguente viene utilizzata: (intervallo di tentativi iniziale) * Math.pow (intervallo Backoff coefficiente (), (numero di tentativi) - 2).</span><span class="sxs-lookup"><span data-stu-id="45f7d-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="45f7d-164">Numero massimo di tentativi: hello massimo di ripetizione tentativi tooperform all'interno di un processo.</span><span class="sxs-lookup"><span data-stu-id="45f7d-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="45f7d-165">criteri di esecuzione predefiniti Hello utilizzano hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="45f7d-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="45f7d-166">Nome: Criterio di esecuzione predefinito</span><span class="sxs-lookup"><span data-stu-id="45f7d-166">Name: Default execution policy</span></span>
* <span data-ttu-id="45f7d-167">Timeout del processo: 1 settimana</span><span class="sxs-lookup"><span data-stu-id="45f7d-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="45f7d-168">Intervallo tra tentativi iniziale: 100 millisecondi</span><span class="sxs-lookup"><span data-stu-id="45f7d-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="45f7d-169">Intervallo massimo tra tentativi: 30 minuti</span><span class="sxs-lookup"><span data-stu-id="45f7d-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="45f7d-170">Coefficiente di intervallo tra tentativi: 2</span><span class="sxs-lookup"><span data-stu-id="45f7d-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="45f7d-171">Numero massimo di tentativi: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="45f7d-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="45f7d-172">Creare criteri di esecuzione hello desiderato:</span><span class="sxs-lookup"><span data-stu-id="45f7d-172">Create hello desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="45f7d-173">Aggiornare il criterio di esecuzione personalizzato</span><span class="sxs-lookup"><span data-stu-id="45f7d-173">Update a custom execution policy</span></span>
<span data-ttu-id="45f7d-174">Aggiornare tooupdate criteri di esecuzione hello desiderato:</span><span class="sxs-lookup"><span data-stu-id="45f7d-174">Update hello desired execution policy tooupdate:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="45f7d-175">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="45f7d-175">Cancel a job</span></span>
<span data-ttu-id="45f7d-176">I processi di database elastico supportano le richieste di annullamento dei processi.</span><span class="sxs-lookup"><span data-stu-id="45f7d-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="45f7d-177">Se i processi di Database elastico rileva una richiesta di annullamento per un processo in fase di esecuzione, verrà eseguito un tentativo con il processo di hello toostop.</span><span class="sxs-lookup"><span data-stu-id="45f7d-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="45f7d-178">E’ possibile cancellare un processo in due modi diversi tramite i processi di database elastici:</span><span class="sxs-lookup"><span data-stu-id="45f7d-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="45f7d-179">L'annullamento attualmente in esecuzione attività: se un annullamento viene rilevato durante un'attività è attualmente in esecuzione, verrà tentato un annullamento all'interno di hello aspetto dell'attività hello attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45f7d-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="45f7d-180">Ad esempio: se è presente una query a lunga esecuzione viene eseguita quando viene eseguito un tentativo di annullamento, sarà presente una query di hello toocancel tentativo.</span><span class="sxs-lookup"><span data-stu-id="45f7d-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="45f7d-181">Annullamento tentativi dell'attività: Se un annullamento viene rilevato dal thread di controllo hello prima di un'attività viene avviata per l'esecuzione, hello controllo thread evitare avvio attività hello e dichiarare richiesta hello come annullata.</span><span class="sxs-lookup"><span data-stu-id="45f7d-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="45f7d-182">Se è richiesto un annullamento di processo per un processo padre, la richiesta di annullamento hello sarà rispettata per il processo padre hello e per tutti i relativi processi figlio.</span><span class="sxs-lookup"><span data-stu-id="45f7d-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="45f7d-183">toosubmit una richiesta di annullamento, utilizzare hello **Stop AzureSqlJobExecution** cmdlet e set hello **JobExecutionId** parametro.</span><span class="sxs-lookup"><span data-stu-id="45f7d-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="45f7d-184">Eliminare un processo in base al nome e la cronologia del processo di hello</span><span class="sxs-lookup"><span data-stu-id="45f7d-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="45f7d-185">I processi di database elastici supportano l'eliminazione asincrona dei processi.</span><span class="sxs-lookup"><span data-stu-id="45f7d-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="45f7d-186">Un processo può essere contrassegnato per l'eliminazione e sistema hello eliminerà processo hello e tutta la relativa cronologia processo dopo aver completato tutte le esecuzioni di processo per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="45f7d-187">sistema Hello non annullerà automaticamente le esecuzioni di processo attivo.</span><span class="sxs-lookup"><span data-stu-id="45f7d-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="45f7d-188">Invece, Stop-AzureSqlJobExecution deve essere richiamato toocancel esecuzioni di processi attivi.</span><span class="sxs-lookup"><span data-stu-id="45f7d-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="45f7d-189">l'eliminazione di processo tootrigger, utilizzare hello **Remove AzureSqlJob** cmdlet e set hello **JobName** parametro.</span><span class="sxs-lookup"><span data-stu-id="45f7d-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="45f7d-190">Creare una destinazione database personalizzata</span><span class="sxs-lookup"><span data-stu-id="45f7d-190">Create a custom database target</span></span>
<span data-ttu-id="45f7d-191">Le destinazioni personalizzate per i database possono essere definite nei processi di database elastici che possono essere utilizzati per l'esecuzione diretta o per l'inclusione in un gruppo di database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="45f7d-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="45f7d-192">Poiché **pool elastici** non sono ancora direttamente supportate tramite hello APIs di PowerShell, sufficiente creare un personalizzati database di destinazione e la destinazione della raccolta di database personalizzata che comprende tutti i database nel pool di hello hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="45f7d-193">Impostare le seguenti variabili tooreflect hello desiderato database informazioni hello:</span><span class="sxs-lookup"><span data-stu-id="45f7d-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="45f7d-194">Creare una destinazione per la raccolta dei database personalizzata</span><span class="sxs-lookup"><span data-stu-id="45f7d-194">Create a custom database collection target</span></span>
<span data-ttu-id="45f7d-195">Una destinazione di raccolta database personalizzato può essere definito tooenable esecuzione tra più destinazioni definita per il database.</span><span class="sxs-lookup"><span data-stu-id="45f7d-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="45f7d-196">Dopo aver creato un gruppo di database, database possono essere destinazione di raccolta personalizzato toohello associato.</span><span class="sxs-lookup"><span data-stu-id="45f7d-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="45f7d-197">Impostare hello seguente configurazione di destinazione di variabili tooreflect hello raccolta personalizzata desiderata:</span><span class="sxs-lookup"><span data-stu-id="45f7d-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="45f7d-198">Aggiungere database tooa personalizzato database raccolta di destinazione</span><span class="sxs-lookup"><span data-stu-id="45f7d-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="45f7d-199">Destinazioni di database possono essere associate a un database personalizzato insieme destinazioni toocreate un gruppo di database.</span><span class="sxs-lookup"><span data-stu-id="45f7d-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="45f7d-200">Ogni volta che viene creato un processo che è associata una destinazione di raccolta di database personalizzati, sarà espanso tootarget hello database toohello associato gruppo in fase di esecuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="45f7d-201">Aggiungere la raccolta personalizzata specifica tooa hello desiderato database:</span><span class="sxs-lookup"><span data-stu-id="45f7d-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="45f7d-202">Esaminare i database hello all'interno di una destinazione di raccolta di database personalizzati</span><span class="sxs-lookup"><span data-stu-id="45f7d-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="45f7d-203">Hello utilizzare **Get AzureSqlJobTarget** database di cmdlet tooretrieve hello figlio all'interno di una destinazione di raccolta database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="45f7d-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="45f7d-204">Creare un processo tooexecute uno script per una destinazione di raccolta database personalizzato</span><span class="sxs-lookup"><span data-stu-id="45f7d-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="45f7d-205">Hello utilizzare **New AzureSqlJob** toocreate cmdlet un processo rispetto a un gruppo di database definiti da una destinazione di raccolta database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="45f7d-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="45f7d-206">I processi di Database elastici espanderà processo hello in più processi figlio, ogni database tooa corrispondente associata alla destinazione di raccolta di database personalizzata hello e assicurarsi che viene eseguito lo script di hello in tutti i database.</span><span class="sxs-lookup"><span data-stu-id="45f7d-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="45f7d-207">Nuovamente, è importante che gli script siano idempotenti toobe resilienti tooretries.</span><span class="sxs-lookup"><span data-stu-id="45f7d-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="45f7d-208">Raccolta dei dati tra database</span><span class="sxs-lookup"><span data-stu-id="45f7d-208">Data collection across databases</span></span>
<span data-ttu-id="45f7d-209">**I processi di Database elastici** supporta l'esecuzione di una query in un gruppo di database e lo invia tabella hello risultati tooa del database specificato.</span><span class="sxs-lookup"><span data-stu-id="45f7d-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="45f7d-210">è possibile eseguire query di tabella Hello dopo i risultati della query di hello fatti toosee hello da ogni database.</span><span class="sxs-lookup"><span data-stu-id="45f7d-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="45f7d-211">Ciò rende disponibile un tooexecute meccanismo asincrona una query tra molti database.</span><span class="sxs-lookup"><span data-stu-id="45f7d-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="45f7d-212">Casi di errore, ad esempio uno dei database hello temporaneamente non disponibile vengono gestiti automaticamente tramite tentativi.</span><span class="sxs-lookup"><span data-stu-id="45f7d-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="45f7d-213">tabella di destinazione specificato Hello verrà creata automaticamente se non esiste ancora, schema hello corrispondente di hello restituiti set di risultati.</span><span class="sxs-lookup"><span data-stu-id="45f7d-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="45f7d-214">Se un'esecuzione di script restituisce più set di risultati, i processi di Database elastico invierà hello prima uno toohello fornito tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="45f7d-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="45f7d-215">Hello lo script di PowerShell seguente può essere utilizzato tooexecute uno script di raccogliere i risultati in una tabella specificata.</span><span class="sxs-lookup"><span data-stu-id="45f7d-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="45f7d-216">Questo script presuppone che uno script T-SQL sia stato creato e che restituisca un singolo set di risultati e che una destinazione di raccolta database personalizzata sia stata creata.</span><span class="sxs-lookup"><span data-stu-id="45f7d-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="45f7d-217">Impostare hello seguenti script hello desiderato tooreflect, credenziali e destinazione di esecuzione:</span><span class="sxs-lookup"><span data-stu-id="45f7d-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="45f7d-218">Creare e avviare un processo per scenari di raccolta dati</span><span class="sxs-lookup"><span data-stu-id="45f7d-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="45f7d-219">Creare una pianificazione per l'esecuzione del processo utilizzando un trigger di processo</span><span class="sxs-lookup"><span data-stu-id="45f7d-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="45f7d-220">Hello lo script di PowerShell seguente può essere utilizzato toocreate una pianificazione ricorrente.</span><span class="sxs-lookup"><span data-stu-id="45f7d-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="45f7d-221">Questo script usa l'intervallo di minuti, ma New-AzureSqlJobSchedule supporta anche i parametri -DayInterval, -HourInterval, -MonthInterval e -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="45f7d-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="45f7d-222">Le pianificazioni che vengono eseguite una sola volta possono essere create specificando -OneTime.</span><span class="sxs-lookup"><span data-stu-id="45f7d-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="45f7d-223">Creare una nuova pianificazione:</span><span class="sxs-lookup"><span data-stu-id="45f7d-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="45f7d-224">Creare un processo eseguito su una pianificazione temporale di un toohave trigger di processo</span><span class="sxs-lookup"><span data-stu-id="45f7d-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="45f7d-225">Un trigger di processo può essere definito toohave un processo eseguito in base tooa tempo di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="45f7d-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="45f7d-226">Hello lo script di PowerShell seguente può essere utilizzato toocreate un trigger di processo.</span><span class="sxs-lookup"><span data-stu-id="45f7d-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="45f7d-227">Hello set seguenti variabili toocorrespond toohello desiderato processo e pianificazione:</span><span class="sxs-lookup"><span data-stu-id="45f7d-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="45f7d-228">Rimuovere un processo di toostop associazione pianificata l'esecuzione su pianificazione</span><span class="sxs-lookup"><span data-stu-id="45f7d-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="45f7d-229">esecuzione del processo tramite un trigger di processo, il trigger di processo hello ripresenta toodiscontinue può essere rimosso.</span><span class="sxs-lookup"><span data-stu-id="45f7d-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="45f7d-230">Rimuovere un toostop trigger di processo un processo venga eseguito secondo pianificazione tooa utilizzando hello **Remove AzureSqlJobTrigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45f7d-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="45f7d-231">Importare tooExcel risultati query di database elastico</span><span class="sxs-lookup"><span data-stu-id="45f7d-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="45f7d-232">È possibile importare i risultati di hello da di un file di Excel tooan query.</span><span class="sxs-lookup"><span data-stu-id="45f7d-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="45f7d-233">Avviare Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="45f7d-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="45f7d-234">Passare toohello **dati** della barra multifunzione.</span><span class="sxs-lookup"><span data-stu-id="45f7d-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="45f7d-235">Fare clic su **Da altre origini** e quindi su **Da SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="45f7d-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importazione di Excel da altre origini](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="45f7d-237">In hello **connessione guidata dati** digitare le credenziali di nome e l'account di accesso server hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="45f7d-238">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="45f7d-238">Then click **Next**.</span></span>
5. <span data-ttu-id="45f7d-239">Nella finestra di dialogo hello **database selezionare hello che contiene dati hello da**selezionare hello **ElasticDBQuery** database.</span><span class="sxs-lookup"><span data-stu-id="45f7d-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="45f7d-240">Seleziona hello **clienti** tabella nella visualizzazione elenco hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="45f7d-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="45f7d-241">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="45f7d-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="45f7d-242">In hello **l'importazione dei dati** del modulo **selezionare la modalità tooview questi dati nella cartella di lavoro**selezionare **tabella** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="45f7d-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="45f7d-243">Tutte le righe di hello **clienti** tabella, archiviata in partizioni diverse popolare un foglio di Excel hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45f7d-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45f7d-244">Next steps</span></span>
<span data-ttu-id="45f7d-245">È ora possibile usare le funzioni dei dati di Excel.</span><span class="sxs-lookup"><span data-stu-id="45f7d-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="45f7d-246">Utilizzare la stringa di connessione hello con il nome del server, nome del database e le credenziali di BI e dati integrazione strumenti toohello elastico query database tooconnect.</span><span class="sxs-lookup"><span data-stu-id="45f7d-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="45f7d-247">Assicurarsi che SQL Server sia supportato come origine dati per lo strumento.</span><span class="sxs-lookup"><span data-stu-id="45f7d-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="45f7d-248">Fare riferimento a database elastico query toohello e le tabelle esterne come qualsiasi altro database di SQL Server e le tabelle di SQL Server si connetterà toowith lo strumento.</span><span class="sxs-lookup"><span data-stu-id="45f7d-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="45f7d-249">Costi</span><span class="sxs-lookup"><span data-stu-id="45f7d-249">Cost</span></span>
<span data-ttu-id="45f7d-250">Non è senza costi aggiuntivi per l'utilizzo di funzionalità di query di Database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="45f7d-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="45f7d-251">In questo momento questa funzionalità è disponibile solo per i database premium come un punto finale, tuttavia, le partizioni hello possono essere di qualsiasi livello di servizio.</span><span class="sxs-lookup"><span data-stu-id="45f7d-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="45f7d-252">Per informazioni sui prezzi, vedere [Dettagli prezzi del database SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="45f7d-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
