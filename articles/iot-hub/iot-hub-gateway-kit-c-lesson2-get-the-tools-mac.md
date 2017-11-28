---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 2: Ottenere gli strumenti (macOS) | Documentazione Microsoft'
description: Installare gli strumenti nel computer Mac, creare un hub IoT e registrare il dispositivo nell'hub IoT hello.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, servizio cloud iot, software per internet delle cose, interfaccia della riga di comando di azure, installare python in mac, installare git in mac, esecuzione di gulp, installare node js in mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="6809c-104">Ottenere strumenti hello (MacOS)</span><span class="sxs-lookup"><span data-stu-id="6809c-104">Get hello tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6809c-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="6809c-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="6809c-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6809c-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="6809c-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="6809c-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="6809c-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6809c-108">What you will do</span></span>

- <span data-ttu-id="6809c-109">Installare Git, Node.js, Gulp e Python.</span><span class="sxs-lookup"><span data-stu-id="6809c-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="6809c-110">Installare hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="6809c-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="6809c-111">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6809c-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6809c-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6809c-112">What you will learn</span></span>

<span data-ttu-id="6809c-113">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="6809c-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="6809c-114">Come tooinstall [Git](https://git-scm.com/) e [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="6809c-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="6809c-115">Git è un sistema distribuito open source di controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="6809c-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="6809c-116">applicazione di esempio Hello per questa lezione viene archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="6809c-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="6809c-117">Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="6809c-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="6809c-118">Come toouse [NPM](https://www.npmjs.com/) tooinstall Node.js gli strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6809c-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="6809c-119">Hello versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="6809c-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="6809c-120">NPM è uno dei gestori di pacchetti hello per Node.js.</span><span class="sxs-lookup"><span data-stu-id="6809c-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="6809c-121">Come tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6809c-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="6809c-122">Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="6809c-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="6809c-123">Dispone di un elevato supporto per funzionalità quali debug, controllo Git incorporato, evidenziazione della sintassi, completamento intelligente del codice, frammenti di codice e refactoring del codice.</span><span class="sxs-lookup"><span data-stu-id="6809c-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="6809c-124">Come tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="6809c-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="6809c-125">Python è un linguaggio di programmazione dinamico, interpretato, generico e di alto livello molto diffuso.</span><span class="sxs-lookup"><span data-stu-id="6809c-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="6809c-126">Come tooinstall hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="6809c-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="6809c-127">Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="6809c-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="6809c-128">Si lavora direttamente da una riga di comando di tooprovision e gestire le risorse.</span><span class="sxs-lookup"><span data-stu-id="6809c-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="6809c-129">Come un hub IoT toouse hello toocreate CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="6809c-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6809c-130">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="6809c-130">What you need</span></span>

- <span data-ttu-id="6809c-131">Un toodownload connessione Internet hello strumenti e software.</span><span class="sxs-lookup"><span data-stu-id="6809c-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="6809c-132">Un computer Mac che esegue OS X Yosemite (10.10) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6809c-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="6809c-133">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="6809c-133">Install Git and Node.js</span></span>

<span data-ttu-id="6809c-134">tooinstall Git e Node.js, utilizzare l'utilità di gestione dei pacchetti Homebrew hello attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6809c-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="6809c-135">[Scaricare](http://brew.sh/) e installare Homebrew.</span><span class="sxs-lookup"><span data-stu-id="6809c-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="6809c-136">Se è già stato installato Homebrew, è possibile passare toostep 2.</span><span class="sxs-lookup"><span data-stu-id="6809c-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="6809c-137">Premere `Cmd + Space` e immettere `Terminal` tooopen un terminale.</span><span class="sxs-lookup"><span data-stu-id="6809c-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="6809c-138">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6809c-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="6809c-139">Installare Git e Node.js eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6809c-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="6809c-140">Installare gli strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="6809c-140">Install Node.js development tools</span></span>

<span data-ttu-id="6809c-141">Utilizzare [file gulp.js](http://gulpjs.com/) tooautomate distribuzione ed esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="6809c-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="6809c-142">gulp tooinstall, eseguire hello comando terminal hello seguente:</span><span class="sxs-lookup"><span data-stu-id="6809c-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="6809c-143">Se si verificano problemi relativi all'installazione di hello, vedere hello [risoluzione dei problemi guida](iot-hub-gateway-kit-c-troubleshooting.md) per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="6809c-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="6809c-144">Nodo, NPM e Gulp sono gli script di automazione di richiesto toorun sviluppati in Node.js.</span><span class="sxs-lookup"><span data-stu-id="6809c-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="6809c-145">Installare Python</span><span class="sxs-lookup"><span data-stu-id="6809c-145">Install Python</span></span>

<span data-ttu-id="6809c-146">Sebbene Mac OS X venga fornito con Python 2.7, si consiglia di installare Python tramite Homebrew.</span><span class="sxs-lookup"><span data-stu-id="6809c-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="6809c-147">Vedere [Installazione di Python in Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="6809c-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="6809c-148">Installare Python e pip eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6809c-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="6809c-149">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="6809c-149">Install hello Azure CLI</span></span>

<span data-ttu-id="6809c-150">hello tooinstall CLI di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="6809c-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="6809c-151">Eseguire i seguenti comandi in terminal hello hello:</span><span class="sxs-lookup"><span data-stu-id="6809c-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="6809c-152">installazione di Hello potrebbe richiedere 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="6809c-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="6809c-153">Verificare l'installazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6809c-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="6809c-154">Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="6809c-154">You should see hello following output if hello installation is successful.</span></span>

   ![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="6809c-156">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6809c-156">Install Visual Studio Code</span></span>

<span data-ttu-id="6809c-157">Utilizzare Visual Studio Code in un secondo momento nei file di configurazione di hello tooedit dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6809c-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="6809c-158">[Scaricare](https://code.visualstudio.com/docs/setup/osx) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6809c-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="6809c-159">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="6809c-159">Summary</span></span>

<span data-ttu-id="6809c-160">Aver installato tutti gli strumenti necessario hello e software nel computer Mac.</span><span class="sxs-lookup"><span data-stu-id="6809c-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="6809c-161">L'attività successiva è toouse hello Azure CLI toocreate un hub IoT e registrare il dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6809c-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6809c-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6809c-162">Next steps</span></span>
[<span data-ttu-id="6809c-163">Creare un hub IoT e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="6809c-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
