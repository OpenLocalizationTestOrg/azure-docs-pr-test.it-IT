---
title: Informazioni sui criteri di sicurezza dei microservizi di Azure | Documentazione Microsoft
description: Panoramica dell'esecuzione di un'applicazione di Service Fabric con account di sicurezza di sistema e locali, incluso il punto SetupEntry in cui un'applicazione deve eseguire un'azione con privilegi prima dell'avvio
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: e673b45a43a06d18040c3437caf8765704d5c36a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="f6c4e-103">Configurare i criteri di sicurezza per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="f6c4e-103">Configure security policies for your application</span></span>
<span data-ttu-id="f6c4e-104">Azure Service Fabric consente di proteggere le applicazioni in esecuzione nel cluster con account utente diversi.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-104">By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts.</span></span> <span data-ttu-id="f6c4e-105">Service Fabric permette anche di proteggere le risorse usate dalle applicazioni in fase di distribuzione con l'account utente, ad esempio file, directory e certificati.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-105">Service Fabric also helps secure the resources that are used by applications at the time of deployment under the user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="f6c4e-106">In questo modo le applicazioni in esecuzione, anche in un ambiente ospitato condiviso, sono reciprocamente protette.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="f6c4e-107">Per impostazione predefinita, le applicazioni di Service Fabric vengono eseguite con lo stesso account con cui viene eseguito il processo Fabric.exe.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-107">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span></span> <span data-ttu-id="f6c4e-108">Service Fabric consente anche di eseguire le applicazioni con un account utente locale o un account di sistema locale, specificato nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-108">Service Fabric also provides the capability to run applications under a local user account or local system account, which is specified within the application manifest.</span></span> <span data-ttu-id="f6c4e-109">I tipi di account supportati dal sistema locale sono **LocalUser**, **NetworkService**, **LocalService** e **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="f6c4e-110">Quando si esegue Service Fabric in Windows Server nel data center usando il programma di installazione autonomo, è possibile usare gli account di dominio di Active Directory, inclusi gli account del servizio gestito del gruppo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-110">When you're running Service Fabric on Windows Server in your datacenter by using the standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="f6c4e-111">È possibile definire e creare gruppi di utenti per aggiungere uno o più utenti a ogni gruppo e gestirli insieme.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-111">You can define and create user groups so that one or more users can be added to each group to be managed together.</span></span> <span data-ttu-id="f6c4e-112">Questo aspetto è utile quando sono presenti più utenti per punti di ingresso del servizio differenti che devono avere determinati privilegi comuni disponibili a livello di gruppo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-112">This is useful when there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span>

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="f6c4e-113">Configurare i criteri per il punto di ingresso dell'installazione del servizio</span><span class="sxs-lookup"><span data-stu-id="f6c4e-113">Configure the policy for a service setup entry point</span></span>
<span data-ttu-id="f6c4e-114">Come descritto nel [modello applicativo](service-fabric-application-model.md), il punto di ingresso dell'installazione, **SetupEntryPoint**, è un punto di ingresso con privilegi che viene eseguito con le stesse credenziali di Service Fabric, in genere, l'account *NetworkService*, prima di qualsiasi altro punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-114">As described in the [application model](service-fabric-application-model.md), the setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with the same credentials as Service Fabric (typically the *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="f6c4e-115">L'eseguibile specificato da **EntryPoint** è in genere l'host del servizio a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-115">The executable that is specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="f6c4e-116">Un punto di ingresso dell'installazione separato consente di evitare di dover eseguire l'eseguibile dell'host del servizio con privilegi elevati per lunghi periodi di tempo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-116">So having a separate setup entry point avoids having to run the service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="f6c4e-117">L'eseguibile specificato da **EntryPoint** viene eseguito dopo che **SetupEntryPoint** termina correttamente.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-117">The executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="f6c4e-118">Il processo risultante viene monitorato e riavviato ed inizia di nuovo con **SetupEntryPoint**, se termina o si arresta in modo anomalo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-118">The resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="f6c4e-119">Il seguente è un semplice esempio di manifesto del servizio in cui sono presenti SetupEntryPoint e l'elemento EntryPoint principale per il servizio.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-119">The following is a simple service manifest example that shows the SetupEntryPoint and the main EntryPoint for the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-the-policy-by-using-a-local-account"></a><span data-ttu-id="f6c4e-120">Configurare i criteri usando un account locale</span><span class="sxs-lookup"><span data-stu-id="f6c4e-120">Configure the policy by using a local account</span></span>
<span data-ttu-id="f6c4e-121">Dopo aver configurato un punto di ingresso di configurazione per il servizio, è possibile modificare le autorizzazioni di sicurezza in base alle quali viene eseguito nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-121">After you configure the service to have a setup entry point, you can change the security permissions that it runs under in the application manifest.</span></span> <span data-ttu-id="f6c4e-122">L'esempio seguente illustra come configurare il servizio in modo che venga eseguito con i privilegi dell'account amministratore utenti.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-122">The following example shows how to configure the service to run under user administrator account privileges.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

<span data-ttu-id="f6c4e-123">Creare prima di tutto una sezione **Principals** con un nome utente, ad esempio SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="f6c4e-124">Ciò indica che l'utente è un membro del gruppo di sistema Administrators.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-124">This indicates that the user is a member of the Administrators system group.</span></span>

<span data-ttu-id="f6c4e-125">Successivamente, configurare nella sezione **ServiceManifestImport** un criterio per applicare tale entità a **SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-125">Next, under the **ServiceManifestImport** section, configure a policy to apply this principal to **SetupEntryPoint**.</span></span> <span data-ttu-id="f6c4e-126">Ciò indica a Service Fabric che quando viene eseguito il file **mySetup.bat**, deve essere un profilo `RunAs` con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-126">This tells Service Fabric that when the **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="f6c4e-127">Dato che *non* sono stati applicati criteri al punto di ingresso principale, il codice in **MyServiceHost.exe** viene eseguito con l'account **NetworkService** di sistema,</span><span class="sxs-lookup"><span data-stu-id="f6c4e-127">Given that you have *not* applied a policy to the main entry point, the code in **MyServiceHost.exe** runs under the system **NetworkService** account.</span></span> <span data-ttu-id="f6c4e-128">ossia l'account predefinito con cui vengono eseguiti tutti i punti di ingresso del servizio.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-128">This is the default account that all service entry points are run as.</span></span>

<span data-ttu-id="f6c4e-129">A questo punto, aggiungere il file MySetup.bat al progetto di Visual Studio per testare i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-129">Let's now add the file MySetup.bat to the Visual Studio project to test the administrator privileges.</span></span> <span data-ttu-id="f6c4e-130">In Visual Studio fare clic con il pulsante destro del mouse sul progetto di servizio e aggiungere un nuovo file denominato MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-130">In Visual Studio, right-click the service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="f6c4e-131">Verificare quindi che il file MySetup.bat sia incluso nel pacchetto del servizio.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-131">Next, ensure that the MySetup.bat file is included in the service package.</span></span> <span data-ttu-id="f6c4e-132">Per impostazione predefinita, non è incluso.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-132">By default, it is not.</span></span> <span data-ttu-id="f6c4e-133">Selezionare il file, fare clic con il pulsante destro del mouse per visualizzare il menu di scelta rapida e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-133">Select the file, right-click to get the context menu, and choose **Properties**.</span></span> <span data-ttu-id="f6c4e-134">Nella finestra di dialogo delle proprietà verificare che **Copia nella directory di output** sia impostato su **Copia se più recente**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-134">In the Properties dialog box, ensure that **Copy to Output Directory** is set to **Copy if newer**.</span></span> <span data-ttu-id="f6c4e-135">Vedere lo screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-135">See the following screenshot.</span></span>

![CopyToOutput di Visual Studio per il file batch SetupEntryPoint][image1]

<span data-ttu-id="f6c4e-137">Aprire il file MySetup.bat e aggiungere i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-137">Now open the MySetup.bat file and add the following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="f6c4e-138">Successivamente, compilare e distribuire la soluzione a un cluster di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-138">Next, build and deploy the solution to a local development cluster.</span></span> <span data-ttu-id="f6c4e-139">Dopo aver avviato il servizio, come mostrato in Service Fabric Explorer, sarà possibile verificare la corretta esecuzione del file MySetup.bat in due modi.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-139">After the service has started, as shown in Service Fabric Explorer, you can see that the MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="f6c4e-140">Avviare un prompt dei comandi di PowerShell e digitare:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="f6c4e-141">Annotare il nome del nodo in cui il servizio è stato distribuito e avviato in Service Fabric Explorer, ad esempio Node 2.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-141">Then, note the name of the node where the service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="f6c4e-142">Passare quindi alla cartella di lavoro dell'istanza dell'applicazione per trovare il file out.txt che mostra il valore di **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-142">Next, navigate to the application instance work folder to find the out.txt file that shows the value of **TestVariable**.</span></span> <span data-ttu-id="f6c4e-143">Se, ad esempio, il servizio è stato distribuito in Node 2, è possibile passare a questo percorso per **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-143">For example, if this service was deployed to Node 2, then you can go to this path for the **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a><span data-ttu-id="f6c4e-144">Configurare i criteri usando gli account di sistema locale</span><span class="sxs-lookup"><span data-stu-id="f6c4e-144">Configure the policy by using local system accounts</span></span>
<span data-ttu-id="f6c4e-145">Spesso è preferibile eseguire lo script di avvio usando un account di sistema locale invece di un account amministratore.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-145">Often, it's preferable to run the startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="f6c4e-146">L'esecuzione dei criteri RunAs come membro del gruppo Administrators in genere non ha esito positivo in quanto per i computer è abilitato il controllo di accesso dell'utente per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-146">Running the RunAs policy as a member of the Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="f6c4e-147">In questi casi, **è consigliabile eseguire SetupEntryPoint come LocalSystem invece che come utente locale aggiunto al gruppo Administrators**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-147">In such cases, **the recommendation is to run the SetupEntryPoint as LocalSystem, instead of as a local user added to Administrators group**.</span></span> <span data-ttu-id="f6c4e-148">L'esempio seguente illustra l'impostazione di SetupEntryPoint per l'esecuzione come LocalSystem:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-148">The following example shows setting the SetupEntryPoint to run as LocalSystem:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="f6c4e-149">Avviare i comandi PowerShell da un punto di ingresso dell'installazione</span><span class="sxs-lookup"><span data-stu-id="f6c4e-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="f6c4e-150">Per eseguire PowerShell dal punto **SetupEntryPoint**, è possibile eseguire **PowerShell.exe** in un file batch che punta a un file di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-150">To run PowerShell from the **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points to a PowerShell file.</span></span> <span data-ttu-id="f6c4e-151">Aggiungere prima di tutto un file PowerShell al progetto del servizio, ad esempio **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-151">First, add a PowerShell file to the service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="f6c4e-152">Ricordarsi di impostare la proprietà *Copia se più recente* in modo che il file venga incluso anche nel pacchetto servizio.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-152">Remember to set the *Copy if newer* property so that the file is also included in the service package.</span></span> <span data-ttu-id="f6c4e-153">L'esempio seguente illustra un file batch di esempio per avviare un file PowerShell denominato MySetup.ps1, che imposta una variabile di ambiente di sistema denominata **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-153">The following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="f6c4e-154">MySetup.bat per avviare il file PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-154">MySetup.bat to start a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="f6c4e-155">Nel file di PowerShell aggiungere quanto segue per impostare una variabile di ambiente di sistema:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-155">In the PowerShell file, add the following to set a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="f6c4e-156">Per impostazione predefinita, quando viene eseguito, il file batch cerca i file nella cartella dell'applicazione denominata **work**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-156">By default, when the batch file runs, it looks at the application folder called **work** for files.</span></span> <span data-ttu-id="f6c4e-157">In questo caso, quando MySetup.bat viene eseguito, il file MySetup.ps1 deve trovarsi nella stessa cartella, ovvero la cartella **code package** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-157">In this case, when MySetup.bat runs, we want this to find the MySetup.ps1 file in the same folder, which is the application **code package** folder.</span></span> <span data-ttu-id="f6c4e-158">Per modificare questa cartella, impostare la cartella di lavoro:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-158">To change this folder, set the working folder:</span></span>
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="f6c4e-159">Uso del reindirizzamento della console per il debug locale</span><span class="sxs-lookup"><span data-stu-id="f6c4e-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="f6c4e-160">A volte può essere utile visualizzare l'output della console dall'esecuzione di uno script a scopo di debug.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-160">Occasionally, it's useful to see the console output from running a script for debugging purposes.</span></span> <span data-ttu-id="f6c4e-161">A questo scopo, è possibile impostare criteri di reindirizzamento della console che scrivono l'output in un file.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-161">To do this, you can set a console redirection policy, which writes the output to a file.</span></span> <span data-ttu-id="f6c4e-162">L'output del file viene scritto nella cartella dell'applicazione denominata **log** nel nodo in cui l'applicazione viene distribuita ed eseguita.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-162">The file output is written to the application folder called **log** on the node where the application is deployed and run.</span></span> <span data-ttu-id="f6c4e-163">Vedere la posizione in cui si trova nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-163">(See where to find this in the preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="f6c4e-164">Non usare mai i criteri di reindirizzamento della console in un'applicazione distribuita nell'ambiente di produzione, perché ciò può incidere sul failover dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-164">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="f6c4e-165">Usare questa opzione *solo* a scopo di sviluppo e debug locale.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="f6c4e-166">L'esempio seguente illustra come impostare il reindirizzamento della console con un valore FileRetentionCount:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-166">The following example shows setting the console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="f6c4e-167">Se si modifica il file MySetup.ps1 per scrivere un comando **Echo**, questo verrà scritto nel file di output a scopo di debug:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-167">If you now change the MySetup.ps1 file to write an **Echo** command, this will write to the output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

<span data-ttu-id="f6c4e-168">**Dopo avere eseguito il debug dello script, rimuovere immediatamente i criteri di reindirizzamento della console**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="f6c4e-169">Configurare i criteri per i pacchetti di codice del servizio</span><span class="sxs-lookup"><span data-stu-id="f6c4e-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="f6c4e-170">Nei passaggi precedenti è stato illustrato come applicare i criteri RunAs a SetupEntryPoint.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-170">In the preceding steps, you saw how to apply a RunAs policy to SetupEntryPoint.</span></span> <span data-ttu-id="f6c4e-171">A questo punto è possibile vedere come creare entità diverse che possono essere applicate come criteri del servizio.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-171">Let's look a little deeper into how to create different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="f6c4e-172">Creare gruppi di utenti locali</span><span class="sxs-lookup"><span data-stu-id="f6c4e-172">Create local user groups</span></span>
<span data-ttu-id="f6c4e-173">È possibile definire e creare gruppi di utenti che permettono di aggiungere uno o più utenti a un gruppo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-173">You can define and create user groups that allow one or more users to be added to a group.</span></span> <span data-ttu-id="f6c4e-174">Questo aspetto è utile quando sono presenti più utenti per punti di ingresso del servizio differenti che devono avere determinati privilegi comuni disponibili a livello di gruppo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-174">This is useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span> <span data-ttu-id="f6c4e-175">L'esempio seguente illustra un gruppo locale denominato **LocalAdminGroup** con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-175">The following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="f6c4e-176">Due utenti, Customer1 e Customer2, diventano membri di questo gruppo locale.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a><span data-ttu-id="f6c4e-177">Creare utenti locali</span><span class="sxs-lookup"><span data-stu-id="f6c4e-177">Create local users</span></span>
<span data-ttu-id="f6c4e-178">È possibile creare un utente locale che può essere usato per proteggere un servizio all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-178">You can create a local user that can be used to help secure a service within the application.</span></span> <span data-ttu-id="f6c4e-179">Quando viene specificato un tipo di account **LocalUser** nella sezione Principals del manifesto dell'applicazione, Service Fabric crea account utente locali nei computer in cui viene distribuita l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-179">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span></span> <span data-ttu-id="f6c4e-180">Per impostazione predefinita, questi account non hanno gli stessi nomi di quelli specificati nel manifesto dell'applicazione (Customer3 nell'esempio seguente).</span><span class="sxs-lookup"><span data-stu-id="f6c4e-180">By default, these accounts do not have the same names as those specified in the application manifest (for example, Customer3 in the following sample).</span></span> <span data-ttu-id="f6c4e-181">Vengono invece generati in modo dinamico e hanno password casuali.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="f6c4e-182">Se un'applicazione richiede che l'account utente e la password siano uguali in tutti i computer, ad esempio per abilitare l'autenticazione NTLM, il manifesto del cluster deve impostare NTLMAuthenticationEnabled su true.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-182">If an application requires that the user account and password be same on all machines (for example, to enable NTLM authentication), the cluster manifest must set NTLMAuthenticationEnabled to true.</span></span> <span data-ttu-id="f6c4e-183">Il manifesto del cluster deve anche specificare un elemento NTLMAuthenticationPasswordSecret che verrà usato per generare la stessa password in tutti i computer.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-183">The cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used to generate the same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a><span data-ttu-id="f6c4e-184">Assegnare criteri ai pacchetti di codice del servizio</span><span class="sxs-lookup"><span data-stu-id="f6c4e-184">Assign policies to the service code packages</span></span>
<span data-ttu-id="f6c4e-185">La sezione **RunAsPolicy** di un oggetto **ServiceManifestImport** specifica l'account nella sezione Principals che deve essere usato per eseguire un pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-185">The **RunAsPolicy** section for a **ServiceManifestImport** specifies the account from the principals section that should be used to run a code package.</span></span> <span data-ttu-id="f6c4e-186">Associa anche i pacchetti di codice nel manifesto del servizio agli account utente nella sezione Principals.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-186">It also associates code packages from the service manifest with user accounts in the principals section.</span></span> <span data-ttu-id="f6c4e-187">È possibile specificare questa opzione per i punti di ingresso principale o di configurazione oppure specificare `All` per applicarla a entrambi.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-187">You can specify this for the setup or main entry points, or you can specify `All` to apply it to both.</span></span> <span data-ttu-id="f6c4e-188">L'esempio seguente illustra l'applicazione di diversi criteri:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-188">The following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="f6c4e-189">Se **EntryPointType** non è specificato, il valore predefinito è impostato su EntryPointType="Main".</span><span class="sxs-lookup"><span data-stu-id="f6c4e-189">If **EntryPointType** is not specified, the default is set to EntryPointType=”Main”.</span></span> <span data-ttu-id="f6c4e-190">Specificare l'oggetto **SetupEntryPoint** risulta particolarmente utile per eseguire determinate operazioni di configurazione con privilegi elevati con un account di sistema,</span><span class="sxs-lookup"><span data-stu-id="f6c4e-190">Specifying **SetupEntryPoint** is especially useful when you want to run certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="f6c4e-191">mentre il codice del servizio effettivo può essere eseguito con un account con privilegi inferiori.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-191">The actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-to-all-service-code-packages"></a><span data-ttu-id="f6c4e-192">Applicare un criterio predefinito a tutti i pacchetti di codice del servizio</span><span class="sxs-lookup"><span data-stu-id="f6c4e-192">Apply a default policy to all service code packages</span></span>
<span data-ttu-id="f6c4e-193">La sezione **DefaultRunAsPolicy** consente di specificare un account utente predefinito per tutti i pacchetti di codice per i quali non è definito un oggetto **RunAsPolicy** specifico.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-193">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="f6c4e-194">Se la maggior parte dei pacchetti di codice specificati nel manifesto del servizio usato da un'applicazione deve essere eseguita con lo stesso utente, l'applicazione può definire solo criteri RunAs predefiniti con questo account utente.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-194">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="f6c4e-195">L'esempio seguente mostra che se l'oggetto **RunAsPolicy** non è specificato per un pacchetto di codice, questo deve essere eseguito con l'account **MyDefaultAccount** specificato nella sezione Principals.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-195">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** specified in the principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="f6c4e-196">Uso di un utente o un gruppo di dominio di Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6c4e-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="f6c4e-197">Per un'istanza di Service Fabric installata in Windows Server con il programma di installazione autonomo, è possibile eseguire il servizio con le credenziali per un account utente o di gruppo di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-197">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service under the credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="f6c4e-198">Si tratta di Active Directory locale nel dominio e non di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6c4e-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f6c4e-199">Usando un utente o un gruppo del dominio, sarà quindi possibile accedere ad altre risorse del dominio (ad esempio, condivisioni file) a cui sono state concesse le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-199">By using a domain user or group, you can then access other resources in the domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="f6c4e-200">L'esempio seguente illustra un utente di Active Directory denominato *TestUser* con la password del dominio crittografata con un certificato denominato *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-200">The following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="f6c4e-201">È possibile usare il comando `Invoke-ServiceFabricEncryptText` PowerShell per creare il testo crittografato segreto.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-201">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text.</span></span> <span data-ttu-id="f6c4e-202">Vedere [Gestione dei segreti nelle applicazioni di Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="f6c4e-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="f6c4e-203">È necessario distribuire la chiave privata del certificato per decrittografare la password nel computer locale con un metodo fuori banda; in Azure questa operazione viene eseguita usando Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-203">You must deploy the private key of the certificate to decrypt the password to the local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="f6c4e-204">Quando distribuisce il pacchetto servizio nel computer, Service Fabric può quindi decrittografare il segreto e, con il nome utente, eseguire l'autenticazione ad Active Directory per l'esecuzione con queste credenziali.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-204">Then, when Service Fabric deploys the service package to the machine, it is able to decrypt the secret and (along with the user name) authenticate with Active Directory to run under those credentials.</span></span>

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="f6c4e-205">Usare un account del servizio gestito del gruppo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="f6c4e-206">Per un'istanza di Service Fabric installata in Windows Server con il programma di installazione autonomo, è possibile eseguire il servizio come account del servizio gestito del gruppo (gMSA).</span><span class="sxs-lookup"><span data-stu-id="f6c4e-206">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="f6c4e-207">Si noti che si tratta di Active Directory locale nel dominio e non di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6c4e-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f6c4e-208">Usando un account gMSA, nel `Application Manifest` non viene archiviata alcuna password o password crittografata.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-208">By using a gMSA there is no password or encrypted password stored in the `Application Manifest`.</span></span>

<span data-ttu-id="f6c4e-209">L'esempio seguente mostra come creare un account gMSA denominato *svc-Test$*, come distribuire tale account del servizio gestito ai nodi del cluster e come configurare l'entità utente.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-209">The following example shows how to create a gMSA account called *svc-Test$*; how to deploy that managed service account to the cluster nodes; and how to configure the user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="f6c4e-210">Prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-210">Prerequisites.</span></span>
- <span data-ttu-id="f6c4e-211">Il dominio richiede una chiave radice del Servizio distribuzione chiavi.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-211">The domain needs a KDS root key.</span></span>
- <span data-ttu-id="f6c4e-212">Il dominio deve essere a livello funzionale di Windows Server 2012 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-212">The domain needs to be at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="f6c4e-213">Esempio</span><span class="sxs-lookup"><span data-stu-id="f6c4e-213">Example</span></span>
1. <span data-ttu-id="f6c4e-214">Chiedere a un amministratore di dominio di Active Directory di creare un account del servizio gestito del gruppo usando il cmdlet `New-ADServiceAccount` e assicurarsi che `PrincipalsAllowedToRetrieveManagedPassword` includa tutti i nodi del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-214">Have an active directory domain administrator create a group managed service account using the `New-ADServiceAccount` commandlet and ensure that the `PrincipalsAllowedToRetrieveManagedPassword` includes all of the service fabric cluster nodes.</span></span> <span data-ttu-id="f6c4e-215">Si noti che `AccountName`, `DnsHostName` e `ServicePrincipalName` devono essere univoci.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="f6c4e-216">In ognuno dei nodi del cluster di Service Fabric, ad esempio `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`, installare e testare l'account del servizio gestito del gruppo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-216">On each of the service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test the gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="f6c4e-217">Configurare l'entità utente e RunAsPolicy per fare riferimento all'utente.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-217">Configure the User principal, and configure the RunAsPolicy to reference the user.</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="f6c4e-218">Assegnare un criterio di accesso di sicurezza per gli endpoint HTTP e HTTPS</span><span class="sxs-lookup"><span data-stu-id="f6c4e-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="f6c4e-219">Se si applicano criteri RunAs a un servizio e il manifesto del servizio dichiara le risorse dell'endpoint con il protocollo HTTP, è necessario specificare **SecurityAccessPolicy** per garantire che le porte allocate a questi endpoint siano correttamente inserite nell'elenco di controllo di accesso per l'account utente RunAs con cui viene eseguito il servizio.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-219">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy** to ensure that ports allocated to these endpoints are correctly access-control listed for the RunAs user account that the service runs under.</span></span> <span data-ttu-id="f6c4e-220">In caso contrario, **http.sys** non ha accesso al servizio e le chiamate del client hanno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-220">Otherwise, **http.sys** does not have access to the service, and you get failures with calls from the client.</span></span> <span data-ttu-id="f6c4e-221">L'esempio seguente applica l'account Customer1 a un endpoint denominato **EndpointName**, a cui assegna diritti di accesso completi.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-221">The following example applies the Customer1 account to an endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="f6c4e-222">Per l'endpoint HTTPS, è necessario indicare anche il nome del certificato da restituire al client.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-222">For the HTTPS endpoint, you also have to indicate the name of the certificate to return to the client.</span></span> <span data-ttu-id="f6c4e-223">A tale scopo, è possibile usare **EndpointBindingPolicy**con il certificato definito nella sezione Certificates del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-223">You can do this by using **EndpointBindingPolicy**, with the certificate defined in a certificates section in the application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="f6c4e-224">Aggiornamento di più applicazioni con endpoint https</span><span class="sxs-lookup"><span data-stu-id="f6c4e-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="f6c4e-225">È necessario prestare attenzione a non utilizzare la **stessa porta** per istanze diverse della stessa applicazione quando si usa http**s**.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-225">You need to be careful not to use the **same port** for different instances of the same application when using http**s**.</span></span> <span data-ttu-id="f6c4e-226">Ciò è dovuto al fatto che Service Fabric non sarà in grado di aggiornare il certificato per una delle istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-226">The reason is that Service Fabric won't be able to upgrade the cert for one of the application instances.</span></span> <span data-ttu-id="f6c4e-227">Ad esempio, se sia l'applicazione 1 che l'applicazione 2 desiderano eseguire l'aggiornamento del certificato 1 al certificato 2.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-227">For example, if application 1 or application 2 both want to upgrade their cert 1 to cert 2.</span></span> <span data-ttu-id="f6c4e-228">Al momento dell'aggiornamento, Service Fabric potrebbe avere eliminato la registrazione del certificato 1 con http.sys anche se è ancora utilizzato dall'altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-228">When the upgrade happens, Service Fabric might have cleaned up the cert 1 registration with http.sys even though the other application is still using it.</span></span> <span data-ttu-id="f6c4e-229">Per evitare questo problema, Service Fabric rileva che è già presente un'altra istanza dell'applicazione registrata sulla porta con il certificato (a causa di http.sys) e l'operazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-229">To prevent this, Service Fabric detects that there is already another application instance registered on the port with the certificate (due to http.sys) and fails the operation.</span></span>

<span data-ttu-id="f6c4e-230">Pertanto Service Fabric non supporta l'aggiornamento di due servizi diversi mediante **la stessa porta** in istanze dell'applicazione diverse.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-230">Hence Service Fabric does not support upgrading two different services using **the same port** in different application instances.</span></span> <span data-ttu-id="f6c4e-231">In altre parole, non è possibile utilizzare lo stesso certificato in servizi diversi sulla stessa porta.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-231">In other words, you cannot use the same certificate on different services on the same port.</span></span> <span data-ttu-id="f6c4e-232">Se è necessario avere un certificato condiviso sulla stessa porta, occorre verificare che i servizi si trovino su computer diversi con vincoli di posizionamento.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-232">If you need to have a shared certificate on the same port, you need to ensure that the services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="f6c4e-233">In alternativa, utilizzare le porte dinamiche di Service Fabric se possibile per ogni servizio in ogni istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="f6c4e-234">Se si verifica un errore di aggiornamento con https, viene visualizzato un avviso indicante che l'API del server Windows HTTP non supporta più certificati per le applicazioni che condividono una porta.</span><span class="sxs-lookup"><span data-stu-id="f6c4e-234">If you see an upgrade fail with https, an error warning saying "The Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="f6c4e-235">Esempio completo del manifesto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f6c4e-235">A complete application manifest example</span></span>
<span data-ttu-id="f6c4e-236">Il manifesto dell'applicazione seguente illustra molte delle impostazioni:</span><span class="sxs-lookup"><span data-stu-id="f6c4e-236">The following application manifest shows many of the different settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed the EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="f6c4e-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6c4e-237">Next steps</span></span>
* [<span data-ttu-id="f6c4e-238">Informazioni sul modello applicativo</span><span class="sxs-lookup"><span data-stu-id="f6c4e-238">Understand the application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="f6c4e-239">Specificare le risorse in un manifesto del servizio</span><span class="sxs-lookup"><span data-stu-id="f6c4e-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="f6c4e-240">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="f6c4e-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
