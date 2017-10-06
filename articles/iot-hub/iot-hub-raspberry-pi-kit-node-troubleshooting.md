---
title: Connect Raspberry PI (C) tooAzure IoT - risoluzione dei problemi | Documenti Microsoft
description: Risoluzione dei problemi di pagina per un'esperienza hello Raspberry Pi Node.js
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Problemi di IoT, Internet delle cose
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="9ca0e-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9ca0e-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="9ca0e-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="9ca0e-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="9ca0e-106">un'applicazione Hello viene eseguita correttamente, ma hello LED è lampeggiante non</span><span class="sxs-lookup"><span data-stu-id="9ca0e-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="9ca0e-107">Questo problema è sempre connettività circuito toohardware correlati.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="9ca0e-108">Utilizzare hello problemi tooidentify i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ca0e-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="9ca0e-109">Verificare che si è scelto di hello corretto **GPIO** sulla Lavagna.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="9ca0e-110">le porte Hello due **GPIO GND (6 Pin)** e **04 GPIO (7 Pin)**.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="9ca0e-111">Verificare che la polarità hello del LED sia corretta.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="9ca0e-112">parte di più Hello deve indicare hello **positivo**, pin anode.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="9ca0e-113">Hello utilizzare **aggiungere 3,3 v** e **GND Pin** Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="9ca0e-114">Considera Pi hello power controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="9ca0e-115">Verificare che hello LED funziona correttamente.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-115">Check that hello LED works fine.</span></span>

![Specifiche del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="9ca0e-117">Altri problemi hardware</span><span class="sxs-lookup"><span data-stu-id="9ca0e-117">Other hardware issues</span></span>
<span data-ttu-id="9ca0e-118">Per informazioni sulla risoluzione dei problemi comuni in Raspberry Pi 3, vedere hello [pagina sulla risoluzione dei problemi ufficiale](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="9ca0e-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="9ca0e-119">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="9ca0e-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="9ca0e-120">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="9ca0e-120">No response during gulp tasks</span></span>
<span data-ttu-id="9ca0e-121">Se si verificano problemi nell'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="9ca0e-122">Provare a eseguire attività gulp corrente tooterminate utilizzando Ctrl + C e quindi eseguire hello comando all'interno dei messaggi di debug toosee finestra console seguente.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="9ca0e-123">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="9ca0e-124">Problemi di individuazione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="9ca0e-124">Device discovery issues</span></span>
<span data-ttu-id="9ca0e-125">Per semplificare la risoluzione dei problemi comuni con hello `devdisco` comando, controllare hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="9ca0e-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="9ca0e-126">Problemi di npm</span><span class="sxs-lookup"><span data-stu-id="9ca0e-126">npm issues</span></span>
<span data-ttu-id="9ca0e-127">Provare tooupdate del pacchetto npm utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9ca0e-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="9ca0e-128">Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository esempio](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9ca0e-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="9ca0e-129">Debug remoto</span><span class="sxs-lookup"><span data-stu-id="9ca0e-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="9ca0e-130">Eseguire l'applicazione di esempio hello in modalità debug</span><span class="sxs-lookup"><span data-stu-id="9ca0e-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="9ca0e-131">Quando il motore di debug di hello è pronto, è necessario vedere ```Debugger listening on port 5858``` nell'output di console hello.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="9ca0e-132">Configurare il dispositivo remoto di Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="9ca0e-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="9ca0e-133">Aprire hello **Debug** pannello sul lato sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="9ca0e-134">Fare clic su hello verde **Avvia debug** pulsante (F5).</span><span class="sxs-lookup"><span data-stu-id="9ca0e-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="9ca0e-135">Visual Studio Code apre un file launch.json.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="9ca0e-136">Aggiornare file Launch hello con hello dopo contenuto.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="9ca0e-137">Sostituire `[device hostname or IP address]` con hello dispositivo effettivo IP indirizzo o il nome host.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="9ca0e-138">toolearn ulteriori informazioni su hello il debug di Visual Studio, fare riferimento troppo[debug in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="9ca0e-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
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
            "remoteRoot": null
        }
    ]
}
```

![Configurazione del debug remoto](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="9ca0e-140">Collegare l'applicazione remota toohello</span><span class="sxs-lookup"><span data-stu-id="9ca0e-140">Attach toohello remote application</span></span>
<span data-ttu-id="9ca0e-141">Fare clic su hello verde **Avvia debug** (F5) pulsante toostart debug.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="9ca0e-142">Lettura [JavaScript in Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn ulteriori informazioni sul debugger hello.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Debug remoto interattivo](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="9ca0e-144">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="9ca0e-144">Azure CLI issues</span></span>
<span data-ttu-id="9ca0e-145">Hello Azure interfaccia della riga di comando (CLI di Azure) è una build di anteprima.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="9ca0e-146">soluzioni tooseek, è possibile utilizzare hello [Guida all'installazione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="9ca0e-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="9ca0e-147">Se si verificano i bug con lo strumento di hello, file un [problema](https://github.com/Azure/azure-cli/issues) in hello **problemi** sezione del repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="9ca0e-148">Per semplificare la risoluzione dei problemi, controllare hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="9ca0e-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="9ca0e-149">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="9ca0e-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="9ca0e-150">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="9ca0e-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="9ca0e-151">Durante l'installazione di pip, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="9ca0e-152">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="9ca0e-153">Alcuni pacchetti pip da un'installazione precedente sono stati creati da radice, causando l'errore di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="9ca0e-154">soluzione hello è tooremove tali pacchetti installati dalla radice.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="9ca0e-155">Usare questa attività di hello toocomplete i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ca0e-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="9ca0e-156">Passare a /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="9ca0e-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="9ca0e-157">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="9ca0e-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="9ca0e-158">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="9ca0e-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="9ca0e-159">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="9ca0e-160">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="9ca0e-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="9ca0e-161">Se è stato eseguito correttamente il provisioning dell'hub IoT di Azure con Azure CLI, ed è necessario un strumento toomanage hello i dispositivi che si connettono tooyour IoT hub, provare a hello gli strumenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="9ca0e-162">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="9ca0e-162">Device explorer</span></span>
<span data-ttu-id="9ca0e-163">Hello [Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) strumento viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="9ca0e-164">Comunica con i seguenti hello [gli endpoint IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="9ca0e-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="9ca0e-165">*Gestione delle identità dispositivo* tooprovision e gestire i dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="9ca0e-166">*Ricezione da dispositivo a cloud* è possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="9ca0e-167">*Inviare cloud a dispositivo* in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="9ca0e-168">Configurare la stringa di connessione hub IoT all'interno di questo strumento di toouse tutte le relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="9ca0e-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="9ca0e-169">iothub-explorer</span></span>
<span data-ttu-id="9ca0e-170">[l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage per i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="9ca0e-171">È possibile utilizzare hello strumento toomanage hello dispositivi nel Registro di sistema di hello identità, il monitoraggio dei messaggi da dispositivo a cloud e inviare messaggi di cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="9ca0e-172">tooinstall hello ultima versione (versione provvisoria) dello strumento di hub IOT Esplora di hello, eseguire hello comando nell'ambiente della riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9ca0e-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="9ca0e-173">È possibile utilizzare hello tooget ulteriori informazioni su tutti hello hub IOT Esplora comandi e i relativi parametri di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9ca0e-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="9ca0e-174">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9ca0e-174">Azure portal</span></span>
<span data-ttu-id="9ca0e-175">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="9ca0e-176">È inoltre possibile hello toouse [portale di Azure](../azure-portal-overview.md) toohelp provisioning, gestire ed eseguire il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="9ca0e-177">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9ca0e-177">Azure Storage issues</span></span>
<span data-ttu-id="9ca0e-178">[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com) è un'applicazione autonoma da Microsoft che è possibile utilizzare toowork con dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="9ca0e-179">Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="9ca0e-180">È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca0e-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

