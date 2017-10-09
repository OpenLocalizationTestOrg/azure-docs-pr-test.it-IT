---
title: Connect Arduino (C) tooAzure IoT - risoluzione dei problemi | Documenti Microsoft
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
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="f7f82-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f7f82-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="f7f82-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="f7f82-105">Hardware issues</span></span>
<span data-ttu-id="f7f82-106">Per informazioni sulla risoluzione dei problemi più comuni sulla Lavagna Adafruit sfumatura M0 Wi-Fi Arduino, vedere hello [pagina sulla risoluzione dei problemi ufficiale](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="f7f82-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see hello [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="f7f82-107">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="f7f82-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="f7f82-108">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="f7f82-108">No response during gulp tasks</span></span>
<span data-ttu-id="f7f82-109">Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug.</span><span class="sxs-lookup"><span data-stu-id="f7f82-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="f7f82-110">Provare a eseguire attività gulp corrente tooterminate utilizzando `Ctrl + C`, e quindi eseguire hello seguendo comando all'interno dei messaggi di debug toosee finestra console.</span><span class="sxs-lookup"><span data-stu-id="f7f82-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="f7f82-111">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="f7f82-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="f7f82-112">Oppure è possibile aggiungere `--listen` informazioni del log dispositivo toooutput tooopen porta seriale.</span><span class="sxs-lookup"><span data-stu-id="f7f82-112">Or you can add `--listen` tooopen serial port toooutput device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="f7f82-113">Problemi di NPM</span><span class="sxs-lookup"><span data-stu-id="f7f82-113">NPM issues</span></span>
<span data-ttu-id="f7f82-114">Provare tooupdate del pacchetto NPM con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f7f82-114">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="f7f82-115">Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository esempio][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="f7f82-115">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="f7f82-116">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f7f82-116">Azure-CLI issues</span></span>
<span data-ttu-id="f7f82-117">Hello Azure interfaccia della riga di comando (CLI di Azure) è una build di anteprima.</span><span class="sxs-lookup"><span data-stu-id="f7f82-117">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="f7f82-118">Cercare soluzioni in hello [Guida all'installazione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluzioni.</span><span class="sxs-lookup"><span data-stu-id="f7f82-118">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="f7f82-119">Provare a eseguire tooupgrade cli di Azure toolatest versione quando i comandi non funzionano come previsto.</span><span class="sxs-lookup"><span data-stu-id="f7f82-119">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="f7f82-120">Se si verificano i bug con lo strumento di hello, file un [problema](https://github.com/Azure/azure-cli/issues) in hello **problemi** sezione del repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="f7f82-120">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="f7f82-121">Per informazioni sulla risoluzione dei problemi comuni, controllare hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="f7f82-121">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="f7f82-122">Se vengono soddisfatti, "Impossibile trovare una versione che soddisfa il requisito di hello", versione toolastest di pip tooupgrade comando che segue hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f7f82-122">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="f7f82-123">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="f7f82-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="f7f82-124">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="f7f82-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="f7f82-125">Durante l'installazione di **pip**, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="f7f82-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="f7f82-126">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="f7f82-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="f7f82-127">Alcuni **pip** da radice, causando l'errore di autorizzazione hello sono stati creati i pacchetti da un'installazione precedente.</span><span class="sxs-lookup"><span data-stu-id="f7f82-127">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="f7f82-128">soluzione hello è tooremove tali pacchetti installati dalla radice.</span><span class="sxs-lookup"><span data-stu-id="f7f82-128">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="f7f82-129">Usare questa attività di hello toocomplete i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f7f82-129">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="f7f82-130">Passare a /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="f7f82-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="f7f82-131">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="f7f82-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="f7f82-132">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="f7f82-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="f7f82-133">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="f7f82-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="f7f82-134">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="f7f82-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="f7f82-135">Se hai eseguito correttamente il provisioning dell'hub IoT di Azure con `azure-cli`, ed è necessario un strumento toomanage hello i dispositivi che si connettono tooyour IoT hub, hello provare gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f7f82-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="f7f82-136">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="f7f82-136">Device Explorer</span></span>
<span data-ttu-id="f7f82-137">[Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f82-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="f7f82-138">Comunica con i seguenti hello [gli endpoint IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="f7f82-138">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="f7f82-139">*Gestione delle identità dispositivo* tooprovision e gestire i dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f7f82-139">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="f7f82-140">*Ricezione da dispositivo a cloud* è possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f7f82-140">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="f7f82-141">*Inviare cloud a dispositivo* in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f7f82-141">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="f7f82-142">Configurare il `IoT hub connection string` all'interno di questo strumento toouse tutte le relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f7f82-142">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="f7f82-143">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="f7f82-143">IoT hub Explorer</span></span>
<span data-ttu-id="f7f82-144">[Hub IoT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage client dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="f7f82-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="f7f82-145">Si può utilizzare hello strumento toomanage hello dispositivi nel Registro di identità hello, il monitoraggio dei messaggi da dispositivo a cloud e inviare comandi cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f7f82-145">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="f7f82-146">tooinstall hello ultima versione (versione provvisoria) dello strumento di hub IOT Esplora di hello, eseguire hello comando nell'ambiente della riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f7f82-146">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="f7f82-147">È possibile utilizzare hello tooget ulteriori informazioni su tutti hello hub IOT Esplora comandi e i relativi parametri di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f7f82-147">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="f7f82-148">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f7f82-148">Azure portal</span></span>
<span data-ttu-id="f7f82-149">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f82-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="f7f82-150">È inoltre possibile hello toouse [portale di Azure](../azure-portal-overview.md) toohelp provisioning, gestire ed eseguire il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f82-150">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="f7f82-151">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f7f82-151">Azure storage issues</span></span>
<span data-ttu-id="f7f82-152">[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com) è un'applicazione autonoma da Microsoft che è possibile utilizzare toowork con dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="f7f82-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="f7f82-153">Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="f7f82-153">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="f7f82-154">È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f82-154">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md