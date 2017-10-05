---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 1: Ottenere gli strumenti (Windows) | Documentazione Microsoft'
description: Scaricare e installare il software e gli strumenti necessari per la prima applicazione di esempio per Edison in Windows 7 e versioni successive.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: strumenti di sviluppo arduino, sviluppo iot, software iot, software per internet delle cose, installare git in windows, installare node js in windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 7d29a358-544d-4657-a504-5ed9b79c2925
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9d614d17f262b81a75d6128cbc5898dc18ab906
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="eab5c-104">Ottenere gli strumenti (Windows 7 o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="eab5c-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="eab5c-105">[Windows 7 o versione successiva][windows]</span><span class="sxs-lookup"><span data-stu-id="eab5c-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="eab5c-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="eab5c-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="eab5c-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="eab5c-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="eab5c-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="eab5c-108">What you will do</span></span>
<span data-ttu-id="eab5c-109">Scaricare gli strumenti di sviluppo e il software per la prima applicazione di esempio per Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="eab5c-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="eab5c-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="eab5c-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="eab5c-111">Anche se il linguaggio di programmazione della logica principale è C, le lezioni fanno uso di strumenti Node.js per compilare e distribuire applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="eab5c-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eab5c-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="eab5c-112">What you will learn</span></span>
<span data-ttu-id="eab5c-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="eab5c-113">In this article, you will learn:</span></span>

* <span data-ttu-id="eab5c-114">Come installare Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="eab5c-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="eab5c-115">[Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source.</span><span class="sxs-lookup"><span data-stu-id="eab5c-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="eab5c-116">L'applicazione di esempio per questo articolo è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="eab5c-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="eab5c-117">[Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="eab5c-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="eab5c-118">Come usare NPM per installare altri strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="eab5c-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="eab5c-119">Il requisito di versione minima per Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="eab5c-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="eab5c-120">[NPM](https://www.npmjs.com) è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="eab5c-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eab5c-121">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="eab5c-121">What you need</span></span>

<span data-ttu-id="eab5c-122">Per completare questa operazione saranno necessari:</span><span class="sxs-lookup"><span data-stu-id="eab5c-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="eab5c-123">Una connessione Internet per scaricare gli strumenti di sviluppo e il software.</span><span class="sxs-lookup"><span data-stu-id="eab5c-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="eab5c-124">Un computer che esegue Windows.</span><span class="sxs-lookup"><span data-stu-id="eab5c-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="eab5c-125">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="eab5c-125">Install Git and Node.js</span></span>

<span data-ttu-id="eab5c-126">Fare clic sui collegamenti seguenti per scaricare e installare Git e Node.js LTS per Windows.</span><span class="sxs-lookup"><span data-stu-id="eab5c-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="eab5c-127">Ottenere Git per Windows</span><span class="sxs-lookup"><span data-stu-id="eab5c-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="eab5c-128">Ottenere Node.js LTS per Windows</span><span class="sxs-lookup"><span data-stu-id="eab5c-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="eab5c-129">Installare altri strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="eab5c-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="eab5c-130">Usare [gulp.js](http://gulpjs.com) per automatizzare la distribuzione dell'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="eab5c-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="eab5c-131">Avviare il prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="eab5c-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="eab5c-132">Installare `gulp` eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="eab5c-132">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="eab5c-133">Se si verificano problemi durante l'installazione di Node.js e di questi strumenti di sviluppo di Node.js aggiuntivi nel computer, vedere la [guida alla risoluzione dei problemi][troubleshooting] per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="eab5c-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="eab5c-134">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="eab5c-134">Install Visual Studio Code</span></span>

<span data-ttu-id="eab5c-135">[Scaricare](https://code.visualstudio.com/docs/setup/windows) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="eab5c-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="eab5c-136">Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="eab5c-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="eab5c-137">Più avanti nell'esercitazione si userà questo editor per modificare il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="eab5c-137">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="eab5c-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="eab5c-138">Summary</span></span>

<span data-ttu-id="eab5c-139">Sono stati installati gli strumenti di sviluppo e il software necessari per la prima applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="eab5c-139">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="eab5c-140">L'attività successiva consiste nella creazione, distribuzione ed esecuzione dell'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="eab5c-140">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eab5c-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eab5c-141">Next steps</span></span>

<span data-ttu-id="eab5c-142">[Creare e distribuire l'applicazione per il lampeggiamento][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="eab5c-142">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
