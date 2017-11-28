---
title: 'Dispositivo simulato e gateway Azure IoT: risoluzione dei problemi | Documentazione Microsoft'
description: Pagina sulla risoluzione dei problemi del gateway Intel NUC
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Problemi di IoT, Internet delle cose
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="67dcb-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="67dcb-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="67dcb-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="67dcb-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="67dcb-106">Impossibile connettere SensorTag di Texas Instruments</span><span class="sxs-lookup"><span data-stu-id="67dcb-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="67dcb-107">problemi di connettività SensorTag tootroubleshoot, utilizzare hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="67dcb-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="67dcb-108">Problema relativo a Intel NUC</span><span class="sxs-lookup"><span data-stu-id="67dcb-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="67dcb-109">problemi di avvio tootroubleshoot, fare riferimento troppo[risolvere i problemi di avvio non Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="67dcb-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="67dcb-110">problemi del sistema operativo tootroubleshoot, fare riferimento troppo[risolvere i problemi del sistema operativo di Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="67dcb-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="67dcb-111">tootroubleshoot altri problemi, fare riferimento troppo[Blink codici e un segnale acustico per Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="67dcb-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="67dcb-112">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="67dcb-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="67dcb-113">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="67dcb-113">No response during gulp tasks</span></span>

<span data-ttu-id="67dcb-114">Se si verificano problemi nell'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug.</span><span class="sxs-lookup"><span data-stu-id="67dcb-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="67dcb-115">Provare a eseguire attività gulp corrente tooterminate utilizzando `Ctrl + C`, e quindi eseguire hello seguendo comando all'interno dei messaggi di debug toosee finestra console.</span><span class="sxs-lookup"><span data-stu-id="67dcb-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="67dcb-116">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="67dcb-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="67dcb-117">Problemi di individuazione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="67dcb-117">Device discovery issues</span></span>

<span data-ttu-id="67dcb-118">Per semplificare la risoluzione dei problemi comuni con hello `discover-sensortag` comando, controllare hello [pagina wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="67dcb-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="67dcb-119">Problemi di npm</span><span class="sxs-lookup"><span data-stu-id="67dcb-119">npm issues</span></span>

<span data-ttu-id="67dcb-120">Provare tooupdate del pacchetto npm eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="67dcb-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="67dcb-121">Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository esempio](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="67dcb-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="67dcb-122">Debug remoto</span><span class="sxs-lookup"><span data-stu-id="67dcb-122">Remote Debugging</span></span>
> <span data-ttu-id="67dcb-123">Le istruzioni riportate di seguito consentono di eseguire il debug degli script node.js usati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="67dcb-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="67dcb-124">Eseguire l'applicazione di esempio hello in modalità debug</span><span class="sxs-lookup"><span data-stu-id="67dcb-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="67dcb-125">Eseguire l'applicazione di esempio hello in modalità di debug eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="67dcb-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="67dcb-126">Quando il motore di debug di hello è pronto, è necessario vedere `Debugger listening on port 5858` nell'output di console hello.</span><span class="sxs-lookup"><span data-stu-id="67dcb-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="67dcb-127">Configurare il dispositivo remoto di Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="67dcb-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="67dcb-128">Aprire hello **Debug** pannello sul lato sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="67dcb-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="67dcb-129">Fare clic su hello verde **Avvia debug** pulsante (F5).</span><span class="sxs-lookup"><span data-stu-id="67dcb-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="67dcb-130">In Visual Studio Code viene aperto un file `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="67dcb-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="67dcb-131">Hello aggiornamento `launch.json` file con hello dopo contenuto.</span><span class="sxs-lookup"><span data-stu-id="67dcb-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="67dcb-132">Sostituire `[device hostname or IP address]` con hello dispositivo effettivo IP indirizzo o il nome host.</span><span class="sxs-lookup"><span data-stu-id="67dcb-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

   ``` json
   {
     "version": "0.2.0",
     "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configurazione del debug remoto](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="67dcb-134">Collegare l'applicazione remota toohello</span><span class="sxs-lookup"><span data-stu-id="67dcb-134">Attach toohello remote application</span></span>

<span data-ttu-id="67dcb-135">Fare clic su hello verde **Avvia debug** (F5) pulsante toostart debug.</span><span class="sxs-lookup"><span data-stu-id="67dcb-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="67dcb-136">Lettura [JavaScript in Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn ulteriori informazioni sul debugger hello.</span><span class="sxs-lookup"><span data-stu-id="67dcb-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Debug dell'esempio BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="67dcb-138">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="67dcb-138">Azure CLI issues</span></span>

<span data-ttu-id="67dcb-139">Hello Azure interfaccia della riga di comando (CLI di Azure) è una build di anteprima.</span><span class="sxs-lookup"><span data-stu-id="67dcb-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="67dcb-140">soluzioni tooseek, è possibile utilizzare hello [Guida all'installazione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="67dcb-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="67dcb-141">Se si verificano i bug con lo strumento di hello, file un [problema](https://github.com/Azure/azure-cli/issues) in hello **problemi** sezione del repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="67dcb-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="67dcb-142">Per semplificare la risoluzione dei problemi, controllare hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="67dcb-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="67dcb-143">Se vengono soddisfatti, "Impossibile trovare una versione che soddisfa il requisito di hello", versione toolastest di pip tooupgrade comando che segue hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="67dcb-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="67dcb-144">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="67dcb-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="67dcb-145">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="67dcb-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="67dcb-146">Durante l'installazione di pip, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="67dcb-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="67dcb-147">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="67dcb-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="67dcb-148">Alcuni pacchetti pip da un'installazione precedente sono stati creati da radice, causando l'errore di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="67dcb-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="67dcb-149">soluzione hello è tooremove tali pacchetti installati dalla radice.</span><span class="sxs-lookup"><span data-stu-id="67dcb-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="67dcb-150">Usare questa attività di hello toocomplete i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="67dcb-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="67dcb-151">Andare troppo`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="67dcb-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="67dcb-152">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="67dcb-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="67dcb-153">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="67dcb-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="67dcb-154">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="67dcb-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="67dcb-155">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="67dcb-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="67dcb-156">Se è stato eseguito correttamente il provisioning dell'hub IoT di Azure con hello CLI di Azure ed è necessario un strumento toomanage hello i dispositivi che si connettono tooyour IoT hub, provare a hello gli strumenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="67dcb-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="67dcb-157">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="67dcb-157">Device Explorer</span></span>

<span data-ttu-id="67dcb-158">[Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure.</span><span class="sxs-lookup"><span data-stu-id="67dcb-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="67dcb-159">Comunica con i seguenti hello [gli endpoint IoT Hub](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="67dcb-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="67dcb-160">Tooprovision di gestione di identità dispositivo e gestire i dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="67dcb-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="67dcb-161">È possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo di ricezione da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="67dcb-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="67dcb-162">Inviata da cloud a dispositivo in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="67dcb-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="67dcb-163">Configurare la stringa di connessione hub IoT all'interno di questo strumento di toouse tutte le relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="67dcb-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="67dcb-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="67dcb-164">iothub-explorer</span></span>

<span data-ttu-id="67dcb-165">[l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage client dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="67dcb-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="67dcb-166">Si può utilizzare hello strumento toomanage hello dispositivi nel Registro di identità hello, il monitoraggio dei messaggi da dispositivo a cloud e inviare comandi cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="67dcb-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="67dcb-167">tooinstall hello più recente (versione non definitiva) dello strumento di hub IOT-explorer hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="67dcb-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="67dcb-168">tooget ulteriori informazioni su tutti hello hub IOT Esplora comandi e i relativi parametri, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="67dcb-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="67dcb-169">Hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="67dcb-169">hello Azure portal</span></span>

<span data-ttu-id="67dcb-170">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="67dcb-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="67dcb-171">È inoltre possibile hello toouse [portale di Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provisioning, gestire ed eseguire il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="67dcb-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="67dcb-172">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="67dcb-172">Azure Storage issues</span></span>

<span data-ttu-id="67dcb-173">[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com/) è un'applicazione autonoma da Microsoft che è possibile utilizzare toowork con dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="67dcb-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="67dcb-174">Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="67dcb-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="67dcb-175">È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="67dcb-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
