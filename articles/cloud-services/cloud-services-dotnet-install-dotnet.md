---
title: Installare .NET nei ruoli di Servizi cloud di Azure | Microsoft Docs
description: Questo articolo illustra come installare manualmente .NET Framework nei ruoli Web e di lavoro del servizio cloud
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
ms.openlocfilehash: a9cffa275ae6b9315b821d3160b17a997a1523f7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="0bb29-103">Installare .NET nei ruoli di Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="0bb29-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="0bb29-104">Questo articolo illustra come installare versioni di .NET Framework non incluse nel sistema operativo guest di Azure.</span><span class="sxs-lookup"><span data-stu-id="0bb29-104">This article describes how to install versions of .NET Framework that don't come with the Azure Guest OS.</span></span> <span data-ttu-id="0bb29-105">È possibile usare .NET nel sistema operativo guest per configurare i ruoli Web e di lavoro del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0bb29-105">You can use .NET on the Guest OS to configure your cloud service web and worker roles.</span></span>

<span data-ttu-id="0bb29-106">Ad esempio, è possibile installare .NET 4.6.1 nella famiglia di sistemi operativi guest 4, non disponibile in nessuna versione di .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="0bb29-106">For example, you can install .NET 4.6.1 on the Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="0bb29-107">La famiglia di sistemi operativi guest 5 è inclusa in .NET 4.6. Per le informazioni più recenti sulle versioni del sistema operativo guest di Azure, vedere [Novità sulle versioni del sistema operativo guest di Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="0bb29-107">(The Guest OS family 5 does come with .NET 4.6.) For the latest information on the Azure Guest OS releases, see the [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="0bb29-108">Azure SDK 2.9 contiene una restrizione relativa alla distribuzione di .NET 4.6 nella famiglia di sistemi operativi guest 4 o versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="0bb29-108">The Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on the Guest OS family 4 or earlier.</span></span> <span data-ttu-id="0bb29-109">Nel sito di [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) è disponibile una correzione alla restrizione.</span><span class="sxs-lookup"><span data-stu-id="0bb29-109">A fix for the restriction is available on the [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="0bb29-110">Per installare .NET nei ruoli Web e di lavoro, includere il programma di installazione Web di .NET come parte del progetto di servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0bb29-110">To install .NET on your web and worker roles, include the .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="0bb29-111">Avviare il programma di installazione come parte delle attività di avvio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="0bb29-111">Start the installer as part of the role's startup tasks.</span></span> 

## <a name="add-the-net-installer-to-your-project"></a><span data-ttu-id="0bb29-112">Aggiungere al progetto il programma di installazione .NET</span><span class="sxs-lookup"><span data-stu-id="0bb29-112">Add the .NET installer to your project</span></span>
<span data-ttu-id="0bb29-113">Per scaricare il programma di installazione Web per .NET Framework, scegliere la versione da installare:</span><span class="sxs-lookup"><span data-stu-id="0bb29-113">To download the web installer for the .NET Framework, choose the version that you want to install:</span></span>

* [<span data-ttu-id="0bb29-114">Programma di installazione Web di .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="0bb29-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="0bb29-115">Programma di installazione Web di .NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="0bb29-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="0bb29-116">Per aggiungere il programma di installazione per un ruolo *Web*:</span><span class="sxs-lookup"><span data-stu-id="0bb29-116">To add the installer for a *web* role:</span></span>
  1. <span data-ttu-id="0bb29-117">In **Ruoli** del progetto di servizio cloud in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul ruolo *Web* e scegliere **Aggiungi** > **Nuova cartella**.</span><span class="sxs-lookup"><span data-stu-id="0bb29-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="0bb29-118">Creare una cartella denominata **bin**.</span><span class="sxs-lookup"><span data-stu-id="0bb29-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="0bb29-119">Fare clic con il pulsante destro del mouse sulla cartella bin e scegliere **Aggiungi** > **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="0bb29-119">Right-click the bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="0bb29-120">Selezionare il programma di installazione .NET e aggiungerlo alla cartella bin.</span><span class="sxs-lookup"><span data-stu-id="0bb29-120">Select the .NET installer and add it to the bin folder.</span></span>
  
<span data-ttu-id="0bb29-121">Per aggiungere il programma di installazione per un ruolo *di lavoro*:</span><span class="sxs-lookup"><span data-stu-id="0bb29-121">To add the installer for a *worker* role:</span></span>
* <span data-ttu-id="0bb29-122">Fare clic con il pulsante destro del mouse sul ruolo *di lavoro* e scegliere **Aggiungi** > **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="0bb29-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="0bb29-123">Selezionare il programma di installazione .NET e aggiungerlo al ruolo.</span><span class="sxs-lookup"><span data-stu-id="0bb29-123">Select the .NET installer and add it to the role.</span></span> 

<span data-ttu-id="0bb29-124">I file aggiunti in questo modo alla cartella di contenuto del ruolo vengono aggiunti automaticamente al pacchetto del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0bb29-124">When files are added in this way to the role content folder, they're automatically added to your cloud service package.</span></span> <span data-ttu-id="0bb29-125">I file vengono quindi distribuiti in una posizione analoga nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0bb29-125">The files are then deployed to a consistent location on the virtual machine.</span></span> <span data-ttu-id="0bb29-126">Ripetere questo processo per tutti i ruoli Web e di lavoro nel servizio cloud, in modo che tutti i ruoli abbiano una copia del programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="0bb29-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="0bb29-127">Anche se l'applicazione è destinata a .NET 4.6, è necessario installare .NET 4.6.1 nel ruolo del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0bb29-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="0bb29-128">Il sistema operativo guest include l'[aggiornamento 3098779](https://support.microsoft.com/kb/3098779) e l'[aggiornamento 3097997](https://support.microsoft.com/kb/3097997) della Knowledge Base.</span><span class="sxs-lookup"><span data-stu-id="0bb29-128">The Guest OS includes the Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="0bb29-129">Se .NET 4.6 viene installato sugli aggiornamenti della Knowledge Base, possono verificarsi problemi durante l'esecuzione delle applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="0bb29-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of the Knowledge Base updates.</span></span> <span data-ttu-id="0bb29-130">Per evitare tali problemi, installare .NET 4.6.1 anziché la versione 4.6.</span><span class="sxs-lookup"><span data-stu-id="0bb29-130">To avoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="0bb29-131">Per altre informazioni, vedere l'[articolo 3118750 della Knowledge Base](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="0bb29-131">For more information, see the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Contenuto del ruolo con i file del programma di installazione][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="0bb29-133">Definire le attività di avvio per i ruoli</span><span class="sxs-lookup"><span data-stu-id="0bb29-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="0bb29-134">È possibile usare le attività di avvio per eseguire operazioni prima dell'avvio di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="0bb29-134">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="0bb29-135">Per assicurarsi che il framework venga installato prima di eseguire qualsiasi codice dell'applicazione, installare .NET Framework come parte dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="0bb29-135">Installing the .NET Framework as part of the startup task ensures that the framework is installed before any application code is run.</span></span> <span data-ttu-id="0bb29-136">Per altre informazioni sulle attività di avvio, vedere [Eseguire attività di avvio in Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="0bb29-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="0bb29-137">Aggiungere il contenuto seguente al file ServiceDefinition.csdef nel nodo **WebRole** o **WorkerRole** per tutti i ruoli:</span><span class="sxs-lookup"><span data-stu-id="0bb29-137">Add the following content to the ServiceDefinition.csdef file under the **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="0bb29-138">La configurazione precedente esegue il comando `install.cmd` della console con privilegi di amministratore per installare .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="0bb29-138">The preceding configuration runs the console command `install.cmd` with administrator privileges to install the .NET Framework.</span></span> <span data-ttu-id="0bb29-139">La configurazione crea anche un elemento **LocalStorage** con nome **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="0bb29-139">The configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="0bb29-140">Lo script di avvio imposta la cartella temporanea per l'uso di questa risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="0bb29-140">The startup script sets the temp folder to use this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="0bb29-141">Perché il framework venga installato correttamente, impostare le dimensioni della risorsa su almeno 1.024 MB.</span><span class="sxs-lookup"><span data-stu-id="0bb29-141">To ensure correct installation of the framework, set the size of this resource to at least 1,024 MB.</span></span>
    
    <span data-ttu-id="0bb29-142">Per altre informazioni sulle attività di avvio, vedere [Attività di avvio comuni del servizio cloud](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="0bb29-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="0bb29-143">Creare un file denominato **install.cmd** e aggiungere al file lo script di installazione seguente.</span><span class="sxs-lookup"><span data-stu-id="0bb29-143">Create a file named **install.cmd** and add the following install script to the file.</span></span>

    <span data-ttu-id="0bb29-144">Lo script verifica se la versione di .NET Framework specificata è già installata nel computer eseguendo una query sul registro.</span><span class="sxs-lookup"><span data-stu-id="0bb29-144">The script checks whether the specified version of the .NET Framework is already installed on the machine by querying the registry.</span></span> <span data-ttu-id="0bb29-145">Se la versione di .NET non è installata, viene avviato il programma di installazione Web di .NET.</span><span class="sxs-lookup"><span data-stu-id="0bb29-145">If the .NET version is not installed, then the .NET web installer is opened.</span></span> <span data-ttu-id="0bb29-146">Per consentire la risoluzione di eventuali problemi, lo script registra tutte le attività in un file denominato startuptasklog-(data e ora corrente).txt memorizzato nell'archiviazione locale **InstallLogs**.</span><span class="sxs-lookup"><span data-stu-id="0bb29-146">To help troubleshoot any issues, the script logs all activity to the file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0bb29-147">Usare un editor di testo di base, come Blocco note di Windows, per creare il file install.cmd.</span><span class="sxs-lookup"><span data-stu-id="0bb29-147">Use a basic text editor like Windows Notepad to create the install.cmd file.</span></span> <span data-ttu-id="0bb29-148">Se si usa Visual Studio per creare un file di testo e si modifica l'estensione in cmd, il file potrebbe ancora contenere un byte order mark UTF-8.</span><span class="sxs-lookup"><span data-stu-id="0bb29-148">If you use Visual Studio to create a text file and change the extension to .cmd, the file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="0bb29-149">Il byte order mark può provocare un errore quando viene eseguita la prima riga dello script.</span><span class="sxs-lookup"><span data-stu-id="0bb29-149">This mark can cause an error when the first line of the script is run.</span></span> <span data-ttu-id="0bb29-150">Per evitare questo errore, creare la prima riga dello script come istruzione REM che possa essere ignorata dall'elaborazione dell'ordine dei byte.</span><span class="sxs-lookup"><span data-stu-id="0bb29-150">To avoid this error, make the first line of the script a REM statement that can be skipped by the byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set the value of netfx to install appropriate .NET Framework. 
    REM ***** To install .NET 4.5.2 set the variable netfx to "NDP452" *****
    REM ***** To install .NET 4.6 set the variable netfx to "NDP46" *****
    REM ***** To install .NET 4.6.1 set the variable netfx to "NDP461" *****
    REM ***** To install .NET 4.6.2 set the variable netfx to "NDP462" *****
    REM ***** To install .NET 4.7 set the variable netfx to "NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed to correctly install .NET 4.6.1, otherwise you may see an out of disk space error *****
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
    echo Restarting to complete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="0bb29-151">Questo script mostra come installare .NET 4.5.2 o la versione 4.6 per la continuità, anche se .NET 4.5.2 è già disponibile nel sistema operativo guest di Azure.</span><span class="sxs-lookup"><span data-stu-id="0bb29-151">This script shows how to install .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on the Azure Guest OS.</span></span> <span data-ttu-id="0bb29-152">Installare direttamente .NET 4.6.1 anziché la versione 4.6, come descritto nell'[articolo 3118750 della Knowledge Base](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="0bb29-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="0bb29-153">Aggiungere il file install.cmd a ogni ruolo tramite **Aggiungi** > **Elemento esistente** in **Esplora soluzioni**, come descritto in precedenza in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="0bb29-153">Add the install.cmd file to each role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="0bb29-154">Al termine, tutti i ruoli avranno a disposizione il file del programma di installazione di .NET e il file install.cmd.</span><span class="sxs-lookup"><span data-stu-id="0bb29-154">After this step is complete, all roles should have the .NET installer file and the install.cmd file.</span></span>

   ![Contenuto del ruolo con tutti i file][2]

## <a name="configure-diagnostics-to-transfer-startup-logs-to-blob-storage"></a><span data-ttu-id="0bb29-156">Configurare la diagnostica per trasferire i log di avvio nell'archivio BLOB</span><span class="sxs-lookup"><span data-stu-id="0bb29-156">Configure Diagnostics to transfer startup logs to Blob storage</span></span>
<span data-ttu-id="0bb29-157">Per semplificare la risoluzione dei problemi di installazione, è possibile configurare Diagnostica di Azure per trasferire i file di log generati dallo script di avvio o dal programma di installazione di .NET nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0bb29-157">To simplify troubleshooting installation issues, you can configure Azure Diagnostics to transfer any log files generated by the startup script or the .NET installer to Azure Blob storage.</span></span> <span data-ttu-id="0bb29-158">Con questo approccio è possibile visualizzare i log scaricando i file di log dall'archivio BLOB anziché collegandosi al ruolo tramite desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="0bb29-158">By using this approach, you can view the logs by downloading the log files from Blob storage rather than having to remote desktop into the role.</span></span>

<span data-ttu-id="0bb29-159">Per configurare la diagnostica, aprire il diagnostics.wadcfgx e aggiungere il contenuto seguente al nodo **Directory**:</span><span class="sxs-lookup"><span data-stu-id="0bb29-159">To configure Diagnostics, open the diagnostics.wadcfgx file and add the following content under the **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="0bb29-160">Questo codice XML permette di configurare Diagnostica di Azure per il trasferimento di tutti i file presenti nella directory dei log della risorsa **NETFXInstall** nell'account di archiviazione di Diagnostica nel contenitore BLOB **netfx-install**.</span><span class="sxs-lookup"><span data-stu-id="0bb29-160">This XML configures Diagnostics to transfer the files in the log directory in the **NETFXInstall** resource to the Diagnostics storage account in the **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="0bb29-161">Distribuire il servizio cloud</span><span class="sxs-lookup"><span data-stu-id="0bb29-161">Deploy your cloud service</span></span>
<span data-ttu-id="0bb29-162">Quando si distribuisce il servizio cloud, le attività di avvio installano .NET Framework, se non è già installato.</span><span class="sxs-lookup"><span data-stu-id="0bb29-162">When you deploy your cloud service, the startup tasks install the .NET Framework if it's not already installed.</span></span> <span data-ttu-id="0bb29-163">Durante l'installazione del framework, i ruoli dei servizi cloud sono in stato *occupato*.</span><span class="sxs-lookup"><span data-stu-id="0bb29-163">Your cloud service roles are in the *busy* state while the framework is being installed.</span></span> <span data-ttu-id="0bb29-164">Se l'installazione del framework richiede un riavvio, potrebbero essere riavviati anche i ruoli del servizio.</span><span class="sxs-lookup"><span data-stu-id="0bb29-164">If the framework installation requires a restart, the service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0bb29-165">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0bb29-165">Additional resources</span></span>
* <span data-ttu-id="0bb29-166">[Installazione di .NET Framework][Installing the .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="0bb29-166">[Installing the .NET Framework][Installing the .NET Framework]</span></span>
* <span data-ttu-id="0bb29-167">[Determinare quali sono le versioni di .NET Framework installate][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="0bb29-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="0bb29-168">[Risoluzione dei problemi di installazione di .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="0bb29-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing the .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
