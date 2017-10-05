---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 2: Ottenere gli strumenti (macOS) | Documentazione Microsoft'
description: Installare gli strumenti nel computer Mac, creare un hub IoT e registrare il dispositivo nell'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, servizio cloud iot, software per internet delle cose, interfaccia della riga di comando di azure, installare python in mac, installare git in mac, esecuzione di gulp, installare node js in mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d86332816130de7a6951a74ceb215c8ce476d5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="78bd9-104">Ottenere gli strumenti (macOS)</span><span class="sxs-lookup"><span data-stu-id="78bd9-104">Get the tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="78bd9-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="78bd9-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="78bd9-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="78bd9-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="78bd9-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="78bd9-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="78bd9-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="78bd9-108">What you will do</span></span>

- <span data-ttu-id="78bd9-109">Installare Git, Node.js, Gulp e Python.</span><span class="sxs-lookup"><span data-stu-id="78bd9-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="78bd9-110">Installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="78bd9-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="78bd9-111">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="78bd9-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="78bd9-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="78bd9-112">What you will learn</span></span>

<span data-ttu-id="78bd9-113">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="78bd9-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="78bd9-114">Come installare [Git](https://git-scm.com/) e [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="78bd9-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="78bd9-115">Git è un sistema distribuito open source di controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="78bd9-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="78bd9-116">L'applicazione di esempio per questa lezione è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="78bd9-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="78bd9-117">Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="78bd9-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="78bd9-118">Come usare [NPM](https://www.npmjs.com/) per installare gli strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="78bd9-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="78bd9-119">La versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="78bd9-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="78bd9-120">NPM è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="78bd9-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="78bd9-121">Come installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="78bd9-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="78bd9-122">Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="78bd9-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="78bd9-123">Offre un eccellente supporto per il debug, il controllo di Git incorporato, l'evidenziazione della sintassi, il completamento intelligente del codice, i frammenti e il refactoring del codice.</span><span class="sxs-lookup"><span data-stu-id="78bd9-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="78bd9-124">Come installare Python.</span><span class="sxs-lookup"><span data-stu-id="78bd9-124">How to install Python.</span></span>
  - <span data-ttu-id="78bd9-125">Python è un linguaggio di programmazione dinamico, interpretato, generico e di alto livello molto diffuso.</span><span class="sxs-lookup"><span data-stu-id="78bd9-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="78bd9-126">Come installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="78bd9-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="78bd9-127">L'interfaccia della riga di comando di Azure offre un'esperienza di riga di comando multipiattaforma per Azure.</span><span class="sxs-lookup"><span data-stu-id="78bd9-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="78bd9-128">Il provisioning e la gestione delle risorse vengono eseguiti direttamente dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="78bd9-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="78bd9-129">Come usare l'interfaccia della riga di comando di Azure per creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="78bd9-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="78bd9-130">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="78bd9-130">What you need</span></span>

- <span data-ttu-id="78bd9-131">Connessione Internet per scaricare gli strumenti e il software.</span><span class="sxs-lookup"><span data-stu-id="78bd9-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="78bd9-132">Un computer Mac che esegue OS X Yosemite (10.10) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="78bd9-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="78bd9-133">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="78bd9-133">Install Git and Node.js</span></span>

<span data-ttu-id="78bd9-134">Per installare Git e Node.js, usare l'utilità di gestione pacchetti Homebrew attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="78bd9-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="78bd9-135">[Scaricare](http://brew.sh/) e installare Homebrew.</span><span class="sxs-lookup"><span data-stu-id="78bd9-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="78bd9-136">Se Homebrew è già installato, andare al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="78bd9-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="78bd9-137">Premere `Cmd + Space` e immettere `Terminal` per aprire un terminale.</span><span class="sxs-lookup"><span data-stu-id="78bd9-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="78bd9-138">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="78bd9-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="78bd9-139">Installare Git e Node.js eseguendo questi comandi:</span><span class="sxs-lookup"><span data-stu-id="78bd9-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="78bd9-140">Installare gli strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="78bd9-140">Install Node.js development tools</span></span>

<span data-ttu-id="78bd9-141">Usare [gulp.js](http://gulpjs.com/) per automatizzare la distribuzione e l'esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="78bd9-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="78bd9-142">Per installare gulp, eseguire questo comando nel terminale:</span><span class="sxs-lookup"><span data-stu-id="78bd9-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="78bd9-143">Se si verificano problemi nell'installazione, vedere la [guida alla risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md) per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="78bd9-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="78bd9-144">Node, NPM e Gulp sono necessari per eseguire gli script di automazione sviluppati in Node.js.</span><span class="sxs-lookup"><span data-stu-id="78bd9-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="78bd9-145">Installare Python</span><span class="sxs-lookup"><span data-stu-id="78bd9-145">Install Python</span></span>

<span data-ttu-id="78bd9-146">Sebbene Mac OS X venga fornito con Python 2.7, si consiglia di installare Python tramite Homebrew.</span><span class="sxs-lookup"><span data-stu-id="78bd9-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="78bd9-147">Vedere [Installazione di Python in Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="78bd9-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="78bd9-148">Installare Python ed eseguire i parametri di inizializzazione del programma tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="78bd9-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="78bd9-149">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="78bd9-149">Install the Azure CLI</span></span>

<span data-ttu-id="78bd9-150">Per installare l'interfaccia della riga di comando di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="78bd9-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="78bd9-151">Eseguire questi comandi nel terminale:</span><span class="sxs-lookup"><span data-stu-id="78bd9-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="78bd9-152">L'installazione potrebbe richiedere 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="78bd9-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="78bd9-153">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="78bd9-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="78bd9-154">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="78bd9-154">You should see the following output if the installation is successful.</span></span>

   ![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="78bd9-156">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="78bd9-156">Install Visual Studio Code</span></span>

<span data-ttu-id="78bd9-157">Visual Studio Code verrà usato più avanti nell'esercitazione per modificare i file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="78bd9-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="78bd9-158">[Scaricare](https://code.visualstudio.com/docs/setup/osx) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="78bd9-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="78bd9-159">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="78bd9-159">Summary</span></span>

<span data-ttu-id="78bd9-160">È stata eseguita l'installazione di tutti gli strumenti e il software necessari sul computer Mac.</span><span class="sxs-lookup"><span data-stu-id="78bd9-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="78bd9-161">L'attività successiva consiste nell'utilizzare l'interfaccia della riga di comando di Azure per creare un hub IoT e registrarvi il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="78bd9-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78bd9-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78bd9-162">Next steps</span></span>
[<span data-ttu-id="78bd9-163">Creare un hub IoT e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="78bd9-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
