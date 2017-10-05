---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 2: Ottenere gli strumenti (Ubuntu) | Documentazione Microsoft'
description: Installare gli strumenti e il software nel computer host che esegue Ubuntu, creare un hub IoT e registrare il dispositivo nell'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, servizio cloud iot, software per internet delle cose, interfaccia della riga di comando di azure, installare git in ubuntu, esecuzione di gulp, installare node js in ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 234b60e1f8eaff52ce07f54d4d12de2421cc1a52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="e3f4d-104">Ottenere gli strumenti (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="e3f4d-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3f4d-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="e3f4d-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="e3f4d-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e3f4d-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="e3f4d-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="e3f4d-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="e3f4d-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e3f4d-108">What you will do</span></span>

- <span data-ttu-id="e3f4d-109">Installare Git, Node.js, Gulp e Python.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="e3f4d-110">Installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="e3f4d-111">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e3f4d-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="e3f4d-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e3f4d-112">What you will learn</span></span>

<span data-ttu-id="e3f4d-113">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="e3f4d-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="e3f4d-114">Come installare Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="e3f4d-115">Git è un sistema distribuito open source di controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="e3f4d-116">L'applicazione di esempio per questa lezione è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="e3f4d-117">Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="e3f4d-118">Come usare NPM per installare gli strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="e3f4d-119">La versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="e3f4d-120">NPM è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="e3f4d-121">Come installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="e3f4d-122">Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e3f4d-123">Dispone di un elevato supporto per funzionalità quali debug, controllo Git incorporato, evidenziazione della sintassi, completamento intelligente del codice, frammenti di codice e refactoring del codice.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="e3f4d-124">Come installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e3f4d-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="e3f4d-125">L'interfaccia della riga di comando di Azure offre un'esperienza di riga di comando multipiattaforma per Azure.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="e3f4d-126">Il provisioning e la gestione delle risorse vengono eseguiti direttamente dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="e3f4d-127">Come usare l'interfaccia della riga di comando di Azure per creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e3f4d-128">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="e3f4d-128">What you need</span></span>

- <span data-ttu-id="e3f4d-129">Connessione Internet per scaricare gli strumenti e il software.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="e3f4d-130">Un computer che esegue Ubuntu 16.04 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="e3f4d-131">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="e3f4d-131">Install Git and Node.js</span></span>

<span data-ttu-id="e3f4d-132">Per installare Git e Node.js, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e3f4d-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="e3f4d-133">Premere `Ctrl + Alt + T` per aprire un terminale.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="e3f4d-134">Eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3f4d-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="e3f4d-135">Installare gli strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="e3f4d-135">Install Node.js development tools</span></span>

<span data-ttu-id="e3f4d-136">Usare [gulp.js](http://gulpjs.com/) per automatizzare la distribuzione e l'esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="e3f4d-137">Per installare gulp, eseguire questo comando nel terminale:</span><span class="sxs-lookup"><span data-stu-id="e3f4d-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="e3f4d-138">Se si verificano problemi con l'installazione, vedere la [Guida alla risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md) per trovare le soluzioni ai problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="e3f4d-139">Node, NPM e Gulp sono necessari per eseguire gli script di automazione sviluppati in Node.js.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="e3f4d-140">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e3f4d-140">Install the Azure CLI</span></span>

<span data-ttu-id="e3f4d-141">Per installare l'interfaccia della riga di comando di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="e3f4d-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="e3f4d-142">Eseguire questi comandi nel terminale:</span><span class="sxs-lookup"><span data-stu-id="e3f4d-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="e3f4d-143">L'installazione potrebbe richiedere 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="e3f4d-144">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e3f4d-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="e3f4d-145">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="e3f4d-146">![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="e3f4d-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="e3f4d-147">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e3f4d-147">Install Visual Studio Code</span></span>

<span data-ttu-id="e3f4d-148">Visual Studio Code verrà usato più avanti nell'esercitazione per modificare i file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="e3f4d-149">[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="e3f4d-150">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="e3f4d-150">Summary</span></span>

<span data-ttu-id="e3f4d-151">Sono stati installati tutto il software e tutti gli strumenti necessari nel computer host.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="e3f4d-152">L'attività successiva consiste nell'usare l'interfaccia della riga di comando di Azure per creare un hub IoT e registrarvi il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3f4d-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3f4d-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3f4d-153">Next steps</span></span>
[<span data-ttu-id="e3f4d-154">Creare un hub IoT e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="e3f4d-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
