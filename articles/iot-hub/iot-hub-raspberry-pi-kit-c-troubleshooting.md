---
title: Connect Raspberry PI (C) tooAzure IoT - risoluzione dei problemi | Documenti Microsoft
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
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="205bb-104">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="205bb-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="205bb-105">Problemi hardware</span><span class="sxs-lookup"><span data-stu-id="205bb-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="205bb-106">un'applicazione Hello viene eseguita correttamente, ma hello LED è lampeggiante non</span><span class="sxs-lookup"><span data-stu-id="205bb-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="205bb-107">Questo problema è sempre la connettività di circuito hardware toohello correlati.</span><span class="sxs-lookup"><span data-stu-id="205bb-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="205bb-108">Utilizzare hello problemi tooidentify i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="205bb-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="205bb-109">Verificare che si è scelto di hello corretto **GPIO** sulla Lavagna.</span><span class="sxs-lookup"><span data-stu-id="205bb-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="205bb-110">le porte Hello due **GPIO GND (6 Pin)** e **04 GPIO (7 Pin)**.</span><span class="sxs-lookup"><span data-stu-id="205bb-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="205bb-111">Verificare che la polarità hello del LED sia corretta.</span><span class="sxs-lookup"><span data-stu-id="205bb-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="205bb-112">parte di più Hello deve indicare hello **positivo**, pin anode.</span><span class="sxs-lookup"><span data-stu-id="205bb-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="205bb-113">Hello utilizzare **aggiungere 3,3 v** e **GND Pin** Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="205bb-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="205bb-114">Considera Pi hello power controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="205bb-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="205bb-115">Verificare che hello LED funziona correttamente.</span><span class="sxs-lookup"><span data-stu-id="205bb-115">Check that hello LED works fine.</span></span>

![Specifiche del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="205bb-117">Altri problemi hardware</span><span class="sxs-lookup"><span data-stu-id="205bb-117">Other hardware issues</span></span>
<span data-ttu-id="205bb-118">Per informazioni sulla risoluzione dei problemi comuni in Raspberry Pi 3, vedere hello [pagina sulla risoluzione dei problemi ufficiale](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="205bb-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="205bb-119">Problemi del pacchetto Node.js</span><span class="sxs-lookup"><span data-stu-id="205bb-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="205bb-120">Nessuna risposta durante le attività gulp</span><span class="sxs-lookup"><span data-stu-id="205bb-120">No response during gulp tasks</span></span>
<span data-ttu-id="205bb-121">Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug.</span><span class="sxs-lookup"><span data-stu-id="205bb-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="205bb-122">Provare a eseguire attività gulp corrente tooterminate utilizzando `Ctrl + C`, e quindi eseguire hello seguendo comando all'interno dei messaggi di debug toosee finestra console.</span><span class="sxs-lookup"><span data-stu-id="205bb-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="205bb-123">È possibile visualizzare i messaggi di errore dettagliati nell'output della console.</span><span class="sxs-lookup"><span data-stu-id="205bb-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="205bb-124">Problemi di individuazione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="205bb-124">Device discovery issues</span></span>
<span data-ttu-id="205bb-125">Per semplificare la risoluzione dei problemi comuni con hello `devdisco` comando, controllare hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="205bb-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="205bb-126">Problemi di NPM</span><span class="sxs-lookup"><span data-stu-id="205bb-126">NPM issues</span></span>
<span data-ttu-id="205bb-127">Provare tooupdate del pacchetto NPM con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="205bb-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="205bb-128">Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository di esempio](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="205bb-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="205bb-129">Debug remoto</span><span class="sxs-lookup"><span data-stu-id="205bb-129">Remote debugging</span></span>

<span data-ttu-id="205bb-130">Il supporto remoto sarà disponibile presto in Visual Studio Code C/C++ Extension.</span><span class="sxs-lookup"><span data-stu-id="205bb-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="205bb-131">Nel frattempo è possibile usare GDB tramite il terminale SSH preferito:</span><span class="sxs-lookup"><span data-stu-id="205bb-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="205bb-132">Problemi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="205bb-132">Azure-CLI issues</span></span>
<span data-ttu-id="205bb-133">Hello Azure interfaccia della riga di comando (CLI di Azure) è una build di anteprima.</span><span class="sxs-lookup"><span data-stu-id="205bb-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="205bb-134">Cercare soluzioni in hello [Guida all'installazione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluzioni.</span><span class="sxs-lookup"><span data-stu-id="205bb-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="205bb-135">Provare a eseguire tooupgrade cli di Azure toolatest versione quando i comandi non funzionano come previsto.</span><span class="sxs-lookup"><span data-stu-id="205bb-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="205bb-136">Se si verificano i bug con lo strumento di hello, file un [problema](https://github.com/Azure/azure-cli/issues) in hello **problemi** sezione del repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="205bb-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="205bb-137">Per informazioni sulla risoluzione dei problemi comuni, controllare hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="205bb-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="205bb-138">Se vengono soddisfatti, "Impossibile trovare una versione che soddisfa il requisito di hello", versione toolastest di pip tooupgrade comando che segue hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="205bb-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="205bb-139">Problemi di installazione di Python</span><span class="sxs-lookup"><span data-stu-id="205bb-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="205bb-140">Problemi di installazione di pacchetti legacy (macOS)</span><span class="sxs-lookup"><span data-stu-id="205bb-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="205bb-141">Durante l'installazione di **pip**, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**.</span><span class="sxs-lookup"><span data-stu-id="205bb-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="205bb-142">Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente.</span><span class="sxs-lookup"><span data-stu-id="205bb-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="205bb-143">Alcuni **pip** da radice, causando l'errore di autorizzazione hello sono stati creati i pacchetti da un'installazione precedente.</span><span class="sxs-lookup"><span data-stu-id="205bb-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="205bb-144">soluzione hello è tooremove tali pacchetti installati dalla radice.</span><span class="sxs-lookup"><span data-stu-id="205bb-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="205bb-145">Usare questa attività di hello toocomplete i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="205bb-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="205bb-146">Passare a /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="205bb-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="205bb-147">Elencare i pacchetti creati dall'utente root: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="205bb-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="205bb-148">Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="205bb-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="205bb-149">Reinstallare Python.</span><span class="sxs-lookup"><span data-stu-id="205bb-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="205bb-150">Problemi di Hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="205bb-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="205bb-151">Se hai eseguito correttamente il provisioning dell'hub IoT di Azure con `azure-cli`, ed è necessario un strumento toomanage hello i dispositivi che si connettono tooyour IoT hub, hello provare gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="205bb-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="205bb-152">Esplora dispositivi</span><span class="sxs-lookup"><span data-stu-id="205bb-152">Device Explorer</span></span>
<span data-ttu-id="205bb-153">[Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure.</span><span class="sxs-lookup"><span data-stu-id="205bb-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="205bb-154">Comunica con i seguenti hello [gli endpoint IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="205bb-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="205bb-155">*Gestione delle identità dispositivo* tooprovision e gestire i dispositivi registrati con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="205bb-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="205bb-156">*Ricezione da dispositivo a cloud* è possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="205bb-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="205bb-157">*Inviare cloud a dispositivo* in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="205bb-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="205bb-158">Configurare il `IoT hub connection string` all'interno di questo strumento toouse tutte le relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="205bb-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="205bb-159">IoT Hub Explorer</span><span class="sxs-lookup"><span data-stu-id="205bb-159">IoT hub Explorer</span></span>
<span data-ttu-id="205bb-160">[Hub IoT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage client dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="205bb-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="205bb-161">Si può utilizzare hello strumento toomanage hello dispositivi nel Registro di identità hello, il monitoraggio dei messaggi da dispositivo a cloud e inviare comandi cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="205bb-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="205bb-162">tooinstall hello ultima versione (versione provvisoria) dello strumento di hub IOT Esplora di hello, eseguire hello comando nell'ambiente della riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="205bb-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="205bb-163">È possibile utilizzare hello tooget ulteriori informazioni su tutti hello hub IOT Esplora comandi e i relativi parametri di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="205bb-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="205bb-164">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="205bb-164">Azure portal</span></span>
<span data-ttu-id="205bb-165">Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="205bb-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="205bb-166">È inoltre possibile hello toouse [portale di Azure](../azure-portal-overview.md) toohelp provisioning, gestire ed eseguire il debug delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="205bb-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="205bb-167">Problemi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="205bb-167">Azure storage issues</span></span>
<span data-ttu-id="205bb-168">[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com) è un'applicazione autonoma da Microsoft che è possibile utilizzare toowork con dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="205bb-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="205bb-169">Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="205bb-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="205bb-170">È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="205bb-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
