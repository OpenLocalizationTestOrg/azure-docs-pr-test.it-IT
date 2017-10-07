---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 1: ottenere gli strumenti (macOS) | Documenti Microsoft'
description: Scaricare e installare gli strumenti necessari hello e software per l'applicazione di esempio per Pi prima hello in macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, software per internet delle cose, installare git in mac, esecuzione di gulp, installare node js in mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="ed586-104">Ottenere strumenti hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="ed586-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed586-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="ed586-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="ed586-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="ed586-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="ed586-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="ed586-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="ed586-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ed586-108">What you will do</span></span>
<span data-ttu-id="ed586-109">Scaricare strumenti di sviluppo hello e software di hello per l'applicazione di esempio per i 3 Pi Raspberry prima hello.</span><span class="sxs-lookup"><span data-stu-id="ed586-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="ed586-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ed586-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ed586-111">Sebbene hello linguaggio della logica principale hello di programmazione C, Node.js tools e vengono utilizzati nei dispositivi toodiscover lezioni di hello, compilare e distribuire applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="ed586-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ed586-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ed586-112">What you will learn</span></span>
<span data-ttu-id="ed586-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="ed586-113">In this article, you will learn:</span></span>

* <span data-ttu-id="ed586-114">Come tooinstall Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="ed586-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="ed586-115">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="ed586-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="ed586-116">applicazione di esempio Hello per questo articolo viene archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="ed586-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="ed586-117">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ed586-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="ed586-118">Come toouse NPM tooinstall aggiuntive Node.js gli strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="ed586-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="ed586-119">Hello versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="ed586-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="ed586-120">[NPM](https://www.npmjs.com) è uno dei hello gestori di pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="ed586-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ed586-121">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="ed586-121">What you need</span></span>
<span data-ttu-id="ed586-122">toocomplete questa operazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="ed586-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="ed586-123">Un toodownload connessione Internet hello gli strumenti di sviluppo e hello software.</span><span class="sxs-lookup"><span data-stu-id="ed586-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="ed586-124">Un computer Mac che esegue macOS Yosemite (10.10) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="ed586-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="ed586-125">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="ed586-125">Install Git and Node.js</span></span>
<span data-ttu-id="ed586-126">tooinstall Git e Node.js, utilizzare hello [Homebrew](http://brew.sh) utilità di gestione del pacchetto attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ed586-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="ed586-127">Installare Homebrew.</span><span class="sxs-lookup"><span data-stu-id="ed586-127">Install Homebrew.</span></span> <span data-ttu-id="ed586-128">Se è già stato installato Homebrew, è possibile passare toostep 2.</span><span class="sxs-lookup"><span data-stu-id="ed586-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="ed586-129">Premere `Cmd + Space` e immettere `Terminal` tooopen un terminale.</span><span class="sxs-lookup"><span data-stu-id="ed586-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="ed586-130">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ed586-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="ed586-131">Installare Git e Node.js eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ed586-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="ed586-132">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="ed586-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="ed586-133">Utilizzare [file gulp.js](http://gulpjs.com) distribuzione hello tooautomate di tooyour di applicazione di esempio hello Pi.</span><span class="sxs-lookup"><span data-stu-id="ed586-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="ed586-134">Hello utilizzare [dispositivo-individuazione-cli](https://github.com/Azure/device-discovery-cli) tooretrieve informazioni di rete sui dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="ed586-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="ed586-135">Installare `gulp` e `device-discovery-cli` eseguendo hello comando terminal hello seguente:</span><span class="sxs-lookup"><span data-stu-id="ed586-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="ed586-136">Se si verificano problemi di installazione di Node.js e questi strumenti di sviluppo aggiuntive su macOS, vedere hello [risoluzione dei problemi guida](iot-hub-raspberry-pi-kit-c-troubleshooting.md) per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="ed586-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="ed586-137">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ed586-137">Install Visual Studio Code</span></span>
<span data-ttu-id="ed586-138">[Scaricare](https://code.visualstudio.com/docs/setup/osx) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ed586-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="ed586-139">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="ed586-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="ed586-140">Utilizzare questo editor in un secondo momento nel codice di esempio di hello tooedit esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="ed586-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="ed586-141">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="ed586-141">Summary</span></span>
<span data-ttu-id="ed586-142">È stato installato Strumenti di sviluppo hello necessarie e software per la prima applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="ed586-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="ed586-143">attività successiva Hello è toocreate, distribuire ed eseguire l'applicazione di esempio hello in Pi.</span><span class="sxs-lookup"><span data-stu-id="ed586-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed586-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed586-144">Next steps</span></span>
[<span data-ttu-id="ed586-145">Creare e distribuire un'applicazione hello blink</span><span class="sxs-lookup"><span data-stu-id="ed586-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

