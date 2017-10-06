---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 1: ottenere gli strumenti (Windows) | Documenti Microsoft'
description: Scaricare e installare gli strumenti necessari hello e software per l'applicazione di esempio per Pi prima hello in Windows 7 e versioni successive.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, software per internet delle cose, installare git in windows, installare node js in windows, installare npm in windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="f08ba-104">Ottenere strumenti hello (Windows 7 o versioni successive)</span><span class="sxs-lookup"><span data-stu-id="f08ba-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f08ba-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="f08ba-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="f08ba-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f08ba-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f08ba-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="f08ba-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="f08ba-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f08ba-108">What you will do</span></span>
<span data-ttu-id="f08ba-109">Scaricare strumenti di sviluppo hello e software di hello per hello prima applicazione di esempio per Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="f08ba-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="f08ba-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f08ba-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f08ba-111">Sebbene hello linguaggio della logica principale hello di programmazione C, Node.js tools e vengono utilizzati nei dispositivi toodiscover lezioni di hello, compilare e distribuire applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="f08ba-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f08ba-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f08ba-112">What you will learn</span></span>
<span data-ttu-id="f08ba-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="f08ba-113">In this article, you will learn:</span></span>

* <span data-ttu-id="f08ba-114">Come tooinstall Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="f08ba-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="f08ba-115">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="f08ba-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="f08ba-116">applicazione di esempio Hello per questo articolo viene archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="f08ba-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="f08ba-117">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f08ba-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="f08ba-118">Come toouse NPM tooinstall aggiuntive Node.js gli strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="f08ba-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="f08ba-119">requisito di versione minima di Hello di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="f08ba-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="f08ba-120">[NPM](https://www.npmjs.com) è uno dei hello gestori di pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="f08ba-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f08ba-121">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="f08ba-121">What you need</span></span>

<span data-ttu-id="f08ba-122">toocomplete questa operazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="f08ba-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="f08ba-123">Un toodownload connessione Internet hello gli strumenti di sviluppo e hello software.</span><span class="sxs-lookup"><span data-stu-id="f08ba-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="f08ba-124">Un computer che esegue Windows.</span><span class="sxs-lookup"><span data-stu-id="f08ba-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="f08ba-125">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="f08ba-125">Install Git and Node.js</span></span>

<span data-ttu-id="f08ba-126">Fare clic sui collegamenti hello sotto toodownload e installare Git e LTS Node.js per Windows.</span><span class="sxs-lookup"><span data-stu-id="f08ba-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="f08ba-127">Ottenere Git per Windows</span><span class="sxs-lookup"><span data-stu-id="f08ba-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="f08ba-128">Ottenere Node.js LTS per Windows</span><span class="sxs-lookup"><span data-stu-id="f08ba-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="f08ba-129">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="f08ba-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="f08ba-130">Utilizzare [file gulp.js](http://gulpjs.com) distribuzione hello tooautomate di tooPi applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="f08ba-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="f08ba-131">Hello utilizzare [dispositivo-individuazione-cli](https://github.com/Azure/device-discovery-cli) tooretrieve informazioni di rete sui dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="f08ba-131">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="f08ba-132">Avviare il prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f08ba-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="f08ba-133">Installare `gulp` e `device-discovery-cli` eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f08ba-133">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="f08ba-134">Se si verificano problemi di installazione di Node.js e questi strumenti di sviluppo Node.js aggiuntivi nel computer in uso, vedere hello [risoluzione dei problemi guida](iot-hub-raspberry-pi-kit-c-troubleshooting.md) per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="f08ba-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="f08ba-135">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f08ba-135">Install Visual Studio Code</span></span>

<span data-ttu-id="f08ba-136">[Scaricare](https://code.visualstudio.com/docs/setup/windows) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f08ba-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="f08ba-137">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="f08ba-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f08ba-138">Utilizzare questo editor in un secondo momento nel codice di esempio di hello tooedit esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="f08ba-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="f08ba-139">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="f08ba-139">Summary</span></span>

<span data-ttu-id="f08ba-140">È stato installato Strumenti di sviluppo hello necessarie e software per la prima applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="f08ba-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="f08ba-141">attività successiva Hello è toocreate, distribuire ed eseguire l'applicazione di esempio hello in Pi.</span><span class="sxs-lookup"><span data-stu-id="f08ba-141">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f08ba-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f08ba-142">Next steps</span></span>

[<span data-ttu-id="f08ba-143">Creare e distribuire un'applicazione hello blink</span><span class="sxs-lookup"><span data-stu-id="f08ba-143">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
