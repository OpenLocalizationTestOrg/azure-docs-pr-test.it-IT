---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 2: Ottenere gli strumenti (Windows) | Documentazione Microsoft'
description: Installare strumenti di hello e software hello nel computer host che eseguono Windows, creare un hub IoT e registrare il dispositivo nell'hub IoT hello.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, servizio cloud iot, software per internet delle cose, interfaccia della riga di comando di azure, installare git in windows, esecuzione di gulp, installare node js in windows, installare npm in windows, installare python in windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="420b5-104">Ottenere strumenti hello (Windows 7 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="420b5-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="420b5-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="420b5-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="420b5-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="420b5-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="420b5-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="420b5-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="420b5-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="420b5-108">What you will do</span></span>

- <span data-ttu-id="420b5-109">Installare Git, Node.js, Gulp e Python.</span><span class="sxs-lookup"><span data-stu-id="420b5-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="420b5-110">Installare hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="420b5-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="420b5-111">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="420b5-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="420b5-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="420b5-112">What you will learn</span></span>

<span data-ttu-id="420b5-113">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="420b5-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="420b5-114">Come tooinstall [Git](https://git-scm.com/) e [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="420b5-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="420b5-115">Git è un sistema distribuito open source di controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="420b5-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="420b5-116">applicazione di esempio Hello per questa lezione viene archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="420b5-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="420b5-117">Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="420b5-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="420b5-118">Come toouse [NPM](https://www.npmjs.com/) tooinstall Node.js gli strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="420b5-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="420b5-119">Hello versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="420b5-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="420b5-120">NPM è uno dei gestori di pacchetti hello per Node.js.</span><span class="sxs-lookup"><span data-stu-id="420b5-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="420b5-121">Come tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="420b5-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="420b5-122">Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="420b5-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="420b5-123">Dispone di un elevato supporto per funzionalità quali debug, controllo Git incorporato, evidenziazione della sintassi, completamento intelligente del codice, frammenti di codice e refactoring del codice.</span><span class="sxs-lookup"><span data-stu-id="420b5-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="420b5-124">Come tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="420b5-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="420b5-125">Python è un linguaggio di programmazione dinamico, interpretato, generico e di alto livello molto diffuso.</span><span class="sxs-lookup"><span data-stu-id="420b5-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="420b5-126">Come tooinstall hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="420b5-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="420b5-127">Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="420b5-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="420b5-128">Si lavora direttamente da una riga di comando di tooprovision e gestire le risorse.</span><span class="sxs-lookup"><span data-stu-id="420b5-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="420b5-129">Come un hub IoT toouse hello toocreate CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="420b5-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="420b5-130">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="420b5-130">What you need</span></span>

- <span data-ttu-id="420b5-131">Un toodownload connessione Internet hello strumenti e software.</span><span class="sxs-lookup"><span data-stu-id="420b5-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="420b5-132">Computer Windows.</span><span class="sxs-lookup"><span data-stu-id="420b5-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="420b5-133">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="420b5-133">Install Git and Node.js</span></span>

<span data-ttu-id="420b5-134">Fare clic su hello seguente toodownload collegamenti e installare Git e LTS Node.js per Windows.</span><span class="sxs-lookup"><span data-stu-id="420b5-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="420b5-135">Ottenere Git per Windows</span><span class="sxs-lookup"><span data-stu-id="420b5-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="420b5-136">Ottenere Node.js LTS per Windows</span><span class="sxs-lookup"><span data-stu-id="420b5-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="420b5-137">Installare gli strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="420b5-137">Install Node.js development tools</span></span>

<span data-ttu-id="420b5-138">Utilizzare [file gulp.js](http://gulpjs.com/) tooautomate distribuzione ed esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="420b5-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="420b5-139">Premere `Windows + R`, tipo `cmd` e premere `Enter` tooopen una finestra del prompt dei comandi, e quindi eseguire hello finestra di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="420b5-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="420b5-140">Se si verificano problemi relativi all'installazione di hello, vedere hello [risoluzione dei problemi guida](iot-hub-gateway-kit-c-sim-troubleshooting.md) per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="420b5-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="420b5-141">Nodo, NPM e Gulp sono gli script di automazione di richiesto toorun sviluppati in Node.js.</span><span class="sxs-lookup"><span data-stu-id="420b5-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="420b5-142">Installare Python</span><span class="sxs-lookup"><span data-stu-id="420b5-142">Install Python</span></span>

<span data-ttu-id="420b5-143">È possibile scegliere Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="420b5-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="420b5-144">In questa esercitazione si userà Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="420b5-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="420b5-145">Se è già stato installato python, andare toohello nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="420b5-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="420b5-146">Ottenere Python per Windows</span><span class="sxs-lookup"><span data-stu-id="420b5-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="420b5-147">È inoltre necessario percorso hello tooadd delle cartelle hello in Python.exe e pip.exe sono installati toohello sistema `PATH` variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="420b5-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="420b5-148">Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="420b5-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="420b5-149">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="420b5-149">Install hello Azure CLI</span></span>

<span data-ttu-id="420b5-150">hello tooinstall CLI di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="420b5-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="420b5-151">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="420b5-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="420b5-152">Installare hello CLI di Azure eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="420b5-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="420b5-153">installazione di Hello potrebbe richiedere 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="420b5-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="420b5-154">Verificare l'installazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="420b5-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="420b5-155">Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="420b5-155">You should see hello following output if hello installation is successful.</span></span>

   ![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="420b5-157">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="420b5-157">Install Visual Studio Code</span></span>

<span data-ttu-id="420b5-158">Utilizzare Visual Studio Code in un secondo momento nei file di configurazione di hello tooedit dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="420b5-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="420b5-159">[Scaricare](https://code.visualstudio.com/docs/setup/windows) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="420b5-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="420b5-160">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="420b5-160">Summary</span></span>

<span data-ttu-id="420b5-161">Aver installato tutti gli strumenti necessario hello e software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="420b5-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="420b5-162">L'attività successiva è toouse hello Azure CLI toocreate un hub IoT e registrare il dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="420b5-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="420b5-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="420b5-163">Next steps</span></span>
[<span data-ttu-id="420b5-164">Creare un hub IoT e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="420b5-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
