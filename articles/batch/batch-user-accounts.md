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
# <a name="run-tasks-under-user-accounts-in-batch"></a>Eseguire attività con account utente in Batch

In Azure Batch un'attività viene sempre eseguita con un account utente. Per impostazione predefinita, le attività vengono eseguite con account utente standard, senza le autorizzazioni di amministratore perché le impostazioni predefinite dell'account utente in genere sono sufficienti. Per alcuni scenari, tuttavia, è account utente di toobe utile tooconfigure in grado di hello in cui si desidera un toorun di attività. In questo articolo vengono descritti tipi di hello degli account utente e come è possibile configurare per il proprio scenario.

## <a name="types-of-user-accounts"></a>Tipi di account utente

Azure Batch offre due tipi di account utente per l'esecuzione di attività:

- **Account utente automatici.** Gli account utente di auto sono account utente predefiniti che vengono creati automaticamente dal servizio Batch hello. Per impostazione predefinita, le attività vengono eseguite con un account utente automatico. È possibile configurare una specifica di auto-utente hello per tooindicate un'attività in cui auto-l'utente deve essere eseguito account un'attività. Specifica di auto-utente Hello permette di livello l'elevazione dei privilegi di toospecify hello e l'ambito dell'account utente automatica hello che verrà eseguita l'attività hello. 

- **Account utente non anonimi.** Quando si crea il pool di hello, è possibile specificare uno o più account utente denominato per un pool. Ogni account utente viene creato in ogni nodo del pool di hello. Toohello inoltre il nome account, specificare password dell'account utente hello, elevazione livello e, per il pool di Linux, la chiave privata SSH hello. Quando si aggiunge un'attività, è possibile specificare l'account utente in cui eseguire l'attività denominata hello.

> [!IMPORTANT] 
> versione del servizio Batch Hello 2017-01-01.4.0 introduce una modifica che è necessario aggiornare il codice toocall tale versione. Nel caso di migrazione del codice da una versione precedente di Batch, si noti che hello **runElevated** proprietà non è più supportata nelle librerie client API REST o un Batch di hello. Hello utilizzare nuovo **userIdentity** proprietà di un livello di attività toospecify l'elevazione dei privilegi. Vedere hello sezione [aggiornare la libreria client di Batch della versione più recente di codice toohello](#update-your-code-to-the-latest-batch-client-library) per le linee guida rapide per l'aggiornamento del codice Batch se si utilizza una delle librerie client hello.
>
>

> [!NOTE] 
> gli account utente di Hello descritti in questo articolo supporta Remote Desktop Protocol (RDP) o Secure Shell (SSH), per motivi di sicurezza. 
>
> tooconnect tooa nodo in esecuzione hello Linux configurazione della macchina virtuale tramite SSH, vedere [tooa utilizzo remoto del Desktop Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md). toonodes tooconnect che esegue Windows tramite RDP, vedere [connessione macchina virtuale Windows Server tooa](../virtual-machines/windows/connect-logon.md).<br /><br />
> tooconnect tooa nodo in esecuzione hello configurazione del servizio cloud tramite RDP, vedere [abilitare connessione Desktop remoto per un ruolo in servizi Cloud di Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).
>
>

## <a name="user-account-access-toofiles-and-directories"></a>Directory e toofiles di accesso di account utente

Un account utente di auto sia un account utente denominato avere la directory di lavoro dell'attività di lettura/scrittura accesso toohello directory condivisa e directory di multi-istanza attività. Entrambi i tipi di account dispone di accesso in lettura toohello avvio e processo di preparazione directory.

Se un'attività viene eseguito con hello stesso account utilizzato per l'esecuzione di un'attività di avvio, l'attività hello ha accesso in lettura-scrittura toohello inizio attività directory. Analogamente, se un'attività viene eseguito con hello stesso account utilizzato per l'esecuzione di un'attività di preparazione del processo, l'attività hello è directory attività di accesso in lettura-scrittura toohello processo preparazione. Se un'attività viene eseguito con un account diverso di attività di avvio hello o attività di preparazione del processo, attività hello è solo l'accesso in lettura toohello rispettive directory.

Per altre informazioni sull'accesso a file e directory da parte un'attività, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md#files-and-directories).

## <a name="elevated-access-for-tasks"></a>Accesso con privilegi elevati per le attività 

livello di elevazione dei privilegi dell'account utente di Hello indica se un'attività viene eseguito l'accesso con privilegi elevato. Un account utente automatico e un account utente non anonimo consentono entrambi l'accesso con privilegi elevati. sono Hello due opzioni per il livello di elevazione dei privilegi:

- **NonAdmin:** hello attività viene eseguita come utente standard senza accesso con privilegi elevati. livello di elevazione Hello predefinito per un account utente di Batch è sempre **NonAdmin**.
- **Amministratore:** hello attività in esecuzione come utente con accesso con privilegi elevati e funziona con le autorizzazioni di amministratore complete. 

## <a name="auto-user-accounts"></a>Account utente automatici

Per impostazione predefinita, in Batch le attività vengono eseguite con un account utente automatico, come utente standard senza accesso con privilegi elevati e con un ambito di attività. Quando si specifica auto utente hello è configurato per l'ambito di attività, il servizio di Batch hello crea un account utente automatica per l'attività solo.

ambito tootask alternativo Hello è ambito pool. Quando si specifica auto utente hello per un'attività è configurata per l'ambito di pool, attività hello viene eseguito con un account utente automaticamente attività tooany disponibile nel pool di hello. Per ulteriori informazioni sull'ambito di pool, vedere sezione hello [eseguire un'attività come hello auto-utente con ambito pool](#run-a-task-as-the-autouser-with-pool-scope).   

ambito predefinito Hello è diversa per i nodi Windows e Linux:

- Nei nodi Windows le attività vengono eseguite nell'ambito di attività per impostazione predefinita.
- I nodi Linux vengono sempre eseguiti nell'ambito di pool.

Esistono quattro possibili configurazioni per la specifica di auto-utente hello, ognuno dei quali corrisponde account utente univoco automatica tooa:

- Accesso senza privilegi di amministratore con ambito di attività (specifica di auto-utente hello predefinita)
- Accesso con privilegi di amministratore (elevati) con ambito di attività
- Accesso senza privilegi di amministratore con ambito di pool
- Accesso con privilegi di amministratore con ambito di pool

> [!IMPORTANT] 
> Attività in esecuzione nell'ambito di attività non è di fatto accesso tooother attività in un nodo. Tuttavia, un utente malintenzionato con account di accesso toohello potrebbe aggirare questa restrizione inviando un'attività che viene eseguito con privilegi di amministratore e accede alle altre directory di attività. Un utente malintenzionato può anche usare RDP o SSH nodo tooa tooconnect. È importante tooprotect accesso tooyour Batch account chiavi tooprevent tale scenario. Se si ritiene che l'account sia stato compromesso, essere tooregenerate che le chiavi.
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>Eseguire un'attività come utente automatico con accesso con privilegi elevati

Quando è necessario toorun un'attività con accesso con privilegi elevati, è possibile configurare specifica di auto-utente hello per i privilegi di amministratore. Ad esempio, un'attività di avvio potrebbe essere necessario software tooinstall di accesso con privilegi elevati nel nodo hello.

> [!NOTE] 
> In generale, è consigliabile toouse solo quando è necessario l'accesso con privilegi elevati. È consigliabile concedere hello con privilegi minimi necessari tooachieve hello il risultato desiderato. Ad esempio, se un'attività di avvio consente di installare software per l'utente corrente di hello, anziché per tutti gli utenti, potrebbe essere in grado di tooavoid concessione dell'accesso con privilegi elevati tootasks. È possibile configurare una specifica di auto-utente hello per l'accesso di ambito e l'utente non amministratore pool per tutte le attività che è necessario toorun in hello stesso account, inclusi hello attività di avvio. 
>
>

Hello frammenti di codice seguente mostra come tooconfigure hello specifica auto-utente. esempi di Hello impostano il livello di elevazione hello troppo`Admin` e hello ambito troppo`Task`. Ambito di attività è l'impostazione predefinita di hello, ma è incluso qui per i migliori risultati hello di esempio.

#### <a name="batch-net"></a>Batch .NET

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Batch Java

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Batch Python

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>Eseguire un'attività come utente automatico con ambito di pool

Quando viene eseguito il provisioning di un nodo, vengono creati due pool a livello di auto-account di ogni nodo nel pool di hello, con accesso con privilegi elevati e senza l'accesso con privilegi elevati. L'impostazione di ambito di toopool ambito hello automatica dell'utente per una determinata attività esegue l'attività di hello in uno di questi due pool a livello di auto-account. 

Quando si specifica l'ambito di pool per hello. auto-utente, tutte le attività eseguite con privilegi di amministratore eseguiti hello stesso account utente con livello di pool automatico. In modo analogo, le attività eseguite senza privilegi di amministratore vengono eseguite anche con un unico account utente automatico a livello di pool. 

> [!NOTE] 
> Hello due pool a livello di auto-account sono account distinti. Attività in esecuzione con account di amministrazione a livello di pool di hello non possono condividere dati con attività in esecuzione con account standard hello e viceversa. 
>
>

Hello toorunning vantaggio in hello stesso account utente di auto è che le attività sono in grado di tooshare dati con altre attività in esecuzione su hello stesso nodo.

La condivisione di informazioni riservate tra le attività è uno scenario in cui è utile l'esecuzione di attività con uno degli account utente a livello di pool automatico hello due. Si supponga, ad esempio, che un'attività di avvio deve tooprovision una chiave privata nel nodo hello che è possibile utilizzare altre attività. È possibile utilizzare Data Protection API (DPAPI) di Windows hello, ma richiede privilegi di amministratore. In alternativa, è possibile proteggere segreto hello a livello di utente hello. Attività in esecuzione in hello stesso account utente potrà accedere hello segreto senza accesso con privilegi elevati.

Condividere un altro scenario in cui può essere toorun attività con un account utente automatica con ambito di pool è un file di interfaccia MPI (Message Passing). Una condivisione di file MPI è utile quando i nodi hello hello MPI attività necessità toowork su hello stessi dati di file. nodo head Hello crea una condivisione file che i nodi figlio di hello possono accedere se sono in esecuzione con hello stesso account utente di auto. 

Hello seguente frammento di codice imposta ambito di toopool ambito hello automatica dell'utente per un'attività in .NET per Batch. livello di elevazione Hello viene omesso, viene eseguito attività hello hello standard a livello di pool di auto-account di.

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>Account utente non anonimi

Quando si crea un pool, è possibile definire gli account utente non anonimi. A un account utente non anonimo sono associati un nome e una password definiti dall'utente. È possibile specificare il livello di elevazione hello per un account utente denominato. Per i nodi Linux, è anche possibile specificare una chiave privata SSH.

Esiste un account utente denominato su tutti i nodi nel pool di hello e tooall disponibili attività è in esecuzione su tali nodi. In un pool è possibile definire un numero qualsiasi di utenti non anonimi. Quando si aggiunge un'attività o un insieme di attività, è possibile specificare che tale attività hello viene eseguito con uno degli account utente definito nel pool di hello denominato hello.

Un account utente denominato è utile quando si desidera toorun tutte le attività in un processo in hello stesso account utente isolandoli l'uno dall'attività in esecuzione in altri processi in hello contemporaneamente. È possibile ad esempio creare un utente non anonimo per ogni processo ed eseguire le attività di ogni processo con tale account. Ogni processo può condividere un segreto con le proprie attività, ma non con attività in esecuzione in altri processi.

È anche possibile utilizzare un toorun di account utente non anonimo un'attività che imposta le autorizzazioni per le risorse esterne, ad esempio condivisioni file. Con un account utente non anonimo, controllare l'identità utente hello si può utilizzare tale autorizzazioni tooset di identità utente.  

Gli account utente non anonimi consentono di abilitare il protocollo SSH senza password tra i nodi Linux. È possibile utilizzare un account utente denominato con nodi di Linux che richiedono attività di multi-istanza toorun. Ogni nodo nel pool di hello può eseguire attività con un account utente definito nel pool intero hello. Per ulteriori informazioni sulle attività di più istanze, vedere [utilizzare più\-istanza attività applicazioni MPI toorun](batch-mpi.md).

### <a name="create-named-user-accounts"></a>Creare account utente non anonimi

toocreate denominato gli account utente in Batch, aggiungere una raccolta di pool di toohello gli account utente. Hello frammenti di codice seguenti mostrano come toocreate denominati account utente in .NET, Java e Python. Questi codice frammenti di codice mostra come toocreate sia e gli account in un pool denominato non amministratore. esempi di Hello creano pool utilizzando hello configurazione del servizio cloud, ma è utilizzare hello stesso approccio quando si crea un pool di Windows o Linux utilizzando la configurazione della macchina virtuale hello.

#### <a name="batch-net-example-windows"></a>Esempio per Batch .NET (Windows)

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

#### <a name="batch-net-example-linux"></a>Esempio per Batch .NET (Linux)

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


#### <a name="batch-java-example"></a>Esempio per Batch Java

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

#### <a name="batch-python-example"></a>Esempio per Batch Python

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>Eseguire un'attività con un account utente non anonimo con accesso con privilegi elevati

toorun un'attività come del utente con privilegi elevati, set di attività di hello **UserIdentity** tooa proprietà denominato account utente che è stato creato con il relativo **ElevationLevel** impostata troppo`Admin`.

Questo frammento di codice specifica che attività hello deve essere eseguito con un account utente non anonimo. Questo account utente non anonimo è stato definito nel pool di hello quando è stato creato il pool di hello. In questo caso, hello denominato account utente è stato creato con le autorizzazioni di amministratore:

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>Aggiornare la libreria client di Batch della versione più recente di codice toohello

versione del servizio Batch Hello 2017-01-01.4.0 introduce una modifica di rilievo, sostituendo hello **runElevated** proprietà disponibili nelle versioni precedenti con hello **userIdentity** proprietà. Hello le tabelle seguenti fornisce una semplice mapping che è possibile utilizzare tooupdate il codice da versioni precedenti di librerie client hello.

### <a name="batch-net"></a>Batch .NET

| Versione precedente                  | Versione aggiornata                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| `CloudTask.RunElevated` non specificato | Non sono necessari aggiornamenti                                                                                               |

### <a name="batch-java"></a>Batch Java

| Versione precedente                      | Versione aggiornata                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| `CloudTask.withRunElevated` non specificato | Non sono necessari aggiornamenti                                                                                                                     |

### <a name="batch-python"></a>Batch Python

| Versione precedente                      | Versione aggiornata                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`, dove <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`, dove <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| `run_elevated` non specificato | Non sono necessari aggiornamenti                                                                                                                                  |


## <a name="next-steps"></a>Passaggi successivi

### <a name="batch-forum"></a>Forum di Batch

Hello [Forum di Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) su MSDN è un ottimo posizionare toodiscuss Batch e porre domande sul servizio hello. Leggere i post aggiunti e inviare domande durante le procedure di sviluppo delle soluzioni Batch.
