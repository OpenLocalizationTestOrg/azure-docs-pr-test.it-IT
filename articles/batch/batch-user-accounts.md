---
title: "Eseguire attività con account utente in Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="fb2b5-103">Eseguire attività con account utente in Batch</span><span class="sxs-lookup"><span data-stu-id="fb2b5-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="fb2b5-104">In Azure Batch un'attività viene sempre eseguita con un account utente.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="fb2b5-105">Per impostazione predefinita, le attività vengono eseguite con account utente standard, senza le autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="fb2b5-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="fb2b5-106">perché le impostazioni predefinite dell'account utente in genere sono sufficienti.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="fb2b5-107">Per determinati scenari, tuttavia, è utile essere in grado di configurare l'account utente con cui si intende eseguire un'attività.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="fb2b5-108">Questo articolo illustra i tipi di account utente e il modo in cui è possibile configurarli per lo scenario in uso.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="fb2b5-109">Tipi di account utente</span><span class="sxs-lookup"><span data-stu-id="fb2b5-109">Types of user accounts</span></span>

<span data-ttu-id="fb2b5-110">Azure Batch offre due tipi di account utente per l'esecuzione di attività:</span><span class="sxs-lookup"><span data-stu-id="fb2b5-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="fb2b5-111">**Account utente automatici.**</span><span class="sxs-lookup"><span data-stu-id="fb2b5-111">**Auto-user accounts.**</span></span> <span data-ttu-id="fb2b5-112">Gli account utente automatici sono predefiniti e vengono creati automaticamente dal servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="fb2b5-113">Per impostazione predefinita, le attività vengono eseguite con un account utente automatico.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="fb2b5-114">È possibile configurare la specifica di utente automatico per un'attività per indicare con quale account utente automatico l'attività deve essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="fb2b5-115">La specifica di utente automatico consente di specificare il livello di elevazione dei privilegi e l'ambito dell'account utente automatico con cui verrà eseguita l'attività.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="fb2b5-116">**Account utente non anonimi.**</span><span class="sxs-lookup"><span data-stu-id="fb2b5-116">**A named user account.**</span></span> <span data-ttu-id="fb2b5-117">È possibile specificare uno o più account utente non anonimi per un pool al momento della creazione del pool stesso.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="fb2b5-118">Ogni account utente viene creato in ogni nodo del pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="fb2b5-119">Oltre al nome, specificare la password dell'account utente, il livello di elevazione dei privilegi e, per i pool Linux, la chiave privata SSH.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="fb2b5-120">Quando si aggiunge un'attività, è possibile specificare l'account utente non anonimo con cui eseguirla.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="fb2b5-121">Nella versione 2017-01-01.4.0 del servizio Batch è stata introdotta una modifica significativa che richiede l'aggiornamento del codice per chiamare tale versione.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="fb2b5-122">Se si esegue la migrazione di codice da una versione precedente di Batch, si noti che la proprietà **runElevated** non è più supportata nelle librerie client API REST o Batch.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="fb2b5-123">Per specificare il livello di elevazione dei privilegi, usare la nuova proprietà **userIdentity** di un'attività.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="fb2b5-124">Per linee guida rapide sull'aggiornamento del codice Batch se si usa una delle librerie client, vedere la sezione [Aggiornare il codice alla libreria client Batch più recente](#update-your-code-to-the-latest-batch-client-library).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="fb2b5-125">Per motivi di sicurezza, gli account utente descritti in questo articolo non supportano i protocolli RDP (Remote Desktop Protocol) o SSH (Secure Shell).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="fb2b5-126">Per connettersi a un nodo che esegue la configurazione della macchina virtuale Linux tramite SSH, vedere [Installare e configurare Desktop remoto per connettersi a una VM Linux di Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="fb2b5-127">Per connettersi ai nodi che eseguono Windows tramite RDP, vedere [Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="fb2b5-128">Per connettersi a un nodo che esegue la configurazione del servizio cloud tramite RDP, vedere [Impostare una connessione Desktop remoto per un ruolo nei servizi cloud di Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="fb2b5-129">Accesso degli account utente a file e directory</span><span class="sxs-lookup"><span data-stu-id="fb2b5-129">User account access to files and directories</span></span>

<span data-ttu-id="fb2b5-130">Un account utente automatico e un account utente non anonimo hanno entrambi accesso in lettura e scrittura alla directory di lavoro dell'attività, alla directory condivisa e alla directory di attività a istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="fb2b5-131">Entrambi i tipi di account hanno anche accesso in lettura alle directory di avvio e a quelle di preparazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="fb2b5-132">Se un'attività viene eseguita con lo stesso account usato per l'esecuzione di un'attività di avvio, tale attività ha accesso in lettura e scrittura alla directory dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="fb2b5-133">In modo analogo, se un'attività viene eseguita con lo stesso account usato per l'esecuzione di un'attività di preparazione dei processi, tale attività ha accesso in lettura e scrittura anche alla directory dell'attività di preparazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="fb2b5-134">Se un'attività viene eseguita con un account diverso rispetto a quello usato per l'attività di avvio o per quella di preparazione dei processi, tale attività ha solo accesso in lettura alla directory corrispondente.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="fb2b5-135">Per altre informazioni sull'accesso a file e directory da parte un'attività, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="fb2b5-136">Accesso con privilegi elevati per le attività</span><span class="sxs-lookup"><span data-stu-id="fb2b5-136">Elevated access for tasks</span></span> 

<span data-ttu-id="fb2b5-137">Il livello di elevazione dei privilegi dell'account utente indica se un'attività viene eseguita con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="fb2b5-138">Un account utente automatico e un account utente non anonimo consentono entrambi l'accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="fb2b5-139">Le due opzioni per il livello di elevazione dei privilegi sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb2b5-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="fb2b5-140">**NonAdmin** (Non amministratore): l'attività viene eseguita come utente standard senza accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="fb2b5-141">Il livello di elevazione dei privilegi predefinito per un account utente Batch è sempre **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="fb2b5-142">**Admin** (Amministratore): l'attività viene eseguita come utente con accesso con privilegi elevati e opera con le autorizzazioni di amministratore complete.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="fb2b5-143">Account utente automatici</span><span class="sxs-lookup"><span data-stu-id="fb2b5-143">Auto-user accounts</span></span>

<span data-ttu-id="fb2b5-144">Per impostazione predefinita, in Batch le attività vengono eseguite con un account utente automatico, come utente standard senza accesso con privilegi elevati e con un ambito di attività.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="fb2b5-145">Quando per l'ambito di attività è configurata la specifica di utente automatico, il servizio Batch crea un account utente di questo tipo solo per l'attività.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="fb2b5-146">L'alternativa all'ambito di attività è l'ambito di pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="fb2b5-147">Quando per l'ambito di pool è configurata la specifica di utente automatico, l'attività viene eseguita con un account di questo tipo disponibile per qualsiasi attività nel pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="fb2b5-148">Per altre informazioni sull'ambito di pool, vedere la sezione [Eseguire un'attività con l'account utente automatico con ambito di pool](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="fb2b5-149">L'ambito predefinito è diverso in nodi Windows e Linux:</span><span class="sxs-lookup"><span data-stu-id="fb2b5-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="fb2b5-150">Nei nodi Windows le attività vengono eseguite nell'ambito di attività per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="fb2b5-151">I nodi Linux vengono sempre eseguiti nell'ambito di pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="fb2b5-152">Esistono quattro possibili configurazioni per la specifica di utente automatico, ognuna delle quali corrisponde a un account utente automatico univoco:</span><span class="sxs-lookup"><span data-stu-id="fb2b5-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="fb2b5-153">Accesso senza privilegi di amministratore con ambito di attività (specifica di utente automatico predefinito)</span><span class="sxs-lookup"><span data-stu-id="fb2b5-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="fb2b5-154">Accesso con privilegi di amministratore (elevati) con ambito di attività</span><span class="sxs-lookup"><span data-stu-id="fb2b5-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="fb2b5-155">Accesso senza privilegi di amministratore con ambito di pool</span><span class="sxs-lookup"><span data-stu-id="fb2b5-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="fb2b5-156">Accesso con privilegi di amministratore con ambito di pool</span><span class="sxs-lookup"><span data-stu-id="fb2b5-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="fb2b5-157">Le attività in esecuzione nell'ambito di attività non dispongono dell'accesso standard ad altre attività in un nodo.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="fb2b5-158">Un utente malintenzionato con accesso all'account, tuttavia, potrebbe aggirare questa restrizione inviando un'attività che viene eseguita con privilegi di amministratore e che può accedere alle directory di altre attività.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="fb2b5-159">Un utente malintenzionato potrebbe anche usare il protocollo RDP o SSH per connettersi a un nodo.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="fb2b5-160">È importante pertanto proteggere l'accesso alle chiavi dell'account Batch per impedire che si verifichi uno scenario di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="fb2b5-161">Se si sospetta che l'account sia stato compromesso, assicurarsi di rigenerare le chiavi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="fb2b5-162">Eseguire un'attività come utente automatico con accesso con privilegi elevati</span><span class="sxs-lookup"><span data-stu-id="fb2b5-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="fb2b5-163">Quando è necessario eseguire un'attività con accesso con privilegi elevati, è possibile configurare la specifica di utente automatico per i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="fb2b5-164">A un'attività di avvio, ad esempio, potrebbe essere necessario l'accesso con privilegi elevati per installare il software nel nodo.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="fb2b5-165">In generale, è consigliabile usare l'accesso con privilegi elevati solo quando è necessario</span><span class="sxs-lookup"><span data-stu-id="fb2b5-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="fb2b5-166">e concedere esclusivamente i privilegi minimi necessari per ottenere il risultato desiderato.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="fb2b5-167">Se ad esempio un'attività di avvio consente di installare software per l'utente corrente, anziché per tutti gli utenti, è possibile evitare di concedere l'accesso con privilegi elevati alle attività.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="fb2b5-168">È possibile configurare la specifica di utente automatico per l'ambito di pool e senza privilegi di amministratore per tutte le attività che devono essere eseguite con lo stesso account, tra cui l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="fb2b5-169">I frammenti di codice seguente illustrano come configurare la specifica di utente automatico.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="fb2b5-170">Gli esempi impostano il livello di elevazione dei privilegi su `Admin` e su `Task`.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="fb2b5-171">L'ambito di attività è l'impostazione predefinita, ma in questo caso viene inclusa a scopo di esempio.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="fb2b5-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="fb2b5-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="fb2b5-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="fb2b5-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="fb2b5-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="fb2b5-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="fb2b5-175">Eseguire un'attività come utente automatico con ambito di pool</span><span class="sxs-lookup"><span data-stu-id="fb2b5-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="fb2b5-176">Quando viene eseguito il provisioning di un nodo, a livello di pool vengono creati due account utente automatici per ogni nodo del pool, uno con accesso con privilegi elevati e uno senza accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="fb2b5-177">Se si imposta l'ambito dell'utente automatico sull'ambito di pool per una determinata attività, questa verrà eseguita con uno di tali due account a livello di pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="fb2b5-178">Quando si specifica l'ambito di pool per l'utente automatico, tutte le attività eseguite con privilegi di amministratore vengono eseguite con lo stesso account utente automatico a livello di pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="fb2b5-179">In modo analogo, le attività eseguite senza privilegi di amministratore vengono eseguite anche con un unico account utente automatico a livello di pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="fb2b5-180">I due account utente automatici a livello di pool sono account separati.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="fb2b5-181">Le attività in esecuzione con l'account amministrativo a livello di pool non possono condividere dati con quelle in esecuzione con l'account standard e viceversa.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="fb2b5-182">Il vantaggio di eseguire attività con lo stesso account utente automatico consiste nel fatto che le attività sono in grado di condividere dati con altre attività in esecuzione nello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="fb2b5-183">La condivisione di segreti tra le attività è uno scenario in cui l'esecuzione di attività con uno dei due account utente automatici a livello di pool è particolarmente utile.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="fb2b5-184">Si supponga ad esempio che un'attività di avvio richieda il provisioning di un segreto sul nodo che può essere usato da altre attività.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="fb2b5-185">È possibile usare l'API di protezione dati di Windows (DPAPI), ma in questo caso sono necessari anche i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="fb2b5-186">In alternativa, è possibile proteggere il segreto a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="fb2b5-187">Le attività in esecuzione con lo stesso account utente possono accedere al segreto senza accesso con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="fb2b5-188">Un altro scenario in cui può essere opportuno eseguire attività con un account utente automatico con ambito di pool è la condivisione di file di tipo MPI (Message Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="fb2b5-189">Una condivisione di file MPI è utile quando i nodi nell'attività MPI devono usare gli stessi dati di file.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="fb2b5-190">Il nodo head crea una condivisione di file cui i nodi figlio possono accedere se sono in esecuzione con lo stesso account utente automatico.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="fb2b5-191">Il frammento di codice seguente imposta l'ambito dell'utente automatico sull'ambito di pool per un'attività in Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="fb2b5-192">Il livello di elevazione dei privilegi viene omesso, in modo che l'attività venga eseguita con l'account utente automatico standard a livello di pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="fb2b5-193">Account utente non anonimi</span><span class="sxs-lookup"><span data-stu-id="fb2b5-193">Named user accounts</span></span>

<span data-ttu-id="fb2b5-194">Quando si crea un pool, è possibile definire gli account utente non anonimi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="fb2b5-195">A un account utente non anonimo sono associati un nome e una password definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="fb2b5-196">Per un account utente non anonimo, è possibile specificare il livello di elevazione dei privilegi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="fb2b5-197">Per i nodi Linux, è anche possibile specificare una chiave privata SSH.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="fb2b5-198">Un account utente non anonimo è presente in tutti i nodi del pool ed è disponibile per tutte le attività in esecuzione su tali nodi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="fb2b5-199">In un pool è possibile definire un numero qualsiasi di utenti non anonimi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="fb2b5-200">Quando si aggiunge un'attività o una raccolta di attività, è possibile specificare che l'attività venga eseguita con uno degli account utente non anonimi definiti nel pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="fb2b5-201">Un account utente non anonimo è utile quando si vuole che tutte le attività in un processo vengano eseguite con lo stesso account utente, ma si vuole anche isolarle dalle attività in esecuzione contemporaneamente in altri processi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="fb2b5-202">È possibile ad esempio creare un utente non anonimo per ogni processo ed eseguire le attività di ogni processo con tale account.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="fb2b5-203">Ogni processo può condividere un segreto con le proprie attività, ma non con attività in esecuzione in altri processi.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="fb2b5-204">È anche possibile usare un account utente non anonimo per eseguire un'attività che imposta le autorizzazioni in risorse esterne, ad esempio in condivisioni di file.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="fb2b5-205">Con un account utente non anonimo è possibile controllare l'identità dell'utente e usare tale identità per impostare le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="fb2b5-206">Gli account utente non anonimi consentono di abilitare il protocollo SSH senza password tra i nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="fb2b5-207">È possibile usare un account utente non anonimo con nodi Linux per cui è necessario eseguire attività a istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="fb2b5-208">Ogni nodo nel pool può eseguire attività con un account utente definito nell'intero pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="fb2b5-209">Per altre informazioni sulle attività a istanze multiple, vedere [Usare le attività a istanze multiple per eseguire applicazioni MPI (Message Passing Interface) in Batch](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="fb2b5-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="fb2b5-210">Creare account utente non anonimi</span><span class="sxs-lookup"><span data-stu-id="fb2b5-210">Create named user accounts</span></span>

<span data-ttu-id="fb2b5-211">Per creare account utente non anonimi in Batch, aggiungere una raccolta di account utente al pool.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="fb2b5-212">I frammenti di codice seguenti illustrano come creare account utente non anonimi in .NET, Java e Python in un pool,</span><span class="sxs-lookup"><span data-stu-id="fb2b5-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="fb2b5-213">sia con privilegi di amministratore che senza.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="fb2b5-214">Gli esempi creano pool usando la configurazione del servizio cloud, ma si usa lo stesso approccio quando si crea un pool di Windows o Linux tramite la configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="fb2b5-215">Esempio per Batch .NET (Windows)</span><span class="sxs-lookup"><span data-stu-id="fb2b5-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
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

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="fb2b5-216">Esempio per Batch .NET (Linux)</span><span class="sxs-lookup"><span data-stu-id="fb2b5-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
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

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="fb2b5-217">Esempio per Batch Java</span><span class="sxs-lookup"><span data-stu-id="fb2b5-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="fb2b5-218">Esempio per Batch Python</span><span class="sxs-lookup"><span data-stu-id="fb2b5-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="fb2b5-219">Eseguire un'attività con un account utente non anonimo con accesso con privilegi elevati</span><span class="sxs-lookup"><span data-stu-id="fb2b5-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="fb2b5-220">Per eseguire un'attività come utente con privilegi elevati, impostarne la proprietà **UserIdentity** su un account utente non anonimo creato con la proprietà **ElevationLevel** impostata su `Admin`.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="fb2b5-221">Questo frammento di codice specifica che l'attività deve essere eseguita con un account utente non anonimo.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="fb2b5-222">Tale account utente è stato definito nel pool al momento della relativa creazione.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="fb2b5-223">In questo caso l'account utente non anonimo è stato creato con le autorizzazioni di amministratore:</span><span class="sxs-lookup"><span data-stu-id="fb2b5-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="fb2b5-224">Aggiornare il codice in base alla libreria client Batch più recente</span><span class="sxs-lookup"><span data-stu-id="fb2b5-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="fb2b5-225">Nella versione 2017-01-01.4.0 del servizio Batch è stata introdotta una modifica significativa, ovvero la proprietà **runElevated** disponibile nelle versioni precedenti è stata sostituita con la proprietà **userIdentity**.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="fb2b5-226">Le tabelle seguenti illustrano una semplice corrispondenza che consente di aggiornare il codice dalle versioni precedenti delle librerie client.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="fb2b5-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="fb2b5-227">Batch .NET</span></span>

| <span data-ttu-id="fb2b5-228">Versione precedente</span><span class="sxs-lookup"><span data-stu-id="fb2b5-228">If your code uses...</span></span>                  | <span data-ttu-id="fb2b5-229">Versione aggiornata</span><span class="sxs-lookup"><span data-stu-id="fb2b5-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="fb2b5-230">`CloudTask.RunElevated` non specificato</span><span class="sxs-lookup"><span data-stu-id="fb2b5-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="fb2b5-231">Non sono necessari aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="fb2b5-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="fb2b5-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="fb2b5-232">Batch Java</span></span>

| <span data-ttu-id="fb2b5-233">Versione precedente</span><span class="sxs-lookup"><span data-stu-id="fb2b5-233">If your code uses...</span></span>                      | <span data-ttu-id="fb2b5-234">Versione aggiornata</span><span class="sxs-lookup"><span data-stu-id="fb2b5-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="fb2b5-235">`CloudTask.withRunElevated` non specificato</span><span class="sxs-lookup"><span data-stu-id="fb2b5-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="fb2b5-236">Non sono necessari aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="fb2b5-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="fb2b5-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="fb2b5-237">Batch Python</span></span>

| <span data-ttu-id="fb2b5-238">Versione precedente</span><span class="sxs-lookup"><span data-stu-id="fb2b5-238">If your code uses...</span></span>                      | <span data-ttu-id="fb2b5-239">Versione aggiornata</span><span class="sxs-lookup"><span data-stu-id="fb2b5-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="fb2b5-240">`user_identity=user`, dove</span><span class="sxs-lookup"><span data-stu-id="fb2b5-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="fb2b5-241">`user_identity=user`, dove</span><span class="sxs-lookup"><span data-stu-id="fb2b5-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="fb2b5-242">`run_elevated` non specificato</span><span class="sxs-lookup"><span data-stu-id="fb2b5-242">`run_elevated` not specified</span></span> | <span data-ttu-id="fb2b5-243">Non sono necessari aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="fb2b5-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="fb2b5-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb2b5-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="fb2b5-245">Forum di Batch</span><span class="sxs-lookup"><span data-stu-id="fb2b5-245">Batch Forum</span></span>

<span data-ttu-id="fb2b5-246">Il [forum di Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) su MSDN consente di seguire discussioni su Batch e di inviare domande sul servizio.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="fb2b5-247">Leggere i post aggiunti e inviare domande durante le procedure di sviluppo delle soluzioni Batch.</span><span class="sxs-lookup"><span data-stu-id="fb2b5-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>