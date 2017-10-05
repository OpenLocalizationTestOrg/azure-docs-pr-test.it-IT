---
title: 'Connettere Arduino ad Azure IoT: lezione 1: Ottenere gli strumenti (Ubuntu) | Documentazione Microsoft'
description: Scaricare e installare il software e gli strumenti necessari per la prima applicazione di esempio per Adafruit Feather M0 WiFi in Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: strumenti di sviluppo arduino, sviluppo iot, software iot, software per internet delle cose, installare git in ubuntu, installare node js in ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 7572f191-420d-41f0-923b-7ea86c0bfa73
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 90b1c12659c33517142e2048d8f5f629f6d6b4c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="fa4b2-104">Ottenere gli strumenti (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="fa4b2-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="fa4b2-105">[Windows 7 o versione successiva][windows]</span><span class="sxs-lookup"><span data-stu-id="fa4b2-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="fa4b2-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="fa4b2-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="fa4b2-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="fa4b2-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="fa4b2-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="fa4b2-108">What you will do</span></span>

<span data-ttu-id="fa4b2-109">Scaricare gli strumenti di sviluppo e il software per la prima applicazione di esempio per la scheda Arduino per Adafruit Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="fa4b2-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="fa4b2-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="fa4b2-111">Anche se il linguaggio di programmazione della logica principale è Arduino, nelle lezioni vengono usati gli strumenti Node.js per compilare e distribuire applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-111">Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fa4b2-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="fa4b2-112">What you will learn</span></span>
<span data-ttu-id="fa4b2-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="fa4b2-113">In this article, you will learn:</span></span>

* <span data-ttu-id="fa4b2-114">Come installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="fa4b2-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="fa4b2-115">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="fa4b2-116">L'applicazione di esempio per questo articolo è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="fa4b2-117">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="fa4b2-118">Come usare NPM per installare altri strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="fa4b2-119">La versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="fa4b2-120">[NPM](https://www.npmjs.com) è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fa4b2-121">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="fa4b2-121">What you need</span></span>
<span data-ttu-id="fa4b2-122">Per completare questa operazione saranno necessari:</span><span class="sxs-lookup"><span data-stu-id="fa4b2-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="fa4b2-123">Una connessione Internet per scaricare gli strumenti di sviluppo e il software.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="fa4b2-124">Un computer che esegue Ubuntu 16.04 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="fa4b2-125">Installare Git, Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="fa4b2-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="fa4b2-126">Usare la scelta rapida da tastiera `Ctrl + Alt + T` per aprire un terminale ed eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="fa4b2-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="fa4b2-127">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="fa4b2-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="fa4b2-128">Usare [gulp.js](http://gulpjs.com) per automatizzare la distribuzione dell'applicazione di esempio nella scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="fa4b2-129">Installare `gulp`, `device-discovery-cli` eseguendo questo comando nel terminale:</span><span class="sxs-lookup"><span data-stu-id="fa4b2-129">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="fa4b2-130">Se si verificano problemi durante l'installazione in Ubuntu di Node.js e di questi strumenti di sviluppo aggiuntivi, vedere la [guida alla risoluzione dei problemi][troubleshooting] per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="fa4b2-131">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fa4b2-131">Install Visual Studio Code</span></span>
<span data-ttu-id="fa4b2-132">[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="fa4b2-133">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="fa4b2-134">Più avanti nell'esercitazione si userà questo editor per modificare il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="fa4b2-135">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="fa4b2-135">Summary</span></span>
<span data-ttu-id="fa4b2-136">Sono stati installati gli strumenti di sviluppo e il software necessari per la prima applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="fa4b2-137">L'attività successiva consiste nella creazione, la distribuzione e l'esecuzione dell'applicazione di esempio nella scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="fa4b2-137">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa4b2-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa4b2-138">Next steps</span></span>
<span data-ttu-id="fa4b2-139">[Creare e distribuire l'applicazione di esempio per il lampeggiamento][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="fa4b2-139">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]</span></span>

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md