---
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 1: ottenere gli strumenti (Ubuntu) | Documenti Microsoft'
description: Scaricare e installare gli strumenti necessari hello e software per l'applicazione di esempio per Pi prima hello in Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: sviluppo iot, software iot, software per internet delle cose, installare git in ubuntu, esecuzione di gulp, installare node js in ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="07b19-104">Ottenere strumenti hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="07b19-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="07b19-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="07b19-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="07b19-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="07b19-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="07b19-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="07b19-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="07b19-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="07b19-108">What you will do</span></span>
<span data-ttu-id="07b19-109">Scaricare strumenti di sviluppo hello e software di hello per hello prima applicazione di esempio per Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="07b19-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="07b19-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="07b19-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="07b19-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="07b19-111">What you will learn</span></span>
<span data-ttu-id="07b19-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="07b19-112">In this article, you will learn:</span></span>

* <span data-ttu-id="07b19-113">Come tooinstall Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="07b19-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="07b19-114">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="07b19-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="07b19-115">applicazione di esempio Hello per questo articolo viene archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="07b19-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="07b19-116">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="07b19-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="07b19-117">Come toouse NPM tooinstall aggiuntive Node.js gli strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="07b19-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="07b19-118">Hello versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="07b19-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="07b19-119">[NPM](https://www.npmjs.com) è uno dei hello gestori di pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="07b19-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="07b19-120">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="07b19-120">What do you need</span></span>
<span data-ttu-id="07b19-121">toocomplete questa operazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="07b19-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="07b19-122">Un toodownload connessione Internet hello gli strumenti di sviluppo e hello software.</span><span class="sxs-lookup"><span data-stu-id="07b19-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="07b19-123">Un computer che esegue Ubuntu 16.04 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="07b19-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="07b19-124">Installare Git, Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="07b19-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="07b19-125">Utilizzare hello tasto di scelta rapida `Ctrl + Alt + T` tooopen un hello terminal ed eseguire seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="07b19-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="07b19-126">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="07b19-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="07b19-127">Utilizzare [file gulp.js](http://gulpjs.com) distribuzione hello tooautomate di tooPi applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="07b19-127">You use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="07b19-128">Utilizzare inoltre hello [dispositivo-individuazione-cli](https://github.com/Azure/device-discovery-cli) tooretrieve informazioni di rete sui dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="07b19-128">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="07b19-129">Installare `gulp` e `device-discovery-cli` eseguendo hello comando terminal hello seguente:</span><span class="sxs-lookup"><span data-stu-id="07b19-129">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="07b19-130">Se si verificano problemi di installazione di Node.js e questi strumenti di sviluppo aggiuntive in Ubuntu, vedere hello [risoluzione dei problemi guida](iot-hub-raspberry-pi-kit-node-troubleshooting.md) per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="07b19-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="07b19-131">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="07b19-131">Install Visual Studio Code</span></span>
<span data-ttu-id="07b19-132">[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="07b19-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="07b19-133">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="07b19-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="07b19-134">Utilizzare questo editor in un secondo momento nel codice di esempio di hello tooedit esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="07b19-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="07b19-135">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="07b19-135">Summary</span></span>
<span data-ttu-id="07b19-136">È stato installato Strumenti di sviluppo hello necessarie e software per la prima applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="07b19-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="07b19-137">attività successiva Hello è toocreate, distribuire ed eseguire l'applicazione di esempio hello in Pi.</span><span class="sxs-lookup"><span data-stu-id="07b19-137">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07b19-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07b19-138">Next steps</span></span>
[<span data-ttu-id="07b19-139">Creare e distribuire l'applicazione di esempio hello blink</span><span class="sxs-lookup"><span data-stu-id="07b19-139">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

