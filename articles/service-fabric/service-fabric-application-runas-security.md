---
title: aaaLearn sui criteri di sicurezza di Azure microservizi | Documenti Microsoft
description: Una panoramica di come toorun un'applicazione di Service Fabric nel sistema e gli account di sicurezza locale, compreso il punto di SetupEntry hello in cui un'applicazione deve tooperform alcune privilegiato azione prima che venga avviato
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
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="f68ff-103">Configurare i criteri di sicurezza per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="f68ff-103">Configure security policies for your application</span></span>
<span data-ttu-id="f68ff-104">Tramite Azure Service Fabric, è possibile proteggere le applicazioni in esecuzione nel cluster hello con account utente diversi.</span><span class="sxs-lookup"><span data-stu-id="f68ff-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="f68ff-105">Service Fabric consente anche di hello sicuro le risorse usate dalle applicazioni in fase di hello della distribuzione con account utente di hello, ad esempio, file, directory e i certificati.</span><span class="sxs-lookup"><span data-stu-id="f68ff-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="f68ff-106">In questo modo le applicazioni in esecuzione, anche in un ambiente ospitato condiviso, sono reciprocamente protette.</span><span class="sxs-lookup"><span data-stu-id="f68ff-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="f68ff-107">Per impostazione predefinita, le applicazioni di Service Fabric eseguiti con account di hello cui viene eseguito il processo Fabric.exe hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="f68ff-108">Service Fabric fornisce anche funzionalità di hello toorun applicazioni tramite un account di sistema locale, che viene specificato nel manifesto dell'applicazione hello o un account utente locale.</span><span class="sxs-lookup"><span data-stu-id="f68ff-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="f68ff-109">I tipi di account supportati dal sistema locale sono **LocalUser**, **NetworkService**, **LocalService** e **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="f68ff-110">Quando si esegue Service Fabric in Windows Server nel Data Center tramite il programma di installazione di hello autonomo, è possibile utilizzare l'account di dominio Active Directory, inclusi gli account del servizio gestito di gruppo.</span><span class="sxs-lookup"><span data-stu-id="f68ff-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="f68ff-111">È possibile definire e creare gruppi di utenti in modo che è possibile aggiungere uno o più utenti tooeach gruppo toobe gestiti insieme.</span><span class="sxs-lookup"><span data-stu-id="f68ff-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="f68ff-112">Ciò è utile quando sono presenti più utenti per i punti di ingresso del servizio diverso e devono toohave determinati privilegi comune che sono disponibili a livello di gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="f68ff-113">Configurare i criteri di hello per un punto di ingresso del programma di installazione del servizio</span><span class="sxs-lookup"><span data-stu-id="f68ff-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="f68ff-114">Come descritto in hello [modello applicativo](service-fabric-application-model.md), hello punto di ingresso, il programma di installazione **SetupEntryPoint**, è un punto di ingresso con privilegi che viene eseguito con hello stesso credenziali come Service Fabric (in genere hello *NetworkService* account) prima di qualsiasi altro punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="f68ff-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="f68ff-115">file eseguibile Hello specificato da **EntryPoint** è in genere l'host del servizio hello con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="f68ff-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="f68ff-116">Pertanto, con una voce di programma di installazione separato punto si evita host del servizio hello toorun eseguibile con privilegi elevati per lunghi periodi di tempo.</span><span class="sxs-lookup"><span data-stu-id="f68ff-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="f68ff-117">Hello eseguibile che **EntryPoint** specifica viene eseguito dopo **SetupEntryPoint** termina correttamente.</span><span class="sxs-lookup"><span data-stu-id="f68ff-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="f68ff-118">Hello processo risultante viene monitorato e riavviato e inizia nuovamente con **SetupEntryPoint** se mai termina o arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="f68ff-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="f68ff-119">esempio Hello è riportato un esempio di manifesto servizio semplice che mostra hello SetupEntryPoint e il punto di ingresso principale per il servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

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

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="f68ff-120">Configurare i criteri di hello utilizzando un account locale</span><span class="sxs-lookup"><span data-stu-id="f68ff-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="f68ff-121">Dopo aver configurato hello servizio toohave un punto di ingresso del programma di installazione, è possibile modificare le autorizzazioni di sicurezza hello utilizzabile nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="f68ff-122">Hello di esempio seguente viene illustrato come tooconfigure hello toorun servizio con privilegi di account utente amministratore.</span><span class="sxs-lookup"><span data-stu-id="f68ff-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

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

<span data-ttu-id="f68ff-123">Creare prima di tutto una sezione **Principals** con un nome utente, ad esempio SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="f68ff-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="f68ff-124">Questo indica che l'utente hello è un membro del gruppo di amministratori di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="f68ff-125">Quindi, in hello **oggetto ServiceManifestImport** sezione, configurare un criterio tooapply questa entità troppo**SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="f68ff-126">In questo modo Service Fabric che quando hello **MySetup.bat** file viene eseguito, dovrebbe essere `RunAs` con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f68ff-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="f68ff-127">Disponendo di *non* applicato a un punto di ingresso principale toohello criteri, il codice hello in **MyServiceHost.exe** viene eseguito il sistema hello **NetworkService** account.</span><span class="sxs-lookup"><span data-stu-id="f68ff-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="f68ff-128">Si tratta di account predefinito hello che vengono eseguiti tutti i punti di ingresso del servizio.</span><span class="sxs-lookup"><span data-stu-id="f68ff-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="f68ff-129">Aggiungere ora hello file MySetup.bat toohello Visual Studio progetto tootest hello privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f68ff-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="f68ff-130">In Visual Studio, fare clic sul progetto servizio hello e aggiungere un nuovo file denominato MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="f68ff-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="f68ff-131">Verificare quindi che file MySetup.bat hello è incluso nel pacchetto di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="f68ff-132">Per impostazione predefinita, non è incluso.</span><span class="sxs-lookup"><span data-stu-id="f68ff-132">By default, it is not.</span></span> <span data-ttu-id="f68ff-133">Selezionare il file hello, menu di scelta rapida hello tooget destro e scegliere **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="f68ff-134">Nella finestra di dialogo Proprietà hello, assicurarsi che **copiare tooOutput Directory** è troppo**copia se più recente**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="f68ff-135">Vedere la seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-135">See hello following screenshot.</span></span>

![CopyToOutput di Visual Studio per il file batch SetupEntryPoint][image1]

<span data-ttu-id="f68ff-137">Ora aprire il file MySetup.bat hello e aggiungere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f68ff-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="f68ff-138">Successivamente, compilare e distribuire cluster di sviluppo locale tooa soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="f68ff-139">Dopo aver avviato il servizio di hello, come illustrato in Service Fabric Explorer, è possibile visualizzare che file hello MySetup.bat ha avuto esito positivo in un due modi.</span><span class="sxs-lookup"><span data-stu-id="f68ff-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="f68ff-140">Avviare un prompt dei comandi di PowerShell e digitare:</span><span class="sxs-lookup"><span data-stu-id="f68ff-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="f68ff-141">Quindi, annotare il nome di hello del nodo di hello in cui il servizio di hello è stato distribuito e avviato, ad esempio, in Service Fabric Explorer - nodo 2.</span><span class="sxs-lookup"><span data-stu-id="f68ff-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="f68ff-142">Passare toohello applicazione istanza lavoro cartella toofind hello file out.txt che Mostra valore hello **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="f68ff-143">Ad esempio, se questo servizio è stato distribuito tooNode 2, è possibile passare il percorso di toothis per hello **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="f68ff-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="f68ff-144">Configurare criteri di hello tramite gli account di sistema locale</span><span class="sxs-lookup"><span data-stu-id="f68ff-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="f68ff-145">Spesso, è preferibile toorun script di avvio hello utilizzando un account di sistema locale anziché un account amministratore.</span><span class="sxs-lookup"><span data-stu-id="f68ff-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="f68ff-146">Esecuzione di criteri di RunAs hello come membro del gruppo Administrators in genere non funziona correttamente poiché macchine dispongono di controllo accesso utente (UAC) abilitata per impostazione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="f68ff-147">In questi casi, **hello consiglia hello toorun SetupEntryPoint come LocalSystem, anziché come un gruppo di utenti locale aggiunto tooAdministrators**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="f68ff-148">Hello riportato di seguito impostazione hello SetupEntryPoint toorun come LocalSystem:</span><span class="sxs-lookup"><span data-stu-id="f68ff-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="f68ff-149">Avviare i comandi PowerShell da un punto di ingresso dell'installazione</span><span class="sxs-lookup"><span data-stu-id="f68ff-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="f68ff-150">toorun PowerShell da hello **SetupEntryPoint** punto, è possibile eseguire **PowerShell.exe** in un file batch che punta tooa PowerShell file.</span><span class="sxs-lookup"><span data-stu-id="f68ff-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="f68ff-151">Aggiungere innanzitutto un progetto di servizio toohello file di PowerShell, ad esempio, **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="f68ff-152">Ricordare hello tooset *copia se più recente* proprietà in modo che tale file hello è anche incluso nel pacchetto di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="f68ff-153">Hello esempio seguente viene illustrato un file batch di esempio che avvia un file di PowerShell denominato MySetup.ps1, che consente di impostare una variabile di ambiente system denominata **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="f68ff-154">MySetup.bat toostart un file di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f68ff-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="f68ff-155">Nel file PowerShell hello aggiungere hello tooset una variabile di ambiente di sistema seguente:</span><span class="sxs-lookup"><span data-stu-id="f68ff-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="f68ff-156">Per impostazione predefinita, quando viene eseguito il file batch di hello, Cerca nella cartella dell'applicazione hello **lavoro** per i file.</span><span class="sxs-lookup"><span data-stu-id="f68ff-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="f68ff-157">In questo caso, quando MySetup.bat è in esecuzione, si vuole che questo hello toofind MySetup.ps1 file hello stessa cartella, ovvero un'applicazione hello **pacchetto di codice** cartella.</span><span class="sxs-lookup"><span data-stu-id="f68ff-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="f68ff-158">toochange questa cartella, la cartella di lavoro hello set:</span><span class="sxs-lookup"><span data-stu-id="f68ff-158">toochange this folder, set hello working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="f68ff-159">Uso del reindirizzamento della console per il debug locale</span><span class="sxs-lookup"><span data-stu-id="f68ff-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="f68ff-160">In alcuni casi, è utile toosee output della console hello dall'esecuzione di uno script a scopo di debug.</span><span class="sxs-lookup"><span data-stu-id="f68ff-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="f68ff-161">toodo, è possibile impostare un criterio di reindirizzamento della console, che scrive file tooa output di hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="f68ff-162">Hello file di output viene chiamato cartella dell'applicazione scritta toohello **log** nel nodo hello in cui un'applicazione hello viene distribuita ed eseguita.</span><span class="sxs-lookup"><span data-stu-id="f68ff-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="f68ff-163">(Vedere dove toofind in hello sopra riportato.)</span><span class="sxs-lookup"><span data-stu-id="f68ff-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="f68ff-164">Non utilizzare mai criterio di reindirizzamento console hello in un'applicazione che viene distribuita nell'ambiente di produzione, perché ciò può influire sul failover dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="f68ff-165">Usare questa opzione *solo* a scopo di sviluppo e debug locale.</span><span class="sxs-lookup"><span data-stu-id="f68ff-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="f68ff-166">Hello esempio seguente viene illustrato il reindirizzamento della console con un valore FileRetentionCount impostazione hello:</span><span class="sxs-lookup"><span data-stu-id="f68ff-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="f68ff-167">Se si modifica ora hello MySetup.ps1 file toowrite un **Echo** comando, si scriverà toohello i file di output a scopo di debug:</span><span class="sxs-lookup"><span data-stu-id="f68ff-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="f68ff-168">**Dopo avere eseguito il debug dello script, rimuovere immediatamente i criteri di reindirizzamento della console**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="f68ff-169">Configurare i criteri per i pacchetti di codice del servizio</span><span class="sxs-lookup"><span data-stu-id="f68ff-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="f68ff-170">In hello passaggi precedenti, si è visto come tooapply un tooSetupEntryPoint criteri RunAs.</span><span class="sxs-lookup"><span data-stu-id="f68ff-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="f68ff-171">Vediamo un po' più approfondita in come entità diverse toocreate che possono essere applicate come servizio criteri.</span><span class="sxs-lookup"><span data-stu-id="f68ff-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="f68ff-172">Creare gruppi di utenti locali</span><span class="sxs-lookup"><span data-stu-id="f68ff-172">Create local user groups</span></span>
<span data-ttu-id="f68ff-173">È possibile definire e creare gruppi di utenti che consentono di utilizzare uno o più utenti toobe aggiunto tooa del gruppo.</span><span class="sxs-lookup"><span data-stu-id="f68ff-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="f68ff-174">Ciò è utile se sono presenti più utenti per i punti di ingresso del servizio diverso e devono toohave determinati privilegi comune che sono disponibili a livello di gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="f68ff-175">Hello esempio seguente viene illustrato un gruppo locale denominato **LocalAdminGroup** che disponga dei privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f68ff-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="f68ff-176">Due utenti, Customer1 e Customer2, diventano membri di questo gruppo locale.</span><span class="sxs-lookup"><span data-stu-id="f68ff-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="f68ff-177">Creare utenti locali</span><span class="sxs-lookup"><span data-stu-id="f68ff-177">Create local users</span></span>
<span data-ttu-id="f68ff-178">È possibile creare un utente locale che può essere utilizzati toohelp protetto come un servizio all'interno di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="f68ff-179">Quando un **UtenteLocale** tipo di account viene specificato nella sezione di entità hello del manifesto dell'applicazione hello, Service Fabric crea gli account utente locali nei computer in cui viene distribuita un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="f68ff-180">Per impostazione predefinita, questi account non dispone hello nomi identici a quelli specificati in un'applicazione hello manifesto (ad esempio, nel seguente esempio hello Customer3).</span><span class="sxs-lookup"><span data-stu-id="f68ff-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="f68ff-181">Vengono invece generati in modo dinamico e hanno password casuali.</span><span class="sxs-lookup"><span data-stu-id="f68ff-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="f68ff-182">Se un'applicazione richiede che la password e account utente di hello corrispondere in tutti i computer (ad esempio, l'autenticazione NTLM tooenable), manifesto del cluster hello necessario impostare NTLMAuthenticationEnabled tootrue.</span><span class="sxs-lookup"><span data-stu-id="f68ff-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="f68ff-183">Hello manifesto del cluster deve inoltre specificare un NTLMAuthenticationPasswordSecret utilizzato toogenerate hello stessa password in tutti i computer.</span><span class="sxs-lookup"><span data-stu-id="f68ff-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="f68ff-184">Assegnare i criteri toohello pacchetti di codice di servizio</span><span class="sxs-lookup"><span data-stu-id="f68ff-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="f68ff-185">Hello **RunAsPolicy** sezione un **oggetto ServiceManifestImport** Specifica account hello dalla sezione entità hello che deve essere utilizzati toorun un pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="f68ff-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="f68ff-186">Codice pacchetti dal servizio hello manifesto inoltre associa gli account utente nella sezione delle entità hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="f68ff-187">È possibile specificare questo valore per il programma di installazione di hello o i punti di ingresso principale o è possibile specificare `All` tooapply è tooboth.</span><span class="sxs-lookup"><span data-stu-id="f68ff-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="f68ff-188">Hello seguente illustra i diversi criteri applicati:</span><span class="sxs-lookup"><span data-stu-id="f68ff-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="f68ff-189">Se **EntryPointType** non viene specificato, impostazione predefinita di hello è tooEntryPointType = "Main".</span><span class="sxs-lookup"><span data-stu-id="f68ff-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="f68ff-190">Specifica di **SetupEntryPoint** è particolarmente utile quando si desidera toorun determinate operazioni di installazione con privilegi elevati con un account di sistema.</span><span class="sxs-lookup"><span data-stu-id="f68ff-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="f68ff-191">codice di servizio effettivo Hello può essere eseguito con un account con privilegi inferiori.</span><span class="sxs-lookup"><span data-stu-id="f68ff-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="f68ff-192">Applicare un pacchetti di codice predefiniti criteri tooall servizio</span><span class="sxs-lookup"><span data-stu-id="f68ff-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="f68ff-193">Utilizzare hello **DefaultRunAsPolicy** toospecify sezione un account utente predefinito per tutti i pacchetti di codice che non dispongono di uno specifico **RunAsPolicy** definito.</span><span class="sxs-lookup"><span data-stu-id="f68ff-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="f68ff-194">Se la maggior parte dei pacchetti di codice hello specificati nel manifesto del servizio hello utilizzato da un'applicazione è necessario toorun in hello stesso utente, hello applicazione possono essere definite solo criteri con tale account utente RunAs predefiniti.</span><span class="sxs-lookup"><span data-stu-id="f68ff-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="f68ff-195">Hello esempio seguente specifica che se un pacchetto di codice non dispone di un **RunAsPolicy** specificato, il pacchetto di codice hello deve essere in esecuzione hello **MyDefaultAccount** specificato nella sezione delle entità hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="f68ff-196">Uso di un utente o un gruppo di dominio di Active Directory</span><span class="sxs-lookup"><span data-stu-id="f68ff-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="f68ff-197">Per un'istanza di Service Fabric è stato installato in Windows Server tramite il programma di installazione di hello autonomo, è possibile eseguire il servizio di hello con le credenziali di hello per un account utente o gruppo di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f68ff-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="f68ff-198">Si tratta di Active Directory locale nel dominio e non di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f68ff-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f68ff-199">Usando un utente di dominio o un gruppo, possono quindi accedere altre risorse nel dominio hello (ad esempio, le condivisioni di file) che sono state concesse autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="f68ff-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="f68ff-200">Hello riportato di seguito un utente di Active Directory denominato *TestUser* con loro dominio password crittografata usando un certificato denominato *NomeCert*.</span><span class="sxs-lookup"><span data-stu-id="f68ff-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="f68ff-201">È possibile utilizzare hello `Invoke-ServiceFabricEncryptText` testo secret crittografato hello toocreate del comando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f68ff-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="f68ff-202">Vedere [Gestione dei segreti nelle applicazioni di Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="f68ff-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="f68ff-203">È necessario distribuire la chiave privata hello del hello certificato toodecrypt hello password toohello computer utilizzando un metodo fuori banda (in Azure, si tratta di con Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="f68ff-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="f68ff-204">Quindi quando Service Fabric distribuisce computer toohello pacchetto del servizio hello, è in grado di toodecrypt hello segreto e (insieme al nome utente hello) l'autenticazione con Active Directory toorun con tali credenziali.</span><span class="sxs-lookup"><span data-stu-id="f68ff-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="f68ff-205">Usare un account del servizio gestito del gruppo.</span><span class="sxs-lookup"><span data-stu-id="f68ff-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="f68ff-206">Per un'istanza di Service Fabric è stato installato in Windows Server tramite il programma di installazione di hello autonomo, è possibile eseguire il servizio di hello come un gruppo di Account del servizio gestito (gMSA).</span><span class="sxs-lookup"><span data-stu-id="f68ff-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="f68ff-207">Si noti che si tratta di Active Directory locale nel dominio e non di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f68ff-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f68ff-208">Utilizzando un account non è disponibile la password o archiviata in hello `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="f68ff-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="f68ff-209">Hello esempio seguente viene illustrato come toocreate un account gestito denominato *svc Test$*; come toodeploy grado di gestire i nodi del cluster toohello account del servizio; e come tooconfigure hello dell'entità utente.</span><span class="sxs-lookup"><span data-stu-id="f68ff-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="f68ff-210">Prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="f68ff-210">Prerequisites.</span></span>
- <span data-ttu-id="f68ff-211">dominio Hello richiede una chiave radice del servizio distribuzione CHIAVI.</span><span class="sxs-lookup"><span data-stu-id="f68ff-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="f68ff-212">dominio Hello deve toobe in un Windows Server 2012 o un livello di funzionalità in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="f68ff-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="f68ff-213">Esempio</span><span class="sxs-lookup"><span data-stu-id="f68ff-213">Example</span></span>
1. <span data-ttu-id="f68ff-214">Dispone un amministratore di dominio active directory creare un account del servizio gestito di gruppo utilizzando hello `New-ADServiceAccount` cmdlet e assicurarsi che hello `PrincipalsAllowedToRetrieveManagedPassword` include tutti i nodi del cluster hello service fabric.</span><span class="sxs-lookup"><span data-stu-id="f68ff-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="f68ff-215">Si noti che `AccountName`, `DnsHostName` e `ServicePrincipalName` devono essere univoci.</span><span class="sxs-lookup"><span data-stu-id="f68ff-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="f68ff-216">In ognuno dei nodi del cluster di infrastruttura servizio hello (ad esempio, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), installare e testare hello gMSA.</span><span class="sxs-lookup"><span data-stu-id="f68ff-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="f68ff-217">Configurazione dell'entità utente hello e configurare hello RunAsPolicy tooreference hello utente.</span><span class="sxs-lookup"><span data-stu-id="f68ff-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="f68ff-218">Assegnare un criterio di accesso di sicurezza per gli endpoint HTTP e HTTPS</span><span class="sxs-lookup"><span data-stu-id="f68ff-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="f68ff-219">Se si applica a un servizio di tooa criteri RunAs e manifesto del servizio hello dichiara le risorse di endpoint con protocollo hello HTTP, è necessario specificare un **SecurityAccessPolicy** tooensure che porte allocato endpoint toothese siano correttamente controllo di accesso elencate per hello account utente RunAs cui viene eseguito il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="f68ff-220">In caso contrario, **http.sys** dispone di accesso toohello servizio e ottenere gli errori con chiamate da client hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="f68ff-221">esempio Hello applica endpoint dell'account hello Customer1 tooan chiamato **EndpointName**, che fornisce i diritti di accesso completo.</span><span class="sxs-lookup"><span data-stu-id="f68ff-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="f68ff-222">Per l'endpoint HTTPS hello, è inoltre tooindicate nome di hello del client di toohello tooreturn certificato hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="f68ff-223">È possibile farlo tramite **EndpointBindingPolicy**, con il certificato di hello definito in una sezione di certificati nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="f68ff-224">Aggiornamento di più applicazioni con endpoint https</span><span class="sxs-lookup"><span data-stu-id="f68ff-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="f68ff-225">È necessario fare attenzione toobe non toouse hello **stessa porta** per istanze diverse di hello stessa applicazione quando si usa http**s**.</span><span class="sxs-lookup"><span data-stu-id="f68ff-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="f68ff-226">motivo di Hello è che Service Fabric non sarà in grado di tooupgrade cert di hello per una delle istanze dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f68ff-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="f68ff-227">Ad esempio, se l'applicazione 1 o dell'applicazione 2 entrambi desidera tooupgrade loro toocert cert 1, 2.</span><span class="sxs-lookup"><span data-stu-id="f68ff-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="f68ff-228">Quando si verifica l'aggiornamento di hello, Service Fabric potrebbero essere eliminate registrazione cert 1 hello con http.sys anche se hello altre applicazioni in uso.</span><span class="sxs-lookup"><span data-stu-id="f68ff-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="f68ff-229">tooprevent, Service Fabric rileva che esiste già un'altra istanza dell'applicazione registrata sulla porta hello con certificato hello (scadenza toohttp.sys) e l'operazione di hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f68ff-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="f68ff-230">Pertanto Service Fabric supporta l'aggiornamento di due servizi diversi utilizzando **hello stessa porta** in istanze diverse dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f68ff-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="f68ff-231">In altre parole, non è possibile utilizzare hello stesso certificato in servizi diversi in hello stessa porta.</span><span class="sxs-lookup"><span data-stu-id="f68ff-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="f68ff-232">Se è necessario toohave condivisa certificato sul hello stessa porta, è necessario tooensure tale hello i servizi vengono inseriti in computer diversi con vincoli di posizionamento.</span><span class="sxs-lookup"><span data-stu-id="f68ff-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="f68ff-233">In alternativa, utilizzare le porte dinamiche di Service Fabric se possibile per ogni servizio in ogni istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f68ff-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="f68ff-234">Se viene visualizzato un errore di aggiornamento con https, un avviso di errore indicante che "hello API HTTP Server di Windows non supporta più certificati per le applicazioni che condividono una porta."</span><span class="sxs-lookup"><span data-stu-id="f68ff-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="f68ff-235">Esempio completo del manifesto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f68ff-235">A complete application manifest example</span></span>
<span data-ttu-id="f68ff-236">Hello manifesto dell'applicazione di seguito sono illustrati molti dei hello impostazioni diverse:</span><span class="sxs-lookup"><span data-stu-id="f68ff-236">hello following application manifest shows many of hello different settings:</span></span>

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
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
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


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="f68ff-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f68ff-237">Next steps</span></span>
* [<span data-ttu-id="f68ff-238">Comprendere il modello di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f68ff-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="f68ff-239">Specificare le risorse in un manifesto del servizio</span><span class="sxs-lookup"><span data-stu-id="f68ff-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="f68ff-240">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="f68ff-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
