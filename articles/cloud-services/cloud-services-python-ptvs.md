---
title: aaaGet avviato con Python e i servizi Cloud di Azure | Documenti Microsoft
description: Panoramica dell'utilizzo di Python Tools per Visual Studio toocreate servizi cloud Azure inclusi i ruoli web e ruoli di lavoro.
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="2b66a-103">Ruoli Web e ruoli di lavoro Python con Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b66a-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="2b66a-104">Questo articolo offre una panoramica dell'uso dei ruoli Web e di lavoro Phyton con [Python Tools for Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="2b66a-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="2b66a-105">Informazioni su come toouse toocreate di Visual Studio e distribuire un servizio Cloud di base che usa Python.</span><span class="sxs-lookup"><span data-stu-id="2b66a-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b66a-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2b66a-106">Prerequisites</span></span>
* [<span data-ttu-id="2b66a-107">Visual Studio 2013, 2015 o 2017</span><span class="sxs-lookup"><span data-stu-id="2b66a-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="2b66a-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="2b66a-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="2b66a-109">[Strumenti di Azure SDK per VS 2013][Azure SDK Tools for VS 2013] o</span><span class="sxs-lookup"><span data-stu-id="2b66a-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="2b66a-110">[Strumenti di Azure SDK per VS 2015][Azure SDK Tools for VS 2015] o</span><span class="sxs-lookup"><span data-stu-id="2b66a-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="2b66a-111">[Strumenti di Azure SDK per VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="2b66a-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="2b66a-112">[Python 2.7 a 32 bit][Python 2.7 32-bit] o [Python 3.5 a 32 bit][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="2b66a-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="2b66a-113">Cosa sono i ruoli Web e di lavoro Python?</span><span class="sxs-lookup"><span data-stu-id="2b66a-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="2b66a-114">Azure offre tre modelli di calcolo per l'esecuzione di applicazioni: [funzionalità App Web in Servizio app di Azure][execution model-web sites], [macchine virtuali di Azure][execution model-vms] e [Servizi cloud di Azure][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="2b66a-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="2b66a-115">Tutti e tre i modelli supportano Python.</span><span class="sxs-lookup"><span data-stu-id="2b66a-115">All three models support Python.</span></span> <span data-ttu-id="2b66a-116">Servizi cloud, che include ruoli Web e di lavoro, fornisce la tecnologia di *piattaforma distribuita come servizio (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="2b66a-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="2b66a-117">All'interno di un servizio cloud, un ruolo web fornisce un front-end web dedicato di Internet Information Services (IIS) web server toohost applicazioni, mentre un ruolo di lavoro può eseguire le attività asincrone, con esecuzione prolungata o perpetue indipendentemente dall'interazione dell'utente o input.</span><span class="sxs-lookup"><span data-stu-id="2b66a-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="2b66a-118">Per altre informazioni, vedere [Informazioni sul servizio cloud].</span><span class="sxs-lookup"><span data-stu-id="2b66a-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="2b66a-119">*Ricerca toobuild un semplice sito Web?*</span><span class="sxs-lookup"><span data-stu-id="2b66a-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="2b66a-120">Se lo scenario prevede solo un front-end di sito Web è semplice, considerare l'utilizzo di funzionalità delle App Web lightweight hello in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2b66a-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="2b66a-121">Come si espande il sito Web e i requisiti cambiano, è possibile aggiornare facilmente tooa servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="2b66a-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="2b66a-122">Vedere hello <a href="/develop/python/">Centro per sviluppatori Python</a> per gli articoli che analizzano sviluppo della funzionalità di App Web hello in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2b66a-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="2b66a-123">Creazione del progetto</span><span class="sxs-lookup"><span data-stu-id="2b66a-123">Project creation</span></span>
<span data-ttu-id="2b66a-124">In Visual Studio, è possibile selezionare **servizio Cloud di Azure** in hello **nuovo progetto** nella finestra di dialogo **Python**.</span><span class="sxs-lookup"><span data-stu-id="2b66a-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![Finestra di dialogo Nuovo progetto](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="2b66a-126">Nella procedura guidata di servizio Cloud di Azure hello, è possibile creare nuovo sito web e ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2b66a-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Finestra di dialogo del servizio cloud di Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="2b66a-128">modello di ruolo di lavoro Hello viene fornito con tooan tooconnect tramite codice boilerplate account di archiviazione di Azure o Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2b66a-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Soluzione del servizio cloud](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="2b66a-130">È possibile aggiungere web o lavoro ruoli tooan servizio cloud esistente in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="2b66a-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="2b66a-131">È possibile scegliere i progetti esistenti tooadd nella soluzione o crearne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="2b66a-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![Comando per l'aggiunta di un ruolo](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="2b66a-133">Il servizio cloud può contenere ruoli implementati in linguaggi diversi.</span><span class="sxs-lookup"><span data-stu-id="2b66a-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="2b66a-134">Ad esempio, è possibile avere un ruolo Web Python implementato usando Django, con ruoli di lavoro Python o C#.</span><span class="sxs-lookup"><span data-stu-id="2b66a-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="2b66a-135">È possibile mettere facilmente in comunicazione i ruoli con code di bus di servizio o code di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2b66a-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="2b66a-136">Installare Python nel servizio cloud hello</span><span class="sxs-lookup"><span data-stu-id="2b66a-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="2b66a-137">gli script di installazione Hello installati con Visual Studio (in fase di hello in questo articolo è stato ultimo aggiornamento) non funzionano.</span><span class="sxs-lookup"><span data-stu-id="2b66a-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="2b66a-138">Questa sezione illustra una soluzione alternativa.</span><span class="sxs-lookup"><span data-stu-id="2b66a-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="2b66a-139">problema principale di Hello con gli script di installazione di hello è che non si installa python.</span><span class="sxs-lookup"><span data-stu-id="2b66a-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="2b66a-140">Prima di tutto definire due [le attività di avvio](cloud-services-startup-tasks.md) in hello [Servicedefinition](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span><span class="sxs-lookup"><span data-stu-id="2b66a-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="2b66a-141">prima attività Hello (**PrepPython.ps1**) Scarica e installa il runtime di Python hello.</span><span class="sxs-lookup"><span data-stu-id="2b66a-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="2b66a-142">seconda attività Hello (**PipInstaller.ps1**) viene eseguito tooinstall pip eventuali dipendenze, è possibile.</span><span class="sxs-lookup"><span data-stu-id="2b66a-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="2b66a-143">sono stati scritti Hello seguente script di destinazione 3.5 Python.</span><span class="sxs-lookup"><span data-stu-id="2b66a-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="2b66a-144">Se si vuole toouse hello versione 2. x di python, hello set **PYTHON2** variabile file troppo**su** per attività di avvio hello due e attività di runtime hello: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="2b66a-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

<span data-ttu-id="2b66a-145">Hello **PYTHON2** e **PYPATH** variabili devono essere aggiunti toohello attività di avvio di worker.</span><span class="sxs-lookup"><span data-stu-id="2b66a-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="2b66a-146">Hello **PYPATH** variabile viene utilizzata solo se hello **PYTHON2** impostata troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="2b66a-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="2b66a-147">File ServiceDefinition.csdef di esempio</span><span class="sxs-lookup"><span data-stu-id="2b66a-147">Sample ServiceDefinition.csdef</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



<span data-ttu-id="2b66a-148">Successivamente, creare hello **PrepPython.ps1** e **PipInstaller.ps1** file hello **. / bin** cartella del ruolo.</span><span class="sxs-lookup"><span data-stu-id="2b66a-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="2b66a-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="2b66a-149">PrepPython.ps1</span></span>
<span data-ttu-id="2b66a-150">Questo script installa Python.</span><span class="sxs-lookup"><span data-stu-id="2b66a-150">This script installs python.</span></span> <span data-ttu-id="2b66a-151">Se hello **PYTHON2** variabile di ambiente viene impostata troppo**su**, quindi Python 2.7 è installato, in caso contrario Python 3.5 è installato.</span><span class="sxs-lookup"><span data-stu-id="2b66a-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a><span data-ttu-id="2b66a-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="2b66a-152">PipInstaller.ps1</span></span>
<span data-ttu-id="2b66a-153">Questo script consente di chiamare di pip e installa tutte le dipendenze di hello in hello **requirements.txt** file.</span><span class="sxs-lookup"><span data-stu-id="2b66a-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="2b66a-154">Se hello **PYTHON2** variabile di ambiente viene impostata troppo**su**, viene usato Python 2.7, in caso contrario viene usato Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="2b66a-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="2b66a-155">Modificare LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="2b66a-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="2b66a-156">Nel caso di hello di un **ruolo di lavoro** progetto **LauncherWorker.ps1** file è un file di avvio hello tooexecute obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="2b66a-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="2b66a-157">In un **ruolo web** del progetto, hello file di avvio viene invece definito nelle proprietà del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="2b66a-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="2b66a-158">Hello **bin\LaunchWorker.ps1** è stato originariamente creato toodo molto lavoro Prepara ma non funziona.</span><span class="sxs-lookup"><span data-stu-id="2b66a-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="2b66a-159">Sostituire il contenuto di hello in tale file con lo script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="2b66a-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="2b66a-160">Questo script chiama hello **worker.py** file dal progetto di python.</span><span class="sxs-lookup"><span data-stu-id="2b66a-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="2b66a-161">Se hello **PYTHON2** variabile di ambiente viene impostata troppo**su**, viene usato Python 2.7, in caso contrario viene usato Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="2b66a-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a><span data-ttu-id="2b66a-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="2b66a-162">ps.cmd</span></span>
<span data-ttu-id="2b66a-163">modelli di Visual Studio Hello dovrebbero creare un **ps.cmd** file hello **. / bin** cartella.</span><span class="sxs-lookup"><span data-stu-id="2b66a-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="2b66a-164">Questo script di PowerShell effettua una chiamata hello PowerShell script wrapper precedente e fornisce la registrazione in base al nome del wrapper PowerShell hello chiamato hello.</span><span class="sxs-lookup"><span data-stu-id="2b66a-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="2b66a-165">Se questo file non è stato creato, di seguito è indicato il contenuto necessario.</span><span class="sxs-lookup"><span data-stu-id="2b66a-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="2b66a-166">Esecuzione locale</span><span class="sxs-lookup"><span data-stu-id="2b66a-166">Run locally</span></span>
<span data-ttu-id="2b66a-167">Se si imposta il progetto servizio cloud come progetto di avvio hello e premere F5, il servizio di cloud hello viene eseguito nell'emulatore di Azure locale hello.</span><span class="sxs-lookup"><span data-stu-id="2b66a-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="2b66a-168">Anche se PTVS supporta l'avvio di emulatore hello, il debug (ad esempio, i punti di interruzione) non funziona.</span><span class="sxs-lookup"><span data-stu-id="2b66a-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="2b66a-169">toodebug i ruoli web e di lavoro, è possibile impostare il progetto di ruolo hello come progetto di avvio hello e che, anziché eseguire il debug.</span><span class="sxs-lookup"><span data-stu-id="2b66a-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="2b66a-170">È anche possibile impostare più progetti di avvio.</span><span class="sxs-lookup"><span data-stu-id="2b66a-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="2b66a-171">Soluzione hello e quindi scegliere **Imposta progetti di avvio**.</span><span class="sxs-lookup"><span data-stu-id="2b66a-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Proprietà del progetto di avvio della soluzione](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="2b66a-173">Pubblicare tooAzure</span><span class="sxs-lookup"><span data-stu-id="2b66a-173">Publish tooAzure</span></span>
<span data-ttu-id="2b66a-174">toopublish, fare clic sul progetto servizio cloud hello nella soluzione hello e quindi selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="2b66a-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Accesso per la pubblicazione di Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="2b66a-176">Seguire la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="2b66a-176">Follow hello wizard.</span></span> <span data-ttu-id="2b66a-177">Se necessario, abilitare Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2b66a-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="2b66a-178">Desktop remoto è utile quando è necessario aggiungere toodebug.</span><span class="sxs-lookup"><span data-stu-id="2b66a-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="2b66a-179">Dopo aver finito di configurare le impostazioni, fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="2b66a-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="2b66a-180">Alcuni lo stato di avanzamento visualizzato nella finestra di output di hello, quindi verrà visualizzata finestra Log attività di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2b66a-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Finestra Log attività di Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="2b66a-182">Distribuzione richiede diversi minuti toocomplete, quindi il sito web e/o i ruoli di lavoro vengono eseguiti in Azure!</span><span class="sxs-lookup"><span data-stu-id="2b66a-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="2b66a-183">Esaminare i log</span><span class="sxs-lookup"><span data-stu-id="2b66a-183">Investigate logs</span></span>
<span data-ttu-id="2b66a-184">Dopo la macchina virtuale nel servizio cloud hello viene avviato e consente di installare Python, è possibile esaminare hello registri toofind eventuali messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="2b66a-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="2b66a-185">Tali registri si trovano in hello **C:\Resources\Directory\\\LogFiles {ruolo}** cartella.</span><span class="sxs-lookup"><span data-stu-id="2b66a-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="2b66a-186">**PrepPython.err.txt** contiene almeno un errore da quando script hello tenta toodetect se è installato Python e **PipInstaller.err.txt** potrebbe segnalare una versione obsoleta del pip.</span><span class="sxs-lookup"><span data-stu-id="2b66a-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b66a-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b66a-187">Next steps</span></span>
<span data-ttu-id="2b66a-188">Per informazioni più dettagliate sull'utilizzo dei ruoli web e di lavoro in strumenti Python per Visual Studio, vedere la documentazione di PTVS hello:</span><span class="sxs-lookup"><span data-stu-id="2b66a-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="2b66a-189">[Progetti servizio cloud][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="2b66a-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="2b66a-190">Per ulteriori informazioni sull'utilizzo di servizi di Azure dai ruoli web e di lavoro, ad esempio l'utilizzo di archiviazione di Azure o Bus di servizio, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="2b66a-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="2b66a-191">[Servizio BLOB][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="2b66a-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="2b66a-192">[Servizio tabelle][Table Service]</span><span class="sxs-lookup"><span data-stu-id="2b66a-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="2b66a-193">[Servizio di accodamento][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="2b66a-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="2b66a-194">[Code del bus di servizio][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="2b66a-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="2b66a-195">[Argomenti del bus di servizio][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="2b66a-195">[Service Bus Topics][Service Bus Topics]</span></span>

<!--Link references-->

[Informazioni sul servizio cloud]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
