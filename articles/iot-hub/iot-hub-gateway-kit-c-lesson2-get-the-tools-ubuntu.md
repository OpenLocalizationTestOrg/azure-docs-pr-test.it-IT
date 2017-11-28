---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 2: Ottenere gli strumenti (Ubuntu) | Documentazione Microsoft'
description: Installare strumenti di hello e software hello nel computer host che eseguono Ubuntu, creare un hub IoT e registrare il dispositivo nell'hub IoT hello.
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
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="f0bbe-104">Ottenere strumenti hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="f0bbe-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0bbe-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="f0bbe-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="f0bbe-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f0bbe-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f0bbe-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="f0bbe-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="f0bbe-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f0bbe-108">What you will do</span></span>

- <span data-ttu-id="f0bbe-109">Installare Git, Node.js, Gulp e Python.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="f0bbe-110">Installare hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="f0bbe-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="f0bbe-111">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f0bbe-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="f0bbe-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f0bbe-112">What you will learn</span></span>

<span data-ttu-id="f0bbe-113">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="f0bbe-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f0bbe-114">Come tooinstall Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="f0bbe-115">Git è un sistema distribuito open source di controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="f0bbe-116">applicazione di esempio Hello per questa lezione viene archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="f0bbe-117">Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="f0bbe-118">Come gli strumenti di sviluppo toouse NPM tooinstall Node.js.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="f0bbe-119">Hello versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="f0bbe-120">NPM è uno dei gestori di pacchetti hello per Node.js.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="f0bbe-121">Come tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="f0bbe-122">Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f0bbe-123">Dispone di un elevato supporto per funzionalità quali debug, controllo Git incorporato, evidenziazione della sintassi, completamento intelligente del codice, frammenti di codice e refactoring del codice.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="f0bbe-124">Come tooinstall hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="f0bbe-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="f0bbe-125">Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="f0bbe-126">Si lavora direttamente da una riga di comando di tooprovision e gestire le risorse.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="f0bbe-127">Come un hub IoT toouse hello toocreate CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f0bbe-128">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="f0bbe-128">What you need</span></span>

- <span data-ttu-id="f0bbe-129">Un toodownload connessione Internet hello strumenti e software.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="f0bbe-130">Un computer che esegue Ubuntu 16.04 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="f0bbe-131">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="f0bbe-131">Install Git and Node.js</span></span>

<span data-ttu-id="f0bbe-132">tooinstall Git e Node.js, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="f0bbe-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="f0bbe-133">Premere `Ctrl + Alt + T` tooopen un terminale.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="f0bbe-134">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f0bbe-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="f0bbe-135">Installare gli strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="f0bbe-135">Install Node.js development tools</span></span>

<span data-ttu-id="f0bbe-136">Utilizzare [file gulp.js](http://gulpjs.com/) tooautomate distribuzione ed esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="f0bbe-137">gulp tooinstall, eseguire hello comando terminal hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f0bbe-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="f0bbe-138">Se si verificano problemi relativi all'installazione di hello, vedere hello [risoluzione dei problemi guida](iot-hub-gateway-kit-c-troubleshooting.md) per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="f0bbe-139">Nodo, NPM e Gulp sono gli script di automazione di richiesto toorun sviluppati in Node.js.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="f0bbe-140">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="f0bbe-140">Install hello Azure CLI</span></span>

<span data-ttu-id="f0bbe-141">hello tooinstall CLI di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="f0bbe-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="f0bbe-142">Eseguire i seguenti comandi in terminal hello hello:</span><span class="sxs-lookup"><span data-stu-id="f0bbe-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="f0bbe-143">installazione di Hello potrebbe richiedere 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="f0bbe-144">Verificare l'installazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f0bbe-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="f0bbe-145">Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="f0bbe-146">![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="f0bbe-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="f0bbe-147">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f0bbe-147">Install Visual Studio Code</span></span>

<span data-ttu-id="f0bbe-148">Utilizzare Visual Studio Code in un secondo momento nei file di configurazione di hello tooedit dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="f0bbe-149">[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="f0bbe-150">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="f0bbe-150">Summary</span></span>

<span data-ttu-id="f0bbe-151">Aver installato tutti gli strumenti necessario hello e software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="f0bbe-152">L'attività successiva è toouse hello Azure CLI toocreate un hub IoT e registrare il dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f0bbe-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0bbe-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f0bbe-153">Next steps</span></span>
[<span data-ttu-id="f0bbe-154">Creare un hub IoT e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="f0bbe-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
