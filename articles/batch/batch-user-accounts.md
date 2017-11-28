---
title: "attività aaaRun con account utente di Azure Batch | Documenti Microsoft"
description: "Configurare gli account utente per l'esecuzione di attività in Azure Batch"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="452af-103">Eseguire attività con account utente in Batch</span><span class="sxs-lookup"><span data-stu-id="452af-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="452af-104">In Azure Batch un'attività viene sempre eseguita con un account utente.</span><span class="sxs-lookup"><span data-stu-id="452af-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="452af-105">Per impostazione predefinita, le attività vengono eseguite con account utente standard, senza le autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="452af-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="452af-106">perché le impostazioni predefinite dell'account utente in genere sono sufficienti.</span><span class="sxs-lookup"><span data-stu-id="452af-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="452af-107">Per alcuni scenari, tuttavia, è account utente di toobe utile tooconfigure in grado di hello in cui si desidera un toorun di attività.</span><span class="sxs-lookup"><span data-stu-id="452af-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="452af-108">In questo articolo vengono descritti tipi di hello degli account utente e come è possibile configurare per il proprio scenario.</span><span class="sxs-lookup"><span data-stu-id="452af-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="452af-109">Tipi di account utente</span><span class="sxs-lookup"><span data-stu-id="452af-109">Types of user accounts</span></span>

<span data-ttu-id="452af-110">Azure Batch offre due tipi di account utente per l'esecuzione di attività:</span><span class="sxs-lookup"><span data-stu-id="452af-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="452af-111">**Account utente automatici.**</span><span class="sxs-lookup"><span data-stu-id="452af-111">**Auto-user accounts.**</span></span> <span data-ttu-id="452af-112">Gli account utente di auto sono account utente predefiniti che vengono creati automaticamente dal servizio Batch hello.</span><span class="sxs-lookup"><span data-stu-id="452af-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="452af-113">Per impostazione predefinita, le attività vengono eseguite con un account utente automatico.</span><span class="sxs-lookup"><span data-stu-id="452af-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="452af-114">È possibile configurare una specifica di auto-utente hello per tooindicate un'attività in cui auto-l'utente deve essere eseguito account un'attività.</span><span class="sxs-lookup"><span data-stu-id="452af-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="452af-115">Specifica di auto-utente Hello permette di livello l'elevazione dei privilegi di toospecify hello e l'ambito dell'account utente automatica hello che verrà eseguita l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="452af-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="452af-116">**Account utente non anonimi.**</span><span class="sxs-lookup"><span data-stu-id="452af-116">**A named user account.**</span></span> <span data-ttu-id="452af-117">Quando si crea il pool di hello, è possibile specificare uno o più account utente denominato per un pool.</span><span class="sxs-lookup"><span data-stu-id="452af-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="452af-118">Ogni account utente viene creato in ogni nodo del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="452af-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="452af-119">Toohello inoltre il nome account, specificare password dell'account utente hello, elevazione livello e, per il pool di Linux, la chiave privata SSH hello.</span><span class="sxs-lookup"><span data-stu-id="452af-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="452af-120">Quando si aggiunge un'attività, è possibile specificare l'account utente in cui eseguire l'attività denominata hello.</span><span class="sxs-lookup"><span data-stu-id="452af-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="452af-121">versione del servizio Batch Hello 2017-01-01.4.0 introduce una modifica che è necessario aggiornare il codice toocall tale versione.</span><span class="sxs-lookup"><span data-stu-id="452af-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="452af-122">Nel caso di migrazione del codice da una versione precedente di Batch, si noti che hello **runElevated** proprietà non è più supportata nelle librerie client API REST o un Batch di hello.</span><span class="sxs-lookup"><span data-stu-id="452af-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="452af-123">Hello utilizzare nuovo **userIdentity** proprietà di un livello di attività toospecify l'elevazione dei privilegi.</span><span class="sxs-lookup"><span data-stu-id="452af-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="452af-124">Vedere hello sezione [aggiornare la libreria client di Batch della versione più recente di codice toohello](#update-your-code-to-the-latest-batch-client-library) per le linee guida rapide per l'aggiornamento del codice Batch se si utilizza una delle librerie client hello.</span><span class="sxs-lookup"><span data-stu-id="452af-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="452af-125">gli account utente di Hello descritti in questo articolo supporta Remote Desktop Protocol (RDP) o Secure Shell (SSH), per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="452af-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="452af-126">tooconnect tooa nodo in esecuzione hello Linux configurazione della macchina virtuale tramite SSH, vedere [tooa utilizzo remoto del Desktop Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="452af-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="452af-127">toonodes tooconnect che esegue Windows tramite RDP, vedere [connessione macchina virtuale Windows Server tooa](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="452af-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="452af-128">tooconnect tooa nodo in esecuzione hello configurazione del servizio cloud tramite RDP, vedere [abilitare connessione Desktop remoto per un ruolo in servizi Cloud di Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="452af-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="452af-129">Directory e toofiles di accesso di account utente</span><span class="sxs-lookup"><span data-stu-id="452af-129">User account access toofiles and directories</span></span>

<span data-ttu-id="452af-130">Un account utente di auto sia un account utente denominato avere la directory di lavoro dell'attività di lettura/scrittura accesso toohello directory condivisa e directory di multi-istanza attività.</span><span class="sxs-lookup"><span data-stu-id="452af-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="452af-131">Entrambi i tipi di account dispone di accesso in lettura toohello avvio e processo di preparazione directory.</span><span class="sxs-lookup"><span data-stu-id="452af-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="452af-132">Se un'attività viene eseguito con hello stesso account utilizzato per l'esecuzione di un'attività di avvio, l'attività hello ha accesso in lettura-scrittura toohello inizio attività directory.</span><span class="sxs-lookup"><span data-stu-id="452af-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="452af-133">Analogamente, se un'attività viene eseguito con hello stesso account utilizzato per l'esecuzione di un'attività di preparazione del processo, l'attività hello è directory attività di accesso in lettura-scrittura toohello processo preparazione.</span><span class="sxs-lookup"><span data-stu-id="452af-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="452af-134">Se un'attività viene eseguito con un account diverso di attività di avvio hello o attività di preparazione del processo, attività hello è solo l'accesso in lettura toohello rispettive directory.</span><span class="sxs-lookup"><span data-stu-id="452af-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="452af-135">Per altre informazioni sull'accesso a file e directory da parte un'attività, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="452af-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="452af-136">Accesso con privilegi elevati per le attività</span><span class="sxs-lookup"><span data-stu-id="452af-136">Elevated access for tasks</span></span> 

<span data-ttu-id="452af-137">livello di elevazione dei privilegi dell'account utente di Hello indica se un'attività viene eseguito l'accesso con privilegi elevato.</span><span class="sxs-lookup"><span data-stu-id="452af-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="452af-138">Un account utente automatico e un account utente non anonimo consentono entrambi l'accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="452af-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="452af-139">sono Hello due opzioni per il livello di elevazione dei privilegi:</span><span class="sxs-lookup"><span data-stu-id="452af-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="452af-140">**NonAdmin:** hello attività viene eseguita come utente standard senza accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="452af-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="452af-141">livello di elevazione Hello predefinito per un account utente di Batch è sempre **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="452af-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="452af-142">**Amministratore:** hello attività in esecuzione come utente con accesso con privilegi elevati e funziona con le autorizzazioni di amministratore complete.</span><span class="sxs-lookup"><span data-stu-id="452af-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="452af-143">Account utente automatici</span><span class="sxs-lookup"><span data-stu-id="452af-143">Auto-user accounts</span></span>

<span data-ttu-id="452af-144">Per impostazione predefinita, in Batch le attività vengono eseguite con un account utente automatico, come utente standard senza accesso con privilegi elevati e con un ambito di attività.</span><span class="sxs-lookup"><span data-stu-id="452af-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="452af-145">Quando si specifica auto utente hello è configurato per l'ambito di attività, il servizio di Batch hello crea un account utente automatica per l'attività solo.</span><span class="sxs-lookup"><span data-stu-id="452af-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="452af-146">ambito tootask alternativo Hello è ambito pool.</span><span class="sxs-lookup"><span data-stu-id="452af-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="452af-147">Quando si specifica auto utente hello per un'attività è configurata per l'ambito di pool, attività hello viene eseguito con un account utente automaticamente attività tooany disponibile nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="452af-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="452af-148">Per ulteriori informazioni sull'ambito di pool, vedere sezione hello [eseguire un'attività come hello auto-utente con ambito pool](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="452af-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="452af-149">ambito predefinito Hello è diversa per i nodi Windows e Linux:</span><span class="sxs-lookup"><span data-stu-id="452af-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="452af-150">Nei nodi Windows le attività vengono eseguite nell'ambito di attività per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="452af-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="452af-151">I nodi Linux vengono sempre eseguiti nell'ambito di pool.</span><span class="sxs-lookup"><span data-stu-id="452af-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="452af-152">Esistono quattro possibili configurazioni per la specifica di auto-utente hello, ognuno dei quali corrisponde account utente univoco automatica tooa:</span><span class="sxs-lookup"><span data-stu-id="452af-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="452af-153">Accesso senza privilegi di amministratore con ambito di attività (specifica di auto-utente hello predefinita)</span><span class="sxs-lookup"><span data-stu-id="452af-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="452af-154">Accesso con privilegi di amministratore (elevati) con ambito di attività</span><span class="sxs-lookup"><span data-stu-id="452af-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="452af-155">Accesso senza privilegi di amministratore con ambito di pool</span><span class="sxs-lookup"><span data-stu-id="452af-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="452af-156">Accesso con privilegi di amministratore con ambito di pool</span><span class="sxs-lookup"><span data-stu-id="452af-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="452af-157">Attività in esecuzione nell'ambito di attività non è di fatto accesso tooother attività in un nodo.</span><span class="sxs-lookup"><span data-stu-id="452af-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="452af-158">Tuttavia, un utente malintenzionato con account di accesso toohello potrebbe aggirare questa restrizione inviando un'attività che viene eseguito con privilegi di amministratore e accede alle altre directory di attività.</span><span class="sxs-lookup"><span data-stu-id="452af-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="452af-159">Un utente malintenzionato può anche usare RDP o SSH nodo tooa tooconnect.</span><span class="sxs-lookup"><span data-stu-id="452af-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="452af-160">È importante tooprotect accesso tooyour Batch account chiavi tooprevent tale scenario.</span><span class="sxs-lookup"><span data-stu-id="452af-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="452af-161">Se si ritiene che l'account sia stato compromesso, essere tooregenerate che le chiavi.</span><span class="sxs-lookup"><span data-stu-id="452af-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="452af-162">Eseguire un'attività come utente automatico con accesso con privilegi elevati</span><span class="sxs-lookup"><span data-stu-id="452af-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="452af-163">Quando è necessario toorun un'attività con accesso con privilegi elevati, è possibile configurare specifica di auto-utente hello per i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="452af-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="452af-164">Ad esempio, un'attività di avvio potrebbe essere necessario software tooinstall di accesso con privilegi elevati nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="452af-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="452af-165">In generale, è consigliabile toouse solo quando è necessario l'accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="452af-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="452af-166">È consigliabile concedere hello con privilegi minimi necessari tooachieve hello il risultato desiderato.</span><span class="sxs-lookup"><span data-stu-id="452af-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="452af-167">Ad esempio, se un'attività di avvio consente di installare software per l'utente corrente di hello, anziché per tutti gli utenti, potrebbe essere in grado di tooavoid concessione dell'accesso con privilegi elevati tootasks.</span><span class="sxs-lookup"><span data-stu-id="452af-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="452af-168">È possibile configurare una specifica di auto-utente hello per l'accesso di ambito e l'utente non amministratore pool per tutte le attività che è necessario toorun in hello stesso account, inclusi hello attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="452af-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="452af-169">Hello frammenti di codice seguente mostra come tooconfigure hello specifica auto-utente.</span><span class="sxs-lookup"><span data-stu-id="452af-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="452af-170">esempi di Hello impostano il livello di elevazione hello troppo`Admin` e hello ambito troppo`Task`.</span><span class="sxs-lookup"><span data-stu-id="452af-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="452af-171">Ambito di attività è l'impostazione predefinita di hello, ma è incluso qui per i migliori risultati hello di esempio.</span><span class="sxs-lookup"><span data-stu-id="452af-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="452af-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="452af-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="452af-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="452af-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="452af-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="452af-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="452af-175">Eseguire un'attività come utente automatico con ambito di pool</span><span class="sxs-lookup"><span data-stu-id="452af-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="452af-176">Quando viene eseguito il provisioning di un nodo, vengono creati due pool a livello di auto-account di ogni nodo nel pool di hello, con accesso con privilegi elevati e senza l'accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="452af-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="452af-177">L'impostazione di ambito di toopool ambito hello automatica dell'utente per una determinata attività esegue l'attività di hello in uno di questi due pool a livello di auto-account.</span><span class="sxs-lookup"><span data-stu-id="452af-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="452af-178">Quando si specifica l'ambito di pool per hello. auto-utente, tutte le attività eseguite con privilegi di amministratore eseguiti hello stesso account utente con livello di pool automatico.</span><span class="sxs-lookup"><span data-stu-id="452af-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="452af-179">In modo analogo, le attività eseguite senza privilegi di amministratore vengono eseguite anche con un unico account utente automatico a livello di pool.</span><span class="sxs-lookup"><span data-stu-id="452af-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="452af-180">Hello due pool a livello di auto-account sono account distinti.</span><span class="sxs-lookup"><span data-stu-id="452af-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="452af-181">Attività in esecuzione con account di amministrazione a livello di pool di hello non possono condividere dati con attività in esecuzione con account standard hello e viceversa.</span><span class="sxs-lookup"><span data-stu-id="452af-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="452af-182">Hello toorunning vantaggio in hello stesso account utente di auto è che le attività sono in grado di tooshare dati con altre attività in esecuzione su hello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="452af-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="452af-183">La condivisione di informazioni riservate tra le attività è uno scenario in cui è utile l'esecuzione di attività con uno degli account utente a livello di pool automatico hello due.</span><span class="sxs-lookup"><span data-stu-id="452af-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="452af-184">Si supponga, ad esempio, che un'attività di avvio deve tooprovision una chiave privata nel nodo hello che è possibile utilizzare altre attività.</span><span class="sxs-lookup"><span data-stu-id="452af-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="452af-185">È possibile utilizzare Data Protection API (DPAPI) di Windows hello, ma richiede privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="452af-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="452af-186">In alternativa, è possibile proteggere segreto hello a livello di utente hello.</span><span class="sxs-lookup"><span data-stu-id="452af-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="452af-187">Attività in esecuzione in hello stesso account utente potrà accedere hello segreto senza accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="452af-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="452af-188">Condividere un altro scenario in cui può essere toorun attività con un account utente automatica con ambito di pool è un file di interfaccia MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="452af-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="452af-189">Una condivisione di file MPI è utile quando i nodi hello hello MPI attività necessità toowork su hello stessi dati di file.</span><span class="sxs-lookup"><span data-stu-id="452af-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="452af-190">nodo head Hello crea una condivisione file che i nodi figlio di hello possono accedere se sono in esecuzione con hello stesso account utente di auto.</span><span class="sxs-lookup"><span data-stu-id="452af-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="452af-191">Hello seguente frammento di codice imposta ambito di toopool ambito hello automatica dell'utente per un'attività in .NET per Batch.</span><span class="sxs-lookup"><span data-stu-id="452af-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="452af-192">livello di elevazione Hello viene omesso, viene eseguito attività hello hello standard a livello di pool di auto-account di.</span><span class="sxs-lookup"><span data-stu-id="452af-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="452af-193">Account utente non anonimi</span><span class="sxs-lookup"><span data-stu-id="452af-193">Named user accounts</span></span>

<span data-ttu-id="452af-194">Quando si crea un pool, è possibile definire gli account utente non anonimi.</span><span class="sxs-lookup"><span data-stu-id="452af-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="452af-195">A un account utente non anonimo sono associati un nome e una password definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="452af-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="452af-196">È possibile specificare il livello di elevazione hello per un account utente denominato.</span><span class="sxs-lookup"><span data-stu-id="452af-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="452af-197">Per i nodi Linux, è anche possibile specificare una chiave privata SSH.</span><span class="sxs-lookup"><span data-stu-id="452af-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="452af-198">Esiste un account utente denominato su tutti i nodi nel pool di hello e tooall disponibili attività è in esecuzione su tali nodi.</span><span class="sxs-lookup"><span data-stu-id="452af-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="452af-199">In un pool è possibile definire un numero qualsiasi di utenti non anonimi.</span><span class="sxs-lookup"><span data-stu-id="452af-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="452af-200">Quando si aggiunge un'attività o un insieme di attività, è possibile specificare che tale attività hello viene eseguito con uno degli account utente definito nel pool di hello denominato hello.</span><span class="sxs-lookup"><span data-stu-id="452af-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="452af-201">Un account utente denominato è utile quando si desidera toorun tutte le attività in un processo in hello stesso account utente isolandoli l'uno dall'attività in esecuzione in altri processi in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="452af-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="452af-202">È possibile ad esempio creare un utente non anonimo per ogni processo ed eseguire le attività di ogni processo con tale account.</span><span class="sxs-lookup"><span data-stu-id="452af-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="452af-203">Ogni processo può condividere un segreto con le proprie attività, ma non con attività in esecuzione in altri processi.</span><span class="sxs-lookup"><span data-stu-id="452af-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="452af-204">È anche possibile utilizzare un toorun di account utente non anonimo un'attività che imposta le autorizzazioni per le risorse esterne, ad esempio condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="452af-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="452af-205">Con un account utente non anonimo, controllare l'identità utente hello si può utilizzare tale autorizzazioni tooset di identità utente.</span><span class="sxs-lookup"><span data-stu-id="452af-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="452af-206">Gli account utente non anonimi consentono di abilitare il protocollo SSH senza password tra i nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="452af-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="452af-207">È possibile utilizzare un account utente denominato con nodi di Linux che richiedono attività di multi-istanza toorun.</span><span class="sxs-lookup"><span data-stu-id="452af-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="452af-208">Ogni nodo nel pool di hello può eseguire attività con un account utente definito nel pool intero hello.</span><span class="sxs-lookup"><span data-stu-id="452af-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="452af-209">Per ulteriori informazioni sulle attività di più istanze, vedere [utilizzare più\-istanza attività applicazioni MPI toorun](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="452af-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="452af-210">Creare account utente non anonimi</span><span class="sxs-lookup"><span data-stu-id="452af-210">Create named user accounts</span></span>

<span data-ttu-id="452af-211">toocreate denominato gli account utente in Batch, aggiungere una raccolta di pool di toohello gli account utente.</span><span class="sxs-lookup"><span data-stu-id="452af-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="452af-212">Hello frammenti di codice seguenti mostrano come toocreate denominati account utente in .NET, Java e Python.</span><span class="sxs-lookup"><span data-stu-id="452af-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="452af-213">Questi codice frammenti di codice mostra come toocreate sia e gli account in un pool denominato non amministratore.</span><span class="sxs-lookup"><span data-stu-id="452af-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="452af-214">esempi di Hello creano pool utilizzando hello configurazione del servizio cloud, ma è utilizzare hello stesso approccio quando si crea un pool di Windows o Linux utilizzando la configurazione della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="452af-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="452af-215">Esempio per Batch .NET (Windows)</span><span class="sxs-lookup"><span data-stu-id="452af-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="452af-216">Esempio per Batch .NET (Linux)</span><span class="sxs-lookup"><span data-stu-id="452af-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="452af-217">Esempio per Batch Java</span><span class="sxs-lookup"><span data-stu-id="452af-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="452af-218">Esempio per Batch Python</span><span class="sxs-lookup"><span data-stu-id="452af-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="452af-219">Eseguire un'attività con un account utente non anonimo con accesso con privilegi elevati</span><span class="sxs-lookup"><span data-stu-id="452af-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="452af-220">toorun un'attività come del utente con privilegi elevati, set di attività di hello **UserIdentity** tooa proprietà denominato account utente che è stato creato con il relativo **ElevationLevel** impostata troppo`Admin`.</span><span class="sxs-lookup"><span data-stu-id="452af-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="452af-221">Questo frammento di codice specifica che attività hello deve essere eseguito con un account utente non anonimo.</span><span class="sxs-lookup"><span data-stu-id="452af-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="452af-222">Questo account utente non anonimo è stato definito nel pool di hello quando è stato creato il pool di hello.</span><span class="sxs-lookup"><span data-stu-id="452af-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="452af-223">In questo caso, hello denominato account utente è stato creato con le autorizzazioni di amministratore:</span><span class="sxs-lookup"><span data-stu-id="452af-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="452af-224">Aggiornare la libreria client di Batch della versione più recente di codice toohello</span><span class="sxs-lookup"><span data-stu-id="452af-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="452af-225">versione del servizio Batch Hello 2017-01-01.4.0 introduce una modifica di rilievo, sostituendo hello **runElevated** proprietà disponibili nelle versioni precedenti con hello **userIdentity** proprietà.</span><span class="sxs-lookup"><span data-stu-id="452af-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="452af-226">Hello le tabelle seguenti fornisce una semplice mapping che è possibile utilizzare tooupdate il codice da versioni precedenti di librerie client hello.</span><span class="sxs-lookup"><span data-stu-id="452af-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="452af-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="452af-227">Batch .NET</span></span>

| <span data-ttu-id="452af-228">Versione precedente</span><span class="sxs-lookup"><span data-stu-id="452af-228">If your code uses...</span></span>                  | <span data-ttu-id="452af-229">Versione aggiornata</span><span class="sxs-lookup"><span data-stu-id="452af-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="452af-230">`CloudTask.RunElevated` non specificato</span><span class="sxs-lookup"><span data-stu-id="452af-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="452af-231">Non sono necessari aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="452af-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="452af-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="452af-232">Batch Java</span></span>

| <span data-ttu-id="452af-233">Versione precedente</span><span class="sxs-lookup"><span data-stu-id="452af-233">If your code uses...</span></span>                      | <span data-ttu-id="452af-234">Versione aggiornata</span><span class="sxs-lookup"><span data-stu-id="452af-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="452af-235">`CloudTask.withRunElevated` non specificato</span><span class="sxs-lookup"><span data-stu-id="452af-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="452af-236">Non sono necessari aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="452af-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="452af-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="452af-237">Batch Python</span></span>

| <span data-ttu-id="452af-238">Versione precedente</span><span class="sxs-lookup"><span data-stu-id="452af-238">If your code uses...</span></span>                      | <span data-ttu-id="452af-239">Versione aggiornata</span><span class="sxs-lookup"><span data-stu-id="452af-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="452af-240">`user_identity=user`, dove</span><span class="sxs-lookup"><span data-stu-id="452af-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="452af-241">`user_identity=user`, dove</span><span class="sxs-lookup"><span data-stu-id="452af-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="452af-242">`run_elevated` non specificato</span><span class="sxs-lookup"><span data-stu-id="452af-242">`run_elevated` not specified</span></span> | <span data-ttu-id="452af-243">Non sono necessari aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="452af-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="452af-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="452af-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="452af-245">Forum di Batch</span><span class="sxs-lookup"><span data-stu-id="452af-245">Batch Forum</span></span>

<span data-ttu-id="452af-246">Hello [Forum di Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) su MSDN è un ottimo posizionare toodiscuss Batch e porre domande sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="452af-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="452af-247">Leggere i post aggiunti e inviare domande durante le procedure di sviluppo delle soluzioni Batch.</span><span class="sxs-lookup"><span data-stu-id="452af-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
