---
title: Risoluzione dei problemi client docker in Windows con Visual Studio | Microsoft Docs
description: Risoluzione dei problemi che si verificano quando si usa Visual Studio per creare e distribuire app Web in Docker su Windows mediante Visual Studio.
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
ms.openlocfilehash: 89fa04a1107b6abb49aefd68066443717ac9b731
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="87506-103">Risoluzione dei problemi di sviluppo di Docker in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87506-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="87506-104">Quando si usa l'anteprima degli Strumenti di Visual Studio per Docker, si possono verificare alcuni problemi a causa della natura dell'anteprima.</span><span class="sxs-lookup"><span data-stu-id="87506-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of the nature of the preview.</span></span>
<span data-ttu-id="87506-105">Di seguito vengono riportati alcuni problemi comuni e le soluzioni relative.</span><span class="sxs-lookup"><span data-stu-id="87506-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="87506-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="87506-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="87506-107">**Contenitori Linux**</span><span class="sxs-lookup"><span data-stu-id="87506-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="87506-108">Si verificano errori di compilazione durante il debug di un'applicazione console o Web .NET Core</span><span class="sxs-lookup"><span data-stu-id="87506-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="87506-109">Questo errore può verificarsi quando l'unità in cui si trova il progetto non viene condivisa con Docker per Windows.</span><span class="sxs-lookup"><span data-stu-id="87506-109">This could be related to not sharing the drive where the project resides with Docker for Windows.</span></span>  <span data-ttu-id="87506-110">È possibile che venga visualizzato un errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="87506-110">You may receive an error like the following:</span></span>

```
The "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with the default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="87506-111">Per risolvere il problema:</span><span class="sxs-lookup"><span data-stu-id="87506-111">To resolve this issue:</span></span>

1. <span data-ttu-id="87506-112">Fare doppio clic su **Docker per Windows** nell'area di notifica e quindi selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="87506-112">Right-click **Docker for Windows** in the notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="87506-113">Fare clic su **Unità condivise** e condividere l'unità in cui si trova il progetto.</span><span class="sxs-lookup"><span data-stu-id="87506-113">Select **Shared Drives** and share the drive where the project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="87506-114">**Contenitori Windows**</span><span class="sxs-lookup"><span data-stu-id="87506-114">**Windows containers**</span></span>

<span data-ttu-id="87506-115">Di seguito sono elencati i possibili errori che possono verificarsi durante il debug di applicazioni console e Web .NET Framework in contenitori Windows.</span><span class="sxs-lookup"><span data-stu-id="87506-115">The following issues are specific to debugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="87506-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="87506-116">Prerequisites</span></span>

1. <span data-ttu-id="87506-117">Visual Studio 2017 RC (o versione successiva) con .NET Core e il carico di lavoro Docker (anteprima) installato.</span><span class="sxs-lookup"><span data-stu-id="87506-117">Visual Studio 2017 RC (or later) with the .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="87506-118">Windows 10 Anniversary Update con le patch di Windows Update più recenti.</span><span class="sxs-lookup"><span data-stu-id="87506-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="87506-119">È in particolare necessario installare [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016).</span><span class="sxs-lookup"><span data-stu-id="87506-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="87506-120">È necessario installare [Docker per Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="87506-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="87506-121">Opzione **Switch to Windows containers** (Passa ai contenitori Windows) selezionata.</span><span class="sxs-lookup"><span data-stu-id="87506-121">**Switch to Windows containers** must be selected.</span></span> <span data-ttu-id="87506-122">Fare doppio clic su **Docker per Windows** nell'area di notifica e quindi selezionare **Switch to Windows containers** (Passa ai contenitori Windows).</span><span class="sxs-lookup"><span data-stu-id="87506-122">In the notification area, click **Docker for Windows**, and then select **Switch to Windows containers**.</span></span> <span data-ttu-id="87506-123">Dopo aver riavviato il computer, verificare che questa impostazione sia stata mantenuta.</span><span class="sxs-lookup"><span data-stu-id="87506-123">After the machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="87506-124">L'output della console non viene visualizzato nella finestra di output di Visual Studio durante il debug di un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="87506-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="87506-125">Si tratta di un problema noto con il debugger di Visual Studio (msvsmon.exe), attualmente non progettato per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="87506-125">This is a known issue with the Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="87506-126">Il supporto per questo scenario potrà essere incluso in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="87506-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="87506-127">Per visualizzare l'output dell'applicazione console in Visual Studio, usare **Docker: Avvia progetto**, che equivale a **Avvia senza eseguire debug**.</span><span class="sxs-lookup"><span data-stu-id="87506-127">To see output from the console application in Visual Studio, use **Docker: Start Project**, which is equivalent to **Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-the-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="87506-128">Il debug di applicazioni Web con la configurazione di rilascio ha esito negativo con l'errore 403 - Accesso negato</span><span class="sxs-lookup"><span data-stu-id="87506-128">Debugging web applications with the release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="87506-129">Per risolvere il problema, aprire web.release.config nella soluzione ed eliminare o impostare come commento le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="87506-129">To work around this issue, open web.release.config in the solution and comment out or delete the following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="87506-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="87506-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="87506-131">**Contenitori Linux**</span><span class="sxs-lookup"><span data-stu-id="87506-131">**Linux containers**</span></span>

#### <a name="unable-to-validate-volume-mapping"></a><span data-ttu-id="87506-132">Non è possibile convalidare il mapping del volume</span><span class="sxs-lookup"><span data-stu-id="87506-132">Unable to validate volume mapping</span></span>
<span data-ttu-id="87506-133">Il mapping del volume è necessario per condividere il codice sorgente e i file binari dell'applicazione con la cartella dell'app nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="87506-133">Volume mapping is required to share the source code and binaries of your application with the app folder in the container.</span></span>  <span data-ttu-id="87506-134">Mapping del volume specifici sono contenuti all'interno dei file docker-compose.dev.debug.yml e docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="87506-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="87506-135">Dal momento che i file vengono modificati nel computer host, i contenitori riflettono queste modifiche in una struttura di cartelle simile.</span><span class="sxs-lookup"><span data-stu-id="87506-135">As files are changed on your host machine, the containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="87506-136">Per abilitare il mapping del volume:</span><span class="sxs-lookup"><span data-stu-id="87506-136">To enable volume mapping:</span></span>

1. <span data-ttu-id="87506-137">Fare clic su **Moby** nell'area di notifica e selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="87506-137">Click **Moby** in the notification area and select **Settings**.</span></span>
2. <span data-ttu-id="87506-138">Selezionare **Unità condivise**.</span><span class="sxs-lookup"><span data-stu-id="87506-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="87506-139">Selezionare l'unità che ospita il progetto e l'unità in cui si trova %USERPROFILE%.</span><span class="sxs-lookup"><span data-stu-id="87506-139">Select the drive that hosts your project and the drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="87506-140">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="87506-140">Click **Apply**.</span></span>

<span data-ttu-id="87506-141">Per verificare il corretto funzionamento del mapping del volume, ricompilare e premere F5 da Visual Studio dopo aver condivisio le unità oppure eseguire il codice seguente da un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="87506-141">To test if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run the following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="87506-142">Questo esempio presuppone che la cartella Utenti si trovi nell'unità C e che sia stata condivisa.</span><span class="sxs-lookup"><span data-stu-id="87506-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="87506-143">Se è stata condivisa un'unità diversa, aggiornare di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="87506-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="87506-144">Eseguire il codice seguente nel contenitore di Linux.</span><span class="sxs-lookup"><span data-stu-id="87506-144">Run the following code in the Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="87506-145">Verrà visualizzato un elenco di cartelle dalla directory Users/Public.</span><span class="sxs-lookup"><span data-stu-id="87506-145">You should see a directory listing from the Users/Public folder.</span></span> <span data-ttu-id="87506-146">Se non vengono visualizzati file e la cartella in /c/Users/Public non è vuota, il mapping del volume non è configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="87506-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="87506-147">Passare alla directory wormhole per visualizzare il contenuto della directory `/c/Users/Public`:</span><span class="sxs-lookup"><span data-stu-id="87506-147">Change to the wormhole directory to see the contents of the `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="87506-148">Quando si usano macchine virtuali Linux, il file system del contenitore fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="87506-148">When you're working with Linux VMs, the container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="87506-149">Build: errore imprevisto dell'attività "PrepareForBuild"</span><span class="sxs-lookup"><span data-stu-id="87506-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="87506-150">Microsoft.DotNet.Docker.CommandLine.ClientException: si è verificato un errore nel tentativo di connessione.</span><span class="sxs-lookup"><span data-stu-id="87506-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying to connect.</span></span>

<span data-ttu-id="87506-151">Verificare che l'host Docker predefinito sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="87506-151">Verify that the default Docker host is running.</span></span> <span data-ttu-id="87506-152">Aprire un prompt dei comandi ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="87506-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="87506-153">Se viene restituito un errore, provare ad avviare l'applicazione desktop **Docker per Windows** .</span><span class="sxs-lookup"><span data-stu-id="87506-153">If this returns an error, then attempt to start the **Docker for Windows** desktop app.</span></span> <span data-ttu-id="87506-154">Se l'applicazione desktop è in esecuzione, l'icona di **Moby** nell'area di notifica dovrebbe essere visibile.</span><span class="sxs-lookup"><span data-stu-id="87506-154">If the desktop app is running, then **Moby** should be visible in the notification area.</span></span> <span data-ttu-id="87506-155">Fare doppio clic su **Moby** e aprire **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="87506-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="87506-156">Fare clic su **Reimposta** e quindi riavviare Docker.</span><span class="sxs-lookup"><span data-stu-id="87506-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-to-add-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="87506-157">Viene visualizzato un messaggio di errore quando si tenta di aggiungere il supporto per Docker o di eseguire il debug (F5) di un'applicazione ASP.NET Core in un contenitore</span><span class="sxs-lookup"><span data-stu-id="87506-157">An error dialog occurs when attempting to add Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="87506-158">In alcuni casi si è osservato che la cache MEF (Managed Extensibility Framework) di Visual Studio può risultare danneggiata dopo la disinstallazione e l'installazione delle estensioni.</span><span class="sxs-lookup"><span data-stu-id="87506-158">After uninstalling and installing extensions, the Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="87506-159">In questo caso possono essere visualizzate diversi messaggi di errore quando si aggiunge il supporto per Docker e/o si prova a eseguire l'applicazione ASP.NET Core o il relativo debug (F5).</span><span class="sxs-lookup"><span data-stu-id="87506-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting to run or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="87506-160">Come soluzione temporanea, eseguire questa procedura per eliminare e rigenerare la cache MEF.</span><span class="sxs-lookup"><span data-stu-id="87506-160">As a temporary workaround, use the following steps to delete and regenerate the MEF cache.</span></span>

1. <span data-ttu-id="87506-161">Chiudere tutte le istanze di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87506-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="87506-162">Aprire %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="87506-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="87506-163">Eliminare le cartelle seguenti:</span><span class="sxs-lookup"><span data-stu-id="87506-163">Delete the following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="87506-164">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87506-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="87506-165">Provare a eseguire di nuovo lo scenario.</span><span class="sxs-lookup"><span data-stu-id="87506-165">Attempt the scenario again.</span></span>
