---
title: 'Connettere Intel Edison (Node) ad Azure IoT: lezione 1: Ottenere gli strumenti (macOS) | Documentazione Microsoft'
description: Scaricare e installare il software e gli strumenti necessari per la prima applicazione di esempio per Edison in macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: strumenti di sviluppo arduino, sviluppo iot, software iot, software per internet delle cose, installare git in mac, installare node js in mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="49899-104">Ottenere gli strumenti (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="49899-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="49899-105">[Windows 7 o versione successiva][windows]</span><span class="sxs-lookup"><span data-stu-id="49899-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="49899-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="49899-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="49899-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="49899-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="49899-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="49899-108">What you will do</span></span>
<span data-ttu-id="49899-109">Scaricare gli strumenti di sviluppo e il software per la prima applicazione di esempio per Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="49899-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="49899-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="49899-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="49899-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="49899-111">What you will learn</span></span>
<span data-ttu-id="49899-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="49899-112">In this article, you will learn:</span></span>

* <span data-ttu-id="49899-113">Come installare Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="49899-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="49899-114">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="49899-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="49899-115">L'applicazione di esempio per questo articolo è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="49899-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="49899-116">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="49899-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="49899-117">Come usare NPM per installare altri strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="49899-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="49899-118">La versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="49899-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="49899-119">[NPM](https://www.npmjs.com) è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="49899-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="49899-120">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="49899-120">What you need</span></span>
<span data-ttu-id="49899-121">Per completare questa operazione saranno necessari:</span><span class="sxs-lookup"><span data-stu-id="49899-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="49899-122">Una connessione Internet per scaricare gli strumenti di sviluppo e il software.</span><span class="sxs-lookup"><span data-stu-id="49899-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="49899-123">Un computer Mac che esegue macOS Yosemite (10.10) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="49899-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="49899-124">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="49899-124">Install Git and Node.js</span></span>
<span data-ttu-id="49899-125">Per installare Git e Node.js, usare l'utilità di gestione pacchetti [Homebrew](http://brew.sh) seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="49899-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="49899-126">Installare Homebrew.</span><span class="sxs-lookup"><span data-stu-id="49899-126">Install Homebrew.</span></span> <span data-ttu-id="49899-127">Se è già stato installato Homebrew, andare al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="49899-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="49899-128">Premere `Cmd + Space` e immettere `Terminal` per aprire un terminale.</span><span class="sxs-lookup"><span data-stu-id="49899-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="49899-129">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="49899-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="49899-130">Installare Git e Node.js eseguendo questi comandi:</span><span class="sxs-lookup"><span data-stu-id="49899-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="49899-131">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="49899-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="49899-132">Usare [gulp.js](http://gulpjs.com) per automatizzare la distribuzione dell'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="49899-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="49899-133">Installare `gulp` eseguendo questo comando nel terminale:</span><span class="sxs-lookup"><span data-stu-id="49899-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="49899-134">Se si verificano problemi durante l'installazione in macOS di Node.js e di questi strumenti di sviluppo aggiuntivi, vedere la [guida alla risoluzione dei problemi][troubleshooting] per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="49899-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="49899-135">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="49899-135">Install Visual Studio Code</span></span>
<span data-ttu-id="49899-136">[Scaricare](https://code.visualstudio.com/docs/setup/osx) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="49899-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="49899-137">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="49899-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="49899-138">Più avanti nell'esercitazione si userà questo editor per modificare il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="49899-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="49899-139">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="49899-139">Summary</span></span>
<span data-ttu-id="49899-140">Sono stati installati gli strumenti di sviluppo e il software necessari per la prima applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="49899-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="49899-141">L'attività successiva consiste nella creazione, distribuzione ed esecuzione dell'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="49899-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49899-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49899-142">Next steps</span></span>
<span data-ttu-id="49899-143">[Creare e distribuire l'applicazione per il lampeggiamento][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="49899-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
