---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: lezione 1: Ottenere gli strumenti (Windows) | Documentazione Microsoft'
description: Scaricare e installare gli strumenti necessari e il software per la prima applicazione di esempio per Pi in Windows 7 e versioni successive.
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
ms.openlocfilehash: 0e58975f4411f97223b2c4374bdd746fe6628c42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="364bd-104">Ottenere gli strumenti (Windows 7 o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="364bd-104">Get the tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="364bd-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="364bd-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="364bd-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="364bd-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="364bd-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="364bd-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="364bd-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="364bd-108">What you will do</span></span>
<span data-ttu-id="364bd-109">Scaricare gli strumenti di sviluppo e il software per la prima applicazione di esempio per Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="364bd-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="364bd-110">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="364bd-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="364bd-111">Anche se il linguaggio di programmazione della logica principale è C, le lezioni fanno uso di strumenti Node.js per individuare i dispositivi e compilare e distribuire applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="364bd-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="364bd-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="364bd-112">What you will learn</span></span>
<span data-ttu-id="364bd-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="364bd-113">In this article, you will learn:</span></span>

* <span data-ttu-id="364bd-114">Come installare Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="364bd-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="364bd-115">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="364bd-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="364bd-116">L'applicazione di esempio per questo articolo è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="364bd-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="364bd-117">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="364bd-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="364bd-118">Come usare NPM per installare altri strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="364bd-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="364bd-119">Il requisito di versione minima per Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="364bd-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="364bd-120">[NPM](https://www.npmjs.com) è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="364bd-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="364bd-121">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="364bd-121">What you need</span></span>

<span data-ttu-id="364bd-122">Per completare questa operazione saranno necessari:</span><span class="sxs-lookup"><span data-stu-id="364bd-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="364bd-123">Una connessione Internet per scaricare gli strumenti di sviluppo e il software.</span><span class="sxs-lookup"><span data-stu-id="364bd-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="364bd-124">Un computer che esegue Windows.</span><span class="sxs-lookup"><span data-stu-id="364bd-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="364bd-125">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="364bd-125">Install Git and Node.js</span></span>

<span data-ttu-id="364bd-126">Fare clic sui collegamenti seguenti per scaricare e installare Git e Node.js LTS per Windows.</span><span class="sxs-lookup"><span data-stu-id="364bd-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="364bd-127">Ottenere Git per Windows</span><span class="sxs-lookup"><span data-stu-id="364bd-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="364bd-128">Ottenere Node.js LTS per Windows</span><span class="sxs-lookup"><span data-stu-id="364bd-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="364bd-129">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="364bd-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="364bd-130">Usare [gulp.js](http://gulpjs.com) per automatizzare la distribuzione dell'applicazione di esempio in Pi.</span><span class="sxs-lookup"><span data-stu-id="364bd-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="364bd-131">Usare [device-discovery-cli](https://github.com/Azure/device-discovery-cli) per recuperare informazioni di rete sui dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="364bd-131">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="364bd-132">Avviare il prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="364bd-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="364bd-133">Installare `gulp` e `device-discovery-cli` eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="364bd-133">Install `gulp` and `device-discovery-cli` by running the following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="364bd-134">Se si verificano problemi durante l'installazione di Node.js e di questi strumenti di sviluppo di Node.js aggiuntivi nel computer, vedere la [guida alla risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md) per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="364bd-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="364bd-135">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="364bd-135">Install Visual Studio Code</span></span>

<span data-ttu-id="364bd-136">[Scaricare](https://code.visualstudio.com/docs/setup/windows) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="364bd-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="364bd-137">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="364bd-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="364bd-138">Più avanti nell'esercitazione si userà questo editor per modificare il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="364bd-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="364bd-139">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="364bd-139">Summary</span></span>

<span data-ttu-id="364bd-140">Sono stati installati gli strumenti di sviluppo e il software necessari per la prima applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="364bd-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="364bd-141">L'attività successiva consiste nella creazione, distribuzione ed esecuzione dell'applicazione di esempio nel dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="364bd-141">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="364bd-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="364bd-142">Next steps</span></span>

[<span data-ttu-id="364bd-143">Creare e distribuire l'applicazione per il lampeggiamento</span><span class="sxs-lookup"><span data-stu-id="364bd-143">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
