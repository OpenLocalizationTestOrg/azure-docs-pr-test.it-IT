---
title: 'Connettere Intel Edison (Node) ad Azure IoT: lezione 4: Risoluzione dei problemi | Documentazione Microsoft'
description: Pagina sulla risoluzione dei problemi per Node.js in Intel Edison
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: risoluzione dei problemi in arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="10b56-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="10b56-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="10b56-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="10b56-105">Hardware issues</span></span>
<span data-ttu-id="10b56-106">Per informazioni sulla risoluzione dei problemi più comuni di Intel Edison, vedere la [pagina ufficiale sulla risoluzione dei problemi](https://software.intel.com/en-us/node/637974) relativa.</span><span class="sxs-lookup"><span data-stu-id="10b56-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="10b56-107">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="10b56-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="10b56-108">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="10b56-108">No response during gulp tasks</span></span>
<span data-ttu-id="10b56-109">Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere l'opzione `--verbose` per il debug.</span><span class="sxs-lookup"><span data-stu-id="10b56-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="10b56-110">Provare a terminare le attività gulp correnti con `Ctrl + C` e quindi eseguire questo comando nella finestra della console per visualizzare i messaggi di debug.</span><span class="sxs-lookup"><span data-stu-id="10b56-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="10b56-111">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="10b56-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="10b56-112">Problemi di NPM</span><span class="sxs-lookup"><span data-stu-id="10b56-112">NPM issues</span></span>
<span data-ttu-id="10b56-113">Provare ad aggiornare il pacchetto NPM con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="10b56-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="10b56-114">Se il problema persiste, aggiungere commenti alla fine di questo articolo o definire un problema di GitHub nel [repository degli esempi][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="10b56-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="10b56-115">Debug remoto</span><span class="sxs-lookup"><span data-stu-id="10b56-115">Remote debugging</span></span>

### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="10b56-116">Eseguire l'applicazione di esempio in modalità di debug</span><span class="sxs-lookup"><span data-stu-id="10b56-116">Run the sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="10b56-117">Quando il motore di debug è pronto, è possibile visualizzare ```Debugger listening on port 5858``` nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="10b56-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span></span>

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a><span data-ttu-id="10b56-118">Configurare Visual Studio Code per la connessione al dispositivo remoto</span><span class="sxs-lookup"><span data-stu-id="10b56-118">Configure VS Code to connect to the remote device</span></span>

<span data-ttu-id="10b56-119">Aprire il pannello **Debug** sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="10b56-119">Open the **Debug** panel from the left side.</span></span>

<span data-ttu-id="10b56-120">Fare clic sul pulsante verde **Avvia debug** (F5).</span><span class="sxs-lookup"><span data-stu-id="10b56-120">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="10b56-121">In Visual Studio Code viene aperto un file **launch.json** che è necessario aggiornare.</span><span class="sxs-lookup"><span data-stu-id="10b56-121">VS Code would open a **launch.json** file, which you need to update.</span></span>

<span data-ttu-id="10b56-122">Aggiornare il file **launch.json** con il contenuto seguente e sostituire `[device hostname or IP address]` con l'indirizzo IP o il nome host del dispositivo effettivo.</span><span class="sxs-lookup"><span data-stu-id="10b56-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span></span>  

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

![Configurazione del debug remoto](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="10b56-124">Collegarsi all'applicazione remota</span><span class="sxs-lookup"><span data-stu-id="10b56-124">Attach to the remote application</span></span>

<span data-ttu-id="10b56-125">Fare clic sul pulsante verde **Avvia debug** (F5) per avviare il debug.</span><span class="sxs-lookup"><span data-stu-id="10b56-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="10b56-126">Leggere [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) per altre informazioni sul debugger.</span><span class="sxs-lookup"><span data-stu-id="10b56-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Debug remoto interattivo](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="10b56-128">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="10b56-128">Azure-CLI issues</span></span>
<span data-ttu-id="10b56-129">L'interfaccia della riga di comando di Azure è una versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="10b56-129">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="10b56-130">Per cercare le soluzioni ai problemi, vedere la [guida all'installazione della versione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="10b56-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="10b56-131">Quando i comandi non funzionano come previsto, provare ad aggiornare l'interfaccia della riga di comando di Azure alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="10b56-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="10b56-132">Se si rilevano bug con lo strumento, segnalare un [problema](https://github.com/Azure/azure-cli/issues) nella sezione **Issues** (Problemi) del repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="10b56-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="10b56-133">Per risolvere più facilmente i problemi comuni, controllare il file [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="10b56-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="10b56-134">Se viene visualizzato un messaggio simile a "Impossibile trovare una versione che soddisfi il requisito", eseguire questo comando per aggiornare pip all'ultima versione.</span><span class="sxs-lookup"><span data-stu-id="10b56-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="10b56-135">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="10b56-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="10b56-136">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="10b56-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="10b56-137">Durante l'installazione di **pip**, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="10b56-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="10b56-138">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="10b56-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="10b56-139">Alcuni pacchetti **pip** di un'installazione precedente sono stati creati dall'utente root e questo causa l'errore di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="10b56-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="10b56-140">La soluzione consiste nel rimuovere i pacchetti installati dall'utente root.</span><span class="sxs-lookup"><span data-stu-id="10b56-140">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="10b56-141">Per completare questa attività, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="10b56-141">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="10b56-142">Passare a /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="10b56-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="10b56-143">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="10b56-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="10b56-144">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="10b56-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="10b56-145">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="10b56-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="10b56-146">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="10b56-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="10b56-147">Se è stato completato il provisioning dell'hub IoT di Azure con `azure-cli` ed è necessario uno strumento per gestire i dispositivi che si connettono all'hub IoT, provare gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="10b56-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="10b56-148">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="10b56-148">Device Explorer</span></span>
<span data-ttu-id="10b56-149">[Esplora dispositivi](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette all'hub IoT in Azure.</span><span class="sxs-lookup"><span data-stu-id="10b56-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="10b56-150">Comunica con i seguenti [endpoint dell'hub IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="10b56-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="10b56-151">_Gestione delle identità dispositivo_ per il provisioning e la gestione dei dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="10b56-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="10b56-152">_Ricezione da dispositivo a cloud_ per il monitoraggio dei messaggi inviati dal dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="10b56-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="10b56-153">_Invio da cloud a dispositivo_ per l'invio dei messaggi dall'hub IoT ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="10b56-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="10b56-154">Configurare il valore di `IoT hub connection string` all'interno di questo strumento per usarne tutte le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="10b56-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="10b56-155">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="10b56-155">IoT hub Explorer</span></span>
<span data-ttu-id="10b56-156">[IoT Hub Explorer](https://github.com/Azure/iothub-explorer) è uno strumento di esempio dell'interfaccia della riga di comando multipiattaforma per gestire i dispositivi client.</span><span class="sxs-lookup"><span data-stu-id="10b56-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="10b56-157">È possibile usare questo strumento per gestire i dispositivi nel registro di identità, monitorare i messaggi da dispositivo a cloud e inviare comandi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="10b56-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="10b56-158">Per installare la versione più recente, non definitiva, dello strumento iothub-explorer, eseguire questo comando nell'ambiente della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="10b56-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="10b56-159">Per ottenere altre informazioni su tutti i comandi di iothub explorer e sui relativi parametri, è possibile usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="10b56-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="10b56-160">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="10b56-160">Azure portal</span></span>
<span data-ttu-id="10b56-161">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="10b56-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="10b56-162">Può anche essere utile usare il [portale di Azure](../azure-portal-overview.md) per il provisioning, la gestione e il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="10b56-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="10b56-163">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="10b56-163">Azure storage issues</span></span>
<span data-ttu-id="10b56-164">[Microsoft Azure Storage Explorer (anteprima)](http://storageexplorer.com) è un'app autonoma di Microsoft che permette di usare i dati di [Archiviazione di Azure](https://azure.microsoft.com/en-us/services/storage/) in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="10b56-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="10b56-165">Questo strumento permette di connettersi alla tabella e visualizzarne i dati.</span><span class="sxs-lookup"><span data-stu-id="10b56-165">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="10b56-166">È possibile usare questo strumento per risolvere i problemi di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="10b56-166">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10b56-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10b56-167">Next steps</span></span>
<span data-ttu-id="10b56-168">Questa pagina include solo i problemi più comuni del kit per Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="10b56-168">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="10b56-169">Per segnalare altri problemi da risolvere, è possibile lasciare commenti nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="10b56-169">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="10b56-170">Tornare a [Introduzione a Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="10b56-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started