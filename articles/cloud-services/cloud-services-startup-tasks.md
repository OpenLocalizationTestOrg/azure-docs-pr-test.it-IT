---
title: "Attività di avvio di servizi Cloud di Azure aaaRun | Documenti Microsoft"
description: "Le attività di avvio consentono di preparare l'ambiente del servizio cloud per l'app. Spiega che l'attività di avvio del lavoro e la modalità toomake li"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="fdb95-104">Modalità di avvio tooconfigure ed eseguire attività per un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="fdb95-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="fdb95-105">È possibile utilizzare le operazioni di avvio attività tooperform prima dell'avvio di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="fdb95-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="fdb95-106">Le operazioni che è possibile tooperform includono l'installazione di un componente, la registrazione dei componenti COM, impostano le chiavi del Registro di sistema o l'avvio di un processo a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="fdb95-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="fdb95-107">Attività di avvio non sono applicabili tooVirtual macchine, solo tooCloud servizio Web e ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fdb95-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="fdb95-108">Funzionamento delle attività di avvio</span><span class="sxs-lookup"><span data-stu-id="fdb95-108">How startup tasks work</span></span>
<span data-ttu-id="fdb95-109">Attività di avvio sono azioni che vengono eseguite prima che i ruoli begin e definiti in hello [Servicedefinition] file utilizzando hello [attività] elemento all'interno di hello [avvio]elemento.</span><span class="sxs-lookup"><span data-stu-id="fdb95-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="fdb95-110">Spesso le attività di avvio sono file batch, ma possono essere anche applicazioni console o file batch tramite i quali si avviano script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fdb95-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="fdb95-111">Le variabili di ambiente passano informazioni all'interno di un'attività di avvio e archiviazione locale può essere utilizzato toopass informazioni da un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="fdb95-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="fdb95-112">Ad esempio, una variabile di ambiente può specificare programma tooa di hello percorso desiderato tooinstall e i file possono essere scritti archiviazione toolocal che può quindi essere letti successivamente dai ruoli.</span><span class="sxs-lookup"><span data-stu-id="fdb95-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="fdb95-113">L'attività di avvio è possibile registrare informazioni e directory di toohello errori specificata da hello **TEMP** variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="fdb95-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="fdb95-114">Durante l'attività di avvio, hello hello **TEMP** variabile di ambiente risolve toohello *c:\\risorse\\temp\\[guid]. [ roleName]\\RoleTemp* directory durante l'esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="fdb95-115">Le attività di avvio possono inoltre essere eseguite più volte tra un riavvio e l'altro.</span><span class="sxs-lookup"><span data-stu-id="fdb95-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="fdb95-116">Ad esempio, verrà eseguita l'attività di avvio hello ogni volta che viene riciclato il ruolo di hello e ricicli dei ruoli non includono necessariamente un riavvio.</span><span class="sxs-lookup"><span data-stu-id="fdb95-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="fdb95-117">Attività di avvio devono essere scritti in modo che consenta loro toorun più volte senza problemi.</span><span class="sxs-lookup"><span data-stu-id="fdb95-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="fdb95-118">Attività di avvio devono terminare con un **errorlevel** (o codice di uscita) pari a zero per hello avvio processo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fdb95-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="fdb95-119">Se un'attività di avvio termina con un diverso da zero **errorlevel**, hello ruolo non verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="fdb95-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="fdb95-120">Sequenza di avvio di un ruolo</span><span class="sxs-lookup"><span data-stu-id="fdb95-120">Role startup order</span></span>
<span data-ttu-id="fdb95-121">Hello procedura elenchi hello ruolo avvio in Azure:</span><span class="sxs-lookup"><span data-stu-id="fdb95-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="fdb95-122">istanza di Hello è contrassegnata come **iniziale** e non riceve traffico.</span><span class="sxs-lookup"><span data-stu-id="fdb95-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="fdb95-123">Tutte le attività di avvio vengono eseguite in base tootheir **taskType** attributo.</span><span class="sxs-lookup"><span data-stu-id="fdb95-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="fdb95-124">Hello **semplice** attività vengono eseguite in modo sincrono, uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="fdb95-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="fdb95-125">Hello **background** e **in primo piano** attività sono attività di avvio toohello parallela e avviato in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="fdb95-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="fdb95-126">IIS potrebbe non essere completamente configurato durante la fase di attività di avvio hello nel processo di avvio hello, pertanto potrebbero non essere disponibili dati specifici del ruolo.</span><span class="sxs-lookup"><span data-stu-id="fdb95-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="fdb95-127">Per le attività di avvio che richiedono dati specifici per il ruolo è necessario usare [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="fdb95-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="fdb95-128">processo host del ruolo Hello viene avviato e viene creato il sito di hello in IIS.</span><span class="sxs-lookup"><span data-stu-id="fdb95-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="fdb95-129">Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metodo viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="fdb95-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="fdb95-130">istanza di Hello è contrassegnata come **pronto** e il traffico indirizzato toohello istanza.</span><span class="sxs-lookup"><span data-stu-id="fdb95-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="fdb95-131">Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="fdb95-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="fdb95-132">Esempio di attività di avvio</span><span class="sxs-lookup"><span data-stu-id="fdb95-132">Example of a startup task</span></span>
<span data-ttu-id="fdb95-133">Attività di avvio vengono definite nel hello [Servicedefinition] file hello **attività** elemento.</span><span class="sxs-lookup"><span data-stu-id="fdb95-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="fdb95-134">Hello **commandLine** attributo specifica il nome di hello e parametri del batch di avvio hello file o comando della console, hello **executionContext** attributo specifica il livello di privilegio hello dell'avvio di hello attività e hello **taskType** attributo specifica l'esecuzione delle attività hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="fdb95-135">In questo esempio, una variabile di ambiente **MyVersionNumber**, viene creato per attività di avvio hello e impostare il valore di toohello "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="fdb95-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="fdb95-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="fdb95-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="fdb95-137">Nell'esempio seguente di hello, hello **Startup.cmd** file batch scrive la riga hello "la versione corrente di hello is 1.0.0.0" toohello StartupLog.txt file nella directory hello specificata dalla variabile di ambiente TEMP hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="fdb95-138">Hello `EXIT /B 0` riga assicura l'attività di avvio hello termina con un **errorlevel** pari a zero.</span><span class="sxs-lookup"><span data-stu-id="fdb95-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="fdb95-139">In Visual Studio, hello **copiare tooOutput Directory** proprietà per il file batch di avvio deve essere impostata troppo**Copia sempre** toobe assicurarsi che il file batch di avvio sia correttamente distribuito tooyour in Azure (**approot\\bin** per i ruoli Web, e **approot** per i ruoli di lavoro).</span><span class="sxs-lookup"><span data-stu-id="fdb95-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="fdb95-140">Descrizione degli attributi di Task</span><span class="sxs-lookup"><span data-stu-id="fdb95-140">Description of task attributes</span></span>
<span data-ttu-id="fdb95-141">Hello seguito vengono descritti gli attributi di hello di hello **attività** elemento hello [Servicedefinition] file:</span><span class="sxs-lookup"><span data-stu-id="fdb95-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="fdb95-142">**riga di comando** -specifica la riga di comando hello per attività di avvio hello:</span><span class="sxs-lookup"><span data-stu-id="fdb95-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="fdb95-143">Hello comando, con i parametri della riga di comando facoltativi, che inizia l'attività di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="fdb95-144">Questo è spesso hello filename di un file con estensione cmd o bat di batch.</span><span class="sxs-lookup"><span data-stu-id="fdb95-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="fdb95-145">attività Hello è relativo toohello AppRoot\\cartella Bin per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="fdb95-146">Le variabili di ambiente non vengono espanse per determinare il percorso di hello e dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="fdb95-147">Se è necessaria l'espansione dell'ambiente, è possibile creare un piccolo script con estensione cmd con il quale richiamare l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="fdb95-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="fdb95-148">Può essere un'applicazione console o un file batch che avvia uno [script di PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="fdb95-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="fdb95-149">**executionContext** -specifica il livello di privilegio hello per attività di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="fdb95-150">livello di privilegio Hello può essere limitata o con privilegi elevato:</span><span class="sxs-lookup"><span data-stu-id="fdb95-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="fdb95-151">**limitato**</span><span class="sxs-lookup"><span data-stu-id="fdb95-151">**limited**</span></span>  
  <span data-ttu-id="fdb95-152">attività di avvio Hello viene eseguito con hello stessi privilegi del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="fdb95-153">Quando hello **executionContext** attributo per hello [Runtime] elemento è **limitato**, quindi vengono utilizzati i privilegi di utente.</span><span class="sxs-lookup"><span data-stu-id="fdb95-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="fdb95-154">**elevato**</span><span class="sxs-lookup"><span data-stu-id="fdb95-154">**elevated**</span></span>  
  <span data-ttu-id="fdb95-155">attività di avvio Hello viene eseguito con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="fdb95-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="fdb95-156">In questo modo le attività di avvio programmi tooinstall, apportare modifiche alla configurazione di IIS, eseguire le modifiche del Registro di sistema e altre attività a livello di amministratore senza aumentare il livello di privilegio hello del ruolo hello stesso.</span><span class="sxs-lookup"><span data-stu-id="fdb95-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="fdb95-157">Hello il livello di privilegio dell'attività di avvio non è necessario toobe hello stesso come ruolo hello stesso.</span><span class="sxs-lookup"><span data-stu-id="fdb95-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="fdb95-158">**taskType** -specifica hello modo un'attività di avvio viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="fdb95-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="fdb95-159">**simple**</span><span class="sxs-lookup"><span data-stu-id="fdb95-159">**simple**</span></span>  
  <span data-ttu-id="fdb95-160">Le attività vengono eseguite in modo sincrono, uno alla volta, nell'ordine di hello specificato in hello [Servicedefinition] file.</span><span class="sxs-lookup"><span data-stu-id="fdb95-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="fdb95-161">Quando uno **semplice** attività di avvio termina con un **errorlevel** pari a zero, hello successivamente **semplice** viene eseguita l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="fdb95-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="fdb95-162">Se non sono più **semplice** tooexecute, le attività di avvio, quindi verrà avviato il ruolo hello stesso.</span><span class="sxs-lookup"><span data-stu-id="fdb95-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="fdb95-163">Se hello **semplice** attività termina con un diverso da zero **errorlevel**, hello istanza viene bloccata.</span><span class="sxs-lookup"><span data-stu-id="fdb95-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="fdb95-164">Le successive **semplice** attività di avvio e ruolo hello stesso, non verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="fdb95-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="fdb95-165">tooensure che il file batch termina con un **errorlevel** pari a zero, eseguire il comando hello `EXIT /B 0` alla fine di hello del processo del file batch.</span><span class="sxs-lookup"><span data-stu-id="fdb95-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="fdb95-166">**background**</span><span class="sxs-lookup"><span data-stu-id="fdb95-166">**background**</span></span>  
  <span data-ttu-id="fdb95-167">Le attività vengono eseguite in modo asincrono, in parallelo con avvio hello del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="fdb95-168">**foreground**</span><span class="sxs-lookup"><span data-stu-id="fdb95-168">**foreground**</span></span>  
  <span data-ttu-id="fdb95-169">Le attività vengono eseguite in modo asincrono, in parallelo con avvio hello del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="fdb95-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="fdb95-170">Hello differenza fondamentale tra un **in primo piano** e **background** attività è che un **in primo piano** attività impedisce ruolo hello dal riciclo o arresto fino a quando non dispone di attività hello è terminata.</span><span class="sxs-lookup"><span data-stu-id="fdb95-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="fdb95-171">Hello **background** attività non dispone di questa restrizione.</span><span class="sxs-lookup"><span data-stu-id="fdb95-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="fdb95-172">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="fdb95-172">Environment variables</span></span>
<span data-ttu-id="fdb95-173">Le variabili di ambiente sono un'attività di avvio tooa modo toopass informazioni.</span><span class="sxs-lookup"><span data-stu-id="fdb95-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="fdb95-174">Ad esempio, è possibile inserire hello percorso tooa blob che contiene tooinstall un programma, o numeri di porta che verrà utilizzato il ruolo o funzionalità toocontrol le impostazioni dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="fdb95-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="fdb95-175">Esistono due tipi di variabili di ambiente per attività di avvio. variabili di ambiente statiche e variabili di ambiente basano sui membri di hello [ RoleEnvironment] classe.</span><span class="sxs-lookup"><span data-stu-id="fdb95-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="fdb95-176">Sono entrambi hello [ambiente] sezione di hello [Servicedefinition] file ed entrambi hello utilizzare [variabile] elemento e **nome** attributo.</span><span class="sxs-lookup"><span data-stu-id="fdb95-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="fdb95-177">Hello utilizza le variabili di ambiente statiche **valore** attributo di hello [variabile] elemento.</span><span class="sxs-lookup"><span data-stu-id="fdb95-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="fdb95-178">esempio Hello precedente crea la variabile di ambiente hello **MyVersionNumber** che ha un valore statico di "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="fdb95-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="fdb95-179">Un altro esempio sarebbe toocreate un **StagingOrProduction** variabile di ambiente che è possibile impostare manualmente toovalues di "**di gestione temporanea**"o"**produzione**" tooperform azioni di avvio diverse in base al valore di hello di hello **StagingOrProduction** variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="fdb95-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="fdb95-180">Le variabili di ambiente basate sui membri della classe RoleEnvironment hello non utilizzano hello **valore** attributo di hello [variabile] elemento.</span><span class="sxs-lookup"><span data-stu-id="fdb95-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="fdb95-181">In alternativa, hello [RoleInstanceValue] elemento figlio, con hello appropriato **XPath** valore dell'attributo, viene utilizzati toocreate una variabile di ambiente in base a un membro specifico di hello [ RoleEnvironment] classe.</span><span class="sxs-lookup"><span data-stu-id="fdb95-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="fdb95-182">I valori per hello **XPath** attributo tooaccess vari [ RoleEnvironment] sono disponibili valori [qui](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="fdb95-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="fdb95-183">Ad esempio, toocreate una variabile di ambiente che è "**true**" quando l'istanza di hello è in esecuzione nell'emulatore di calcolo, hello e "**false**" durante l'esecuzione nel cloud hello, utilizzare l'esempio hello [variabile] e [RoleInstanceValue] elementi:</span><span class="sxs-lookup"><span data-stu-id="fdb95-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="fdb95-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdb95-184">Next steps</span></span>
<span data-ttu-id="fdb95-185">Informazioni su come tooperform alcuni [comuni attività di avvio](cloud-services-startup-tasks-common.md) con il servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="fdb95-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="fdb95-186">[Creare il pacchetto](cloud-services-model-and-package.md) del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fdb95-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[Servicedefinition]: cloud-services-model-and-package.md#csdef
[attività]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[avvio]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ambiente]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variabile]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
