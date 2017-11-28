---
title: aaaInstall .NET per i ruoli di servizi Cloud di Azure | Documenti Microsoft
description: In questo articolo viene descritto come toomanually installarvi hello .NET Framework i ruoli web e di lavoro dei servizi cloud
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="53929-103">Installare .NET nei ruoli di Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="53929-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="53929-104">In questo articolo viene descritto come tooinstall versioni di .NET Framework che non provengono con hello del sistema operativo Guest Azure.</span><span class="sxs-lookup"><span data-stu-id="53929-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="53929-105">È possibile utilizzare .NET su hello del sistema operativo Guest tooconfigure i ruoli web e di lavoro del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="53929-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="53929-106">Ad esempio, è possibile installare .NET 4.6.1 in hello famiglia di sistemi operativi Guest 4, non disponibili con qualsiasi versione di .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="53929-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="53929-107">(hello famiglia del sistema operativo Guest 5 viene fornito con .NET 4.6). Per informazioni più recenti di hello in hello versioni del sistema operativo Guest Azure, vedere hello [notizie di versione del sistema operativo Guest Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="53929-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="53929-108">Hello Azure SDK 2.9 contiene una restrizione sulla distribuzione per la famiglia di sistemi operativi Guest hello 4 o versioni precedente di .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="53929-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="53929-109">È disponibile in hello una correzione per la restrizione di hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) sito.</span><span class="sxs-lookup"><span data-stu-id="53929-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="53929-110">tooinstall .NET nei ruoli di lavoro e web, includono hello web programma d'installazione .NET come parte del progetto servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="53929-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="53929-111">Avviare Installazione guidata di hello come parte delle attività di avvio del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="53929-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="53929-112">Aggiungi progetto tooyour programma di installazione di .NET hello</span><span class="sxs-lookup"><span data-stu-id="53929-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="53929-113">programma di installazione di toodownload hello web per .NET Framework, hello scegliere versione hello che si desidera tooinstall:</span><span class="sxs-lookup"><span data-stu-id="53929-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="53929-114">Programma di installazione Web di .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="53929-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="53929-115">Programma di installazione Web di .NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="53929-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="53929-116">il programma di installazione di tooadd hello per un *web* ruolo:</span><span class="sxs-lookup"><span data-stu-id="53929-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="53929-117">In **Ruoli** del progetto di servizio cloud in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul ruolo *Web* e scegliere **Aggiungi** > **Nuova cartella**.</span><span class="sxs-lookup"><span data-stu-id="53929-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="53929-118">Creare una cartella denominata **bin**.</span><span class="sxs-lookup"><span data-stu-id="53929-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="53929-119">Fare clic sulla cartella bin hello e selezionare **Aggiungi** > **elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="53929-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="53929-120">Selezionare il programma di installazione di hello .NET e aggiungerlo toohello nella cartella bin.</span><span class="sxs-lookup"><span data-stu-id="53929-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="53929-121">il programma di installazione di tooadd hello per un *lavoro* ruolo:</span><span class="sxs-lookup"><span data-stu-id="53929-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="53929-122">Fare clic con il pulsante destro del mouse sul ruolo *di lavoro* e scegliere **Aggiungi** > **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="53929-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="53929-123">Selezionare il programma di installazione di hello .NET e aggiungerlo toohello ruolo.</span><span class="sxs-lookup"><span data-stu-id="53929-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="53929-124">Quando vengono aggiunti file nella cartella del contenuto in questo modo toohello ruolo, vengono aggiunte automaticamente tooyour pacchetto del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="53929-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="53929-125">vengono quindi distribuito tooa posizione coerente sulla macchina virtuale hello, i file Hello.</span><span class="sxs-lookup"><span data-stu-id="53929-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="53929-126">Ripetere questo processo per ogni ruolo web e di lavoro nel servizio cloud in modo che tutti i ruoli sono una copia del programma di installazione hello.</span><span class="sxs-lookup"><span data-stu-id="53929-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="53929-127">Anche se l'applicazione è destinata a .NET 4.6, è necessario installare .NET 4.6.1 nel ruolo del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="53929-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="53929-128">Hello del sistema operativo Guest include hello Knowledge Base [aggiornare 3098779](https://support.microsoft.com/kb/3098779) e [aggiornare 3097997](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="53929-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="53929-129">Durante l'esecuzione delle applicazioni .NET se .NET 4.6 è installata nella parte superiore di aggiornamenti della Knowledge Base hello, possono verificarsi i problemi.</span><span class="sxs-lookup"><span data-stu-id="53929-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="53929-130">tooavoid questi problemi, installare .NET 4.6.1 anziché versione 4.6.</span><span class="sxs-lookup"><span data-stu-id="53929-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="53929-131">Per ulteriori informazioni, vedere hello [articolo della Knowledge Base 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="53929-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Contenuto del ruolo con i file del programma di installazione][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="53929-133">Definire le attività di avvio per i ruoli</span><span class="sxs-lookup"><span data-stu-id="53929-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="53929-134">È possibile utilizzare le operazioni di avvio attività tooperform prima dell'avvio di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="53929-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="53929-135">L'installazione di .NET Framework hello come parte dell'attività di avvio hello assicura tale framework hello viene installato prima di eseguita qualsiasi codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="53929-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="53929-136">Per altre informazioni sulle attività di avvio, vedere [Eseguire attività di avvio in Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="53929-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="53929-137">Aggiungere i seguenti file servicedefinition. Csdef toohello contenuto in hello hello **WebRole** o **WorkerRole** nodo per tutti i ruoli:</span><span class="sxs-lookup"><span data-stu-id="53929-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    <span data-ttu-id="53929-138">Hello configurazione precedente viene eseguito il comando di console hello `install.cmd` con tooinstall di privilegi di amministratore hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="53929-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="53929-139">configurazione di Hello crea anche un **LocalStorage** elemento denominato **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="53929-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="53929-140">script di avvio Hello imposta hello cartella temporanea toouse questa risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="53929-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="53929-141">tooensure corretta installazione di framework hello, hello dimensioni del set di tooat questa risorsa almeno 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="53929-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="53929-142">Per altre informazioni sulle attività di avvio, vedere [Attività di avvio comuni del servizio cloud](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="53929-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="53929-143">Creare un file denominato **Install** e aggiungere i seguenti hello installare file di script toohello.</span><span class="sxs-lookup"><span data-stu-id="53929-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="53929-144">script Hello controlla se versione specificata di hello di hello .NET Framework è già installato nel computer di hello eseguendo una query del Registro di sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="53929-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="53929-145">Se la versione di .NET hello non è installata, viene aperto il programma di installazione di hello .NET web.</span><span class="sxs-lookup"><span data-stu-id="53929-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="53929-146">toohelp risolvere eventuali problemi, lo script di hello registra tutte le attività toohello file startuptasklog-(data e ora correnti). txt che viene archiviato in **InstallLogs** archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="53929-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="53929-147">Usare un semplice editor di testo come blocco note di Windows toocreate hello Install file.</span><span class="sxs-lookup"><span data-stu-id="53929-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="53929-148">Se si utilizza Visual Studio toocreate un file di testo e modificare hello estensione too.cmd, file hello potrebbe ancora contenere un contrassegno di ordine dei byte UTF-8.</span><span class="sxs-lookup"><span data-stu-id="53929-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="53929-149">Questo contrassegno può provocare un errore quando viene eseguito prima riga di hello dello script hello.</span><span class="sxs-lookup"><span data-stu-id="53929-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="53929-150">tooavoid questo errore, verificare prima riga di hello di hello script un'istruzione REM che possa essere ignorata dall'elaborazione dell'ordine di byte di hello.</span><span class="sxs-lookup"><span data-stu-id="53929-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="53929-151">Questo script illustra modalità tooinstall .NET 4.5.2 o 4.6 di versione per la continuità, anche se .NET 4.5.2 è già disponibile nel hello del sistema operativo Guest Azure.</span><span class="sxs-lookup"><span data-stu-id="53929-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="53929-152">È necessario installare direttamente .NET 4.6.1 anziché versione 4.6, come descritto in hello [articolo della Knowledge Base 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="53929-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="53929-153">Ruolo Aggiungi hello Install file tooeach utilizzando **Aggiungi** > **elemento esistente** in **Esplora** come descritto in precedenza in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="53929-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="53929-154">Dopo aver completato questo passaggio, tutti i ruoli devono avere file di programma di installazione .NET hello e file Install hello.</span><span class="sxs-lookup"><span data-stu-id="53929-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![Contenuto del ruolo con tutti i file][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="53929-156">Configurare l'archiviazione di diagnostica tootransfer avvio registri tooBlob</span><span class="sxs-lookup"><span data-stu-id="53929-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="53929-157">toosimplify risoluzione dei problemi di installazione, è possibile configurare diagnostica Azure tootransfer qualsiasi file di log generati dall'avvio hello lo script o hello archiviazione Blob tooAzure programma di installazione di .NET.</span><span class="sxs-lookup"><span data-stu-id="53929-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="53929-158">Usando questo approccio, è possibile visualizzare i registri di hello il download dei file di log di hello dall'archiviazione Blob anziché tooremote desktop in ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="53929-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="53929-159">Diagnostica tooconfigure, aprire il file Diagnostics. wadcfgx hello e aggiungere hello dopo contenuto in hello **directory** nodo:</span><span class="sxs-lookup"><span data-stu-id="53929-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="53929-160">Questo codice XML consente di configurare i file di diagnostica tootransfer hello nella directory log hello in hello **NETFXInstall** toohello risorse account di archiviazione di diagnostica di hello **netfx installazione** contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="53929-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="53929-161">Distribuire il servizio cloud</span><span class="sxs-lookup"><span data-stu-id="53929-161">Deploy your cloud service</span></span>
<span data-ttu-id="53929-162">Quando si distribuisce il servizio cloud, le attività di avvio hello installare .NET Framework hello se non è già installato.</span><span class="sxs-lookup"><span data-stu-id="53929-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="53929-163">I ruoli dei servizi cloud sono in hello *occupato* stato durante l'installazione di framework hello.</span><span class="sxs-lookup"><span data-stu-id="53929-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="53929-164">Se l'installazione di framework hello richiede un riavvio, potrebbe essere riavviato anche i ruoli del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="53929-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="53929-165">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="53929-165">Additional resources</span></span>
* <span data-ttu-id="53929-166">[L'installazione di .NET Framework hello][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="53929-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="53929-167">[Determinare quali sono le versioni di .NET Framework installate][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="53929-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="53929-168">[Risoluzione dei problemi di installazione di .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="53929-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
