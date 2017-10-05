---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 1: Ottenere gli strumenti (macOS) | Documentazione Microsoft'
description: Scaricare e installare il software e gli strumenti necessari per la prima applicazione di esempio per Edison in macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: strumenti di sviluppo arduino, sviluppo iot, software iot, software per internet delle cose, installare git in mac, installare node js in mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 3f764f2e-25fa-4dde-9e8d-d278453fccfd
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 27939f731121522f688e606052492bda8ae045fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="2cdc3-104">Ottenere gli strumenti (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="2cdc3-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2cdc3-105">[Windows 7 o versione successiva][windows]</span><span class="sxs-lookup"><span data-stu-id="2cdc3-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="2cdc3-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="2cdc3-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="2cdc3-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="2cdc3-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2cdc3-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2cdc3-108">What you will do</span></span>
<span data-ttu-id="2cdc3-109">Scaricare gli strumenti di sviluppo e il software per la prima applicazione di esempio per Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="2cdc3-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2cdc3-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="2cdc3-111">Anche se il linguaggio di programmazione della logica principale è C, le lezioni fanno uso di strumenti Node.js per compilare e distribuire applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2cdc3-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2cdc3-112">What you will learn</span></span>
<span data-ttu-id="2cdc3-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="2cdc3-113">In this article, you will learn:</span></span>

* <span data-ttu-id="2cdc3-114">Come installare Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="2cdc3-115">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2cdc3-116">L'applicazione di esempio per questo articolo è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2cdc3-117">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2cdc3-118">Come usare NPM per installare altri strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="2cdc3-119">La versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2cdc3-120">[NPM](https://www.npmjs.com) è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2cdc3-121">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="2cdc3-121">What you need</span></span>
<span data-ttu-id="2cdc3-122">Per completare questa operazione saranno necessari:</span><span class="sxs-lookup"><span data-stu-id="2cdc3-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="2cdc3-123">Una connessione Internet per scaricare gli strumenti di sviluppo e il software.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="2cdc3-124">Un computer Mac che esegue macOS Yosemite (10.10) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2cdc3-125">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="2cdc3-125">Install Git and Node.js</span></span>
<span data-ttu-id="2cdc3-126">Per installare Git e Node.js, usare l'utilità di gestione pacchetti [Homebrew](http://brew.sh) seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="2cdc3-127">Installare Homebrew.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-127">Install Homebrew.</span></span> <span data-ttu-id="2cdc3-128">Se è già stato installato Homebrew, andare al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-128">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="2cdc3-129">Premere `Cmd + Space` e immettere `Terminal` per aprire un terminale.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="2cdc3-130">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2cdc3-130">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="2cdc3-131">Installare Git e Node.js eseguendo questi comandi:</span><span class="sxs-lookup"><span data-stu-id="2cdc3-131">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2cdc3-132">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="2cdc3-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="2cdc3-133">Usare [gulp.js](http://gulpjs.com) per automatizzare la distribuzione dell'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="2cdc3-134">Installare `gulp` eseguendo questo comando nel terminale:</span><span class="sxs-lookup"><span data-stu-id="2cdc3-134">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="2cdc3-135">Se si verificano problemi durante l'installazione in macOS di Node.js e di questi strumenti di sviluppo aggiuntivi, vedere la [guida alla risoluzione dei problemi][troubleshooting] per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2cdc3-136">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2cdc3-136">Install Visual Studio Code</span></span>
<span data-ttu-id="2cdc3-137">[Scaricare](https://code.visualstudio.com/docs/setup/osx) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="2cdc3-138">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2cdc3-139">Più avanti nell'esercitazione si userà questo editor per modificare il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2cdc3-140">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2cdc3-140">Summary</span></span>
<span data-ttu-id="2cdc3-141">Sono stati installati gli strumenti di sviluppo e il software necessari per la prima applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="2cdc3-142">L'attività successiva consiste nella creazione, distribuzione ed esecuzione dell'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="2cdc3-142">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cdc3-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2cdc3-143">Next steps</span></span>
<span data-ttu-id="2cdc3-144">[Creare e distribuire l'applicazione per il lampeggiamento][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="2cdc3-144">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
