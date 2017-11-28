---
title: 'Dispositivo SensorTag e gateway Azure IoT: risoluzione dei problemi | Documentazione Microsoft'
description: Pagina sulla risoluzione dei problemi del gateway Intel NUC
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Problemi di IoT, Internet delle cose
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7e80951de55ade6b5140608dcff8ebb064f942ca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="2fc46-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="2fc46-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="2fc46-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="2fc46-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="2fc46-106">Impossibile connettere SensorTag di Texas Instruments</span><span class="sxs-lookup"><span data-stu-id="2fc46-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="2fc46-107">Per risolvere i problemi di connettività di SensorTag, usare l'[app SensorTag](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="2fc46-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="2fc46-108">Problema relativo a Intel NUC</span><span class="sxs-lookup"><span data-stu-id="2fc46-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="2fc46-109">Per risolvere i problemi di avvio, vedere l'articolo relativo alla [risoluzione dei problemi di mancato avvio su Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="2fc46-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="2fc46-110">Per risolvere i problemi del sistema operativo, vedere l'articolo relativo alla [risoluzione dei problemi del sistema operativo su Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="2fc46-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="2fc46-111">Per risolvere altri problemi, vedere l'articolo relativo ai [codici dei lampeggiamenti e dei segnali acustici per Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="2fc46-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="2fc46-112">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="2fc46-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="2fc46-113">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="2fc46-113">No response during gulp tasks</span></span>

<span data-ttu-id="2fc46-114">Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere l'opzione `--verbose` per il debug.</span><span class="sxs-lookup"><span data-stu-id="2fc46-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="2fc46-115">Provare a terminare le attività gulp correnti con `Ctrl + C` e quindi eseguire questo comando nella finestra della console per visualizzare i messaggi di debug.</span><span class="sxs-lookup"><span data-stu-id="2fc46-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="2fc46-116">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="2fc46-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="2fc46-117">Problemi di individuazione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="2fc46-117">Device discovery issues</span></span>

<span data-ttu-id="2fc46-118">Per supporto nella risoluzione dei problemi comuni relativi al comando `discover-sensortag`, vedere la [pagina wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="2fc46-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="2fc46-119">Problemi di npm</span><span class="sxs-lookup"><span data-stu-id="2fc46-119">npm issues</span></span>

<span data-ttu-id="2fc46-120">Provare ad aggiornare il pacchetto npm eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="2fc46-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="2fc46-121">Se il problema persiste, aggiungere commenti alla fine di questo articolo o definire un problema di GitHub nel [repository degli esempi](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="2fc46-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="2fc46-122">Debug remoto</span><span class="sxs-lookup"><span data-stu-id="2fc46-122">Remote Debugging</span></span>
> <span data-ttu-id="2fc46-123">Le istruzioni riportate di seguito consentono di eseguire il debug degli script node.js usati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2fc46-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="2fc46-124">Eseguire l'applicazione di esempio in modalità di debug</span><span class="sxs-lookup"><span data-stu-id="2fc46-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="2fc46-125">Eseguire l'applicazione di esempio in modalità di debug tramite questo comando:</span><span class="sxs-lookup"><span data-stu-id="2fc46-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="2fc46-126">Quando il motore di debug è pronto, nell'output della console dovrebbe essere visibile `Debugger listening on port 5858`.</span><span class="sxs-lookup"><span data-stu-id="2fc46-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="2fc46-127">Configurare Visual Studio Code per la connessione al dispositivo remoto</span><span class="sxs-lookup"><span data-stu-id="2fc46-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="2fc46-128">Aprire il pannello **Debug** sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="2fc46-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="2fc46-129">Fare clic sul pulsante verde **Avvia debug** (F5).</span><span class="sxs-lookup"><span data-stu-id="2fc46-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="2fc46-130">In Visual Studio Code viene aperto un file `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="2fc46-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="2fc46-131">Aggiornare il file `launch.json` con il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="2fc46-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="2fc46-132">Sostituire `[device hostname or IP address]` con il nome host o l'indirizzo IP effettivo del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2fc46-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="2fc46-134">Collegarsi all'applicazione remota</span><span class="sxs-lookup"><span data-stu-id="2fc46-134">Attach to the remote application</span></span>

<span data-ttu-id="2fc46-135">Fare clic sul pulsante verde **Avvia debug** (F5) per avviare il debug.</span><span class="sxs-lookup"><span data-stu-id="2fc46-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="2fc46-136">Leggere [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) per altre informazioni sul debugger.</span><span class="sxs-lookup"><span data-stu-id="2fc46-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Debug dell'esempio BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="2fc46-138">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2fc46-138">Azure CLI issues</span></span>

<span data-ttu-id="2fc46-139">L'interfaccia della riga di comando di Azure è una versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="2fc46-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="2fc46-140">Per cercare le soluzioni ai problemi, vedere la [guida all'installazione della versione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="2fc46-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="2fc46-141">Se si rilevano bug con lo strumento, segnalare un [problema](https://github.com/Azure/azure-cli/issues) nella sezione **Issues** (Problemi) del repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="2fc46-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="2fc46-142">Per risolvere più facilmente i problemi comuni, vedere il file [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="2fc46-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="2fc46-143">Se viene visualizzato un messaggio simile a "Impossibile trovare una versione che soddisfi il requisito", eseguire questo comando per aggiornare pip all'ultima versione.</span><span class="sxs-lookup"><span data-stu-id="2fc46-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="2fc46-144">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="2fc46-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="2fc46-145">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="2fc46-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="2fc46-146">Durante l'installazione di pip, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="2fc46-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="2fc46-147">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="2fc46-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="2fc46-148">Alcuni pacchetti pip di un'installazione precedente sono stati creati dall'utente root e questo causa l'errore di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="2fc46-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="2fc46-149">La soluzione consiste nel rimuovere i pacchetti installati dall'utente root.</span><span class="sxs-lookup"><span data-stu-id="2fc46-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="2fc46-150">Per completare questa attività, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2fc46-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="2fc46-151">Passare a `/usr/local/lib/python2.7/site-packages`.</span><span class="sxs-lookup"><span data-stu-id="2fc46-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="2fc46-152">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="2fc46-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="2fc46-153">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="2fc46-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="2fc46-154">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="2fc46-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="2fc46-155">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="2fc46-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="2fc46-156">Se è stato completato il provisioning dell'hub IoT di Azure con l'interfaccia della riga di comando di Azure ed è necessario uno strumento per gestire i dispositivi che si connettono all'hub IoT, provare gli strumenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="2fc46-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="2fc46-157">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="2fc46-157">Device Explorer</span></span>

<span data-ttu-id="2fc46-158">[Esplora dispositivi](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette all'hub IoT in Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc46-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="2fc46-159">Comunica con i seguenti [endpoint dell'hub IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="2fc46-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="2fc46-160">Gestione delle identità dei dispositivi per il provisioning e la gestione dei dispositivi registrati nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2fc46-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="2fc46-161">Ricezione da dispositivo a cloud per il monitoraggio dei messaggi inviati dal dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2fc46-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="2fc46-162">Invio da cloud a dispositivo per l'invio dei messaggi dall'hub IoT ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2fc46-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="2fc46-163">Configurare la stringa di connessione dell'hub IoT in questo strumento per usarne tutte le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2fc46-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="2fc46-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="2fc46-164">iothub-explorer</span></span>

<span data-ttu-id="2fc46-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) è uno strumento di esempio dell'interfaccia della riga di comando multipiattaforma che permette di gestire i dispositivi client.</span><span class="sxs-lookup"><span data-stu-id="2fc46-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="2fc46-166">È possibile usare questo strumento per gestire i dispositivi nel registro di identità, monitorare i messaggi da dispositivo a cloud e inviare comandi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2fc46-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="2fc46-167">Per installare l'ultima versione, provvisoria, dello strumento iothub-explorer, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="2fc46-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="2fc46-168">Per ottenere altre informazioni su tutti i comandi di iothub explorer e sui relativi parametri, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="2fc46-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="2fc46-169">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2fc46-169">The Azure portal</span></span>

<span data-ttu-id="2fc46-170">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc46-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="2fc46-171">Può anche essere utile usare il [portale di Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) per il provisioning, la gestione e il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc46-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="2fc46-172">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2fc46-172">Azure Storage issues</span></span>

<span data-ttu-id="2fc46-173">[Microsoft Azure Storage Explorer (anteprima)](http://storageexplorer.com/) è un'app autonoma di Microsoft che consente di utilizzare i dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="2fc46-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="2fc46-174">Questo strumento permette di connettersi alla tabella e visualizzarne i dati.</span><span class="sxs-lookup"><span data-stu-id="2fc46-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="2fc46-175">È possibile usare questo strumento per risolvere i problemi di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc46-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
