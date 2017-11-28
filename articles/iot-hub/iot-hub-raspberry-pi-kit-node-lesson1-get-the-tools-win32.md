---
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 1: ottenere gli strumenti (Windows) | Documenti Microsoft'
description: Scaricare e installare gli strumenti necessari hello e software per l'applicazione di esempio per Pi prima hello in Windows 7 e versioni successive.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: sviluppo iot, software iot, software per internet delle cose, installare git in windows, esecuzione di gulp, installare node js in windows, installare npm in windows, installare python in windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ea7f77cc79c70c8c7952b63462b926471fcf71cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="cffb1-104">Ottenere strumenti hello (Windows 7 o versioni successive)</span><span class="sxs-lookup"><span data-stu-id="cffb1-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cffb1-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="cffb1-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="cffb1-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="cffb1-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="cffb1-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="cffb1-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="cffb1-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="cffb1-108">What you will do</span></span>
<span data-ttu-id="cffb1-109">Scaricare strumenti di sviluppo hello e software di hello per hello prima applicazione di esempio per Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="cffb1-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="cffb1-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cffb1-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cffb1-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="cffb1-111">What you will learn</span></span>
<span data-ttu-id="cffb1-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="cffb1-112">In this article, you will learn:</span></span>

* <span data-ttu-id="cffb1-113">Come tooinstall Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="cffb1-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="cffb1-114">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="cffb1-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="cffb1-115">applicazione di esempio Hello per questo articolo viene archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="cffb1-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="cffb1-116">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cffb1-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="cffb1-117">Come toouse NPM tooinstall aggiuntive Node.js gli strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="cffb1-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="cffb1-118">requisito di versione minima di Hello di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="cffb1-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="cffb1-119">[NPM](https://www.npmjs.com) è uno dei hello gestori di pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="cffb1-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cffb1-120">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="cffb1-120">What you need</span></span>
<span data-ttu-id="cffb1-121">toocomplete questa operazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="cffb1-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="cffb1-122">Un toodownload connessione Internet hello gli strumenti di sviluppo e hello software.</span><span class="sxs-lookup"><span data-stu-id="cffb1-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="cffb1-123">Un computer che esegue Windows.</span><span class="sxs-lookup"><span data-stu-id="cffb1-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="cffb1-124">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="cffb1-124">Install Git and Node.js</span></span>
<span data-ttu-id="cffb1-125">Fare clic su hello seguente toodownload collegamenti e installare Git e LTS Node.js per Windows.</span><span class="sxs-lookup"><span data-stu-id="cffb1-125">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="cffb1-126">Ottenere Git per Windows</span><span class="sxs-lookup"><span data-stu-id="cffb1-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="cffb1-127">Ottenere Node.js LTS per Windows</span><span class="sxs-lookup"><span data-stu-id="cffb1-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="cffb1-128">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="cffb1-128">Install additional Node.js development tools</span></span>
<span data-ttu-id="cffb1-129">Utilizzare [file gulp.js](http://gulpjs.com) distribuzione hello tooautomate di tooPi applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="cffb1-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="cffb1-130">Utilizzare inoltre hello [dispositivo-individuazione-cli](https://github.com/Azure/device-discovery-cli) tooretrieve informazioni di rete sui dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="cffb1-130">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="cffb1-131">Avviare il prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cffb1-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="cffb1-132">Installare `gulp` e `device-discovery-cli` eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cffb1-132">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="cffb1-133">Se si verificano problemi di installazione di Node.js e questi strumenti di sviluppo Node.js aggiuntivi nel computer in uso, vedere hello [risoluzione dei problemi guida](iot-hub-raspberry-pi-kit-node-troubleshooting.md) per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="cffb1-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="cffb1-134">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="cffb1-134">Install Visual Studio Code</span></span>
<span data-ttu-id="cffb1-135">[Scaricare](https://code.visualstudio.com/docs/setup/windows) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="cffb1-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="cffb1-136">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="cffb1-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="cffb1-137">Utilizzare questo editor in un secondo momento nel codice di esempio di hello tooedit esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="cffb1-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="cffb1-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="cffb1-138">Summary</span></span>
<span data-ttu-id="cffb1-139">È stato installato Strumenti di sviluppo hello necessarie e software per la prima applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="cffb1-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="cffb1-140">attività successiva Hello è toocreate, distribuire ed eseguire l'applicazione di esempio hello in Pi.</span><span class="sxs-lookup"><span data-stu-id="cffb1-140">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cffb1-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cffb1-141">Next steps</span></span>
[<span data-ttu-id="cffb1-142">Creare e distribuire l'applicazione di esempio hello blink</span><span class="sxs-lookup"><span data-stu-id="cffb1-142">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

