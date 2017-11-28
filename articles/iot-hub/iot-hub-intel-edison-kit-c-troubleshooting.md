---
title: Connect Intel Edison (C) tooAzure IoT - risoluzione dei problemi | Documenti Microsoft
description: Pagina sulla risoluzione dei problemi per l'esperienza C in Intel Edison
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: risoluzione dei problemi in arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c4a71983e3906cfc5ce7c832cf858852b9bd744a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="344ed-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="344ed-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="344ed-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="344ed-105">Hardware issues</span></span>
<span data-ttu-id="344ed-106">Per informazioni sulla risoluzione dei problemi comuni in Edison Intel, vedere hello [pagina sulla risoluzione dei problemi ufficiale](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="344ed-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="344ed-107">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="344ed-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="344ed-108">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="344ed-108">No response during gulp tasks</span></span>
<span data-ttu-id="344ed-109">Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug.</span><span class="sxs-lookup"><span data-stu-id="344ed-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="344ed-110">Provare a eseguire attività gulp corrente tooterminate utilizzando `Ctrl + C`, e quindi eseguire hello seguendo comando all'interno dei messaggi di debug toosee finestra console.</span><span class="sxs-lookup"><span data-stu-id="344ed-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="344ed-111">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="344ed-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="344ed-112">Problemi di NPM</span><span class="sxs-lookup"><span data-stu-id="344ed-112">NPM issues</span></span>
<span data-ttu-id="344ed-113">Provare tooupdate del pacchetto NPM con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="344ed-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="344ed-114">Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository esempio][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="344ed-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="344ed-115">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="344ed-115">Azure-CLI issues</span></span>
<span data-ttu-id="344ed-116">Hello Azure interfaccia della riga di comando (CLI di Azure) è una build di anteprima.</span><span class="sxs-lookup"><span data-stu-id="344ed-116">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="344ed-117">Cercare soluzioni in hello [Guida all'installazione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluzioni.</span><span class="sxs-lookup"><span data-stu-id="344ed-117">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="344ed-118">Provare a eseguire tooupgrade cli di Azure toolatest versione quando i comandi non funzionano come previsto.</span><span class="sxs-lookup"><span data-stu-id="344ed-118">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="344ed-119">Se si verificano i bug con lo strumento di hello, file un [problema](https://github.com/Azure/azure-cli/issues) in hello **problemi** sezione del repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="344ed-119">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="344ed-120">Per informazioni sulla risoluzione dei problemi comuni, controllare hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="344ed-120">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="344ed-121">Se vengono soddisfatti, "Impossibile trovare una versione che soddisfa il requisito di hello", versione toolastest di pip tooupgrade comando che segue hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="344ed-121">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="344ed-122">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="344ed-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="344ed-123">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="344ed-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="344ed-124">Durante l'installazione di **pip**, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="344ed-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="344ed-125">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="344ed-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="344ed-126">Alcuni **pip** da radice, causando l'errore di autorizzazione hello sono stati creati i pacchetti da un'installazione precedente.</span><span class="sxs-lookup"><span data-stu-id="344ed-126">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="344ed-127">soluzione hello è tooremove tali pacchetti installati dalla radice.</span><span class="sxs-lookup"><span data-stu-id="344ed-127">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="344ed-128">Usare questa attività di hello toocomplete i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="344ed-128">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="344ed-129">Passare a /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="344ed-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="344ed-130">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="344ed-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="344ed-131">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="344ed-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="344ed-132">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="344ed-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="344ed-133">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="344ed-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="344ed-134">Se hai eseguito correttamente il provisioning dell'hub IoT di Azure con `azure-cli`, ed è necessario un strumento toomanage hello i dispositivi che si connettono tooyour IoT hub, hello provare gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="344ed-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="344ed-135">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="344ed-135">Device Explorer</span></span>
<span data-ttu-id="344ed-136">[Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure.</span><span class="sxs-lookup"><span data-stu-id="344ed-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="344ed-137">Comunica con i seguenti hello [gli endpoint IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="344ed-137">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="344ed-138">_Gestione delle identità dispositivo_ tooprovision e gestire i dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="344ed-138">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="344ed-139">_Ricezione da dispositivo a cloud_ è possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="344ed-139">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="344ed-140">_Inviare cloud a dispositivo_ in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="344ed-140">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="344ed-141">Configurare il `IoT hub connection string` all'interno di questo strumento toouse tutte le relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="344ed-141">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="344ed-142">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="344ed-142">IoT hub Explorer</span></span>
<span data-ttu-id="344ed-143">[Hub IoT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage client dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="344ed-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="344ed-144">Si può utilizzare hello strumento toomanage hello dispositivi nel Registro di identità hello, il monitoraggio dei messaggi da dispositivo a cloud e inviare comandi cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="344ed-144">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="344ed-145">tooinstall hello ultima versione (versione provvisoria) dello strumento di hub IOT Esplora di hello, eseguire hello comando nell'ambiente della riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="344ed-145">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="344ed-146">È possibile utilizzare hello tooget ulteriori informazioni su tutti hello hub IOT Esplora comandi e i relativi parametri di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="344ed-146">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="344ed-147">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="344ed-147">Azure portal</span></span>
<span data-ttu-id="344ed-148">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="344ed-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="344ed-149">È inoltre possibile hello toouse [portale di Azure](../azure-portal-overview.md) toohelp provisioning, gestire ed eseguire il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="344ed-149">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="344ed-150">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="344ed-150">Azure storage issues</span></span>
<span data-ttu-id="344ed-151">[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com) è un'applicazione autonoma di Microsoft che è possibile utilizzare toowork con [di archiviazione di Azure](https://azure.microsoft.com/en-us/services/storage/) dati in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="344ed-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="344ed-152">Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="344ed-152">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="344ed-153">È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="344ed-153">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="344ed-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="344ed-154">Next steps</span></span>
<span data-ttu-id="344ed-155">Questa pagina include solo i problemi più comuni di hello del kit di Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="344ed-155">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="344ed-156">È anche possibile lasciare commenti nella parte inferiore tooreport problemi per la risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="344ed-156">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="344ed-157">Tornare indietro troppo[introduzione Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="344ed-157">Go back too[Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started