---
title: gli errori di client Docker aaaTroubleshooting in Windows usando Visual Studio | Documenti Microsoft
description: Risolvere i problemi riscontrati quando si utilizza Visual Studio toocreate e distribuire tooDocker App web in Windows usando Visual Studio.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="bebdc-103">Risoluzione dei problemi di sviluppo di Docker in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bebdc-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="bebdc-104">Quando si lavora con Visual Studio Tools per Docker Preview, è possibile riscontrare alcuni problemi a causa di natura hello dell'anteprima di hello.</span><span class="sxs-lookup"><span data-stu-id="bebdc-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="bebdc-105">Di seguito vengono riportati alcuni problemi comuni e le soluzioni relative.</span><span class="sxs-lookup"><span data-stu-id="bebdc-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="bebdc-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="bebdc-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="bebdc-107">**Contenitori Linux**</span><span class="sxs-lookup"><span data-stu-id="bebdc-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="bebdc-108">Si verificano errori di compilazione durante il debug di un'applicazione console o Web .NET Core</span><span class="sxs-lookup"><span data-stu-id="bebdc-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="bebdc-109">Questo potrebbe essere correlato toonot condividono unità hello in cui si trova il progetto hello con Docker per Windows.</span><span class="sxs-lookup"><span data-stu-id="bebdc-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="bebdc-110">Potrebbe essere visualizzato un errore analogo hello seguente:</span><span class="sxs-lookup"><span data-stu-id="bebdc-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="bebdc-111">tooresolve questo problema:</span><span class="sxs-lookup"><span data-stu-id="bebdc-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="bebdc-112">Fare doppio clic su **Docker per Windows** in hello area di notifica e quindi selezionare **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="bebdc-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="bebdc-113">Selezionare **unità condivise** e condividere hello unità in cui si trova il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="bebdc-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="bebdc-114">**Contenitori Windows**</span><span class="sxs-lookup"><span data-stu-id="bebdc-114">**Windows containers**</span></span>

<span data-ttu-id="bebdc-115">Hello problemi descritti di seguito sono toodebugging specifico .NET Framework web e console applicazioni nei contenitori di Windows.</span><span class="sxs-lookup"><span data-stu-id="bebdc-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="bebdc-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bebdc-116">Prerequisites</span></span>

1. <span data-ttu-id="bebdc-117">Visual Studio 2017 RC (o versioni successive) con hello .NET Core e carico di lavoro di anteprima di Docker deve essere installato.</span><span class="sxs-lookup"><span data-stu-id="bebdc-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="bebdc-118">Windows 10 Anniversary Update con le patch di Windows Update più recenti.</span><span class="sxs-lookup"><span data-stu-id="bebdc-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="bebdc-119">È in particolare necessario installare [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016).</span><span class="sxs-lookup"><span data-stu-id="bebdc-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="bebdc-120">È necessario installare [Docker per Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="bebdc-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="bebdc-121">**Passare a contenitori tooWindows** deve essere selezionato.</span><span class="sxs-lookup"><span data-stu-id="bebdc-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="bebdc-122">Nell'area di notifica hello, fare clic su **Docker per Windows**, quindi selezionare **passare contenitori tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="bebdc-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="bebdc-123">Dopo il riavvio del computer hello, assicurarsi che questa impostazione viene mantenuta.</span><span class="sxs-lookup"><span data-stu-id="bebdc-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="bebdc-124">L'output della console non viene visualizzato nella finestra di output di Visual Studio durante il debug di un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="bebdc-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="bebdc-125">Si tratta di un problema noto con debugger di Visual Studio hello (msvsmon.exe), che attualmente non è progettato per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="bebdc-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="bebdc-126">Il supporto per questo scenario potrà essere incluso in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="bebdc-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="bebdc-127">toosee output da un'applicazione console in Visual Studio, usare hello **Docker: Avvia progetto**, che equivale troppo**Avvia senza eseguire debug**.</span><span class="sxs-lookup"><span data-stu-id="bebdc-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="bebdc-128">Debug di applicazioni web con hello versione di configurazione non riesce con errore di accesso negato (403)</span><span class="sxs-lookup"><span data-stu-id="bebdc-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="bebdc-129">toowork questo problema, aprire web.release.config soluzione hello e impostare come commento o eliminare hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="bebdc-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="bebdc-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="bebdc-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="bebdc-131">**Contenitori Linux**</span><span class="sxs-lookup"><span data-stu-id="bebdc-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="bebdc-132">Mapping del volume non è possibile toovalidate</span><span class="sxs-lookup"><span data-stu-id="bebdc-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="bebdc-133">Mapping del volume è il codice sorgente hello tooshare necessarie e i file binari dell'applicazione con cartella dell'applicazione hello nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="bebdc-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="bebdc-134">Mapping del volume specifici sono contenuti all'interno dei file docker-compose.dev.debug.yml e docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="bebdc-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="bebdc-135">Come i file vengono modificati nel computer host, i contenitori di hello riflettono tali modifiche in una struttura di cartelle simile.</span><span class="sxs-lookup"><span data-stu-id="bebdc-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="bebdc-136">mapping del volume tooenable:</span><span class="sxs-lookup"><span data-stu-id="bebdc-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="bebdc-137">Fare clic su **Moby** nell'area di notifica hello e selezionare **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="bebdc-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="bebdc-138">Selezionare **Unità condivise**.</span><span class="sxs-lookup"><span data-stu-id="bebdc-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="bebdc-139">Selezionare un'unità che ospita il progetto e hello sul disco in cui si trova in % USERPROFILE % hello.</span><span class="sxs-lookup"><span data-stu-id="bebdc-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="bebdc-140">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="bebdc-140">Click **Apply**.</span></span>

<span data-ttu-id="bebdc-141">tootest se funziona mapping del volume, ricompilare e selezionare F5 da Visual Studio dopo che sono stati condivisione o hello seguente di codice da un prompt dei comandi eseguire uno o più unità.</span><span class="sxs-lookup"><span data-stu-id="bebdc-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="bebdc-142">Questo esempio presuppone che la cartella Utenti si trovi nell'unità C e che sia stata condivisa.</span><span class="sxs-lookup"><span data-stu-id="bebdc-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="bebdc-143">Se è stata condivisa un'unità diversa, aggiornare di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="bebdc-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="bebdc-144">Eseguire hello seguente codice nel contenitore di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="bebdc-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="bebdc-145">Verrà visualizzato un'elenco delle directory da hello utenti o delle cartelle pubbliche.</span><span class="sxs-lookup"><span data-stu-id="bebdc-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="bebdc-146">Se non vengono visualizzati file e la cartella in /c/Users/Public non è vuota, il mapping del volume non è configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="bebdc-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="bebdc-147">Modificare toohello spaziale toosee hello contenuto della directory di hello `/c/Users/Public` directory:</span><span class="sxs-lookup"><span data-stu-id="bebdc-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="bebdc-148">Quando si lavora con le macchine virtuali Linux, hello contenitore file system è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="bebdc-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="bebdc-149">Build: errore imprevisto dell'attività "PrepareForBuild"</span><span class="sxs-lookup"><span data-stu-id="bebdc-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="bebdc-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Errore durante il tentativo di tooconnect.</span><span class="sxs-lookup"><span data-stu-id="bebdc-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="bebdc-151">Verificare che host Docker di hello predefinito sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bebdc-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="bebdc-152">Aprire un prompt dei comandi ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="bebdc-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="bebdc-153">Se viene restituito un errore, quindi tentare di hello toostart **Docker per Windows** app desktop.</span><span class="sxs-lookup"><span data-stu-id="bebdc-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="bebdc-154">Se viene eseguita l'app desktop hello, quindi **Moby** deve essere visibile nell'area di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="bebdc-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="bebdc-155">Fare doppio clic su **Moby** e aprire **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="bebdc-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="bebdc-156">Fare clic su **Reimposta** e quindi riavviare Docker.</span><span class="sxs-lookup"><span data-stu-id="bebdc-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="bebdc-157">Una finestra di dialogo di errore si verifica durante il tentativo di tooadd Docker supporto o il debug (F5) di un'applicazione ASP.NET Core in un contenitore</span><span class="sxs-lookup"><span data-stu-id="bebdc-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="bebdc-158">Dopo la disinstallazione e l'installazione delle estensioni, può risultare danneggiato hello cache Managed Extensibility Framework (MEF) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bebdc-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="bebdc-159">In questo caso, può provocare diversi messaggi di errore quando si è aggiunta del supporto di Docker e/o il tentativo di toorun o eseguire il debug (F5) dell'applicazione ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="bebdc-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="bebdc-160">Come soluzione alternativa temporanea, utilizzare hello seguendo i passaggi toodelete e rigenerare hello cache MEF.</span><span class="sxs-lookup"><span data-stu-id="bebdc-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="bebdc-161">Chiudere tutte le istanze di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bebdc-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="bebdc-162">Aprire %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="bebdc-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="bebdc-163">Eliminare hello seguenti cartelle:</span><span class="sxs-lookup"><span data-stu-id="bebdc-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="bebdc-164">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bebdc-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="bebdc-165">Tentare nuovamente di scenario hello.</span><span class="sxs-lookup"><span data-stu-id="bebdc-165">Attempt hello scenario again.</span></span>
