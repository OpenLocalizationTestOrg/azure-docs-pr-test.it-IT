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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Ruoli Web e ruoli di lavoro Python con Python Tools for Visual Studio

Questo articolo offre una panoramica dell'uso dei ruoli Web e di lavoro Phyton con [Python Tools for Visual Studio][Python Tools for Visual Studio]. Informazioni su come toouse toocreate di Visual Studio e distribuire un servizio Cloud di base che usa Python.

## <a name="prerequisites"></a>Prerequisiti
* [Visual Studio 2013, 2015 o 2017](https://www.visualstudio.com/)
* [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)
* [Strumenti di Azure SDK per VS 2013][Azure SDK Tools for VS 2013] o  
[Strumenti di Azure SDK per VS 2015][Azure SDK Tools for VS 2015] o  
[Strumenti di Azure SDK per VS 2017][Azure SDK Tools for VS 2017]
* [Python 2.7 a 32 bit][Python 2.7 32-bit] o [Python 3.5 a 32 bit][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>Cosa sono i ruoli Web e di lavoro Python?
Azure offre tre modelli di calcolo per l'esecuzione di applicazioni: [funzionalità App Web in Servizio app di Azure][execution model-web sites], [macchine virtuali di Azure][execution model-vms] e [Servizi cloud di Azure][execution model-cloud services]. Tutti e tre i modelli supportano Python. Servizi cloud, che include ruoli Web e di lavoro, fornisce la tecnologia di *piattaforma distribuita come servizio (PaaS)*. All'interno di un servizio cloud, un ruolo web fornisce un front-end web dedicato di Internet Information Services (IIS) web server toohost applicazioni, mentre un ruolo di lavoro può eseguire le attività asincrone, con esecuzione prolungata o perpetue indipendentemente dall'interazione dell'utente o input.

Per altre informazioni, vedere [Informazioni sul servizio cloud].

> [!NOTE]
> *Ricerca toobuild un semplice sito Web?*
> Se lo scenario prevede solo un front-end di sito Web è semplice, considerare l'utilizzo di funzionalità delle App Web lightweight hello in Azure App Service. Come si espande il sito Web e i requisiti cambiano, è possibile aggiornare facilmente tooa servizio Cloud. Vedere hello <a href="/develop/python/">Centro per sviluppatori Python</a> per gli articoli che analizzano sviluppo della funzionalità di App Web hello in Azure App Service.
> <br />
> 
> 

## <a name="project-creation"></a>Creazione del progetto
In Visual Studio, è possibile selezionare **servizio Cloud di Azure** in hello **nuovo progetto** nella finestra di dialogo **Python**.

![Finestra di dialogo Nuovo progetto](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

Nella procedura guidata di servizio Cloud di Azure hello, è possibile creare nuovo sito web e ruoli di lavoro.

![Finestra di dialogo del servizio cloud di Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

modello di ruolo di lavoro Hello viene fornito con tooan tooconnect tramite codice boilerplate account di archiviazione di Azure o Azure Service Bus.

![Soluzione del servizio cloud](./media/cloud-services-python-ptvs/worker.png)

È possibile aggiungere web o lavoro ruoli tooan servizio cloud esistente in qualsiasi momento.  È possibile scegliere i progetti esistenti tooadd nella soluzione o crearne di nuovi.

![Comando per l'aggiunta di un ruolo](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

Il servizio cloud può contenere ruoli implementati in linguaggi diversi.  Ad esempio, è possibile avere un ruolo Web Python implementato usando Django, con ruoli di lavoro Python o C#.  È possibile mettere facilmente in comunicazione i ruoli con code di bus di servizio o code di archiviazione.

## <a name="install-python-on-hello-cloud-service"></a>Installare Python nel servizio cloud hello
> [!WARNING]
> gli script di installazione Hello installati con Visual Studio (in fase di hello in questo articolo è stato ultimo aggiornamento) non funzionano. Questa sezione illustra una soluzione alternativa.
> 
> 

problema principale di Hello con gli script di installazione di hello è che non si installa python. Prima di tutto definire due [le attività di avvio](cloud-services-startup-tasks.md) in hello [Servicedefinition](cloud-services-model-and-package.md#servicedefinitioncsdef) file. prima attività Hello (**PrepPython.ps1**) Scarica e installa il runtime di Python hello. seconda attività Hello (**PipInstaller.ps1**) viene eseguito tooinstall pip eventuali dipendenze, è possibile.

sono stati scritti Hello seguente script di destinazione 3.5 Python. Se si vuole toouse hello versione 2. x di python, hello set **PYTHON2** variabile file troppo**su** per attività di avvio hello due e attività di runtime hello: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.

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

Hello **PYTHON2** e **PYPATH** variabili devono essere aggiunti toohello attività di avvio di worker. Hello **PYPATH** variabile viene utilizzata solo se hello **PYTHON2** impostata troppo**su**.

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

#### <a name="sample-servicedefinitioncsdef"></a>File ServiceDefinition.csdef di esempio
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



Successivamente, creare hello **PrepPython.ps1** e **PipInstaller.ps1** file hello **. / bin** cartella del ruolo.

#### <a name="preppythonps1"></a>PrepPython.ps1
Questo script installa Python. Se hello **PYTHON2** variabile di ambiente viene impostata troppo**su**, quindi Python 2.7 è installato, in caso contrario Python 3.5 è installato.

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

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
Questo script consente di chiamare di pip e installa tutte le dipendenze di hello in hello **requirements.txt** file. Se hello **PYTHON2** variabile di ambiente viene impostata troppo**su**, viene usato Python 2.7, in caso contrario viene usato Python 3.5.

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

#### <a name="modify-launchworkerps1"></a>Modificare LaunchWorker.ps1
> [!NOTE]
> Nel caso di hello di un **ruolo di lavoro** progetto **LauncherWorker.ps1** file è un file di avvio hello tooexecute obbligatorio. In un **ruolo web** del progetto, hello file di avvio viene invece definito nelle proprietà del progetto hello.
> 
> 

Hello **bin\LaunchWorker.ps1** è stato originariamente creato toodo molto lavoro Prepara ma non funziona. Sostituire il contenuto di hello in tale file con lo script seguente hello.

Questo script chiama hello **worker.py** file dal progetto di python. Se hello **PYTHON2** variabile di ambiente viene impostata troppo**su**, viene usato Python 2.7, in caso contrario viene usato Python 3.5.

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

#### <a name="pscmd"></a>ps.cmd
modelli di Visual Studio Hello dovrebbero creare un **ps.cmd** file hello **. / bin** cartella. Questo script di PowerShell effettua una chiamata hello PowerShell script wrapper precedente e fornisce la registrazione in base al nome del wrapper PowerShell hello chiamato hello. Se questo file non è stato creato, di seguito è indicato il contenuto necessario. 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>Esecuzione locale
Se si imposta il progetto servizio cloud come progetto di avvio hello e premere F5, il servizio di cloud hello viene eseguito nell'emulatore di Azure locale hello.

Anche se PTVS supporta l'avvio di emulatore hello, il debug (ad esempio, i punti di interruzione) non funziona.

toodebug i ruoli web e di lavoro, è possibile impostare il progetto di ruolo hello come progetto di avvio hello e che, anziché eseguire il debug.  È anche possibile impostare più progetti di avvio.  Soluzione hello e quindi scegliere **Imposta progetti di avvio**.

![Proprietà del progetto di avvio della soluzione](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>Pubblicare tooAzure
toopublish, fare clic sul progetto servizio cloud hello nella soluzione hello e quindi selezionare **pubblica**.

![Accesso per la pubblicazione di Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

Seguire la procedura guidata hello. Se necessario, abilitare Desktop remoto. Desktop remoto è utile quando è necessario aggiungere toodebug.

Dopo aver finito di configurare le impostazioni, fare clic su **Pubblica**.

Alcuni lo stato di avanzamento visualizzato nella finestra di output di hello, quindi verrà visualizzata finestra Log attività di Microsoft Azure hello.

![Finestra Log attività di Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

Distribuzione richiede diversi minuti toocomplete, quindi il sito web e/o i ruoli di lavoro vengono eseguiti in Azure!

### <a name="investigate-logs"></a>Esaminare i log
Dopo la macchina virtuale nel servizio cloud hello viene avviato e consente di installare Python, è possibile esaminare hello registri toofind eventuali messaggi di errore. Tali registri si trovano in hello **C:\Resources\Directory\\\LogFiles {ruolo}** cartella. **PrepPython.err.txt** contiene almeno un errore da quando script hello tenta toodetect se è installato Python e **PipInstaller.err.txt** potrebbe segnalare una versione obsoleta del pip.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni più dettagliate sull'utilizzo dei ruoli web e di lavoro in strumenti Python per Visual Studio, vedere la documentazione di PTVS hello:

* [Progetti servizio cloud][Cloud Service Projects]

Per ulteriori informazioni sull'utilizzo di servizi di Azure dai ruoli web e di lavoro, ad esempio l'utilizzo di archiviazione di Azure o Bus di servizio, vedere hello seguenti articoli:

* [Servizio BLOB][Blob Service]
* [Servizio tabelle][Table Service]
* [Servizio di accodamento][Queue Service]
* [Code del bus di servizio][Service Bus Queues]
* [Argomenti del bus di servizio][Service Bus Topics]

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
