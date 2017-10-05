---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: risolvere i problemi | Documentazione Microsoft'
description: Pagina sulla risoluzione dei problemi relativi all'esperienza Node.js del dispositivo Raspberry Pi
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
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="eb6f6-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="eb6f6-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="eb6f6-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="eb6f6-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="eb6f6-106">L'applicazione viene eseguita correttamente, ma il LED non lampeggia</span><span class="sxs-lookup"><span data-stu-id="eb6f6-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="eb6f6-107">Questo problema è sempre correlato alla connettività del circuito hardware.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="eb6f6-108">Per identificare i problemi, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eb6f6-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="eb6f6-109">Assicurarsi di aver scelto il connettore **GPIO** corretto sulla scheda.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="eb6f6-110">Le due porte devono essere **GPIO GND (Pin 6)** e **GPIO 04 (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="eb6f6-111">Assicurarsi che la polarità del LED sia corretta.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="eb6f6-112">La parte più lunga deve indicare il pin anodo, **positivo**.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="eb6f6-113">Usare il **pin da 3,3 V** e il **pin GND** nel dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="eb6f6-114">Trattare il dispositivo Pi come alimentazione CC.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="eb6f6-115">Assicurarsi che il LED funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-115">Check that the LED works fine.</span></span>

![Specifiche del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="eb6f6-117">Altri problemi hardware</span><span class="sxs-lookup"><span data-stu-id="eb6f6-117">Other hardware issues</span></span>
<span data-ttu-id="eb6f6-118">Per informazioni sulla risoluzione dei problemi più comuni del dispositivo Raspberry Pi 3, vedere la relativa [pagina ufficiale sulla risoluzione dei problemi](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="eb6f6-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="eb6f6-119">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="eb6f6-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="eb6f6-120">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="eb6f6-120">No response during gulp tasks</span></span>
<span data-ttu-id="eb6f6-121">Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere l'opzione `--verbose` per il debug.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="eb6f6-122">Provare a terminare le attività gulp correnti con CTRL + C e quindi eseguire questo comando nella finestra della console per visualizzare i messaggi di debug.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="eb6f6-123">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="eb6f6-124">Problemi di individuazione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="eb6f6-124">Device discovery issues</span></span>
<span data-ttu-id="eb6f6-125">Per risolvere più facilmente i problemi comuni relativi al comando `devdisco`, vedere il file [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="eb6f6-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="eb6f6-126">Problemi di npm</span><span class="sxs-lookup"><span data-stu-id="eb6f6-126">npm issues</span></span>
<span data-ttu-id="eb6f6-127">Provare ad aggiornare il pacchetto npm usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eb6f6-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="eb6f6-128">Se il problema persiste, aggiungere commenti alla fine di questo articolo o definire un problema di GitHub nel [repository degli esempi](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="eb6f6-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="eb6f6-129">Debug remoto</span><span class="sxs-lookup"><span data-stu-id="eb6f6-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="eb6f6-130">Eseguire l'applicazione di esempio in modalità di debug</span><span class="sxs-lookup"><span data-stu-id="eb6f6-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="eb6f6-131">Quando il motore di debug è pronto, nell'output della console dovrebbe essere visibile ```Debugger listening on port 5858```.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="eb6f6-132">Configurare Visual Studio Code per la connessione al dispositivo remoto</span><span class="sxs-lookup"><span data-stu-id="eb6f6-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="eb6f6-133">Aprire il pannello **Debug** sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="eb6f6-134">Fare clic sul pulsante verde **Avvia debug** (F5).</span><span class="sxs-lookup"><span data-stu-id="eb6f6-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="eb6f6-135">Visual Studio Code apre un file launch.json.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="eb6f6-136">Aggiornare il file launch.json con il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="eb6f6-137">Sostituire `[device hostname or IP address]` con il nome host o l'indirizzo IP effettivo del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="eb6f6-138">Per altre informazioni sul debug in Visual Studio, vedere la sezione relativa al [debug dell'articolo su Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="eb6f6-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="eb6f6-140">Collegarsi all'applicazione remota</span><span class="sxs-lookup"><span data-stu-id="eb6f6-140">Attach to the remote application</span></span>
<span data-ttu-id="eb6f6-141">Fare clic sul pulsante verde **Avvia debug** (F5) per avviare il debug.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="eb6f6-142">Leggere [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) per altre informazioni sul debugger.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Debug remoto interattivo](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="eb6f6-144">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="eb6f6-144">Azure CLI issues</span></span>
<span data-ttu-id="eb6f6-145">L'interfaccia della riga di comando di Azure è una versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="eb6f6-146">Per cercare le soluzioni ai problemi, vedere la [guida all'installazione della versione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="eb6f6-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="eb6f6-147">Se si rilevano bug con lo strumento, segnalare un [problema](https://github.com/Azure/azure-cli/issues) nella sezione **Issues** (Problemi) del repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="eb6f6-148">Per risolvere più facilmente i problemi comuni, vedere il file [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="eb6f6-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="eb6f6-149">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="eb6f6-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="eb6f6-150">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="eb6f6-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="eb6f6-151">Durante l'installazione di pip, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="eb6f6-152">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="eb6f6-153">Alcuni pacchetti pip di un'installazione precedente sono stati creati dall'utente root e questo causa l'errore di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="eb6f6-154">La soluzione consiste nel rimuovere i pacchetti installati dall'utente root.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="eb6f6-155">Per completare questa attività, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="eb6f6-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="eb6f6-156">Passare a /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="eb6f6-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="eb6f6-157">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="eb6f6-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="eb6f6-158">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="eb6f6-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="eb6f6-159">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="eb6f6-160">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="eb6f6-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="eb6f6-161">Se è stato effettuato il provisioning dell'hub IoT di Azure con l'interfaccia della riga di comando di Azure ed è necessario uno strumento per gestire i dispositivi connessi all'hub IoT, provare gli strumenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="eb6f6-162">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="eb6f6-162">Device explorer</span></span>
<span data-ttu-id="eb6f6-163">Lo strumento [Esplora dispositivi](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) viene eseguito nel computer locale di Windows e si connette all'hub IoT in Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="eb6f6-164">Comunica con i seguenti [endpoint dell'hub IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="eb6f6-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="eb6f6-165">*Gestione delle identità dispositivo* per il provisioning e la gestione dei dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="eb6f6-166">*Ricezione da dispositivo a cloud* per il monitoraggio dei messaggi inviati dal dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="eb6f6-167">*Invio da cloud a dispositivo* per l'invio dei messaggi dall'hub IoT ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="eb6f6-168">Configurare la stringa di connessione dell'hub IoT in questo strumento per usarne tutte le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="eb6f6-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="eb6f6-169">iothub-explorer</span></span>
<span data-ttu-id="eb6f6-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) è uno strumento di esempio dell'interfaccia della riga di comando multipiattaforma che consente di gestire i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="eb6f6-171">È possibile usare questo strumento per gestire i dispositivi nel registro delle identità, monitorare i messaggi da dispositivo a cloud e inviare messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="eb6f6-172">Per installare la versione più recente, non definitiva, dello strumento iothub-explorer, eseguire questo comando nell'ambiente della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="eb6f6-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="eb6f6-173">Per ottenere altre informazioni su tutti i comandi di iothub explorer e sui relativi parametri, è possibile usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eb6f6-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="eb6f6-174">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eb6f6-174">Azure portal</span></span>
<span data-ttu-id="eb6f6-175">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="eb6f6-176">Può anche essere utile usare il [portale di Azure](../azure-portal-overview.md) per il provisioning, la gestione e il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="eb6f6-177">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="eb6f6-177">Azure Storage issues</span></span>
<span data-ttu-id="eb6f6-178">[Microsoft Azure Storage Explorer (anteprima)](http://storageexplorer.com) è un'app autonoma di Microsoft che consente di utilizzare i dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="eb6f6-179">Questo strumento permette di connettersi alla tabella e visualizzarne i dati.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="eb6f6-180">È possibile usare questo strumento per risolvere i problemi di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6f6-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

