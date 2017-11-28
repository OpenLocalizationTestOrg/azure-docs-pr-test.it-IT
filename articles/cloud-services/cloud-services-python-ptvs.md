---
title: Introduzione a Python e Servizi cloud di Azure | Documentazione Microsoft
description: Panoramica dell'uso di Python Tools per Visual Studio per creare servizi cloud di Azure, inclusi ruoli Web e ruoli di lavoro.
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
ms.openlocfilehash: 7d2bc89943087323e92cf06981bbacaf4b8ff060
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="c7ca0-103">Ruoli Web e ruoli di lavoro Python con Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7ca0-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="c7ca0-104">Questo articolo offre una panoramica dell'uso dei ruoli Web e di lavoro Phyton con [Python Tools for Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c7ca0-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="c7ca0-105">Informazioni su come usare Visual Studio per creare e distribuire un servizio cloud di base che usa Python.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-105">Learn how to use Visual Studio to create and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7ca0-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c7ca0-106">Prerequisites</span></span>
* [<span data-ttu-id="c7ca0-107">Visual Studio 2013, 2015 o 2017</span><span class="sxs-lookup"><span data-stu-id="c7ca0-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="c7ca0-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="c7ca0-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="c7ca0-109">[Strumenti di Azure SDK per VS 2013][Azure SDK Tools for VS 2013] o</span><span class="sxs-lookup"><span data-stu-id="c7ca0-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="c7ca0-110">[Strumenti di Azure SDK per VS 2015][Azure SDK Tools for VS 2015] o</span><span class="sxs-lookup"><span data-stu-id="c7ca0-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="c7ca0-111">[Strumenti di Azure SDK per VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="c7ca0-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="c7ca0-112">[Python 2.7 a 32 bit][Python 2.7 32-bit] o [Python 3.5 a 32 bit][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="c7ca0-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="c7ca0-113">Cosa sono i ruoli Web e di lavoro Python?</span><span class="sxs-lookup"><span data-stu-id="c7ca0-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="c7ca0-114">Azure offre tre modelli di calcolo per l'esecuzione di applicazioni: [funzionalità App Web in Servizio app di Azure][execution model-web sites], [macchine virtuali di Azure][execution model-vms] e [Servizi cloud di Azure][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="c7ca0-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="c7ca0-115">Tutti e tre i modelli supportano Python.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-115">All three models support Python.</span></span> <span data-ttu-id="c7ca0-116">Servizi cloud, che include ruoli Web e di lavoro, fornisce la tecnologia di *piattaforma distribuita come servizio (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="c7ca0-117">Nell'ambito di un servizio cloud, un ruolo Web fornisce un server Web IIS (Internet Information Services) dedicato su cui ospitare applicazioni Web front-end, mentre un ruolo di lavoro consente di eseguire attività asincrone, a esecuzione prolungata o perpetue, indipendenti dall'interazione o dall'input degli utenti.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="c7ca0-118">Per altre informazioni, vedere [Informazioni sul servizio cloud].</span><span class="sxs-lookup"><span data-stu-id="c7ca0-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca0-119">*Come creare un semplice sito Web*</span><span class="sxs-lookup"><span data-stu-id="c7ca0-119">*Looking to build a simple website?*</span></span>
> <span data-ttu-id="c7ca0-120">Se si intende creare un semplice sito Web front-end, è possibile usare la funzionalità App Web in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-120">If your scenario involves just a simple website front end, consider using the lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="c7ca0-121">È possibile procedere all'aggiornamento a un servizio cloud con facilità, in base alla crescita del sito Web e all'insorgere di nuove esigenze.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-121">You can easily upgrade to a Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="c7ca0-122">Per articoli che trattano lo sviluppo della funzionalità App Web in Servizio app di Azure, vedere il <a href="/develop/python/">Centro per sviluppatori Python</a>.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-122">See the <a href="/develop/python/">Python Developer Center</a> for articles that cover development of the Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="c7ca0-123">Creazione del progetto</span><span class="sxs-lookup"><span data-stu-id="c7ca0-123">Project creation</span></span>
<span data-ttu-id="c7ca0-124">In Visual Studio è possibile selezionare **Servizio Cloud Azure** nella finestra di dialogo **Nuovo progetto** sotto **Python**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-124">In Visual Studio, you can select **Azure Cloud Service** in the **New Project** dialog box, under **Python**.</span></span>

![Finestra di dialogo Nuovo progetto](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="c7ca0-126">Nella procedura guidata del servizio cloud di Azure è possibile creare nuovi ruoli Web e di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-126">In the Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Finestra di dialogo del servizio cloud di Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="c7ca0-128">Nel modello di ruolo di lavoro è disponibile il codice boilerplate per connettersi a un bus di servizio o a un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-128">The worker role template comes with boilerplate code to connect to an Azure storage account or Azure Service Bus.</span></span>

![Soluzione del servizio cloud](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="c7ca0-130">È possibile aggiungere ruoli di lavoro o Web a un servizio cloud esistente in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-130">You can add web or worker roles to an existing cloud service at any time.</span></span>  <span data-ttu-id="c7ca0-131">È possibile scegliere di aggiungere alla soluzione progetti esistenti oppure crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-131">You can choose to add existing projects in your solution, or create new ones.</span></span>

![Comando per l'aggiunta di un ruolo](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="c7ca0-133">Il servizio cloud può contenere ruoli implementati in linguaggi diversi.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="c7ca0-134">Ad esempio, è possibile avere un ruolo Web Python implementato usando Django, con ruoli di lavoro Python o C#.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="c7ca0-135">È possibile mettere facilmente in comunicazione i ruoli con code di bus di servizio o code di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-the-cloud-service"></a><span data-ttu-id="c7ca0-136">Installare Python nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="c7ca0-136">Install Python on the cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="c7ca0-137">Gli script di installazione installati con Visual Studio al momento dell'ultimo aggiornamento di questo articolo non funzionano.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-137">The setup scripts that are installed with Visual Studio (at the time this article was last updated) do not work.</span></span> <span data-ttu-id="c7ca0-138">Questa sezione illustra una soluzione alternativa.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="c7ca0-139">Il problema principale con gli script di installazione è che non installano Python.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-139">The main problem with the setup scripts is that they do not install python.</span></span> <span data-ttu-id="c7ca0-140">Definire prima due [attività di avvio](cloud-services-startup-tasks.md) nel file [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in the [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="c7ca0-141">La prima attività, **PrepPython.ps1**, scarica e installa il runtime di Python.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-141">The first task (**PrepPython.ps1**) downloads and installs the Python runtime.</span></span> <span data-ttu-id="c7ca0-142">La seconda attività, **PipInstaller.ps1**, esegue pip per installare le eventuali dipendenze.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-142">The second task (**PipInstaller.ps1**) runs pip to install any dependencies you may have.</span></span>

<span data-ttu-id="c7ca0-143">Gli script seguenti sono stati scritti per Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-143">The following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="c7ca0-144">Per usare la versione 2.x di Python, impostare il file di variabile **PYTHON2** su **on** per le due attività di avvio e l'attività di runtime: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-144">If you want to use the version 2.x of python, set the **PYTHON2** variable file to **on** for the two startup tasks and the runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="c7ca0-145">È necessario aggiungere le variabili **PYTHON2** e **PYPATH** all'attività di avvio del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-145">The **PYTHON2** and **PYPATH** variables must be added to the worker startup task.</span></span> <span data-ttu-id="c7ca0-146">La variabile **PYPATH** viene usata solo se la variabile **PYTHON2** è impostata su **on**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-146">The **PYPATH** variable is only used if the **PYTHON2** variable is set to **on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="c7ca0-147">File ServiceDefinition.csdef di esempio</span><span class="sxs-lookup"><span data-stu-id="c7ca0-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="c7ca0-148">Creare ora i file **PrepPython.ps1** e **PipInstaller.ps1** nella cartella **./bin** del ruolo.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-148">Next, create the **PrepPython.ps1** and **PipInstaller.ps1** files in the **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="c7ca0-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="c7ca0-149">PrepPython.ps1</span></span>
<span data-ttu-id="c7ca0-150">Questo script installa Python.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-150">This script installs python.</span></span> <span data-ttu-id="c7ca0-151">Se la variabile di ambiente **PYTHON2** è impostata su **on**, viene installato Python 2.7. In caso contrario, viene installato Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-151">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

        Write-Output "Not found, downloading $url to $outFile$nl"
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

#### <a name="pipinstallerps1"></a><span data-ttu-id="c7ca0-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="c7ca0-152">PipInstaller.ps1</span></span>
<span data-ttu-id="c7ca0-153">Questo script chiama pip e installa tutte le dipendenze presenti nel file **requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-153">This script calls up pip and installs all of the dependencies in the **requirements.txt** file.</span></span> <span data-ttu-id="c7ca0-154">Se la variabile di ambiente **PYTHON2** è impostata su **on**, viene usato Python 2.7. In caso contrario, viene usato Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-154">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="c7ca0-155">Modificare LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="c7ca0-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="c7ca0-156">Nel caso di un progetto **ruolo di lavoro**, è necessario il file **LauncherWorker.ps1** per eseguire il file di avvio.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-156">In the case of a **worker role** project, **LauncherWorker.ps1** file is required to execute the startup file.</span></span> <span data-ttu-id="c7ca0-157">In un progetto **ruolo Web** il file di avvio viene invece definito nelle proprietà del progetto.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-157">In a **web role** project, the startup file is instead defined in the project properties.</span></span>
> 
> 

<span data-ttu-id="c7ca0-158">Il file **bin\LaunchWorker.ps1** è stato originariamente creato per eseguire molte attività preliminari, ma non funziona.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-158">The **bin\LaunchWorker.ps1** was originally created to do a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="c7ca0-159">Sostituire il contenuto del file con lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-159">Replace the contents in that file with the following script.</span></span>

<span data-ttu-id="c7ca0-160">Questo script chiama il file **worker.py** dal progetto Python.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-160">This script calls the **worker.py** file from your python project.</span></span> <span data-ttu-id="c7ca0-161">Se la variabile di ambiente **PYTHON2** è impostata su **on**, viene usato Python 2.7. In caso contrario, viene usato Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-161">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

    # Customize to your local dev environment

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

#### <a name="pscmd"></a><span data-ttu-id="c7ca0-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="c7ca0-162">ps.cmd</span></span>
<span data-ttu-id="c7ca0-163">I modelli di Visual Studio dovrebbero aver creato un file **ps.cmd** nella cartella **./bin**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-163">The Visual Studio templates should have created a **ps.cmd** file in the **./bin** folder.</span></span> <span data-ttu-id="c7ca0-164">Questo script della shell chiama gli script del wrapper di PowerShell precedenti e fornisce la registrazione in base al nome del wrapper di PowerShell chiamato.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-164">This shell script calls out the PowerShell wrapper scripts above and provides logging based on the name of the PowerShell wrapper called.</span></span> <span data-ttu-id="c7ca0-165">Se questo file non è stato creato, di seguito è indicato il contenuto necessario.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="c7ca0-166">Esecuzione locale</span><span class="sxs-lookup"><span data-stu-id="c7ca0-166">Run locally</span></span>
<span data-ttu-id="c7ca0-167">Se si imposta il progetto servizio cloud come progetto di avvio e si preme F5, il servizio cloud viene eseguito nell'emulatore locale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-167">If you set your cloud service project as the startup project and press F5, the cloud service runs in the local Azure emulator.</span></span>

<span data-ttu-id="c7ca0-168">Anche se PTVS supporta l'avvio nell'emulatore, il debug (ad esempio, punti di interruzione) non funziona.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-168">Although PTVS supports launching in the emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="c7ca0-169">Per eseguire il debug dei ruoli di lavoro e Web, è possibile impostare il progetto di ruolo come progetto di avvio e ed eseguirne il debug.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-169">To debug your web and worker roles, you can set the role project as the startup project and debug that instead.</span></span>  <span data-ttu-id="c7ca0-170">È anche possibile impostare più progetti di avvio.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="c7ca0-171">Fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Imposta progetti di avvio**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-171">Right-click the solution and then select **Set StartUp Projects**.</span></span>

![Proprietà del progetto di avvio della soluzione](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-to-azure"></a><span data-ttu-id="c7ca0-173">Pubblicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca0-173">Publish to Azure</span></span>
<span data-ttu-id="c7ca0-174">Per pubblicare, fare clic con il pulsante destro del mouse sul progetto servizio cloud nella soluzione e quindi scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-174">To publish, right-click the cloud service project in the solution and then select **Publish**.</span></span>

![Accesso per la pubblicazione di Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="c7ca0-176">Seguire la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-176">Follow the wizard.</span></span> <span data-ttu-id="c7ca0-177">Se necessario, abilitare Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="c7ca0-178">Desktop remoto è utile quando è necessario eseguire il debug di un elemento.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-178">Remote desktop is helpful when you need to debug something.</span></span>

<span data-ttu-id="c7ca0-179">Dopo aver finito di configurare le impostazioni, fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="c7ca0-180">Nella finestra di output vengono visualizzati alcuni stati, quindi apparirà la finestra Log attività di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-180">Some progress appears in the output window, then you'll see the Microsoft Azure Activity Log window.</span></span>

![Finestra Log attività di Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="c7ca0-182">Sono necessari alcuni minuti per completare la distribuzione, quindi i ruoli di lavoro e/o Web vengono eseguiti in Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-182">Deployment takes several minutes to complete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="c7ca0-183">Esaminare i log</span><span class="sxs-lookup"><span data-stu-id="c7ca0-183">Investigate logs</span></span>
<span data-ttu-id="c7ca0-184">Dopo che la macchina virtuale del servizio cloud è stata avviata e ha installato Python, è possibile esaminare i log per trovare eventuali messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-184">After the cloud service virtual machine starts up and installs Python, you can look at the logs to find any failure messages.</span></span> <span data-ttu-id="c7ca0-185">Questi log si trovano nella cartella **C:\Resources\Directory\\{role}\LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-185">These logs are located in the **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="c7ca0-186">**PrepPython.err.txt** contiene almeno un errore relativo al tentativo dello script di verificare se Python è installato e **PipInstaller.err.txt** può segnalare una versione obsoleta di pip.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-186">**PrepPython.err.txt** has at least one error in it from when the script tries to detect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7ca0-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7ca0-187">Next steps</span></span>
<span data-ttu-id="c7ca0-188">Per informazioni più dettagliate sull'uso di ruoli di lavoro e Web in Python Tools per Visual Studio, vedere la documentazione PTVS:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see the PTVS documentation:</span></span>

* <span data-ttu-id="c7ca0-189">[Progetti servizio cloud][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="c7ca0-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="c7ca0-190">Per altre informazioni dettagliate sull'uso di servizi di Azure dai ruoli di lavoro e Web, ad esempio sull'uso dell'archiviazione o del bus di servizio di Azure, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see the following articles:</span></span>

* <span data-ttu-id="c7ca0-191">[Servizio BLOB][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="c7ca0-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="c7ca0-192">[Servizio tabelle][Table Service]</span><span class="sxs-lookup"><span data-stu-id="c7ca0-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="c7ca0-193">[Servizio di accodamento][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="c7ca0-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="c7ca0-194">[Code del bus di servizio][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="c7ca0-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="c7ca0-195">[Argomenti del bus di servizio][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="c7ca0-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
