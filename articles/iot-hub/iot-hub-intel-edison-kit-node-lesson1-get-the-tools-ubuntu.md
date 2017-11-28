---
title: 'Connettere Intel Edison (Node) ad Azure IoT: lezione 1: Ottenere gli strumenti (Ubuntu) | Documentazione Microsoft'
description: Scaricare e installare il software e gli strumenti necessari per la prima applicazione di esempio per Edison in Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: strumenti di sviluppo arduino, sviluppo iot, software iot, software per internet delle cose, installare git in ubuntu, installare node js in ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 74c5f06c2b12d140814bfb75125d60b83addf70c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="bed9b-104">Ottenere gli strumenti (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="bed9b-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="bed9b-105">[Windows 7 o versione successiva][windows]</span><span class="sxs-lookup"><span data-stu-id="bed9b-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="bed9b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="bed9b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="bed9b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="bed9b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bed9b-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="bed9b-108">What you will do</span></span>
<span data-ttu-id="bed9b-109">Scaricare gli strumenti di sviluppo e il software per la prima applicazione di esempio per Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="bed9b-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="bed9b-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="bed9b-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bed9b-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="bed9b-111">What you will learn</span></span>
<span data-ttu-id="bed9b-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="bed9b-112">In this article, you will learn:</span></span>

* <span data-ttu-id="bed9b-113">Come installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="bed9b-113">How to install Git and Node.js</span></span>
  * <span data-ttu-id="bed9b-114">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="bed9b-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="bed9b-115">L'applicazione di esempio per questo articolo è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="bed9b-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="bed9b-116">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="bed9b-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="bed9b-117">Come usare NPM per installare altri strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="bed9b-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="bed9b-118">La versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="bed9b-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="bed9b-119">[NPM](https://www.npmjs.com) è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="bed9b-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bed9b-120">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="bed9b-120">What you need</span></span>
<span data-ttu-id="bed9b-121">Per completare questa operazione saranno necessari:</span><span class="sxs-lookup"><span data-stu-id="bed9b-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="bed9b-122">Una connessione Internet per scaricare gli strumenti di sviluppo e il software.</span><span class="sxs-lookup"><span data-stu-id="bed9b-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="bed9b-123">Un computer che esegue Ubuntu 16.04 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="bed9b-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="bed9b-124">Installare Git, Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="bed9b-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="bed9b-125">Usare la scelta rapida da tastiera `Ctrl + Alt + T` per aprire un terminale ed eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="bed9b-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="bed9b-126">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="bed9b-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="bed9b-127">Usare [gulp.js](http://gulpjs.com) per automatizzare la distribuzione dell'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="bed9b-127">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="bed9b-128">Installare `gulp` eseguendo questo comando nel terminale:</span><span class="sxs-lookup"><span data-stu-id="bed9b-128">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="bed9b-129">Se si verificano problemi durante l'installazione in Ubuntu di Node.js e di questi strumenti di sviluppo aggiuntivi, vedere la [guida alla risoluzione dei problemi][troubleshooting] per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="bed9b-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="bed9b-130">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bed9b-130">Install Visual Studio Code</span></span>
<span data-ttu-id="bed9b-131">[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bed9b-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="bed9b-132">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="bed9b-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="bed9b-133">Più avanti nell'esercitazione si userà questo editor per modificare il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="bed9b-133">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="bed9b-134">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="bed9b-134">Summary</span></span>
<span data-ttu-id="bed9b-135">Sono stati installati gli strumenti di sviluppo e il software necessari per la prima applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="bed9b-135">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="bed9b-136">L'attività successiva consiste nella creazione, distribuzione ed esecuzione dell'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="bed9b-136">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bed9b-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bed9b-137">Next steps</span></span>
<span data-ttu-id="bed9b-138">[Creare e distribuire l'applicazione di esempio per il lampeggiamento][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="bed9b-138">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
