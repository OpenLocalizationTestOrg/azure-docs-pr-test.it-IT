---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: lezione 1: Ottenere gli strumenti (Ubuntu) | Documentazione Microsoft'
description: Scaricare e installare il software e gli strumenti necessari per la prima applicazione di esempio per Pi in Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, software per internet delle cose, installare git in ubuntu, esecuzione di gulp, installare node js in ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="70cd5-104">Ottenere gli strumenti (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="70cd5-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="70cd5-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="70cd5-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="70cd5-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="70cd5-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="70cd5-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="70cd5-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="70cd5-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="70cd5-108">What you will do</span></span>
<span data-ttu-id="70cd5-109">Scaricare gli strumenti di sviluppo e il software per la prima applicazione di esempio per Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="70cd5-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="70cd5-110">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="70cd5-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="70cd5-111">Anche se il linguaggio di programmazione della logica principale è C, le lezioni fanno uso di strumenti Node.js per individuare i dispositivi e compilare e distribuire applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="70cd5-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="70cd5-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="70cd5-112">What you will learn</span></span>
<span data-ttu-id="70cd5-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="70cd5-113">In this article, you will learn:</span></span>

* <span data-ttu-id="70cd5-114">Come installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="70cd5-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="70cd5-115">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="70cd5-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="70cd5-116">L'applicazione di esempio per questo articolo è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="70cd5-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="70cd5-117">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="70cd5-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="70cd5-118">Come usare NPM per installare altri strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="70cd5-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="70cd5-119">La versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="70cd5-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="70cd5-120">[NPM](https://www.npmjs.com) è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="70cd5-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="70cd5-121">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="70cd5-121">What you need</span></span>
<span data-ttu-id="70cd5-122">Per completare questa operazione saranno necessari:</span><span class="sxs-lookup"><span data-stu-id="70cd5-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="70cd5-123">Una connessione Internet per scaricare gli strumenti di sviluppo e il software.</span><span class="sxs-lookup"><span data-stu-id="70cd5-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="70cd5-124">Un computer che esegue Ubuntu 16.04 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="70cd5-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="70cd5-125">Installare Git, Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="70cd5-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="70cd5-126">Usare la scelta rapida da tastiera `Ctrl + Alt + T` per aprire un terminale ed eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="70cd5-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="70cd5-127">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="70cd5-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="70cd5-128">Usare [gulp.js](http://gulpjs.com) per automatizzare la distribuzione dell'applicazione di esempio in Pi.</span><span class="sxs-lookup"><span data-stu-id="70cd5-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="70cd5-129">Usare [device-discovery-cli](https://github.com/Azure/device-discovery-cli) per recuperare informazioni di rete sui dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="70cd5-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="70cd5-130">Installare `gulp` e `device-discovery-cli` eseguendo questo comando nel terminale:</span><span class="sxs-lookup"><span data-stu-id="70cd5-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="70cd5-131">Se si verificano problemi durante l'installazione in Ubuntu di Node.js e di questi strumenti di sviluppo aggiuntivi, vedere la [guida alla risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md) per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="70cd5-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="70cd5-132">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="70cd5-132">Install Visual Studio Code</span></span>
<span data-ttu-id="70cd5-133">[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="70cd5-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="70cd5-134">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="70cd5-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="70cd5-135">Più avanti nell'esercitazione si userà questo editor per modificare il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="70cd5-135">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="70cd5-136">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="70cd5-136">Summary</span></span>
<span data-ttu-id="70cd5-137">Sono stati installati gli strumenti di sviluppo e il software necessari per la prima applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="70cd5-137">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="70cd5-138">L'attività successiva consiste nella creazione, distribuzione ed esecuzione dell'applicazione di esempio nel dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="70cd5-138">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70cd5-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70cd5-139">Next steps</span></span>
[<span data-ttu-id="70cd5-140">Creare e distribuire l'applicazione per il lampeggiamento</span><span class="sxs-lookup"><span data-stu-id="70cd5-140">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

