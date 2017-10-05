---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: risolvere i problemi | Documentazione Microsoft'
description: Pagina sulla risoluzione dei problemi relativi all'esperienza Node.js del dispositivo Raspberry Pi
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Problemi di IoT, Internet delle cose
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 828669db23fa8d608029134fbe364033456d935a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="22082-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="22082-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="22082-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="22082-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="22082-106">L'applicazione viene eseguita correttamente, ma il LED non lampeggia</span><span class="sxs-lookup"><span data-stu-id="22082-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="22082-107">Questo problema è sempre correlato alla connettività del circuito hardware.</span><span class="sxs-lookup"><span data-stu-id="22082-107">This issue is always related to the hardware circuit connectivity.</span></span> <span data-ttu-id="22082-108">Seguire i passaggi seguenti per identificare i problemi.</span><span class="sxs-lookup"><span data-stu-id="22082-108">Use the following steps to identify problems.</span></span>

1. <span data-ttu-id="22082-109">Assicurarsi di aver scelto il connettore **GPIO** corretto sulla scheda.</span><span class="sxs-lookup"><span data-stu-id="22082-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="22082-110">Le due porte devono essere **GPIO GND (Pin 6)** e **GPIO 04 (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="22082-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="22082-111">Assicurarsi che la polarità del LED sia corretta.</span><span class="sxs-lookup"><span data-stu-id="22082-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="22082-112">La parte più lunga deve indicare il pin anodo, **positivo**.</span><span class="sxs-lookup"><span data-stu-id="22082-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="22082-113">Usare il **pin da 3,3 V** e il **pin GND** nel dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="22082-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="22082-114">Trattare il dispositivo Pi come alimentazione CC.</span><span class="sxs-lookup"><span data-stu-id="22082-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="22082-115">Assicurarsi che il LED funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="22082-115">Check that the LED works fine.</span></span>

![Specifiche del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="22082-117">Altri problemi hardware</span><span class="sxs-lookup"><span data-stu-id="22082-117">Other hardware issues</span></span>
<span data-ttu-id="22082-118">Per informazioni sulla risoluzione dei problemi più comuni del dispositivo Raspberry Pi 3, vedere la relativa [pagina ufficiale sulla risoluzione dei problemi](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="22082-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="22082-119">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="22082-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="22082-120">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="22082-120">No response during gulp tasks</span></span>
<span data-ttu-id="22082-121">Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere l'opzione `--verbose` per il debug.</span><span class="sxs-lookup"><span data-stu-id="22082-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="22082-122">Provare a terminare le attività gulp correnti con `Ctrl + C` e quindi eseguire questo comando nella finestra della console per visualizzare i messaggi di debug.</span><span class="sxs-lookup"><span data-stu-id="22082-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="22082-123">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="22082-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="22082-124">Problemi di individuazione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="22082-124">Device discovery issues</span></span>
<span data-ttu-id="22082-125">Per risolvere più facilmente i problemi comuni relativi al comando `devdisco`, vedere il file [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="22082-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="22082-126">Problemi di NPM</span><span class="sxs-lookup"><span data-stu-id="22082-126">NPM issues</span></span>
<span data-ttu-id="22082-127">Provare ad aggiornare il pacchetto NPM con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22082-127">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="22082-128">Se il problema persiste, aggiungere commenti alla fine di questo articolo o definire un problema di GitHub nel [repository degli esempi](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="22082-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="22082-129">Debug remoto</span><span class="sxs-lookup"><span data-stu-id="22082-129">Remote debugging</span></span>

<span data-ttu-id="22082-130">Il supporto remoto sarà disponibile presto in Visual Studio Code C/C++ Extension.</span><span class="sxs-lookup"><span data-stu-id="22082-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="22082-131">Nel frattempo è possibile usare GDB tramite il terminale SSH preferito:</span><span class="sxs-lookup"><span data-stu-id="22082-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="22082-132">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="22082-132">Azure-CLI issues</span></span>
<span data-ttu-id="22082-133">L'interfaccia della riga di comando di Azure è una versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="22082-133">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="22082-134">Per cercare le soluzioni ai problemi, vedere la [guida all'installazione della versione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="22082-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="22082-135">Quando i comandi non funzionano come previsto, provare ad aggiornare l'interfaccia della riga di comando di Azure alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="22082-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="22082-136">Se si rilevano bug con lo strumento, segnalare un [problema](https://github.com/Azure/azure-cli/issues) nella sezione **Issues** (Problemi) del repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="22082-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="22082-137">Per risolvere più facilmente i problemi comuni, controllare il file [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="22082-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="22082-138">Se viene visualizzato un messaggio simile a "Impossibile trovare una versione che soddisfi il requisito", eseguire questo comando per aggiornare pip all'ultima versione.</span><span class="sxs-lookup"><span data-stu-id="22082-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="22082-139">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="22082-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="22082-140">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="22082-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="22082-141">Durante l'installazione di **pip**, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="22082-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="22082-142">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="22082-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="22082-143">Alcuni pacchetti **pip** di un'installazione precedente sono stati creati dall'utente root e questo causa l'errore di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="22082-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="22082-144">La soluzione consiste nel rimuovere i pacchetti installati dall'utente root.</span><span class="sxs-lookup"><span data-stu-id="22082-144">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="22082-145">Per completare questa attività, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="22082-145">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="22082-146">Passare a /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="22082-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="22082-147">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="22082-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="22082-148">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="22082-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="22082-149">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="22082-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="22082-150">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="22082-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="22082-151">Se è stato completato il provisioning dell'hub IoT di Azure con `azure-cli` ed è necessario uno strumento per gestire i dispositivi che si connettono all'hub IoT, provare gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="22082-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="22082-152">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="22082-152">Device Explorer</span></span>
<span data-ttu-id="22082-153">[Esplora dispositivi](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette all'hub IoT in Azure.</span><span class="sxs-lookup"><span data-stu-id="22082-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="22082-154">Comunica con i seguenti [endpoint dell'hub IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="22082-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="22082-155">*Gestione delle identità dispositivo* per il provisioning e la gestione dei dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="22082-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="22082-156">*Ricezione da dispositivo a cloud* per il monitoraggio dei messaggi inviati dal dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="22082-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="22082-157">*Invio da cloud a dispositivo* per l'invio dei messaggi dall'hub IoT ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="22082-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="22082-158">Configurare il valore di `IoT hub connection string` all'interno di questo strumento per usarne tutte le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="22082-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="22082-159">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="22082-159">IoT hub Explorer</span></span>
<span data-ttu-id="22082-160">[IoT Hub Explorer](https://github.com/Azure/iothub-explorer) è uno strumento di esempio dell'interfaccia della riga di comando multipiattaforma per gestire i dispositivi client.</span><span class="sxs-lookup"><span data-stu-id="22082-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="22082-161">È possibile usare questo strumento per gestire i dispositivi nel registro di identità, monitorare i messaggi da dispositivo a cloud e inviare comandi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22082-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="22082-162">Per installare la versione più recente, non definitiva, dello strumento iothub-explorer, eseguire questo comando nell'ambiente della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="22082-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="22082-163">Per ottenere altre informazioni su tutti i comandi di iothub explorer e sui relativi parametri, è possibile usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22082-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="22082-164">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22082-164">Azure portal</span></span>
<span data-ttu-id="22082-165">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="22082-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="22082-166">Può anche essere utile usare il [portale di Azure](../azure-portal-overview.md) per il provisioning, la gestione e il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="22082-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="22082-167">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="22082-167">Azure storage issues</span></span>
<span data-ttu-id="22082-168">[Microsoft Azure Storage Explorer (anteprima)](http://storageexplorer.com) è un'app autonoma di Microsoft che consente di utilizzare i dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="22082-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="22082-169">Questo strumento permette di connettersi alla tabella e visualizzarne i dati.</span><span class="sxs-lookup"><span data-stu-id="22082-169">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="22082-170">È possibile usare questo strumento per risolvere i problemi di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="22082-170">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
