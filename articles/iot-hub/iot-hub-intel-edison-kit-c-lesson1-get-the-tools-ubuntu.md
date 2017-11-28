---
title: 'Connect Intel Edison (C) tooAzure IoT - lezione 1: ottenere gli strumenti (Ubuntu) | Documenti Microsoft'
description: Scaricare e installare gli strumenti necessari hello e software per l'applicazione di esempio per Edison prima hello in Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: strumenti di sviluppo arduino, sviluppo iot, software iot, software per internet delle cose, installare git in ubuntu, installare node js in ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 4c7b8e04-b892-459b-8b03-85bcaff2465c
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1ebd599def4e8bb33d891517cc76bc2fcdc3c35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="9d0ef-104">Ottenere strumenti hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="9d0ef-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="9d0ef-105">[Windows 7 o versione successiva][windows]</span><span class="sxs-lookup"><span data-stu-id="9d0ef-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="9d0ef-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="9d0ef-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="9d0ef-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="9d0ef-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9d0ef-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="9d0ef-108">What you will do</span></span>
<span data-ttu-id="9d0ef-109">Scaricare strumenti di sviluppo hello e software hello per l'applicazione di esempio prima di hello per le Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="9d0ef-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9d0ef-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="9d0ef-111">Sebbene hello linguaggio della logica principale hello di programmazione C, Node.js tools vengono utilizzati in toobuild lezioni hello e distribuire applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9d0ef-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="9d0ef-112">What you will learn</span></span>
<span data-ttu-id="9d0ef-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="9d0ef-113">In this article, you will learn:</span></span>

* <span data-ttu-id="9d0ef-114">Come tooinstall Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="9d0ef-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="9d0ef-115">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="9d0ef-116">applicazione di esempio Hello per questo articolo viene archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="9d0ef-117">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="9d0ef-118">Come toouse NPM tooinstall aggiuntive Node.js gli strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="9d0ef-119">Hello versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="9d0ef-120">[NPM](https://www.npmjs.com) è uno dei hello gestori di pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9d0ef-121">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="9d0ef-121">What you need</span></span>
<span data-ttu-id="9d0ef-122">toocomplete questa operazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="9d0ef-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="9d0ef-123">Un toodownload connessione Internet hello gli strumenti di sviluppo e hello software.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="9d0ef-124">Un computer che esegue Ubuntu 16.04 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="9d0ef-125">Installare Git, Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="9d0ef-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="9d0ef-126">Utilizzare hello tasto di scelta rapida `Ctrl + Alt + T` tooopen un hello terminal ed eseguire seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="9d0ef-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="9d0ef-127">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="9d0ef-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="9d0ef-128">Utilizzare [file gulp.js](http://gulpjs.com) distribuzione hello tooautomate di tooEdison applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="9d0ef-129">Installare `gulp` eseguendo hello comando terminal hello seguente:</span><span class="sxs-lookup"><span data-stu-id="9d0ef-129">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="9d0ef-130">Se si verificano problemi di installazione di Node.js e questi strumenti di sviluppo aggiuntive in Ubuntu, vedere hello [risoluzione dei problemi guida] [ troubleshooting] per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="9d0ef-131">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9d0ef-131">Install Visual Studio Code</span></span>
<span data-ttu-id="9d0ef-132">[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="9d0ef-133">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="9d0ef-134">Utilizzare questo editor in un secondo momento nel codice di esempio di hello tooedit esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="9d0ef-135">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="9d0ef-135">Summary</span></span>
<span data-ttu-id="9d0ef-136">È stato installato Strumenti di sviluppo hello necessarie e software per la prima applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="9d0ef-137">attività successiva Hello è toocreate, distribuire ed eseguire l'applicazione di esempio hello in Edison.</span><span class="sxs-lookup"><span data-stu-id="9d0ef-137">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d0ef-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d0ef-138">Next steps</span></span>
<span data-ttu-id="9d0ef-139">[Creare e distribuire l'applicazione di esempio hello blink][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="9d0ef-139">[Create and deploy hello blink sample application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
