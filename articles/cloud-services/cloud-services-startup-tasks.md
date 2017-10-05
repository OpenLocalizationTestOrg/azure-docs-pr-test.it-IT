---
title: "Eseguire attività di avvio in Servizi cloud di Azure | Documentazione Microsoft"
description: "Le attività di avvio consentono di preparare l'ambiente del servizio cloud per l'app. Questo argomento illustra il funzionamento e la modalità di esecuzione delle attività di avvio"
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
ms.openlocfilehash: 1c1b3aa86dc8211de0c07c9fb68da5685c86f551
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="50ac1-104">Come configurare ed eseguire attività di avvio per un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="50ac1-104">How to configure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="50ac1-105">È possibile usare le attività di avvio per eseguire operazioni prima dell'avvio di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="50ac1-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="50ac1-106">Le operazioni che si possono eseguire sono l'installazione di un componente, la registrazione dei componenti COM, l'impostazione delle chiavi del Registro di sistema o l'avvio di un processo a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="50ac1-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="50ac1-107">Le attività di avvio non sono applicabili ai ruoli VM, ma solo ai ruoli Web e di lavoro del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="50ac1-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="50ac1-108">Funzionamento delle attività di avvio</span><span class="sxs-lookup"><span data-stu-id="50ac1-108">How startup tasks work</span></span>
<span data-ttu-id="50ac1-109">Le attività di avvio sono azioni effettuate prima dell'inizio dei ruoli e vengono definite nel file [ServiceDefinition.csdef] usando l'elemento [Task] all'interno dell'elemento [Startup].</span><span class="sxs-lookup"><span data-stu-id="50ac1-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span></span> <span data-ttu-id="50ac1-110">Spesso le attività di avvio sono file batch, ma possono essere anche applicazioni console o file batch tramite i quali si avviano script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50ac1-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="50ac1-111">Le variabili di ambiente passano informazioni all'interno di un'attività di avvio e le risorse di archiviazione locale possono essere usate per il passaggio all'esterno di un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span></span> <span data-ttu-id="50ac1-112">In una variabile di ambiente può essere ad esempio specificato il percorso di un programma che si desidera installare e i file possono essere scritti nelle risorse di archiviazione locale e letti successivamente dai ruoli.</span><span class="sxs-lookup"><span data-stu-id="50ac1-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span></span>

<span data-ttu-id="50ac1-113">Con l'attività di avvio è possibile registrare informazioni ed errori nella directory specificata dalla variabile di ambiente **TEMP** .</span><span class="sxs-lookup"><span data-stu-id="50ac1-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span></span> <span data-ttu-id="50ac1-114">Durante l'attività di avvio, la variabile di ambiente **TEMP** viene risolta nella directory *C:\\Resources\\temp\\[guid].[nomeruolo]\\RoleTemp* nell'esecuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="50ac1-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span></span>

<span data-ttu-id="50ac1-115">Le attività di avvio possono inoltre essere eseguite più volte tra un riavvio e l'altro.</span><span class="sxs-lookup"><span data-stu-id="50ac1-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="50ac1-116">Ad esempio, l'attività di avvio viene eseguita a ogni riciclo del ruolo e tali ricicli non includono necessariamente un riavvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="50ac1-117">Le attività di avvio devono essere scritte in modo da poter essere eseguite più volte senza problemi.</span><span class="sxs-lookup"><span data-stu-id="50ac1-117">Startup tasks should be written in a way that allows them to run several times without problems.</span></span>

<span data-ttu-id="50ac1-118">Le attività di avvio devono terminare con un valore di **errorlevel** (o codice di uscita) uguale a zero perché il processo di avvio possa essere completato.</span><span class="sxs-lookup"><span data-stu-id="50ac1-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span></span> <span data-ttu-id="50ac1-119">Se l'attività di avvio termina con un valore di **errorlevel**diverso da zero, il ruolo non verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="50ac1-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="50ac1-120">Sequenza di avvio di un ruolo</span><span class="sxs-lookup"><span data-stu-id="50ac1-120">Role startup order</span></span>
<span data-ttu-id="50ac1-121">Di seguito è riportata la procedura di avvio di un ruolo in Azure:</span><span class="sxs-lookup"><span data-stu-id="50ac1-121">The following lists the role startup procedure in Azure:</span></span>

1. <span data-ttu-id="50ac1-122">L'istanza viene contrassegnata con lo stato **Avvio in corso** e non riceve traffico.</span><span class="sxs-lookup"><span data-stu-id="50ac1-122">The instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="50ac1-123">Tutte le attività di avvio vengono eseguite in base al relativo attributo **taskType** .</span><span class="sxs-lookup"><span data-stu-id="50ac1-123">All startup tasks are executed according to their **taskType** attribute.</span></span>
   
   * <span data-ttu-id="50ac1-124">Le attività di tipo **simple** vengono eseguite in modo sincrono, una alla volta.</span><span class="sxs-lookup"><span data-stu-id="50ac1-124">The **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="50ac1-125">Le attività di tipo **background** e **foreground** vengono avviate in modo asincrono, in parallelo all'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="50ac1-126">È possibile che IIS non sia stato configurato completamente nella fase delle attività di avvio del processo di avvio, pertanto potrebbero non essere disponibili dati specifici per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="50ac1-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="50ac1-127">Per le attività di avvio che richiedono dati specifici per il ruolo è necessario usare [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="50ac1-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="50ac1-128">Viene avviato il processo host del ruolo e il sito viene creato in IIS.</span><span class="sxs-lookup"><span data-stu-id="50ac1-128">The role host process is started and the site is created in IIS.</span></span>
4. <span data-ttu-id="50ac1-129">Viene chiamato il metodo [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="50ac1-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="50ac1-130">L'istanza viene contrassegnata con lo stato **Pronto** e il traffico viene indirizzato all'istanza.</span><span class="sxs-lookup"><span data-stu-id="50ac1-130">The instance is marked as **Ready** and traffic is routed to the instance.</span></span>
6. <span data-ttu-id="50ac1-131">Viene chiamato il metodo [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) .</span><span class="sxs-lookup"><span data-stu-id="50ac1-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="50ac1-132">Esempio di attività di avvio</span><span class="sxs-lookup"><span data-stu-id="50ac1-132">Example of a startup task</span></span>
<span data-ttu-id="50ac1-133">Le attività di avvio vengono definite nel file [ServiceDefinition.csdef] nell'elemento **Task** .</span><span class="sxs-lookup"><span data-stu-id="50ac1-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span></span> <span data-ttu-id="50ac1-134">L'attributo **commandLine** specifica il nome e i parametri del file batch o del comando di console di avvio, l'attributo **executionContext** specifica il livello di privilegio dell'attività di avvio e l'attributo **taskType** specifica la modalità di esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="50ac1-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span></span>

<span data-ttu-id="50ac1-135">In questo esempio viene creata la variabile di ambiente **MyVersionNumber** per l'attività di avvio e il relativo valore viene impostato su "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="50ac1-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span></span>

<span data-ttu-id="50ac1-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="50ac1-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="50ac1-137">Nell'esempio seguente il file batch **Startup.cmd** scrive la riga "The current version is 1.0.0.0" nel file StartupLog.txt nella directory specificata dalla variabile di ambiente TEMP.</span><span class="sxs-lookup"><span data-stu-id="50ac1-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span></span> <span data-ttu-id="50ac1-138">La riga `EXIT /B 0` assicura che l'attività di avvio termini con un argomento **errorlevel** uguale a zero.</span><span class="sxs-lookup"><span data-stu-id="50ac1-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO The current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="50ac1-139">In Visual Studio la proprietà **Copia nella directory di output** per il file batch di avvio deve essere impostata su **Copia sempre** per garantire la distribuzione corretta del file batch di avvio nel progetto in Azure (**approot\\bin** per i ruoli Web e **approot** per i ruoli di lavoro).</span><span class="sxs-lookup"><span data-stu-id="50ac1-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="50ac1-140">Descrizione degli attributi di Task</span><span class="sxs-lookup"><span data-stu-id="50ac1-140">Description of task attributes</span></span>
<span data-ttu-id="50ac1-141">Di seguito vengono descritti gli attributi dell'elemento **Task** nel file [ServiceDefinition.csdef] :</span><span class="sxs-lookup"><span data-stu-id="50ac1-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="50ac1-142">**commandLine** : specifica la riga di comando per l'attività di avvio, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="50ac1-142">**commandLine** - Specifies the command line for the startup task:</span></span>

* <span data-ttu-id="50ac1-143">Il comando, con i parametri della riga di comando facoltativi, che inizia l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-143">The command, with optional command line parameters, which begins the startup task.</span></span>
* <span data-ttu-id="50ac1-144">Questo è spesso il nome del file batch con estensione cmd o bat.</span><span class="sxs-lookup"><span data-stu-id="50ac1-144">Frequently this is the filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="50ac1-145">L'attività è relativa alla cartella AppRoot\\Bin per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="50ac1-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span></span> <span data-ttu-id="50ac1-146">Le variabili di ambiente non vengono espanse per determinare il percorso e il file dell'attività.</span><span class="sxs-lookup"><span data-stu-id="50ac1-146">Environment variables are not expanded in determining the path and file of the task.</span></span> <span data-ttu-id="50ac1-147">Se è necessaria l'espansione dell'ambiente, è possibile creare un piccolo script con estensione cmd con il quale richiamare l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="50ac1-148">Può essere un'applicazione console o un file batch che avvia uno [script di PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="50ac1-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="50ac1-149">**executionContext** : specifica il livello di privilegio per l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-149">**executionContext** - Specifies the privilege level for the startup task.</span></span> <span data-ttu-id="50ac1-150">Il livello di privilegio può essere limitato o elevato:</span><span class="sxs-lookup"><span data-stu-id="50ac1-150">The privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="50ac1-151">**limitato**</span><span class="sxs-lookup"><span data-stu-id="50ac1-151">**limited**</span></span>  
  <span data-ttu-id="50ac1-152">: l'attività di avvio viene eseguita con gli stessi privilegi del ruolo.</span><span class="sxs-lookup"><span data-stu-id="50ac1-152">The startup task runs with the same privileges as the role.</span></span> <span data-ttu-id="50ac1-153">Quando anche l'attributo **executionContext** dell'elemento [Runtime] è **limitato**, vengono usati i privilegi utente.</span><span class="sxs-lookup"><span data-stu-id="50ac1-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="50ac1-154">**elevato**</span><span class="sxs-lookup"><span data-stu-id="50ac1-154">**elevated**</span></span>  
  <span data-ttu-id="50ac1-155">: l'attività di avvio viene eseguita con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="50ac1-155">The startup task runs with administrator privileges.</span></span> <span data-ttu-id="50ac1-156">In questo modo attraverso le attività di avvio è possibile installare programmi, apportare modifiche alla configurazione di IIS, effettuare modifiche al Registro di sistema e altre attività a livello di amministratore senza aumentare il livello di privilegio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="50ac1-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="50ac1-157">Il livello di privilegio dell'attività di avvio non deve essere necessariamente uguale al livello di privilegio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="50ac1-157">The privilege level of a startup task does not need to be the same as the role itself.</span></span>
> 
> 

<span data-ttu-id="50ac1-158">**taskType** : specifica la modalità di esecuzione di un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-158">**taskType** - Specifies the way a startup task is executed.</span></span>

* <span data-ttu-id="50ac1-159">**simple**</span><span class="sxs-lookup"><span data-stu-id="50ac1-159">**simple**</span></span>  
  <span data-ttu-id="50ac1-160">vengono eseguite in modo sincrono, una alla volta, nell'ordine specificato nel file [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="50ac1-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="50ac1-161">Quando un'attività di avvio **simple** termina con un valore **errorlevel** uguale a zero, viene eseguita l'attività di avvio **simple** successiva.</span><span class="sxs-lookup"><span data-stu-id="50ac1-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span></span> <span data-ttu-id="50ac1-162">Se non sono presenti altre attività di avvio **simple** da eseguire, viene avviato il ruolo.</span><span class="sxs-lookup"><span data-stu-id="50ac1-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="50ac1-163">Se l'attività **simple** termina con un valore **errorlevel** diverso da zero, l'istanza viene bloccata.</span><span class="sxs-lookup"><span data-stu-id="50ac1-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span></span> <span data-ttu-id="50ac1-164">Le successive attività di avvio **simple** e il ruolo non vengono avviati.</span><span class="sxs-lookup"><span data-stu-id="50ac1-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="50ac1-165">Per assicurarsi che il file batch termini con un valore **errorlevel** uguale a zero, eseguire il comando `EXIT /B 0` al termine del processo del file batch.</span><span class="sxs-lookup"><span data-stu-id="50ac1-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span></span>
* <span data-ttu-id="50ac1-166">**background**</span><span class="sxs-lookup"><span data-stu-id="50ac1-166">**background**</span></span>  
  <span data-ttu-id="50ac1-167">vengono eseguite in modo asincrono, in parallelo con l'avvio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="50ac1-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span>
* <span data-ttu-id="50ac1-168">**foreground**</span><span class="sxs-lookup"><span data-stu-id="50ac1-168">**foreground**</span></span>  
  <span data-ttu-id="50ac1-169">vengono eseguite in modo asincrono, in parallelo con l'avvio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="50ac1-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span> <span data-ttu-id="50ac1-170">La differenza principale tra un'attività **foreground** e un'attività **background** è che l'attività **foreground** impedisce il riciclo o l'arresto del ruolo fino al termine dell'attività.</span><span class="sxs-lookup"><span data-stu-id="50ac1-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span></span> <span data-ttu-id="50ac1-171">Le attività **background** non prevedono questa restrizione.</span><span class="sxs-lookup"><span data-stu-id="50ac1-171">The **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="50ac1-172">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="50ac1-172">Environment variables</span></span>
<span data-ttu-id="50ac1-173">Le variabili di ambiente costituiscono un modo per passare le informazioni a un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-173">Environment variables are a way to pass information to a startup task.</span></span> <span data-ttu-id="50ac1-174">È ad esempio possibile inserire il percorso di un BLOB contenente un programma da installare, i numeri di porta che verranno usati dal ruolo o impostazioni per controllare le funzionalità dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="50ac1-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span></span>

<span data-ttu-id="50ac1-175">Esistono due tipi di variabili di ambiente per le attività di avvio: le variabili di ambiente statiche e le variabili di ambiente basate sui membri della classe [RoleEnvironment] .</span><span class="sxs-lookup"><span data-stu-id="50ac1-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span></span> <span data-ttu-id="50ac1-176">Entrambi si trovano nella sezione [Environment] del file [ServiceDefinition.csdef] e per entrambi vengono usati l'elemento [Variable] e l'attributo **name**.</span><span class="sxs-lookup"><span data-stu-id="50ac1-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="50ac1-177">Per le variabili di ambiente statiche viene usato l'attributo **value** dell'elemento [Variable] .</span><span class="sxs-lookup"><span data-stu-id="50ac1-177">Static environment variables uses the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="50ac1-178">Nell'esempio precedente viene creata la variabile di ambiente **MyVersionNumber** con un valore statico di "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="50ac1-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="50ac1-179">Un altro esempio potrebbe essere la creazione di una variabile di ambiente **StagingOrProduction** impostabile manualmente sui valori "**staging**" o "**production**" per eseguire azioni di avvio diverse in base al valore della variabile di ambiente **StagingOrProduction**.</span><span class="sxs-lookup"><span data-stu-id="50ac1-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="50ac1-180">Per le variabili di ambiente basate sui membri della classe RoleEnvironment non viene usato l'attributo **value** dell'elemento [Variable] .</span><span class="sxs-lookup"><span data-stu-id="50ac1-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="50ac1-181">Viene invece usato l'elemento figlio [RoleInstanceValue], con il valore appropriato dell'attributo **XPath**, per creare una variabile di ambiente basata su un membro specifico della classe [RoleEnvironment].</span><span class="sxs-lookup"><span data-stu-id="50ac1-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span></span> <span data-ttu-id="50ac1-182">I valori dell'attributo **XPath** per accedere ai diversi valori di [RoleEnvironment] sono disponibili [qui](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="50ac1-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="50ac1-183">Per creare una variabile di ambiente che sia "**true**" se l'istanza è in esecuzione nell'emulatore di calcolo e "**false**" se è in esecuzione nel cloud, ad esempio, usare gli elementi [Variable] e [RoleInstanceValue] seguenti:</span><span class="sxs-lookup"><span data-stu-id="50ac1-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create the environment variable that informs the startup task whether it is running
                in the Compute Emulator or in the cloud. "%ComputeEmulatorRunning%"=="true" when
                running in the Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in the cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="50ac1-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50ac1-184">Next steps</span></span>
<span data-ttu-id="50ac1-185">Informazioni su come eseguire alcune [attività di avvio comuni](cloud-services-startup-tasks-common.md) con il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="50ac1-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="50ac1-186">[Creare il pacchetto](cloud-services-model-and-package.md) del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="50ac1-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

<span data-ttu-id="50ac1-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="50ac1-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="50ac1-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="50ac1-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
<span data-ttu-id="50ac1-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span><span class="sxs-lookup"><span data-stu-id="50ac1-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span></span>
<span data-ttu-id="50ac1-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span><span class="sxs-lookup"><span data-stu-id="50ac1-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span></span>
<span data-ttu-id="50ac1-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="50ac1-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="50ac1-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="50ac1-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="50ac1-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="50ac1-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
<span data-ttu-id="50ac1-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span><span class="sxs-lookup"><span data-stu-id="50ac1-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span></span>
