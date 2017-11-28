---
title: 'Connettere Arduino (C) ad Azure IoT: risolvere i problemi | Documentazione Microsoft'
description: Pagina sulla risoluzione dei problemi per l'esperienza Arduino in Adafruit Feather M0 WiFi
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: risoluzione dei problemi in arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3bb369da9148300a80e7d351522a4d908e926996
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="46a61-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="46a61-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="46a61-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="46a61-105">Hardware issues</span></span>
<span data-ttu-id="46a61-106">Per informazioni sulla risoluzione dei problemi più comuni della scheda Arduino in Adafruit Feather M0 WiFi, vedere la relativa [pagina ufficiale sulla risoluzione dei problemi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="46a61-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see the [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="46a61-107">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="46a61-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="46a61-108">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="46a61-108">No response during gulp tasks</span></span>
<span data-ttu-id="46a61-109">Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere l'opzione `--verbose` per il debug.</span><span class="sxs-lookup"><span data-stu-id="46a61-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="46a61-110">Provare a terminare le attività gulp correnti con `Ctrl + C` e quindi eseguire questo comando nella finestra della console per visualizzare i messaggi di debug.</span><span class="sxs-lookup"><span data-stu-id="46a61-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="46a61-111">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="46a61-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="46a61-112">In alternativa è possibile aggiungere `--listen` per aprire la porta seriale per l'output delle informazioni di log del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="46a61-112">Or you can add `--listen` to open serial port to output device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="46a61-113">Problemi di NPM</span><span class="sxs-lookup"><span data-stu-id="46a61-113">NPM issues</span></span>
<span data-ttu-id="46a61-114">Provare ad aggiornare il pacchetto NPM con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="46a61-114">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="46a61-115">Se il problema persiste, aggiungere commenti alla fine di questo articolo o definire un problema di GitHub nel [repository degli esempi][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="46a61-115">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="46a61-116">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="46a61-116">Azure-CLI issues</span></span>
<span data-ttu-id="46a61-117">L'interfaccia della riga di comando di Azure è una versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="46a61-117">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="46a61-118">Per cercare le soluzioni ai problemi, vedere la [guida all'installazione della versione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="46a61-118">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="46a61-119">Quando i comandi non funzionano come previsto, provare ad aggiornare l'interfaccia della riga di comando di Azure alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="46a61-119">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="46a61-120">Se si rilevano bug con lo strumento, segnalare un [problema](https://github.com/Azure/azure-cli/issues) nella sezione **Issues** (Problemi) del repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="46a61-120">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="46a61-121">Per risolvere più facilmente i problemi comuni, controllare il file [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="46a61-121">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="46a61-122">Se viene visualizzato un messaggio simile a "Impossibile trovare una versione che soddisfi il requisito", eseguire questo comando per aggiornare pip all'ultima versione.</span><span class="sxs-lookup"><span data-stu-id="46a61-122">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="46a61-123">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="46a61-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="46a61-124">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="46a61-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="46a61-125">Durante l'installazione di **pip**, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="46a61-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="46a61-126">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="46a61-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="46a61-127">Alcuni pacchetti **pip** di un'installazione precedente sono stati creati dall'utente root e questo causa l'errore di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="46a61-127">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="46a61-128">La soluzione consiste nel rimuovere i pacchetti installati dall'utente root.</span><span class="sxs-lookup"><span data-stu-id="46a61-128">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="46a61-129">Per completare questa attività, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="46a61-129">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="46a61-130">Passare a /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="46a61-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="46a61-131">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="46a61-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="46a61-132">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="46a61-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="46a61-133">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="46a61-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="46a61-134">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="46a61-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="46a61-135">Se è stato completato il provisioning dell'hub IoT di Azure con `azure-cli` ed è necessario uno strumento per gestire i dispositivi che si connettono all'hub IoT, provare gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="46a61-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="46a61-136">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="46a61-136">Device Explorer</span></span>
<span data-ttu-id="46a61-137">[Esplora dispositivi](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette all'hub IoT in Azure.</span><span class="sxs-lookup"><span data-stu-id="46a61-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="46a61-138">Comunica con i seguenti [endpoint dell'hub IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="46a61-138">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="46a61-139">*Gestione delle identità dispositivo* per il provisioning e la gestione dei dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="46a61-139">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="46a61-140">*Ricezione da dispositivo a cloud* per il monitoraggio dei messaggi inviati dal dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="46a61-140">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="46a61-141">*Invio da cloud a dispositivo* per l'invio dei messaggi dall'hub IoT ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="46a61-141">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="46a61-142">Configurare il valore di `IoT hub connection string` all'interno di questo strumento per usarne tutte le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="46a61-142">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="46a61-143">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="46a61-143">IoT hub Explorer</span></span>
<span data-ttu-id="46a61-144">[IoT Hub Explorer](https://github.com/Azure/iothub-explorer) è uno strumento di esempio dell'interfaccia della riga di comando multipiattaforma per gestire i dispositivi client.</span><span class="sxs-lookup"><span data-stu-id="46a61-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="46a61-145">È possibile usare questo strumento per gestire i dispositivi nel registro di identità, monitorare i messaggi da dispositivo a cloud e inviare comandi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="46a61-145">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="46a61-146">Per installare la versione più recente, non definitiva, dello strumento iothub-explorer, eseguire questo comando nell'ambiente della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="46a61-146">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="46a61-147">Per ottenere altre informazioni su tutti i comandi di iothub explorer e sui relativi parametri, è possibile usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="46a61-147">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="46a61-148">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="46a61-148">Azure portal</span></span>
<span data-ttu-id="46a61-149">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="46a61-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="46a61-150">Può anche essere utile usare il [portale di Azure](../azure-portal-overview.md) per il provisioning, la gestione e il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="46a61-150">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="46a61-151">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="46a61-151">Azure storage issues</span></span>
<span data-ttu-id="46a61-152">[Microsoft Azure Storage Explorer (anteprima)](http://storageexplorer.com) è un'app autonoma di Microsoft che consente di utilizzare i dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="46a61-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="46a61-153">Questo strumento permette di connettersi alla tabella e visualizzarne i dati.</span><span class="sxs-lookup"><span data-stu-id="46a61-153">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="46a61-154">È possibile usare questo strumento per risolvere i problemi di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46a61-154">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md